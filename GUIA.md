# 🛠️ Guía práctica — Taller de Git
### FLISOL 2026 · 10ª Edición · Club de Programación UNViMe

> Esta guía te lleva desde cero hasta abrir tu primer Pull Request.  
> Seguí los pasos en orden. Si algo no funciona, levantá la mano — cada error es parte del aprendizaje.

---

## Antes de empezar

Verificá que Git está instalado abriendo una terminal y corriendo:

```bash
git --version
```

Deberías ver algo como `git version 2.x.x`. Si aparece un error, avisá a un facilitador.

---

## Paso 1 — Configuración inicial

La primera vez que usás Git en una computadora hay que presentarse. Git va a guardar tu nombre y tu email en cada commit que hagas.

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
```

**¿Por qué importa?**  
Cada commit queda firmado con estos datos. En proyectos colaborativos es la forma de saber quién hizo qué cambio y cuándo.

Para verificar que quedó bien guardado:

```bash
git config --global --list
```

---

## Paso 2 — Clonar el repositorio

Clonar significa descargar una copia completa del repositorio a tu computadora, incluyendo todo el historial de cambios.

```bash
git clone https://github.com/pabloesanabriaq/flisol-2026-git-workshop
```

> 📝 Reemplazá la URL con la que te da el facilitador.

Entrá a la carpeta que se creó:

```bash
cd flisol-2026-git-workshop
```

Ahora tenés el proyecto completo en tu máquina. Verificá qué hay adentro:

```bash
ls
```

Deberías ver tres archivos:
- `index.html` — la página del FLISOL
- `style.css` — los estilos de esa página
- `FLISOL.md` — información del evento en texto plano

---

## Paso 3 — Explorar el proyecto y encontrar los errores

Tomá unos minutos para revisar los archivos **antes** de corregir nada.

**Si sabés un poco de HTML/CSS:**  
Abrí `index.html` en el navegador. ¿Ves algo raro? Explorá también `style.css` en un editor de texto.

**Si no sabés nada de programación:**  
Abrí `FLISOL.md` en cualquier editor de texto (el Bloc de Notas funciona). Leé el contenido y buscá errores de tipeo.

### 🔍 Pista — qué buscar

| Archivo | Error |
|---------|-------|
| `style.css` | El header tiene `display: block` — debería ser `display: flex` |
| `index.html` | Un div tiene `margin-left: 9999px` — lo manda fuera de la pantalla |
| `FLISOL.md` | La palabra "décima" está escrita como "desima" |
| `FLISOL.md` | El nombre de la ciudad tiene un error de tipeo |

> 💬 **Momento de discusión** — Antes de tocar nada: ¿cómo describirías este error si le explicaras a alguien qué cambio vas a hacer? Eso es exactamente lo que va a ir en tu mensaje de commit.

---

## Paso 4 — Crear tu propia rama

Nunca trabajes directamente sobre `main`. Las ramas te permiten trabajar de forma aislada sin afectar a nadie más.

Primero, verificá en qué rama estás:

```bash
git status
```

La primera línea dice `On branch main`. Ahora creá tu rama con un nombre descriptivo:

```bash
git checkout -b fix/tu-nombre-descripcion-del-error
```

**Ejemplos de nombres de rama:**
```
fix/ana-header-css
fix/carlos-typo-markdown
fix/sofia-margin-viewport
```

> 💡 Usá letras minúsculas, guiones en lugar de espacios, y sé descriptivo. Los nombres de rama son comunicación.

Verificá que el cambio funcionó:

```bash
git status
```

Ahora la primera línea dice `On branch fix/tu-nombre-...` — estás en tu propia rama. Los cambios que hagas acá no afectan `main` ni a nadie más.

---

## Paso 5 — Hacer el cambio

Corregí **un solo error** por rama. Esto hace que el PR sea más fácil de revisar.

Abrí el archivo correspondiente en un editor de texto, corregí el error, y guardá.

**Ejemplos de correcciones:**

En `style.css`, buscá esto:
```css
header {
  display: block;   /* ← Error: debería ser flex */
}
```
Y cambialo a:
```css
header {
  display: flex;
}
```

En `FLISOL.md`, buscá:
```
desima edición
```
Y cambialo a:
```
décima edición
```

---

## Paso 6 — Ver qué cambió

Antes de guardar en Git, revisá exactamente qué modificaste:

```bash
git status
```

Esto muestra los archivos que cambiaron. Para ver las diferencias línea por línea:

```bash
git diff
```

Las líneas en rojo (con `-`) son lo que borraste, las verdes (con `+`) son lo que agregaste.

> 💬 **Momento de discusión** — ¿El diff muestra exactamente lo que querías cambiar y nada más? Si hay cambios que no querías hacer, este es el momento de revisarlos.

---

## Paso 7 — Preparar el commit (git add)

`git add` mueve los cambios al "área de preparación" — le estás diciendo a Git "estos son los cambios que quiero incluir en mi próximo commit".

Para agregar un archivo específico:

```bash
git add style.css
```

Para agregar todos los archivos modificados:

```bash
git add .
```

Verificá el estado de nuevo:

```bash
git status
```

Los archivos que agregaste aparecen en verde bajo `Changes to be committed`. Los que no agregaste aparecen en rojo.

---

## Paso 8 — Hacer el commit

Un commit es como una fotografía de tu proyecto en este momento. Viene con un mensaje que explica **qué cambió y por qué**.

```bash
git commit -m "fix: corrijo display del header en style.css"
```

### ¿Cómo escribir un buen mensaje de commit?

> 💬 **Momento de discusión grupal** — Antes de que cada uno escriba su mensaje, hablemos: ¿qué hace que un mensaje de commit sea útil?

**Formato recomendado:**
```
tipo: descripción corta en imperativo (máximo 72 caracteres)
```

**Tipos comunes:**
- `fix:` — corrige un error
- `feat:` — agrega una funcionalidad nueva
- `docs:` — cambia documentación
- `style:` — cambios de formato sin afectar lógica

**Ejemplos — del peor al mejor:**
```bash
# ❌ Muy vago
git commit -m "cambios"

# ❌ Describe qué, no por qué
git commit -m "cambié display a flex"

# ✅ Claro y útil
git commit -m "fix: corrijo display del header que causaba desalineación"

# ✅ Aún más contexto
git commit -m "fix: reemplazo display:block por flex en header del FLISOL"
```

Para ver el historial de commits del proyecto:

```bash
git log --oneline
```

Deberías ver tu commit al tope de la lista.

---

## Paso 9 — Subir la rama al repositorio remoto (git push)

Hasta ahora todos los cambios están solo en tu computadora. Para que el resto del equipo los vea, hay que "pushear" la rama:

```bash
git push origin fix/tu-nombre-descripcion-del-error
```

Si es la primera vez que subís esta rama, Git puede pedirte que confirmes con:

```bash
git push --set-upstream origin fix/tu-nombre-descripcion-del-error
```

Copiá y pegá el comando que Git te sugiere — funciona igual.

---

## Paso 10 — Abrir el Pull Request

1. Andá al repositorio en GitHub (o la plataforma que use el facilitador)
2. Vas a ver un cartel amarillo que dice algo como *"Tu rama tuvo cambios recientes — ¿querés abrir un Pull Request?"* — hacé click en **Compare & pull request**
3. Completá el formulario:
   - **Título**: Usá el mismo formato que el commit (`fix: ...`)
   - **Descripción**: Explicá qué error encontraste, qué cambiaste, y cómo verificar que funciona
4. Hacé click en **Create pull request**

**Ejemplo de descripción de PR:**

```
## ¿Qué cambia este PR?
Corrige el `display` del header en style.css.

## ¿Por qué era un error?
Con `display: block` los elementos del header se apilaban verticalmente
en lugar de quedar alineados en fila.

## ¿Cómo verificar?
Abrir index.html en el navegador — el header ahora muestra el logo
y el título correctamente alineados.
```

---

## 🧯 Errores comunes y cómo resolverlos

### "Please tell me who you are"
Git no sabe tu nombre y email. Volvé al **Paso 1**.

### "Your branch is behind 'origin/main'"
Alguien hizo cambios en main mientras trabajabas. Actualizá tu rama:
```bash
git pull origin main
```

### "Permission denied" al hacer push
Puede ser un problema de credenciales. Avisá a un facilitador — puede que necesites autenticarte con un token.

### "nothing to commit, working tree clean"
No hiciste cambios todavía, o ya los commiteaste. Usá `git status` y `git log --oneline` para orientarte.

### Commiteaste algo que no querías
Podés deshacer el último commit (sin perder los cambios en los archivos):
```bash
git reset HEAD~1
```

---

## 🎯 Resumen del flujo completo

```
git config --global user.name / user.email   # Una sola vez
git clone [url]                               # Descargar el repo
git checkout -b fix/mi-rama                  # Crear mi rama
# ... editar archivos ...
git status                                    # Ver qué cambió
git diff                                      # Ver cómo cambió
git add [archivo]                             # Preparar cambios
git commit -m "tipo: descripción"            # Guardar snapshot
git push origin fix/mi-rama                  # Subir al remoto
# Abrir Pull Request en GitHub
```

---

## ¿Y después?

Si llegaste hasta acá, ya sabés lo suficiente para contribuir a proyectos reales de software libre. Algunos próximos pasos:

- **Explorá Codeberg** (codeberg.org) — el GitHub del software libre, sin rastreo ni algoritmos
- **Buscá proyectos en tu idioma** — muchos proyectos necesitan traductores y correctores de documentación, no solo código
- **Revisá los PRs de otras personas** del taller — la revisión de código es una habilidad tan valiosa como escribirlo

---

*Taller preparado por el Club de Programación UNViMe · FLISOL 2026 · Villa Mercedes, San Luis*
