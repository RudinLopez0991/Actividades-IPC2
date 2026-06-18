# Curso de Introducción a la Programación 2

## Laboratorio del Curso

**Estudiante:** Rudin Alexander López Salvatierra
**Carnet:** 200919744

---

# Actividad de Laboratorio: Arquitectura Multi-Nivel (N-Tier) y Patrón MVC en .NET

---

# Parte 1: Fundamentación Teórica y Análisis Crítico

## El Tránsito hacia los Sistemas Distribuidos y Multi-Capa

### 🔹 La Limitación del Monolito Local

Cuando la interfaz de usuario, la lógica de negocio y el almacenamiento de datos residen en una única máquina:

* **Sincronización:**
  Los datos quedan aislados, provocando duplicidad, inconsistencias y conflictos.

* **Escalabilidad:**
  Solo puede escalar verticalmente, lo que genera límites físicos y puntos únicos de fallo.

---

### 🔹 Distinción Crítica (Layers vs. Tiers)

* **Capas Lógicas (Layers):**
  Organización del código por responsabilidades (UI, lógica, datos).

* **Niveles Físicos (Tiers):**
  Separación en infraestructura (servidores independientes conectados en red).

---

### 🔹 Arquitectura de 3 Niveles

| Nivel        | Misión                  | Tecnologías         |
| ------------ | ----------------------- | ------------------- |
| Presentación | Interfaz con el usuario | HTML, CSS, JS       |
| Aplicación   | Lógica de negocio       | .NET, Java, Node.js |
| Datos        | Persistencia            | MySQL, PostgreSQL   |

---

### 🔹 Seguridad Perimetral

No se debe exponer la base de datos directamente a internet.

**Riesgos:**

* Ataques automatizados
* Acceso directo a datos sensibles

**Buena práctica:**
Uso de VPC, subred privada y acceso controlado.

---

## Desacoplamiento con MVC

### 🔹 Problema: Código Espagueti

Mezclar UI + lógica + datos provoca:

* Difícil mantenimiento
* Imposibilidad de pruebas unitarias

---

### 🔹 Solución: MVC

* **Modelo:** Maneja datos y lógica
* **Vista:** Muestra información
* **Controlador:** Intermediario

---

### 🔹 Métricas de Calidad

* **Alta Cohesión:** cada componente tiene una función clara
* **Bajo Acoplamiento:** cambios no afectan todo el sistema

---

# Parte 2: Modelado del Ciclo de Vida

## 1. Mapeo de URLs

| URL                            | Controlador          | Acción    | ID       |
| ------------------------------ | -------------------- | --------- | -------- |
| /ControlAcademico/Login        | ControlAcademico     | Login     | Ninguno  |
| /Estudiante/Historial/20260123 | EstudianteController | Historial | 20260123 |
| /Asignacion/Detalle/10         | AsignacionController | Detalle   | 10       |
| /Home                          | HomeController       | Index     | Ninguno  |

---

## 2. Flujo de Petición

1. Usuario realiza acción
2. Se envía HTTP request
3. Routing identifica controlador
4. Controlador usa el modelo
5. Vista devuelve HTML

---

# Parte 3: Implementación Práctica

## 📁 Estructura

```
ControlAcademicoMvc/
├── Controllers/
├── Models/
├── Views/
└── Program.cs
```

---

## 🧩 Modelo

```csharp
public class Estudiante
{
    public int Carne { get; set; }
    public string Nombre { get; set; } = string.Empty;
    public double Promedio { get; set; }
}
```

---

## Controlador

```csharp
public IActionResult Listar()
{
    return View(_baseDatosMemoria);
}
```

---

## Vista

```html
<h2>Listado de Estudiantes</h2>
```

---

## ⚙ Program.cs

```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

---

# Parte 4: Auditoría

* ✔ Controlador sin lógica excesiva
* ✔ Separación correcta de responsabilidades
* ✔ No hay SQL en vistas

---

# Parte 5: Referencias Bibliográficas

> Facultad de Ingeniería, USAC. (2026). *Sesión 11: Modelado Base y Arquitecturas de Despliegue. Evolución de Sistemas Distribuidos, Fundamentos del Modelo Cliente-Servidor y Diseño Físico Multi-Capas (N-Tier).* Guatemala.

> Facultad de Ingeniería, USAC. (2026). *Sesión 12: Arquitectura y Componentes del Patrón MVC. Desacoplamiento Lógico de Software, Ciclo de Vida de las Peticiones y Enrutamiento en Aplicaciones Interactivas Modernas.* Guatemala.
