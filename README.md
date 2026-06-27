# AI Invoice Management System

Sistema de gestión de facturación automatizado con IA, construido para PYMEs y autónomos del sector hostelería. Convierte mensajes de texto enviados por Telegram en facturas formales en PDF, con cálculo fiscal automático y archivo centralizado.

## El problema

Los negocios pequeños (restaurantes, hostelería, servicios) suelen gestionar su facturación manualmente: cálculo de IVA a mano, redacción de cada factura desde cero, archivo desordenado de documentos y seguimiento impreciso de qué se ha facturado y qué no. Esto consume tiempo administrativo que un negocio pequeño no siempre puede permitirse.

## La solución

Un flujo conversacional por Telegram donde el negocio describe los datos del servicio en lenguaje natural (cliente, importe, fecha, forma de pago...) y el sistema:

1. **Interpreta el mensaje** mediante parsing de texto flexible (reconoce múltiples formatos y sinónimos: "comensales", "pax", "asistentes", etc.)
2. **Calcula automáticamente** la base imponible, el IVA y el desglose por persona
3. **Genera una vista previa** de la factura para que el usuario confirme o cancele antes de emitirla
4. **Crea el PDF** de la factura con diseño profesional (vía Gotenberg)
5. **Archiva el PDF** en Google Drive y registra los datos en Google Sheets para seguimiento fiscal
6. **Numera correlativamente** cada factura de forma automática, consultando el último número emitido

El sistema está en producción, usado activamente por el equipo de un negocio real (5-6 usuarios).

## Stack técnico

- **n8n** — orquestación del workflow completo (21 nodos: triggers, lógica condicional, procesamiento de datos)
- **Telegram Bot API** — interfaz conversacional de entrada y confirmación
- **JavaScript (Code nodes)** — parsing de texto en lenguaje natural, normalización de datos, cálculos fiscales
- **Gotenberg** — generación de PDF a partir de HTML
- **Google Sheets API** — registro y numeración correlativa de facturas
- **Google Drive API** — almacenamiento centralizado de PDFs generados

## Características destacadas

- **Parsing flexible de texto**: reconoce decenas de sinónimos y formatos distintos para cada campo (cliente, NIF, comensales, importe, fecha, forma de pago), incluyendo números en formato europeo (1.234,56€) y americano
- **Soporte multi-factura**: permite generar varias facturas en un solo mensaje, separadas por palabras clave ("primera", "segunda"...)
- **Flujo de confirmación**: ninguna factura se emite sin que el usuario confirme la vista previa, evitando errores
- **Cálculo fiscal automático**: desglose de base imponible e IVA (10%, configurable) a partir del importe total o del precio por persona
- **Manejo de errores guiado**: si el mensaje no se puede interpretar, el sistema responde con un ejemplo claro del formato esperado

## Nota sobre privacidad

Este repositorio contiene una versión del workflow **limpia de datos reales**: nombres de negocio, NIFs, direcciones, teléfonos, emails, IDs de hojas de cálculo y credenciales han sido sustituidos por placeholders genéricos. La lógica y estructura del sistema son las que están en producción.

## Autor

Hugo Gallardo Douville — [LinkedIn](https://linkedin.com/in/hugogallardo-douville)

Proyecto desarrollado como parte de **Aurial**, iniciativa propia de automatización con IA para pequeñas empresas.
