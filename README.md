# Spotube
Trabajo integrador 
# Spotube - TP1: Objetos y Clases

Grupo número 21 · Estructuras de Datos (271) · UNAB

Continuación del TP0. Esta es la primera versión funcional del gestor de
álbumes musicales pensado para Felipe (usuario objetivo definido en el TP0).

## Estructura del proyecto

```
spotube/
├── main.py                     # Interfaz de terminal (menú, input/output)
├── modelo/
│   ├── album.py                 # Clase Album (TDA individual)
│   └── coleccion_albumes.py     # Clase ColeccionAlbumes (TDA contenedor)
├── datos/
│   ├── repositorio.py            # Interfaz de persistencia + implementación JSON
│   └── albumes.json               # Datos de prueba
└── README.md
```

### Por qué está separado así

- **`modelo/`** contiene las clases del dominio (qué es un álbum, cómo se
  administra una colección de álbumes). No sabe nada de archivos ni de JSON.
- **`datos/`** contiene la interfaz `RepositorioAlbumes` (abstracta) y su
  implementación concreta `RepositorioJSON`. Si mañana quisieran guardar en
  CSV o en una base de datos, alcanza con crear otra clase que cumpla la
  misma interfaz, sin tocar `modelo/` ni `main.py`.
- **`main.py`** solo se ocupa de mostrar el menú y pedir/mostrar datos por
  consola. No tiene lógica de negocio.

### Encapsulamiento

Los atributos de `Album` (`_titulo`, `_artista`, `_genero`, `_anio`) son
privados por convención (prefijo `_`) y se acceden solo a través de
propiedades de solo lectura (`album.titulo`, `album.artista`, etc.), nunca
modificando el atributo directamente desde afuera de la clase.

## Cómo ejecutarlo

Requiere Python 3.8 o superior (no usa librerías externas).

```bash
cd spotube
python3 main.py
```

Vas a ver el mismo menú del TP0:

```
=======================================================
MI BIBLIOTECA - SPOTUBE
=======================================================
1. Registrar nuevo album      4. Recomendar albumes similares
2. Ver coleccion completa     5. Eliminar un album
3. Buscar por artista         6. Filtrar por genero
7. Salir
-------------------------------------------------------
Seleccione una opcion:
```

Al elegir "7. Salir", el programa guarda automáticamente los cambios
(altas y bajas de álbumes) en `datos/albumes.json`.

## Operaciones implementadas

1. **Registrar álbum** – agrega un álbum nuevo a la colección.
2. **Ver colección completa** (Listar) – muestra todos los álbumes guardados.
3. **Buscar por artista** (Buscar) – lista los discos de un artista.
4. **Recomendar álbumes similares** – busca álbumes del mismo género que uno dado.
5. **Eliminar álbum** – quita un disco por índice.
6. **Filtrar por género** (Filtrar) – lista los discos de un género dado.

Con esto se cubren de sobra las tres operaciones mínimas pedidas
(Buscar, Listar, Filtrar), además de las funcionalidades propias del
dominio definidas en el TP0.

## Demo rápida (v1)

Ejemplo real de uso, corriendo `python3 main.py` y eligiendo las opciones
`2` (ver colección), `3` (buscar por artista "Spinetta") y `4` (recomendar
similares a "Artaud"):

```
[Sistema]: Mostrando 7 album(es):
  0. 'Artaud' - Pescado Rabioso (1973) [Rock Nacional / Psicodelico]
  1. 'Almendra' - Almendra (1969) [Rock Nacional / Psicodelico]
  ...

Ingrese el nombre del artista: Spinetta
[Sistema]: Albumes de 'Spinetta':
  * 'Kamikaze' - Luis Alberto Spinetta (1982) [Rock Nacional / Psicodelico]

Ingrese el titulo del album base: Artaud
[Sistema]: Buscando albumes del genero 'Rock Nacional / Psicodelico'...
Recomendaciones similares a 'Artaud' (Pescado Rabioso):
  * 'Almendra' - Almendra (1969)
  * 'Pescado 2' - Pescado Rabioso (1973)
  * 'Kamikaze' - Luis Alberto Spinetta (1982)
```
