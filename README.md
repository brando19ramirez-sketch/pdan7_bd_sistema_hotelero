# 📊 CASO PROPUESTO "Sistema de Gestión de Reservas y Operaciones para Cadena Hotelera" 🏨

## 🏨 Contexto del negocio

**HospedaPerú** es una cadena hotelera con presencia en Lima, Cusco, Arequipa y Puno que opera hoteles de 3 y 4 estrellas. En los últimos años, la cadena ha experimentado un incremento en las reservas canceladas de último momento, una mala distribución de habitaciones entre temporadas y un control deficiente del estado de ocupación por sede.

Actualmente, el proceso de reservas es parcialmente manual: se gestiona por correo, llamadas y plataformas externas no integradas, lo que genera duplicidad, pérdida de ingresos y baja satisfacción del huésped.

Por ello, la cadena ha decidido desarrollar un **Sistema de Gestión de Reservas y Operaciones Hoteleras** que permita:

- Registrar y gestionar reservas de habitaciones en todas las sedes
- Controlar el estado de ocupación en tiempo real
- Administrar los servicios adicionales consumidos por el huésped
- Gestionar la facturación y el cobro por estadía
- Generar indicadores de ocupación, ingresos y satisfacción por sede

---

## 🎯 Objetivo del sistema

Diseñar una base de datos que permita:

- Registrar información completa de huéspedes y sus preferencias
- Gestionar la disponibilidad de habitaciones por sede y tipo
- Administrar el ciclo completo de una reserva (creación, check-in, check-out)
- Registrar los servicios consumidos durante la estadía
- Calcular el monto total a cobrar por estancia
- Generar indicadores de ocupación y rentabilidad por hotel

---

## 🧩 Alcance funcional

### 1. 👤 Gestión de Huéspedes

El sistema maneja dos tipos de huéspedes:

**Persona natural**
- DNI o pasaporte, nombres, apellidos, fecha de nacimiento
- Nacionalidad, contacto (email, teléfono)
- Preferencias de habitación

**Empresa (para reservas corporativas)**
- RUC, razón social, sector
- Contacto del representante

> Un huésped puede tener múltiples reservas a lo largo del tiempo.

---

### 2. 🏢 Gestión de Hoteles y Habitaciones

La cadena opera múltiples sedes. Cada **hotel** tiene:
- Nombre, ciudad, categoría (estrellas), dirección, capacidad total

Cada hotel cuenta con **tipos de habitación**:
- Simple, doble, suite, familiar
- Precio base por noche, capacidad máxima de personas, amenidades

Cada **habitación física** pertenece a un tipo y tiene:
- Número de habitación, piso, estado (disponible, ocupada, mantenimiento)

---

### 3. 📝 Reservas

Antes del check-in, el huésped realiza una reserva que incluye:
- Fecha de creación, fechas de entrada y salida
- Número de personas, habitación asignada
- Canal de reserva (web, teléfono, agencia, OTA)
- Estado (confirmada, cancelada, modificada, no-show)

> Cada reserva puede tener una o más habitaciones asignadas (grupos o familias).

---

### 4. 🛎️ Check-in / Check-out

Cuando se confirma el ingreso:
- Se registra el check-in (fecha/hora real de llegada, empleado responsable)
- Se asocian documentos de identidad presentados
- Al finalizar la estadía, se registra el check-out y se genera la liquidación

---

### 5. 🍽️ Servicios Adicionales

Durante la estadía el huésped puede consumir servicios extra:
- Restaurante, lavandería, spa, minibar, tours, estacionamiento
- Cada servicio tiene un precio unitario y una categoría
- Los consumos se registran con fecha, cantidad y monto

> Un consumo se asocia a la reserva activa del huésped.

---

### 6. 💳 Facturación y Pagos

Al momento del check-out se genera una **factura** que incluye:
- Costo total de la estadía (habitación × noches)
- Servicios adicionales consumidos
- Descuentos aplicados (convenios corporativos, fidelización)
- IGV y monto final

Los pagos pueden realizarse en partes o de una sola vez:
- Fecha de pago, monto, método (efectivo, tarjeta, transferencia, OTA)
- Una factura puede tener múltiples pagos (pago adelantado + saldo al salir)

---

### 7. ⭐ Satisfacción del Huésped

Tras el check-out, el sistema permite registrar:
- Encuesta de satisfacción (puntuación por limpieza, atención, instalaciones)
- Comentarios textuales
- Clasificación general del huésped (frecuente, VIP, nuevo)

---

## 📈 Reglas de negocio clave

| Regla | Descripción |
|-------|-------------|
| Huésped → Reservas | Un huésped puede tener **múltiples reservas**, pero cada reserva pertenece a un solo huésped o empresa |
| Reserva → Habitaciones | Una reserva puede incluir **una o más habitaciones**, pero cada habitación solo puede estar ocupada por una reserva activa a la vez |
| Habitación → Tipo | Cada habitación tiene **un solo tipo**, pero un tipo puede tener muchas habitaciones físicas |
| Estadía → Factura | Cada estadía genera **una sola factura**, pero esa factura puede tener **múltiples pagos** |
| Consumo → Reserva | Los servicios adicionales se consumen dentro de una reserva activa; no existe consumo sin reserva |
| Satisfacción → Reserva | El puntaje de satisfacción se registra **una sola vez por reserva**, post check-out |
| Mantenimiento | Una habitación en estado "mantenimiento" **no puede ser asignada** a ninguna reserva |
| Precio dinámico | El precio final puede variar respecto al precio base según temporada, descuentos o convenios corporativos |

---

## 🗂️ Estructura del repositorio

```
📁 DIAGRAMAS/          → Modelo entidad-relación y diagrama relacional
📁 OLTP/               → Scripts SQL (DDL, DML, procedimientos almacenados)
📁 COPIAS DE SEGURIDAD/ → Backups de los scripts
📄 README.md           → Descripción del caso
```

---

*Caso desarrollado como parte del curso de Base de Datos — PDAN7*
