# AS_U3_EXAMEN_PRACTICO

# INFORME FINAL DE AUDITORÍA DE SISTEMAS

## CARÁTULA

**Entidad Auditada:** Chef_Vagrant_Wp Deployment  
**Ubicación:** [Ciudad, País]  
**Período auditado:** [20/06/2025 hasta 27/06/2025]  
**Equipo Auditor:** [Jean Pier Elias Valverde Zamora]  
**Fecha del informe:** [27/06/2025]  


## ÍNDICE

1. [Resumen Ejecutivo](#1-resumen-ejecutivo)  
2. [Antecedentes](#2-antecedentes)  
3. [Objetivos de la Auditoría](#3-objetivos-de-la-auditoría)  
4. [Alcance de la Auditoría](#4-alcance-de-la-auditoría)  
5. [Normativa y Criterios de Evaluación](#5-normativa-y-criterios-de-evaluación)  
6. [Metodología y Enfoque](#6-metodología-y-enfoque)  
7. [Hallazgos y Observaciones](#7-hallazgos-y-observaciones)  
8. [Análisis de Riesgos](#8-análisis-de-riesgos)  
9. [Recomendaciones](#9-recomendaciones)  
10. [Conclusiones](#10-conclusiones)  
11. [Plan de Acción y Seguimiento](#11-plan-de-acción-y-seguimiento)  
12. [Anexos](#12-anexos)  


## 1. RESUMEN EJECUTIVO

La auditoría realizada sobre el entorno Chef_Vagrant_Wp implementado por DevIA360 evidenció riesgos relevantes en la gestión de credenciales, configuraciones de red, registros de auditoría, actualización de software y segregación de ambientes. Se identificó exposición de datos sensibles en archivos de configuración, uso de versiones desactualizadas de aplicaciones y carencia de prácticas adecuadas de seguridad en la infraestructura.

Se recomienda aplicar medidas de mitigación urgentes para garantizar la seguridad, confidencialidad y cumplimiento normativo del entorno de despliegue continuo.
---

## 2. ANTECEDENTES

DevIA360 es una empresa dedicada al desarrollo e integración de soluciones tecnológicas, especializada en infraestructura automatizada para aplicaciones web. Como parte de sus servicios, DevIA360 emplea la solución Chef_Vagrant_Wp que automatiza el despliegue de entornos WordPress mediante herramientas como Vagrant y Chef.

El entorno de despliegue continuo es esencial para garantizar entregas ágiles, consistentes y seguras. No obstante, la complejidad de los procesos y la velocidad de implementación generan posibles vectores de riesgo que requieren ser auditados.
---

## 3. OBJETIVOS DE LA AUDITORÍA

**Objetivo General:**

- [Evaluar la seguridad, eficiencia y cumplimiento normativo del proceso de despliegue continuo de infraestructura WordPress mediante la solución Chef_Vagrant_Wp utilizada por DevIA360, identificando vulnerabilidades técnicas y configuracionales que puedan comprometer la confidencialidad, integridad o disponibilidad de los servicios desplegados.]

**Objetivos Específicos:**

- Revisar la configuración de redes privadas en el entorno Vagrant, identificando posibles deficiencias que impidan la conectividad entre máquinas virtuales o expongan servicios innecesariamente.

- Detectar la presencia de credenciales sensibles almacenadas en texto plano dentro de las recetas Chef o archivos de configuración, evaluando el riesgo de fuga de información confidencial.

- Verificar la existencia y correcto funcionamiento de mecanismos de logging y trazabilidad en las máquinas virtuales para facilitar auditorías y análisis forenses.

- Analizar la correcta segregación de ambientes (desarrollo, pruebas y producción) en las configuraciones de Vagrant y recetas Chef, a fin de evitar mezclas de datos sensibles entre entornos.

- Identificar la utilización de componentes de software o dependencias desactualizadas que puedan introducir vulnerabilidades conocidas en el entorno WordPress y en la infraestructura de soporte.

---

## 4. ALCANCE DE LA AUDITORÍA

- Entorno auditado: Chef-Vagrant-WordPress, incluyendo la infraestructura desplegada mediante Vagrant sobre VirtualBox y la automatización de la instalación de WordPress con Chef y WP-CLI.
- Revisión de:
  - Vagrantfile, para identificar configuraciones inseguras, exposición innecesaria de puertos y posibles errores en la definición de redes privadas.

  - Recetas Chef, incluyendo archivos attributes/default.rb y metadata.rb, para detectar almacenamiento de credenciales en texto plano, versiones desactualizadas de software y ausencia de segregación de ambientes (desarrollo, pruebas, producción).

  - Configuración de red privada, verificando la conectividad entre las máquinas virtuales definidas como database, wordpress y proxy, y evaluando riesgos de accesos no autorizados.

  - Accesos al entorno WordPress, validando el correcto funcionamiento de la instalación automatizada mediante WP-CLI y el acceso a la interfaz web, para confirmar la disponibilidad y seguridad del servicio.

  - Logs y monitoreo, revisando los archivos de registro generados en las máquinas virtuales para asegurar la trazabilidad de operaciones, identificación de errores y soporte a eventuales investigaciones de incidentes.

- Periodo auditado: [Desde 20/06/2025 hasta 27/06/2025]

---

## 5. NORMATIVA Y CRITERIOS DE EVALUACIÓN

- ISO/IEC 27001:2022
  Norma internacional que establece requisitos para un Sistema de Gestión de Seguridad de la Información (SGSI). Se utilizó como marco de referencia para evaluar la confidencialidad, integridad, disponibilidad y trazabilidad en el entorno Chef-Vagrant-WordPress, particularmente en aspectos relacionados con la protección de credenciales, segregación de ambientes y registros de auditoría.

 - OWASP ASVS 4.0.3 (Application Security Verification Standard)
   Estándar de seguridad de aplicaciones utilizado para analizar configuraciones, exposición de puertos, uso de versiones actualizadas de componentes y manejo seguro de credenciales en el proceso de despliegue automatizado.

 - Buenas prácticas DevOps
   Conjunto de prácticas orientadas a la integración segura y eficiente de desarrollo y operaciones. Fueron aplicadas como criterio para evaluar:

    - Gestión de infraestructura como código.

    - Separación de entornos (desarrollo, pruebas, producción).

    - Automatización de despliegues de manera segura.

    - Mantenimiento de logs y trazabilidad de cambios.

    - Políticas internas de seguridad (simuladas)
        Políticas definidas de forma simulada para este ejercicio práctico, utilizadas como criterio de evaluación para validar el cumplimiento de:

        - Protección de información sensible.

        - Restricciones de acceso a redes y servicios.

        - Uso de buenas prácticas en configuración de servidores y servicios web.

---

## 6. METODOLOGÍA Y ENFOQUE

La auditoría se realizó mediante un enfoque técnico y basado en riesgos, combinando análisis manual y ejecución de pruebas técnicas, orientadas a identificar vulnerabilidades en el entorno automatizado Chef-Vagrant-WordPress.

Las actividades específicas desarrolladas fueron:
- Revisión de archivos de configuración (Vagrantfile, recetas Chef).
    Para identificar configuraciones inseguras, exposición de servicios, errores en redes privadas, credenciales en texto plano y uso de versiones obsoletas de componentes.
- Inspección de variables de entorno y credenciales.
- Ejecución de comandos:
  - `vagrant up`
  - `vagrant status`
- Acceso a la interfaz WordPress.
- Captura de evidencias (screenshots).
- Análisis de logs.

---

## 7. HALLAZGOS Y OBSERVACIONES

### Hallazgo N°1 — Puertos expuestos innecesariamente

- **Descripción:** El archivo Vagrantfile expone el puerto 80 del guest al 8080 del host.
- **Evidencia:** [Ver Anexo X - Puertos Vagrantfile]
- **Grado de criticidad:** Medio
- **Criterio vulnerado:** Principio de mínimo privilegio.
- **Causa:** Configuración por defecto.
- **Efecto:** Posible acceso no autorizado desde host o red interna.

---

### Hallazgo N°2 — Credenciales en texto plano

- **Descripción:** Se encontraron credenciales hardcodeadas en archivos Chef.
- **Evidencia:** [Ver Anexo D - Credenciales texto plano]
- **Grado de criticidad:** Alto
- **Criterio vulnerado:** Confidencialidad de la información.
- **Causa:** Falta de uso de mecanismos seguros de vault o secrets manager.
- **Efecto:** Riesgo de robo de credenciales.

---

*(Agrega aquí todos tus hallazgos del examen práctico.)*

---

## 8. ANÁLISIS DE RIESGOS

| Hallazgo | Riesgo asociado | Impacto | Probabilidad | Nivel de Riesgo |
|----------|-----------------|---------|--------------|-----------------|
| 1 | Exposición de servicios innecesarios | Medio | Media | Medio |
| 2 | Robo de credenciales | Alto | Alta | Alto |

---

## 9. RECOMENDACIONES

| Hallazgo | Recomendación |
|----------|---------------|
| 1 | Cerrar puertos no utilizados y documentar exposición solo si es requerida. |
| 2 | Usar vaults o variables de entorno en lugar de credenciales en texto plano. |

---

## 10. CONCLUSIONES

[Conclusión breve sobre el estado general del entorno Chef-Vagrant-WordPress. Indicar si es seguro o presenta debilidades críticas.]

---

## 11. PLAN DE ACCIÓN Y SEGUIMIENTO

| Hallazgo | Recomendación | Responsable | Fecha Comprometida |
|----------|---------------|-------------|--------------------|
| 1 | Cerrar puertos no necesarios. | DevOps | [dd/mm/aaaa] |
| 2 | Migrar credenciales a vault. | DevOps | [dd/mm/aaaa] |

---

## 12. ANEXOS

- [Anexo A] Vagrant Status
- [Anexo B] Pantalla de WordPress en localhost:8080
- [Anexo C] Configuración de red
- [Anexo D] Credenciales en texto plano
- [Anexo E] Metadata.rb versiones
- [Anexo F] Logs
- [Anexo G] Segregación de ambientes
- Otros anexos según hallazgos

Todos los anexos se encuentran en la carpeta:

