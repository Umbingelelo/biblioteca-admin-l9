# biblioteca-admin

Microservicio administrador del broker (L8). NestJS 12, puerto 3020.

- `src/admin/rabbit-admin.service.ts`: toda la conversación con RabbitMQ. AMQP (`RABBIT_URL`) para
  crear y borrar; la API HTTP de management (`RABBIT_ADMIN_URL`) para listar.
- `src/admin/admin.controller.ts`: las ocho rutas de `/v1/admin`, sin una línea de `amqplib`.
- `src/admin/dto/`: los DTOs validados con `class-validator`; `ValidationPipe` global en `main.ts`.
- `src/auth/`: `JwtGuard` y `RolGuard` de L4; toda la clase exige el grupo `bibliotecarios`.

Arranque suelto: copiar `.env.example` a `.env`, rellenarlo, `npm install` y `npm run start:dev`.

Con todo el sistema: tiene `Dockerfile` y está en el `compose.yml` de `biblioteca-plataforma` (servicio `admin`,
puerto 3020), así que `docker compose up -d --build --wait` desde esa carpeta lo levanta junto al resto. El
compose le pasa `RABBIT_URL` y `RABBIT_ADMIN_URL` hacia `rabbit1`; del `.env` salen `COGNITO_ISSUER` y
`COGNITO_CLIENT_ID`.
