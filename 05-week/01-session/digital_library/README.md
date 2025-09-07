# 📚 Biblioteca Digital – Parcial POO Parte 2

## 📖 Descripción
Este proyecto implementa un **sistema de Biblioteca Digital en Python** utilizando los **cuatro pilares de la Programación Orientada a Objetos (POO)**:  
- Encapsulación  
- Abstracción  
- Herencia  
- Polimorfismo  

El sistema permite gestionar **usuarios**, **materiales (libros y revistas)**, **préstamos y devoluciones**, además de generar **reportes de préstamos activos y vencidos** con cálculo de multas por atraso.  

La aplicación funciona en **interfaz de consola (CLI)**.

## 🖥️ Comandos disponibles (CLI)
- **1. Crear usuario** → Registra un nuevo usuario.  
- **2. Listar usuarios** → Muestra todos los usuarios registrados.  
- **3. Crear material (Libro/Revista)** → Registra un libro o revista con stock inicial.  
- **4. Listar materiales** → Muestra los materiales disponibles.  
- **5. Prestar material** → Realiza un préstamo si hay stock.  
- **6. Devolver material** → Registra la devolución y calcula multa si aplica.  
- **7. Reporte de préstamos activos** → Lista todos los préstamos en curso.  
- **8. Reporte de vencidos** → Muestra préstamos atrasados y multa estimada.  
- **0. Salir** → Cierra la aplicación.  

---

## 🧩 Aplicación de los pilares de POO
- **Encapsulación**:  
  Atributos privados (`_stock`, `_documento`) y uso de `@property` para validaciones.  

- **Abstracción**:  
  Clase abstracta `Item(ABC)` que define métodos obligatorios (`dias_prestamo`, `multa_dia`).  

- **Herencia**:  
  `Libro` y `Revista` heredan de `Item`, cada uno con reglas de préstamo y multas específicas.  

- **Polimorfismo**:  
  Los métodos sobrescritos permiten calcular fechas de vencimiento y multas sin usar condicionales.  

---

## ✅ Pruebas mínimas
1. Creación de usuarios (rechaza documentos duplicados).  
2. Creación de materiales (stock ≥ 0).  
3. Préstamos válidos vs. sin stock.  
4. Devoluciones sin retraso (multa = 0).  
5. Devoluciones con retraso (multa calculada).  
6. Reporte de vencidos con atraso y multa estimada.  

---

## 📸 Evidencias
Las evidencias de ejecución están disponibles en el documento del proyecto (PDF).  
Incluyen capturas de:  
- Creación de usuario  
- Creación de material  
- Préstamo y devolución  
- Reportes  

---

## 📂 Enlaces
- **Repositorio GitHub**: https://github.com/diegotrujillo18/programacion-orientada-objetos-2025-b-g1
- **Video de sustentación**: (https://drive.google.com/file/d/1hOAN7nBmUAasOtxediXRP9rjUyX9i0Xb/view?usp=sharing) 

---

## 📚 Referencias
- Python Software Foundation. (2023). *Python 3.11. Documentación oficial*. https://docs.python.org/3/ 
