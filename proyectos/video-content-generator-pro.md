# Video Content Generator Pro

Aplicación web que automatiza la creación de contenido para canales de YouTube y TikTok: genera guiones, prompts de imágenes y metadatos optimizados usando IA, para producir contenido de forma rápida y escalable.

**Ver el sitio:** <https://www.videogenpro.co>

## Qué incluye

- Generación de guiones, prompts de imágenes y metadatos con IA (texto, imágenes, transcripción y voz).
- Cuentas de usuario con registro mediante Google, GitHub, Microsoft y TikTok, y sesiones propias con JWT.
- Cobros con **Stripe, Wompi y MercadoPago**.
- Envío de correos transaccionales (Resend) y monitoreo de errores (Sentry).
- Instalable como aplicación web (PWA).

## Decisiones técnicas

- **Aplicación de una sola tecnología de punta a punta**: TypeScript en el cliente y en el servidor, con API tipada mediante tRPC, de modo que un cambio en el servidor se detecta al compilar el cliente.
- **Menos dependencia de una plataforma propietaria**: el proyecto nació sobre una plataforma de generación de aplicaciones con IA que ofrecía sus propios servicios internos. Reemplacé cada uno por un servicio estándar (modelos de OpenAI, almacenamiento en Amazon S3, correo con Resend) y documenté qué variable de entorno controla cada pieza.
- **Pruebas en dos niveles**: pruebas unitarias y de integración con Vitest, y pruebas de extremo a extremo con Playwright.
- **Base de datos con migraciones** mediante Drizzle ORM, compatible con varios proveedores de MySQL.

## Tecnologías

TypeScript, React 19, Vite, Tailwind CSS, Radix UI, Express, tRPC, MySQL, Drizzle ORM, Stripe, Wompi, MercadoPago, OAuth, JWT, Sentry, Vitest, Playwright, Docker, Railway.

## Sobre el código

El repositorio es privado porque contiene configuración de cobros y de servicios en producción. Puedo mostrarlo y explicarlo en una entrevista.
