# Jerarquía de Figuras Geométricas - POO

## Hecho por Juan Diego Trujillo Narvaez

## Objetivo
Implementar una jerarquía de clases en Python que aplique **abstracción, herencia y polimorfismo**, con **validaciones estrictas** y **documentación**, cumpliendo el contrato de la clase abstracta `FiguraGeometrica`.  
Subclases: `Rectangulo`, `Circulo`, `Triangulo` (área y perímetro obligatorios; triángulo con **Herón**).

## Diseño de la jerarquía

### `FiguraGeometrica` (abstracta)
- **Atributo protegido:** `_color: str` (cadena no vacía).
- **Métodos abstractos:** `area() -> float`, `perimetro() -> float`.
- **Método concreto:** `descripcion() -> str` → “Figura de color {color}”.
- **Notas:** hereda de `abc.ABC`; no se puede instanciar directamente.

### `Rectangulo` (concreta)
- **Privados:** `__ancho: float`, `__alto: float` (ambos > 0).
- **Fórmulas:** `area = ancho * alto`, `perimetro = 2*(ancho + alto)`.

### `Circulo` (concreta)
- **Privado:** `__radio: float` (> 0).
- **Fórmulas:** `area = π * radio²`, `perimetro = 2π * radio`.

### `Triangulo` (concreta)
- **Privados:** `__lado1`, `__lado2`, `__lado3` (todos > 0).
- **Regla:** **desigualdad triangular estricta** (`a+b>c`, `a+c>b`, `b+c>a`).
- **Fórmulas:** `perimetro = a+b+c` y **Herón** para el área:
  - `s = p/2`
  - `area = sqrt( max(0, s(s-a)(s-b)(s-c)) )` (robustez numérica).

## Decisiones de diseño
- **Contrato estricto (ABC):** `@abstractmethod` obliga a implementar `area()`/`perimetro()` con la **misma firma** en todas las subclases.
- **Encapsulamiento:** atributos internos **privados** para dimensiones; `_color` protegido por ser parte de la interfaz común.
- **Validaciones defensivas:** tipo numérico y rango (> 0); en triángulo, desigualdad triangular; color no vacío → **`ValueError`** con mensajes claros.
- **Polimorfismo real:** se opera con una **lista heterogénea** de `FiguraGeometrica` y se invocan `area()` y `perimetro()` sin conocer el tipo concreto.
- **Legibilidad y mantenimiento:** docstrings, nombres claros y funciones auxiliares de validación.

## ¿Cómo se garantiza el contrato de la clase abstracta?
- **No instanciable:** `FiguraGeometrica` hereda de `ABC` y declara métodos con `@abstractmethod`; Python impide instanciarla si faltan implementaciones.
- **Firmas coherentes:** si una subclase cambia u omite `area()` o `perimetro()`, **no se puede instanciar**.
- **Invariantes de estado:** constructores validan entradas; cualquier objeto creado es **coherente** para los cálculos.

## Validaciones y manejo de errores
- Dimensiones **> 0** y color **no vacío** → si no, `ValueError`.
- Triángulo inválido (p. ej., 1, 2, 3) → `ValueError` por desigualdad triangular.
- Mensajes explícitos para mostrar evidencia del manejo de errores.

**Ejemplos de casos inválidos:**
- `Rectangulo(0, 2, "azul")`
- `Circulo(-5, "rojo")`
- `Triangulo(1, 2, 3, "verde")`
- `Rectangulo(3, 4, "   ")`  (color vacío o solo espacios)