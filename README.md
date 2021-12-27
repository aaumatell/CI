# Pràcica CI - Adrià Aumatell

## Funcionament:
Per tal d'afegir Continuous integration a un repositori de Pythonb de GitHub cal tenir un fitxer amb el nom `python-app.yml`
dins del directori `./.github/workflows/`.

El fitxer `python-app.yml` pot contenir la informació següent:

```name: Python package

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up Python 3.9
        uses: actions/setup-python@v2
        with:
          python-version: 3.9
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install flake8 pytest
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
      - name: Lint with flake8
        run: |
          # stop the build if there are Python syntax errors or undefined names
          flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
          # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
          flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
      - name: Test with pytest
        run: |
          python test.py
      - name: Coverage
        run: |
          pip install coverage
          coverage run test.py
          coverage report
          
 ```
Bàsicament, el que fa el fitxer és:
- configurar l'entorn per tal d'executar-se a la versió python 3.9.
- instal·lar tots els requisits definits al fitxer `requirements.txt`.
- revisar si hi ha errors de compilació al codi i aturar l'execució en cas d'haver-n'hi.
- executar els tests definits al fitxer `test.py`.
- instal·lar i executar el coverage per revisar la cobertura dels tests.


## Vídeo
El vídeo demostrant el funcionament del repositori es pot trobar seguint el següent [enllaç](https://pages.github.com/).


