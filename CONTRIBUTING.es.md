# 🤝 Guía de Contribución

[![Branching Strategy](https://img.shields.io/badge/Branching-Cascade_Flow-blue)](CONTRIBUTING.es.md)
[![Workflows](https://img.shields.io/badge/GitHub_Actions-Automated-green)](../../actions)

> 🌐 **Prefer English?** [See English version](CONTRIBUTING.md)

Gracias por tu interés en contribuir a **Danger From The Deep - Godot Edition**. Este documento describe el flujo de trabajo, las convenciones y las mejores prácticas para colaborar en este proyecto.

---

## 📋 Tabla de Contenidos

- [Flujo de Trabajo con Branches](#-flujo-de-trabajo-con-branches)
- [Estructura de Branches](#-estructura-de-branches)
- [Reglas de Merge](#-reglas-de-merge)
- [Cómo Contribuir](#-cómo-contribuir)
- [Workflows Automatizados](#-workflows-automatizados)
- [Resolución de Conflictos](#-resolución-de-conflictos)
- [Mejores Prácticas](#-mejores-prácticas)

---

## 🌳 Flujo de Trabajo con Branches

Este proyecto utiliza un **flujo de cascade (cascada)** con 6 branches principales que representan diferentes etapas del desarrollo:

```
pre-alpha → alpha → beta → rc → rtm → main
```

### Orden de Cascade

Los cambios deben fluir secuencialmente a través de las ramas:

1. **pre-alpha** - Desarrollo activo y experimental
2. **alpha** - Pruebas internas y estabilización
3. **beta** - Pruebas externas y feedback de la comunidad
4. **rc** - Release Candidate (candidato a release)
5. **rtm** - Release To Manufacturing (listo para producción)
6. **main** - Versión estable en producción

---

## 🔧 Estructura de Branches

### Branches Protegidos (No se pueden eliminar)

| Branch | Propósito | Estabilidad | Commits Directos | PRs |
|--------|-----------|-------------|------------------|-----|
| `pre-alpha` | Desarrollo activo, features experimentales | Inestable | ✅ Permitido | ✅ Validados |
| `alpha` | Pruebas internas, features completos | Baja | ✅ Permitido | ✅ Validados |
| `beta` | Pruebas públicas, corrección de bugs | Media | ✅ Permitido | ✅ Validados |
| `rc` | Release candidate, testing final | Alta | ✅ Permitido | ✅ Validados |
| `rtm` | Release to manufacturing | Muy Alta | ✅ Permitido | ✅ Validados |
| `main` | Código en producción | Estable | ❌ **Bloqueado** | ✅ **Solo PRs** |

> ⚠️ **Importante:** La rama `main` **NO acepta commits directos**. Todos los cambios deben ingresar mediante Pull Requests aprobados.

### Branches Temporales

Puedes crear branches temporales para desarrollar features, fixes o experimentos:

**Nomenclatura recomendada:**

```bash
feature/nombre-descriptivo      # Nueva funcionalidad
fix/descripcion-bug              # Corrección de bugs
hotfix/issue-critico             # Corrección urgente
refactor/mejora-codigo           # Refactorización
docs/actualizacion-docs          # Documentación
test/nuevas-pruebas              # Tests
experiment/idea-nueva            # Experimentación
```

**Ejemplos:**
```bash
feature/submarine-torpedos
fix/collision-detection-bug
hotfix/memory-leak-critical
docs/update-api-documentation
```

---

## ⚙️ Reglas de Merge

### ✅ Permitido

1. **Feature branches → pre-alpha**
   ```bash
   feature/nueva-funcionalidad → pre-alpha ✅
   ```
   - Todas las nuevas features deben ir primero a `pre-alpha`

2. **Cascade secuencial entre branches protegidos**
   ```bash
   pre-alpha → alpha ✅
   alpha → beta ✅
   beta → rc ✅
   rc → rtm ✅
   rtm → main ✅ (solo mediante PR)
   ```

3. **Commits directos a branches de desarrollo**
   ```bash
   git checkout alpha
   git commit -m "fix: corrección menor"
   git push origin alpha ✅
   ```
   - Puedes hacer commits directos a: `pre-alpha`, `alpha`, `beta`, `rc`, `rtm`
   - ⚠️ **Excepción**: `main` solo acepta cambios mediante Pull Requests

### ❌ Bloqueado

1. **Feature branches a otras ramas que no sean pre-alpha**
   ```bash
   feature/nueva → alpha ❌
   feature/nueva → main ❌
   ```

2. **Saltar niveles en el cascade**
   ```bash
   pre-alpha → beta ❌  (salta alpha)
   alpha → rc ❌        (salta beta)
   beta → main ❌       (salta rc y rtm)
   ```

3. **Merge en dirección inversa**
   ```bash
   main → rtm ❌
   beta → alpha ❌
   ```

4. **Commits directos a main**
   ```bash
   git checkout main
   git commit -m "fix"
   git push origin main ❌
   ```
   - `main` es una **rama protegida** que solo acepta cambios mediante Pull Requests aprobados
   - GitHub bloqueará automáticamente cualquier intento de commit directo

5. **Eliminar branches protegidos**
   ```bash
   git push origin --delete main ❌
   git push origin --delete pre-alpha ❌
   ```

---

## 🚀 Cómo Contribuir

### Paso 1: Fork y Clone

```bash
# Fork el repositorio en GitHub (botón "Fork")

# Clonar tu fork
git clone https://github.com/TU_USUARIO/dftdg.git
cd dftdg

# Agregar upstream
git remote add upstream https://github.com/NippurElErrante/dftdg.git
```

### Paso 2: Crear Branch de Feature

```bash
# Actualizar pre-alpha
git checkout pre-alpha
git pull upstream pre-alpha

# Crear tu branch
git checkout -b feature/mi-nueva-funcionalidad
```

### Paso 3: Desarrollar

```bash
# Hacer cambios
# ... editar archivos ...

# Commit frecuentes
git add .
git commit -m "feat: agregar nueva funcionalidad X"

# Push a tu fork
git push origin feature/mi-nueva-funcionalidad
```

### Paso 4: Crear Pull Request

1. Ve a GitHub en tu fork
2. Click en **"Compare & pull request"**
3. **Base**: `pre-alpha` (del repo original)
4. **Compare**: `feature/mi-nueva-funcionalidad` (de tu fork)
5. Agrega descripción detallada
6. Click **"Create pull request"**

### Paso 5: Validación Automática

El sistema ejecutará automáticamente:

- ✅ **Validate Cascade Order** - Verifica que el PR siga las reglas de cascade
- ✅ Tests automatizados (si están configurados)

**Si el check pasa:** ✅ Tu PR puede ser mergeado  
**Si el check falla:** ❌ Revisa el error y corrige el destino del PR

### Paso 6: Revisión y Merge

- Un maintainer revisará tu código
- Puede solicitar cambios
- Una vez aprobado, se hará merge a `pre-alpha`
- El cascade a otras ramas se hará manualmente cuando sea apropiado

---

## 🤖 Workflows Automatizados

### 1. Validate Cascade Order

**Se ejecuta:** Automáticamente en cada Pull Request

**Función:** Valida que el PR siga el orden correcto de cascade

**Resultados:**
- ✅ **Pasa** - PR correcto, puede mergearse
- ❌ **Falla** - PR incorrecto, botón de merge bloqueado

**Ejemplo de error:**
```
ERROR: Cannot skip levels. pre-alpha must go to next level first
Expected target: alpha
```

### 2. Cascade Merge (Manual)

**Se ejecuta:** Manualmente desde GitHub Actions

**Función:** Crear PRs en cascada o hacer merge directo entre ramas

**Cómo usarlo:**

1. Ve a **Actions** → **Cascade Merge**
2. Click **"Run workflow"**
3. Configura:
   - **source_branch**: Desde dónde iniciar (ej: `pre-alpha`)
   - **target_branch**: Hasta dónde llegar (vacío = hasta `main`)
   - **mode**: 
     - `create-prs` - Crea PRs para revisión manual (recomendado)
     - `direct-merge` - Merge directo sin PRs (solo emergencias)
4. Click **"Run workflow"**

**Ejemplo de uso:**

Para propagar cambios de `pre-alpha` a todas las demás ramas:

```
source_branch: pre-alpha
target_branch: (vacío)
mode: create-prs
```

Esto creará automáticamente:
- PR #1: pre-alpha → alpha
- PR #2: alpha → beta
- PR #3: beta → rc
- PR #4: rc → rtm
- PR #5: rtm → main

Luego puedes revisar y mergear cada PR manualmente.

---

## 🔧 Resolución de Conflictos

### Durante el Desarrollo

Mantén tu branch actualizado con `pre-alpha`:

```bash
git checkout feature/mi-feature
git fetch upstream
git merge upstream/pre-alpha
# Resolver conflictos si los hay
git push origin feature/mi-feature
```

### Durante el Cascade

Si hay conflictos durante el cascade, el workflow automático:

1. **Detecta el conflicto**
2. **Crea un PR** en lugar de hacer merge directo
3. **Tú resuelves** los conflictos manualmente
4. **Mergeas** el PR después de resolver

---

## ✨ Mejores Prácticas

### Commits

✅ **Usar mensajes descriptivos**
```bash
# Bueno
git commit -m "feat: agregar sistema de torpedos al submarino"
git commit -m "fix: corregir colisión con icebergs"
git commit -m "docs: actualizar guía de instalación"

# Malo
git commit -m "cambios"
git commit -m "fix"
git commit -m "update"
```

✅ **Convención de commits** (recomendado):
- `feat:` - Nueva funcionalidad
- `fix:` - Corrección de bug
- `docs:` - Documentación
- `style:` - Formato, punto y coma faltante, etc.
- `refactor:` - Refactorización de código
- `test:` - Agregar tests
- `chore:` - Tareas de mantenimiento

### Pull Requests

✅ **PR pequeños y enfocados**
- Un PR = Una funcionalidad o fix
- Más fácil de revisar
- Más rápido de mergear

✅ **Descripción clara**
```markdown
## Descripción
Implementa el sistema de torpedos para el submarino U-Boot.

## Cambios
- Añade clase `Torpedo` con física realista
- Implementa UI para lanzamiento de torpedos
- Agrega efectos de sonido y visuales

## Tests
- [x] Tests unitarios para clase Torpedo
- [x] Tests de integración con sistema de combate
- [x] Prueba manual en escenario de batalla

## Screenshots
![torpedo-ui](link-a-imagen)
```

### Branches

✅ **Nombres descriptivos**
```bash
# Bueno
feature/submarine-damage-system
fix/sonar-display-rendering-bug

# Malo
feature/stuff
fix/bug
my-branch
```

✅ **Eliminar branches después de merge**
```bash
# Después de que tu PR fue mergeado
git checkout pre-alpha
git pull upstream pre-alpha
git branch -d feature/mi-feature
git push origin --delete feature/mi-feature
```

### Testing

✅ **Probar antes de hacer PR**
- Compilar el proyecto
- Ejecutar tests existentes
- Probar la funcionalidad manualmente
- Verificar que no rompiste nada existente

---

## 📊 Flujo Completo Ejemplo

```bash
# 1. Actualizar pre-alpha
git checkout pre-alpha
git pull upstream pre-alpha

# 2. Crear feature branch
git checkout -b feature/new-sonar-display

# 3. Desarrollar
# ... hacer cambios ...
git add .
git commit -m "feat: implement new sonar display with better graphics"

# 4. Push
git push origin feature/new-sonar-display

# 5. Crear PR en GitHub
#    Base: pre-alpha
#    Compare: feature/new-sonar-display

# 6. Esperar revisión y merge

# 7. (Opcional) Un maintainer ejecuta Cascade Merge
#    Esto propaga los cambios de pre-alpha → alpha → beta → rc → rtm → main

# 8. Limpiar tu branch local
git checkout pre-alpha
git pull upstream pre-alpha
git branch -d feature/new-sonar-display
git push origin --delete feature/new-sonar-display
```

---

## 🔐 Protecciones de Branches

### Configuración Actual

| Protección | Ramas Afectadas | Descripción |
|------------|-----------------|-------------|
| **No eliminar** | Todas (pre-alpha → main) | No se pueden borrar las 6 ramas principales |
| **Validación de cascade** | Todas (pre-alpha → main) | Los PRs deben seguir el orden secuencial |
| **Solo PRs** | **main** únicamente | Commits directos bloqueados, solo PRs aprobados |

### Rulesets Activos

1. **protected-branches-no-delete**: Previene eliminación de ramas principales
2. **require-cascade-checks**: Valida orden en Pull Requests
3. **main-require-pull-requests**: Bloquea commits directos a main

---

## 🆘 ¿Necesitas Ayuda?

- 💬 **Issues**: [Crear un issue](../../issues/new)
- 📖 **Documentación**: Ver [README](README.es.md)
- 🐛 **Reportar bug**: [Bug report template](../../issues/new?template=bug_report.md)
- 💡 **Sugerir feature**: [Feature request template](../../issues/new?template=feature_request.md)

---

## 📜 Licencia

Al contribuir a este proyecto, aceptas que tus contribuciones se publiquen bajo la **GNU General Public License v3.0 (GPLv3)**.

Ver [LICENSE](LICENSE) para más detalles.

---

## 🙏 Agradecimientos

¡Gracias por contribuir a **Danger From The Deep - Godot Edition**! Tu aporte ayuda a mantener vivo este clásico simulador de submarinos.

**¡Zarpa con nosotros en esta emocionante misión! ⚓🌊**
