# Estándares de Gobernanza y Desarrollo

## 1. Visión General
Este documento establece los protocolos técnicos y operativos para todos los proyectos bajo la organización **Misionary**. El objetivo de estos estándares es garantizar despliegues ágiles, seguridad en la infraestructura y alta satisfacción del cliente final.

## 2. Propiedad del Código y Repositorios
Para asegurar la continuidad operativa y evitar bloqueos de infraestructura (ej. validaciones 2FA de terceros), se establece la siguiente política de alojamiento:
* **Centralización:** Todos los repositorios de código de clientes deben residir bajo la organización de GitHub `misionary-dev`.
* **Accesos:** Los permisos se otorgan mediante el principio de menor privilegio, administrados exclusivamente por el Project Lead.

## 3. Entornos y Despliegues (Railway & n8n)
La infraestructura se gestiona priorizando la automatización y la separación de entornos.

### 3.1 Integración y Despliegue Continuo (CI/CD)
* **Despliegue Automático:** La rama `main` de cada repositorio está conectada directamente a Railway. Todo código fusionado o empujado a `main` activa un despliegue automático a producción.
* **Separación de Entornos:** Los proyectos deben apuntar a una arquitectura de dos instancias en Railway:
  1. **Demo (Staging):** Entorno de pruebas y validación manual.
  2. **Producción:** Entorno estable de cara al cliente.

### 3.2 Gestión de Automatizaciones (n8n)
* Los flujos de trabajo en n8n se gestionan, mantienen y versionan directamente dentro de la instancia de n8n alojada. 
* No es requisito versionar los archivos `.json` de n8n en repositorios de GitHub, a menos que se destinen a plantillas de código abierto.

## 4. Ciclo de Vida del Código y Revisiones
La calidad del código es una responsabilidad compartida, apoyada por herramientas modernas y revisión cruzada.

* **Revisión de Pares (Cross-Review):** Los desarrollos implementan un modelo de revisión cruzada donde el equipo de Frontend audita integraciones de Backend, y viceversa.
* **Asistencia de IA:** Se fomenta el uso de herramientas de Inteligencia Artificial para tareas de depuración (debugging) previas a la revisión humana.
* **Trazabilidad:** Toda tarea o modificación debe estar respaldada por un "Issue" documentado. El ciclo de vida de la tarea finaliza únicamente cuando se cierra el Issue correspondiente.

## 5. Criterios de Aceptación ("Definition of Done")
Un desarrollo o funcionalidad se considera finalizado ("Done") cuando cumple las siguientes condiciones:
1. Ha superado la validación manual exhaustiva en el entorno **Demo**.
2. Ha sido desplegado en **Producción** sin arrojar errores críticos.
3. El cliente no reporta problemas de usabilidad o funcionalidad.
*Nota técnica:* Las oportunidades de mejora en el rendimiento (performance) identificadas post-despliegue se documentarán como nueva deuda técnica para futuras iteraciones, asumiendo una mentalidad de mejora continua.

## 6. Seguridad y Gestión de Secretos
La exposición de credenciales es un riesgo inaceptable.
* **Variables de Entorno:** Las claves de API (Mercado Pago, Gmail, integraciones) y credenciales de bases de datos deben inyectarse exclusivamente a través de variables de entorno en Railway o n8n.
* **Control de Acceso:** El acceso a la lectura y modificación de estas variables está restringido únicamente al Project Lead. Queda estrictamente prohibido compartir secretos en repositorios o canales de texto.

## 7. Comunicación y Protocolo de Emergencias

### 7.1 Comunicación Estándar
* **Asíncrona:** GitHub Issues para el seguimiento técnico.
* **Síncrona:** Grupo oficial de WhatsApp para la coordinación del equipo.

### 7.2 Resolución de Urgencias (Hotfixes)
Ante la caída de un sistema en producción (ej. fuera de horario comercial):
1. **Coordinación Inmediata:** El Project Manager y el desarrollador disponible establecen contacto directo.
2. **Acción Prioritaria:** Se evaluará la ruta más eficiente para restaurar el servicio: aplicar un parche rápido directo a `main` (Hotfix) o revertir el despliegue a la versión anterior (Rollback) desde el panel de Railway.
3. **Post-mortem:** Una vez estabilizado el sistema, se documentará el incidente para prevenir futuras ocurrencias.
