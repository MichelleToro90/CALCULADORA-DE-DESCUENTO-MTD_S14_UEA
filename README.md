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
______________________________________________________________________________________

🔧 Instalación (opcional con entorno virtual)
# 1) Crear y activar entorno virtual (opcional pero recomendado)
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

# 2) No hay dependencias externas que instalar
_______________________________________________________________________________________
▶️ Cómo ejecutar

Desde la carpeta del proyecto:

python main.py


Sigue las instrucciones del programa en la consola.
_______________________________________________________________________________________
🧭 Flujo de uso (paso a paso)

Ingresa nombre y celular del cliente.

Si el cliente ya existe, se actualiza el celular.

Indica cuántos productos (1 a 9).

Para cada producto, escribe: código, descripción, precio unitario, cantidad.

Ingresa % de descuento (ENTER para 10%).

Ingresa % de IVA (ENTER para 12%).

El sistema calcula totales, imprime la factura y guarda todo en facturas.db.
_______________________________________________________________________________________
🧾 Ejemplo de ejecución
=== Sistema de Facturación con Base de Datos (SQLite) ===
Nombre del cliente: Michelle Toro
Número de celular: 0999999999
¿Cuántos productos desea agregar? (1-9): 3

--- Producto 1 ---
Código: P001
Descripción: Cuaderno A4
Precio unitario: 1,50
Cantidad: 5

--- Producto 2 ---
Código: P002
Descripción: Lápiz HB
Precio unitario: 0.25
Cantidad: 10

--- Producto 3 ---
Código: P003
Descripción: Borrador
Precio unitario: 0.60
Cantidad: 4
Porcentaje de DESCUENTO (ENTER para 10%):
Porcentaje de IVA (ENTER para 12%):

========================================================================== 
                          FACTURA (DEMO / BD)
==========================================================================
Cliente : Michelle Toro
Celular : 0999999999
--------------------------------------------------------------------------
CÓD      DESCRIPCIÓN                           CANT        P.U.        TOTAL
--------------------------------------------------------------------------
P001     Cuaderno A4                               5        1.50         7.50
P002     Lápiz HB                                 10        0.25         2.50
P003     Borrador                                  4        0.60         2.40
--------------------------------------------------------------------------
                                     SUBTOTAL:        12.40
                               DESCUENTO (10%):         1.24
                               BASE IMPONIBLE:        11.16
                                    IVA (12%):         1.34
                                        TOTAL:        12.50
==========================================================================

✔ Factura guardada en la base de datos 'facturas.db' con ID: 1



