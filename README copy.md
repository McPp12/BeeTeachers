# BeeTeacher — Entregable 1

Aplicación académica de tutorías, consulta de salones, agenda y bitácora.
Esta versión parte de una base existente cuyo README identifica DICIS-Tracker
(https://github.com/moraxh/DICIS-Tracker) como antecedente. Conservar la atribución
y verificar las licencias aplicables. Las aportaciones E1 se documentan en PR.

## Alcance
Arquitectura prevista: JSON + Google Forms/Sheets + localStorage. No requiere base de datos ni cuentas de usuario.
Agenda, bitácora y favoritos se guardan en el navegador. No compartir datos reales.
La disponibilidad de aulas es una estimación por horario, no un sensor en tiempo real.
Se conservan los enlaces y sincronización existentes de Google Forms/Sheets. Para pruebas de escritura, configurar formularios propios y verificar sus permisos; no enviar datos de prueba a formularios ajenos.

## Instalar
Node 22 (ver frontend/.nvmrc), pnpm 10.11.0, Git.

```powershell
cd frontend
npx --yes pnpm@10.11.0 install --frozen-lockfile
npx --yes pnpm@10.11.0 run dev
```

Abrir http://localhost:3000. No abrir archivos con doble clic.

## Comprobar
```powershell
npx --yes pnpm@10.11.0 run typecheck
npx --yes pnpm@10.11.0 run build
# Al integrar PR E1-07:
npx --yes pnpm@10.11.0 test
# Con servidor iniciado en otra terminal:
node tests/api-smoke.mjs
```

## Estructura real
- frontend/src/app: páginas y Route Handlers de Next.js.
- frontend/src/backend: modelos, repositorios, servicios y validación.
- frontend/src/components: componentes de interfaz.
- frontend/src/hooks: agenda, bitácora, favoritos y otros hooks.
- frontend/src/data: respaldo local de tutores y horarios/aulas del proyecto; evitar datos personales en Git.
- scrapper: extracción de horarios y sincronización; revisar anonimización antes de activar publicación automática.
- frontend/tests: validaciones y smoke de API después de integrar E1-07.

## Flujo de contribución
Issue -> feature nacida de develop -> PR hacia develop -> revisión de compañero
-> CI -> merge. No trabajar directamente sobre master. Cierres E1 y E2 mediante
PR a master; E3 mediante release/1.0.0 y etiqueta v1.0.0 sobre master.

## Próximas entregas
E2 mejora la sincronización CSV, filtros, fechas/semanas de agenda, respaldos y exportación CSV de bitácora.
E3 integra el recorrido de contacto, agenda y bitácora, verifica actualización de horarios,
PWA y documentación y publica release/1.0.0 y v1.0.0.
El contacto externo no confirma automáticamente una asesoría; el acuerdo se registra manualmente.
Las limitaciones de localStorage y el respaldo local ante fallos de Sheets se documentan explícitamente.
