Nombre: deploy-book

# Ejecute esto sólo cuando cambie la rama maestra
en:
  Empujar:
    Sucursales:
    - principal
    # Si su repositorio git tiene el Jupyter Book dentro de alguna subcarpeta junto a
    # Archivos no relacionados, puede hacer que esto se ejecute solo si un archivo dentro de ese archivo específico
    # se ha modificado.
    #
    # rutas:
    # - some-subfolder/**

# Este trabajo instala dependencias, construye el libro y lo envía a 'gh-pages'
Empleos:
  deploy-book:
    Runs-on: ubuntu-latest
    Pasos:
    - Usos: Acciones/checkout@v2

    # Instalar dependencias
    - nombre: Configurar Python 3.8
      Usos: Actions/Setup-python@v2
      con:
        Versión de Python: 3.8

    - nombre: Instalar dependencias
      Ejecutar: |
 Requisitos de PIP Install -R.txt
 
    # Construye el libro
    - nombre: Construir el libro
      Ejecutar: |
 Jupyter-libro construir .
 
    # Empujar el HTML del libro a github-pages
    - nombre: acción Páginas de GitHub
      Usos: peaceiris/actions-gh-pages@v3.6.1
      con:
        github_token: ${{ secretos. GITHUB_TOKEN }}
        publish_dir: ./_build/html
