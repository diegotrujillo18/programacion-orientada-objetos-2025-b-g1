# Sistema de Gestion - Empresa de Transporte (POO en Python)

**Autor:** Juan Diego Trujillo Narvaez  


## Resumen del proyecto
Aplicacion en **Python** que modela la gestion de una **empresa de transporte** usando principios de **POO**:
- **Abstracción** (clases base `Employee`, `Vehicle`).
- **Herencia** (`Driver`/`Mechanic`; `Car`/`Motorcycle`/`Truck`).
- **Polimorfismo** (`costo_por_km()`, `arrancar()`, `describir()`).
- **Encapsulamiento** (atributos privados y `@property`).

El sistema administra **flota**, **personal**, **viajes** y **mantenimientos**, ofrece **CRUD de vehiculos** y reportes en consola. Incluye **datos de prueba** y **menu** listo para la demostracion en Colab.


## Evidencia de la solucion

| Requisito / Criterio | Donde se implementa | Evidencia tecnica |
|---|---|---|
| Abstraccion | `Employee`, `Vehicle` | Metodos abstractos: `rol()`, `costo_por_km()`, `arrancar()` obligatorios en subclases. |
| Herencia | `Employee → Driver/Mechanic` y `Vehicle → Car/Motorcycle/Truck` | Jerarquias funcionales; `Truck` agrega atributo `ejes` y extiende `describir()`. |
| Encapsulamiento | Atributos privados (`__nombre`, `__odometro_km`, `__status`) | Acceso controlado con `@property` y setters; estados con `VehicleStatus` (Enum). |
| Polimorfismo | Metodos sobreescritos | Calculo de costo por km y mensajes de arranque dependen del subtipo. |
| Gestion de flota (CRUD) | Metodos en `Company` | `crear_vehiculo`, `listar_vehiculos`, `eliminar_vehiculo` (con validaciones). |
| Operacion de viajes | `Company.iniciar_viaje` + `TripLog` | Incrementa odometro, costo por km polimorfico, alerta de mantenimiento. |
| Taller y mantenimiento | `enviar_a_taller`, `registrar_mantenimiento` + `MaintenanceRecord` | Flujo controlado por estado (`EN_TALLER` → `DISPONIBLE`). |
| Reportes | `resumen_flota`, `resumen_personal`, `resumen_operaciones` | Salida clara en consola con bitacoras/historiales de viajes y mantenimientos. |
| Demostracion | Menu interactivo | Entradas por `input()`: crear/listar/eliminar, asignar, viajar, taller, reportes. |

## Arquitectura

- **Dominio**: `Vehicle` (abstracta) → `Car`, `Motorcycle`, `Truck` (con `ejes`); `Employee` (abstracta) → `Driver`, `Mechanic`.
- **Aplicacion**: `Company` actua como *fachada* de casos de uso (CRUD, asignaciones, viajes, mantenimientos, reportes).
- **Modelos de datos**: `TripLog`, `MaintenanceRecord` (bitacoras), `VehicleStatus` (Enum).

## Funcionalidades principales

### (CRUD)
- `crear_vehiculo(tipo, marca, modelo, anio, capacidad, ejes=None)`  
  Tipos validos: `car`, `motorcycle`, `truck` (camion exige `ejes>0`).
- `listar_vehiculos(status=None)`  
  Filtra opcionalmente por `VehicleStatus` (`DISPONIBLE`, `EN_VIAJE`, `EN_TALLER`, `FUERA_DE_SERVICIO`).
- `eliminar_vehiculo(vehiculo_id)`  
  Prohibido si esta `EN_VIAJE`; desasigna conductores referenciados para mantener consistencia.

### Personal y Asignaciones
- `asignar_conductor(driver_id, vehiculo_id)` o desasignar con `vehiculo_id=None`.  
  Solo se asigna si el vehiculo esta `DISPONIBLE`.

### Operacion de viajes
- `iniciar_viaje(driver_id, km, comentario)`  
  Valida conductor activo y con vehiculo asignado, calcula costo por km (polimorfismo), actualiza odometro y registra en `TripLog`.  
  **Alerta de mantenimiento** si se supera el umbral de 10.000 km desde el ultimo servicio.

### Taller y mantenimiento
- `enviar_a_taller(vehiculo_id)` → cambia estado a `EN_TALLER`.  
- `registrar_mantenimiento(mechanic_id, vehiculo_id, detalle, costo)` → vuelve a `DISPONIBLE` y registra en `MaintenanceRecord`.

### Reportes
- `resumen_flota()`, `resumen_personal()`, `resumen_operaciones()` con salida legible en consola.

## Menu interactivo 

**Opciones:**
1. Crear vehiculo  
2. Listar vehiculos  
3. Eliminar vehiculo  
4. Asignar/Desasignar conductor  
5. Iniciar viaje  
6. Enviar vehiculo a taller  
7. Registrar mantenimiento  
8. Ver resumen de flota  
9. Ver resumen de personal  
10. Ver resumen de operaciones  
0. Salir

> El proyecto incluye un **seed** de datos: tres vehiculos (auto, moto, camion) y cuatro empleados (2 conductores, 2 mecanicos) con asignaciones iniciales. (Igualmente estos se pueden modificar, es decir, se pueden o agregar o elimar)

## Cómo ejecutar

### En Google Colab
1. Crear una **nueva notebook** y pegar **todo el código** del sistema en una sola celda.
2. Ejecutar la celda → aparecerá el **menú** en consola.
3. Si no ves la caja de entrada, haz **clic** en la celda para enfocarla.

### En local (opcional)
1. Guardar el archivo como `main.py` (todo el código).
2. Ejecutar en terminal:
   ```bash
   python main.py
   ```

## Calidad y decisiones
- Validaciones de negocio para evitar estados inválidos (ej. no eliminar en viaje, no mantenimiento sin taller).
- Tipado gradual (`typing`), nombres expresivos, separación de responsabilidades.
- 100% librerías estándar → portátil y fácil de evaluar.
- Diseñado para **extender** (nuevos vehículos/roles, reglas de negocio y persistencia futura).


## HECHO POR: Juan Diego Trujillo Narvaez.  

