# Danger From The Deep - Godot Edition

![Estado del proyecto](https://img.shields.io/badge/Estado-En_Desarrollo-orange)
![Motor](https://img.shields.io/badge/Godot-4.x-%23478cbf)
![Licencia](https://img.shields.io/badge/Licencia-GPLv3-blue)
![Languages](https://img.shields.io/badge/Languages-ES%20|%20EN-blue)

> 🌐 **¿Prefer English?** [See English version](README.md)

**Danger From The Deep** es un esfuerzo comunitario para revivir y modernizar el clásico simulador de submarinos alemanes de la Segunda Guerra Mundial.

Este proyecto tiene como objetivo migrar el código y la lógica del juego original al motor **Godot Engine**, permitiendo una mayor compatibilidad multiplataforma, mejor rendimiento y facilidad para añadir nuevas características.

## 🎯 Objetivos del Proyecto

1.  **Migración al Motor Godot:** Portar completamente la base del código y los assets de "Danger from the Deep" a un proyecto funcional en Godot Engine.
2.  **Preservación:** Mantener la jugabilidad y la atmósfera del simulador original.
3.  **Mejoras y Expansión:** Implementar:
    *   Mejoras gráficas (iluminación, shaders, modelos de mayor calidad).
    *   Optimizaciones de rendimiento y jugabilidad.
    *   Corrección de bugs históricos del juego original.
    *   Nuevas misiones, barcos o mecánicas de juego.
4.  **Código Abierto:** Mantener el proyecto 100% libre y accesible para la comunidad.

## 📜 Licencia

Este proyecto es software libre. Está licenciado bajo los términos de la **GNU General Public License v3.0 (GPLv3)**.

Al contribuir en este repositorio, aceptas que tus contribuciones se publiquen bajo la misma licencia.

> **Nota:** Aunque el código es libre, por favor verifica la licencia de los assets (modelos 3D, texturas y sonidos) originales, ya que podrían tener restricciones diferentes al código fuente.

## 🚀 Cómo Contribuir

¡Las contribuciones son bienvenidas! Este es un proyecto ambicioso y la colaboración es clave. 

**Para contribuir al código, por favor lee nuestra [Guía de Contribución](CONTRIBUTING.es.md)** que incluye:

- 🌳 Flujo de trabajo con branches (cascade flow)
- ⚙️ Reglas de merge y validación automática
- 🤖 Workflows de GitHub Actions
- ✨ Mejores prácticas y convenciones

### Inicio Rápido

Si estás interesado en contribuir, ya sea con código, arte 2D/3D, sonido, documentación o ideas, sigue estos pasos:

1.  **Fork** este repositorio
2.  Crea una rama desde `pre-alpha` para tu funcionalidad (`git checkout -b feature/nueva-funcionalidad`)
3.  Realiza tus cambios y asegúrate de que el juego siga compilando
4.  Abre un **Pull Request** a `pre-alpha` explicando tus cambios

> 📖 **Documentación completa:** [CONTRIBUTING.es.md](CONTRIBUTING.es.md)

Si eres nuevo en Godot o en el proyecto, revisa la pestaña de "Issues" para ver en qué puedes ayudar.

¡Zarpa con nosotros en esta emocionante misión!

## 🛠️ Estado Actual

*   **Motor:** Godot 4.x (Stable)
*   **Funcionalidades básicas:** [En progreso / Por hacer]
*   **Gráficos:** [Migrando / Nativos]
*   **Branching:** Cascade flow con 6 branches (pre-alpha → alpha → beta → rc → rtm → main)
*   **CI/CD:** Validación automática de PRs con GitHub Actions

## 📦 Instalación

(Instrucciones breves sobre cómo clonar y ejecutar el proyecto)

```bash
git clone https://github.com/NippurElErrante/dftdg.git
cd dftdg
# Abre el proyecto en Godot y ejecuta
```

## 🙏 Créditos

Este proyecto es una adaptación y continuación de **Danger from the Deep**, 
un simulador de submarinos de la Segunda Guerra Mundial.

Todo el crédito por la idea original, gran parte del diseño y del código base
pertenece a los autores del proyecto original:

- Proyecto original: https://sourceforge.net/projects/dangerdeep/
- Autores originales: ver listado en el proyecto de SourceForge

Este repositorio se enfoca en portar y extender el juego usando el motor **Godot Engine**,
respetando la licencia original (GPL) y manteniendo el proyecto como software libre.

## Colaboradores de este repositorio

Gracias a todos los que han contribuido a este proyecto:

<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- Aquí GitHub puede generar automáticamente la lista de colaboradores -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

Para ver la lista completa de colaboradores, visita: [Colaboradores en GitHub](../../graphs/contributors)

Para una lista más detallada de autores y colaboradores, ver [CREDITS.md](./CREDITS.es.md).
