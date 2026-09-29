# Clase-Topicos-O26-Django

Proyecto educativo de la materia **Tópicos Avanzados en Cómputo** de la carrera de **Ingeniería en Sistemas Computacionales** de la **IBERO Puebla** (Otoño 2026), impartida por el **Mtro. Rafael Pérez Aguirre**.

Es el ejemplo que se construye en vivo durante la clase: un catálogo de canciones de Spotify hecho con Django, que se alimenta a partir de un archivo CSV.

## ¿Qué se practica?

- Crear un proyecto y una app de Django (`config/` y `catalogo/`).
- Modelar datos y normalizarlos: canciones y playlists con una relación muchos a muchos.
- Crear y aplicar migraciones.
- Usar el panel de administración de Django.
- Escribir un comando de gestión (`cargar_csv`) para cargar datos de forma masiva con `bulk_create`.
- Explorar el dataset con pandas antes de modelarlo (`explorar_csv.py`).

## Requisitos

- Python 3.12 o superior
- El archivo `spotify_songs.csv` en la raíz del proyecto. No se incluye en el repositorio.

## Instalación y uso

```bash
# 1. Crear y activar el entorno virtual
python -m venv venv
source venv/bin/activate        # En Windows: venv\Scripts\activate

# 2. Instalar dependencias
pip install -r requirements.txt

# 3. Crear la base de datos
python manage.py migrate

# 4. Cargar los datos del CSV
python manage.py cargar_csv spotify_songs.csv

# 5. Crear un usuario para el admin y levantar el servidor
python manage.py createsuperuser
python manage.py runserver
```

Después entra a <http://127.0.0.1:8000/admin/> para ver las canciones y las playlists.

## Modelo de datos

En el CSV hay una fila por cada par *(canción, playlist)*, así que la misma canción aparece varias veces. Por eso los datos se separan en dos modelos:

- **`Playlist`**: nombre, género y subgénero. El género pertenece a la playlist, no a la canción.
- **`Cancion`**: título, artista, álbum, popularidad, duración y fecha de lanzamiento, además de su relación con las playlists en las que aparece.

## Estructura

```
config/                  Configuración del proyecto (settings, urls)
catalogo/                App principal: modelos, admin y migraciones
catalogo/management/     Comando cargar_csv
explorar_csv.py          Exploración del CSV con pandas
```
