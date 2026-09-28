# Guía para crear y entregar Pull Requests

Esta guía define el flujo que debe seguir un desarrollador desde que comienza una tarea asignada hasta que entrega el trabajo para revisión.

El objetivo es mantener trazabilidad entre **Issue → desarrollo → Pull Request → revisión → cierre**.

---

## 1. Antes de comenzar

La tarea debe:

- Estar registrada mediante un Issue.
- Estar asignada al desarrollador.
- Tener estado `Pendiente`.
- Tener el requerimiento y criterios de aceptación definidos.

Antes de realizar cambios, actualizar la rama `develop`:

```bash
git switch develop
git pull origin develop
```

Crear una rama asociada al Issue:

```bash
git switch -c feature/<numero-issue>-<descripcion>
```

Ejemplo para el Issue `#42`:

```bash
git switch -c feature/42-fondo-cajas
```

Una vez iniciado efectivamente el trabajo, cambiar el estado del Issue:

`Pendiente` → `En Desarrollo`

---

## 2. Desarrollo

Implementar únicamente el alcance definido en el Issue.

Si durante el desarrollo se detecta que:

- Falta información.
- Falta un endpoint.
- La API disponible no permite implementar el requerimiento.
- Es necesario modificar algo fuera del alcance.
- Existe un bloqueo que impide continuar.

Se debe informar antes de implementar una solución alternativa o modificar componentes fuera del alcance definido.

---

## 3. Pruebas antes de entregar

Antes de crear el Pull Request, el desarrollador debe probar personalmente la implementación.

Como mínimo debe verificar:

- El proyecto compila correctamente.
- La funcionalidad solicitada funciona.
- Se cumplen todos los criterios de aceptación del Issue.
- La integración con los servicios involucrados funciona correctamente.
- No se rompió funcionalidad relacionada.
- No quedaron cambios accidentales.
- No se incluyeron archivos que no corresponden a la tarea.

> [!IMPORTANT]
> La tarea no se considera terminada solamente porque el código esté escrito.

---

## 4. Revisar los cambios

Antes de realizar el commit:

```bash
git status
git diff
```

Revisar los archivos modificados y confirmar que todos corresponden al Issue.

Luego agregar los cambios:

```bash
git add .
```

Crear el commit utilizando un mensaje descriptivo.

Ejemplo:

```bash
git commit -m "feat: implementa gestion de fondo de cajas"
```

---

## 5. Actualizar la rama con `develop`

Antes de subir la rama, obtener los últimos cambios:

```bash
git fetch origin
git merge origin/develop
```

Si existen conflictos:

1. Resolver los conflictos.
2. Compilar nuevamente.
3. Volver a probar la funcionalidad.
4. Confirmar que los criterios de aceptación continúan cumpliéndose.

Luego subir la rama:

```bash
git push -u origin feature/42-fondo-cajas
```

---

## 6. Crear el Pull Request

Crear el Pull Request en GitHub.

### Rama base

```text
develop
```

### Rama de cambios

Ejemplo:

```text
feature/42-fondo-cajas
```

### Título

El título debe describir claramente la funcionalidad implementada.

Ejemplo:

```text
Implementar gestión de Fondo de Cajas
```

### Vincular el Issue

En la sección **Issue relacionado** del template utilizar:

```text
Closes #42
```

Reemplazando `42` por el número correspondiente.

Esto permite mantener la trazabilidad entre el Issue y el Pull Request.

---

## 7. Completar el template del Pull Request

El Pull Request debe utilizar el template definido por Kofmelk.

No eliminar sus secciones.

Se debe completar:

- Issue relacionado.
- Resumen.
- Cambios realizados.
- Validación realizada.
- Pruebas realizadas.
- Evidencia cuando corresponda.
- Observaciones relevantes.

### Pruebas realizadas

No utilizar descripciones genéricas como:

```text
Probado OK
```

Se deben indicar las pruebas realizadas concretamente.

Ejemplo:

```text
- Se creó un Fondo de Caja con imagen principal.
- Se creó un Fondo sin imágenes de entrenamiento.
- Se agregaron imágenes de entrenamiento.
- Se editó el código y estado de un Fondo existente.
- Se reemplazó la imagen principal.
- Se eliminaron imágenes de entrenamiento.
- Se verificó el límite máximo de 10 imágenes.
- Se eliminó un Fondo utilizando el modal de confirmación.
- Se verificó el filtro de búsqueda.
```

---

## 8. Evidencia

Cuando corresponda, adjuntar evidencia de las pruebas realizadas.

Por ejemplo:

- Capturas de pantalla.
- Resultado visual de la funcionalidad.
- Comportamiento antes/después.
- Información necesaria para reproducir la prueba.

La evidencia complementa las pruebas realizadas, pero **no reemplaza la revisión funcional posterior**.

---

## 9. Entregar a revisión

Una vez que:

- El desarrollo está terminado.
- El desarrollador realizó sus pruebas.
- Se cumplen los criterios de aceptación.
- La rama está actualizada.
- El Pull Request fue creado.
- El template está completo.
- Se adjuntó la evidencia necesaria.

Cambiar el estado del Issue:

`En Desarrollo` → `En Revisión`

A partir de ese momento comienza el proceso de revisión.

> [!IMPORTANT]
> El desarrollador no debe realizar el merge de su propio Pull Request.

---

## 10. Observaciones de revisión

Si durante la revisión se solicitan cambios, **no se debe crear un nuevo Pull Request**.

Las correcciones deben realizarse sobre la misma rama.

Ejemplo:

```bash
git add .
git commit -m "fix: corrige observaciones de revision"
git push
```

El Pull Request se actualizará automáticamente.

El desarrollador debe:

- Revisar todas las observaciones.
- Corregirlas.
- Probar nuevamente los cambios.
- Verificar que una corrección no afectó otra funcionalidad.
- Dejar nuevamente el Pull Request listo para revisión.

Las observaciones relacionadas con la aceptación del trabajo deben mantenerse registradas en GitHub.

---

## 11. Aprobación y cierre

La creación del Pull Request **no significa que la tarea esté terminada**.

La tarea finaliza cuando:

1. El código fue revisado.
2. Se realizó la validación funcional correspondiente.
3. Los criterios de aceptación fueron verificados.
4. Las observaciones fueron resueltas.
5. El Pull Request fue aprobado.
6. Los cambios fueron integrados mediante merge.

Entonces el Issue pasa a:

`Terminado`

---

## Flujo de trabajo

```text
Issue creado
    ↓
Backlog
    ↓
Asignación
    ↓
Pendiente
    ↓
Inicio del desarrollo
    ↓
En Desarrollo
    ↓
Desarrollo + pruebas del desarrollador
    ↓
Pull Request
    ↓
En Revisión
    ↓
Revisión de código + prueba funcional
    ↓
¿Existen observaciones?
    │
    ├── Sí → Corrección → nueva revisión
    │
    └── No
         ↓
      Aprobación
         ↓
       Merge
         ↓
     Terminado
```

---

## Regla principal

> [!IMPORTANT]
> **Crear el Pull Request significa entregar el trabajo para revisión, no terminar la tarea.**
>
> La tarea se considera terminada después de la revisión, validación funcional, aprobación y merge.
