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
📁 Estructura sugerida del proyecto
mi_facturador_cli/
└─ main.py
El archivo facturas.db se creará automáticamente en la misma carpeta al ejecutar el programa por primera vez.
_______________________________________________________________________________________
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
_______________________________________________________________________________________
🗄️ Esquema de base de datos

Tabla clients

id (INTEGER, PK, autoincrement)

name (TEXT, único, normalizado en Título)

phone (TEXT)

Tabla invoices

id (INTEGER, PK, autoincrement)

client_id (INTEGER, FK → clients.id)

date (TEXT, YYYY-MM-DD HH:MM:SS)

discount_pct (REAL) — % de descuento aplicado a la factura

iva_pct (REAL) — % de IVA

subtotal (TEXT) — valores monetarios guardados como texto decimal

discount (TEXT)

taxable_base (TEXT)

iva (TEXT)

total (TEXT)

Tabla items

id (INTEGER, PK, autoincrement)

invoice_id (INTEGER, FK → invoices.id)

code (TEXT)

description (TEXT)

unit_price (TEXT)

quantity (INTEGER)

line_total (TEXT)

Los montos se guardan como texto (string de Decimal) para preservar exactitud y formato.
_______________________________________________________________________________________
🔎 Consultas útiles (desde sqlite3)

Abrir consola SQLite:

sqlite3 facturas.db


Algunos ejemplos:

-- Ver clientes
SELECT * FROM clients;

-- Ver facturas con datos del cliente
SELECT i.id, i.date, c.name, i.subtotal, i.discount, i.taxable_base, i.iva, i.total
FROM invoices i
JOIN clients c ON c.id = i.client_id
ORDER BY i.id DESC;

-- Ver ítems de una factura (reemplaza 1 por el ID que corresponda)
SELECT code, description, unit_price, quantity, line_total
FROM items
WHERE invoice_id = 1;


Salir de la consola SQLite: .quit
_______________________________________________________________________________________
⚙️ Personalización

Descuento por defecto: cambia el valor por defecto en input_decimal(... default=Decimal("10")).

IVA por defecto: cambia default=Decimal("12").

Límite de productos: edita capturar_items(max_items=9).

Rangos y validaciones:

Cantidad: input_entero_rango("Cantidad: ", 1, 10**6)

Precios: input_decimal(... minimo=Decimal("0.00"))

Formato de nombre: se normaliza a Título (Michelle Toro) al guardar/mostrar.
_______________________________________________________________________________________
💰 Nota sobre manejo de dinero

El programa usa decimal.Decimal para evitar errores de redondeo de float.
Acepta coma (,) o punto (.) como separador decimal.
_______________________________________________________________________________________
🧩 Estructura del código (resumen de funciones)

calcular_descuento(monto_total, porcentaje_descuento) → Decimal

init_db() → crea tablas si no existen.

get_or_create_client(con, name, phone) → client_id (crea o actualiza).

insert_invoice(...) / insert_item(...) → inserción en BD.

capturar_items() → lista de productos (1–9).

calcular_totales(items, porcentaje_iva, porcentaje_descuento) → dict con totales.

imprimir_factura_en_consola(...) → salida formateada.

main() → orquesta el flujo.
_______________________________________________________________________________________
🧯 Solución de problemas

“No se reconoce ‘python’”
En Windows, prueba py en lugar de python, o agrega Python al PATH.

Bloqueo de BD (database is locked)
Asegúrate de no tener otra sesión abierta sobre el mismo archivo. Cierra programas que lo estén usando.

Valores inválidos
El programa valida campos numéricos; si ves un aviso, reingresa el valor.

Versión de Python
Usa Python 3.10 o superior.
_______________________________________________________________________________________
📌 Alcance y próximos pasos

Este proyecto es demostrativo y educativo. Posibles mejoras:

Generar PDF del RIDE.

Interfaz gráfica con customtkinter.

Exportar/consultar reportes por fechas o clientes.

Validación avanzada de campos y catálogos de productos.


