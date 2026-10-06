# Cercia Stock Sync Bot

Bot que mantiene el inventario de una tienda en línea sincronizado con un marketplace que **no ofrece API**. Cada vez que cambia un producto en la tienda, el bot replica el cambio en el marketplace casi al instante, manejando el navegador como lo haría una persona.

## El problema

Cada venta o cambio de stock había que repetirlo a mano en el marketplace; si se olvidaba, se podía vender algo que ya no había.

## Cómo funciona

1. Un **trigger de PostgreSQL** registra en una cola cada cambio relevante de un producto (creación, cambio de existencias, activación, desactivación o eliminación).
2. Un segundo trigger avisa con **LISTEN/NOTIFY** apenas se inserta una fila, así que el bot reacciona en segundos sin estar consultando todo el tiempo. Además revisa la cola cada 5 minutos como respaldo, por si se pierde un aviso.
3. El bot, un proceso que corre de forma permanente en un contenedor, agrupa los cambios pendientes por producto, decide **una sola acción** por producto (por ejemplo, eliminar tiene prioridad sobre actualizar stock) y la aplica en el marketplace con **Playwright**.
4. Mantiene una sola sesión abierta y la renueva sola si expira.

## Detalles de confiabilidad

- Si el inicio de sesión falla, no reintenta sin parar ni improvisa otra forma de entrar: marca el estado como bloqueado y la alerta aparece en el panel de la tienda.
- Eliminar un producto en la tienda lo **desactiva** en el marketplace en vez de borrarlo, para no perder ventas o reseñas asociadas.
- Cada acción que ejecuta queda en un registro de auditoría compartido con el sistema principal.
- Una auditoría diaria compara el stock de todo el catálogo contra el del marketplace; solo corrige automáticamente el caso peligroso (el marketplace con más stock del real) y reporta el resto.
- Espera a que la página termine de cargar antes de iniciar sesión, para evitar un fallo de arranque en frío en el que el formulario se enviaba antes de tiempo y dejaba las credenciales en la dirección web.

## Tecnologías

Node.js, Playwright, PostgreSQL (triggers y LISTEN/NOTIFY), Docker, Railway.

## Sobre el código

Es privado porque se conecta con cuentas reales. Puedo mostrarlo y explicarlo en una entrevista.
