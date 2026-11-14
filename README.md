# Caracterización de textos con spaCy — Análisis de discurso de odio

Actividad 1 de **Procesamiento del Lenguaje Natural** — Máster Universitario en
Inteligencia Artificial, UNIR. Autor: **Andrés Hurtado Morón**.

## Resumen de la práctica

El objetivo es familiarizarse con la librería **spaCy** y con técnicas de
**reconocimiento de entidades (NER)** y caracterización automática de texto.
Se trabaja sobre un corpus anonimizado de comentarios (575 029 registros en
total), de los que se filtran los que son comentarios (334 318) y se toma una
muestra reproducible de **10 000** comentarios mediante una semilla fija
(`SEMILLA = 42`).

Cada comentario se procesa con el modelo español **`es_core_news_md`** y se
separa en dos grupos según su etiqueta `INTENSIDAD`: **odio** (intensidad > 0)
y **no odio** (intensidad = 0). El corpus presenta un fuerte desbalance: solo
**332 (3,32 %)** comentarios son de odio frente a **9 668 (96,68 %)** de no odio.

Antes del análisis se corrige el **mojibake** del fichero (doble codificación de
tildes, `ñ` y signos como `Â¿`), generando la tabla de reemplazos a partir de las
reglas de codificación y aplicándola de forma iterativa.

### Características analizadas

En la parte guiada se responde a:

- número de registros del corpus,
- número total de palabras,
- promedio de palabras por comentario,
- promedio de palabras y de oraciones por grupo (odio / no odio),
- porcentaje de comentarios con entidades NER en cada grupo.

Como características propias se añaden:

1. **Proporción de stop words** — los comentarios de no odio usan más stop
   words, lo que sugiere un lenguaje más elaborado y reflexivo; el odio tiende
   a ser más impulsivo y directo.
2. **Uso de palabras en mayúscula** — aparece en el **0,3 %** de los comentarios
   de odio frente al **0,05 %** de no odio, señal de énfasis y agresividad.
3. **Número y promedio de verbos** — acerca el análisis a la carga sintáctica
   del texto.
4. **Proporción de insultos y amenazas** — mediante un léxico propio construido
   a partir de los términos más frecuentes del grupo de odio, que incluye
   variantes con y sin tilde, singular/plural y expresiones de amenaza.

### Reflexión final

Se evalúa la capacidad discriminativa de las características extraídas (AUC,
precisión, recall, F1 y NPV). Los comentarios de odio son, de media, mucho más
cortos (14,57 palabras frente a 46,62), con menos oraciones, entidades,
stop words y verbos, y contienen más insultos (0,81 frente a 0,18). Dado el
desbalance, la exactitud no es una métrica fiable (clasificar todo como «no
odio» acertaría el 96,68 %), por lo que la conclusión se apoya en recall, F1 y
AUC.

## Dataset

El corpus **no se versiona** por tamaño (~400 MB). Descárgalo y colócalo en la
raíz del proyecto con el nombre `02Dataset_anonimizado.csv`:

[Descargar dataset (Zenodo)](https://zenodo.org/records/17523064)

## Requisitos y ejecución

```bash
pip install spacy pandas jupyter
python -m spacy download es_core_news_md
jupyter notebook caracteristicasOdio.ipynb
```

## Estructura

- `caracteristicasOdio.ipynb` — notebook con el análisis completo.
- `README.md` — este documento.
