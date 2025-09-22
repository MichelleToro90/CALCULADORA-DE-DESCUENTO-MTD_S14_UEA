# CALCULADORA-DE-DESCUENTO-MTD_S14_UEA
TAREA UEA S14
Facturador CLI con SQLite (DEMO)

Programa de consola para crear facturas ingresando datos por teclado, calcular descuento e IVA, e insertar todo en una base de datos SQLite (facturas.db).
No requiere librerías externas (usa solo la biblioteca estándar de Python).

Características

Ingreso interactivo de:

Cliente (nombre y celular).

Hasta 9 productos (código, descripción, precio, cantidad).

Cálculos automáticos:

calcular_descuento (10% por defecto, configurable).

Subtotal, descuento, base imponible, IVA y total.

Base de datos con 3 tablas:

clients, invoices, items.

Impresión formateada de la factura en consola.

Manejo correcto de dinero con decimal.Decimal (acepta coma o punto).

Requisitos

Python 3.10+ (por el uso de | en anotaciones de tipos).

Sistema operativo: Windows, macOS o Linux.
