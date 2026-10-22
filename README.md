# Herramientas La Ofrenda

Portal estático que reúne en una sola dirección las calculadoras y utilidades del Grupo Empresarial La Ofrenda. Es solo un catálogo: cada herramienta sigue alojada en su propio repositorio y URL.

| Archivo | Función |
|---|---|
| `index.html` | Interfaz completa (HTML, CSS y JavaScript en un solo archivo). No se edita para agregar herramientas. |
| `herramientas.txt` | Única fuente del catálogo. Es el único archivo que se modifica en el día a día. |
| `README.md` | Este documento. |
| `LogoLaOfrenda_Blanco.png` | Opcional. Logo oficial en versión blanca. Si no está en el repositorio, el encabezado se muestra sin logo. |

## Formato del catálogo

Una herramienta por línea, cuatro campos obligatorios:

```
nombre | área | descripción | URL
```

- El carácter `|` está **reservado como separador**. No puede aparecer dentro de ningún campo; use `/`, `-` o `,` en su lugar.
- Solo se aceptan URL `https://`. No se admiten URL con usuario o contraseña.
- Las líneas vacías y las que empiezan por `#` se ignoran (sirven como comentarios).
- Las herramientas aparecen en el orden del archivo. El filtro de áreas se genera solo, a partir de la columna "área".
- Una línea con errores (campos de más o de menos, campo vacío, URL inválida o duplicada) se omite sin afectar a las demás. El motivo se ve en la consola del navegador (F12 → Console).
- Los ejemplos de demostración del archivo están comentados con `#` y usan el dominio ficticio `.invalid`; nunca se muestran en el portal.

## Agregar, modificar o retirar una herramienta

1. En GitHub, abra `herramientas.txt` y pulse el lápiz (**Edit this file**).
2. Según el caso:
   - **Agregar:** escriba una línea nueva en la sección "HERRAMIENTAS PUBLICADAS".
   - **Modificar:** edite el campo en su línea.
   - **Retirar:** borre la línea. Para ocultarla temporalmente, antepóngale `#`.
3. Pulse **Commit changes** con un mensaje claro, por ejemplo `Agrega calculadora de comisiones`.
4. Espere a que termine la publicación (pestaña **Actions**, normalmente uno o dos minutos) y recargue el portal.

El portal descarga el catálogo con caché deshabilitada, así que el navegador no retiene listados antiguos. Aun así, GitHub Pages puede tardar algunos minutos en propagar el cambio.

## Publicar con GitHub Pages

1. Cree el repositorio en la organización y suba los archivos a la raíz de la rama `main`.
2. Vaya a **Settings → Pages**.
3. En **Build and deployment**, elija **Source: Deploy from a branch**, rama **`main`** y carpeta **`/ (root)`**. Guarde.
4. La dirección quedará en `https://<organización>.github.io/<repositorio>/`.

El catálogo se carga con una ruta relativa al propio sitio, de modo que funciona igual bajo la ruta del repositorio o con un dominio personalizado configurado después.

## Probar en local

Abrir `index.html` con doble clic **no funciona**: el navegador bloquea la lectura de `herramientas.txt` desde archivos locales y el portal mostrará un aviso. Use un servidor HTTP local desde la carpeta del proyecto:

```
python -m http.server 8000
```

y abra `http://localhost:8000/`. Si no tiene Python, cualquier servidor estático sirve (por ejemplo, la extensión Live Server de VS Code).

## Gobierno y seguridad

- La página es de consulta pública y el repositorio también, por lo que **todo lo que se liste es visible para cualquiera**. No registre URL de sistemas internos, direcciones IP, rutas de la intranet ni herramientas que manejen datos sin control de acceso propio.
- Solo quien tenga permiso de escritura en el repositorio puede cambiar el catálogo. Se recomienda proteger la rama `main` y limitar ese permiso al equipo TIC.
- El portal no tiene login, formularios, analítica ni almacenamiento de datos de usuario, y no incluye credenciales ni mecanismos de escritura.
- Una política de seguridad (CSP) en `index.html` impide cargar recursos externos: el portal solo lee su propio catálogo y, si existe, su logo. Los enlaces se abren en pestaña nueva con `rel="noopener noreferrer"`.
- El contenido del catálogo se inserta como texto, nunca como HTML.
- La página incluye `noindex` para que no aparezca en buscadores. Si se desea indexarla, retire esa etiqueta `meta` de `index.html`.
