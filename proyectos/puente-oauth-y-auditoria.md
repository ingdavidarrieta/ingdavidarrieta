# Puente OAuth y auditoría de márgenes

Dos herramientas pequeñas en Python para una tienda de Shopify.

## Puente OAuth de un solo uso

Servicio mínimo en Flask que sirve de punto de retorno (callback) del flujo OAuth de Shopify: recibe el código de autorización, lo cambia por un token de la Admin API llamando a Shopify de servidor a servidor, lo muestra una sola vez en pantalla y **no guarda nada**. Está pensado para apagarse o borrarse después de usarlo, para que el token nunca quede almacenado en un servicio.

## Auditoría de márgenes

Scripts que leen el catálogo de la tienda y calculan, por producto, el margen real después de comisiones, costo de envío absorbido y pasarela de pago, y proponen un **precio sugerido** para alcanzar el margen objetivo. Los cálculos se hacen localmente en Python, sin pasar los datos crudos del catálogo por servicios externos.

## Tecnologías

Python, Flask, OAuth 2.0, API de Shopify (Admin GraphQL), procesamiento de datos con JSON.

## Sobre el código

Es privado porque se relaciona con cuentas y con las reglas de precios del negocio. Puedo mostrarlo y explicarlo en una entrevista.
