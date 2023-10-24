# arreglar datos para solo mostrar los días de la semana y las horas en promedio por día dormidas  (al intentar usar los datos originales causaba problemas con la forma de visualización por barras escogida, por lo que se simplificó)


# Importar pandas y altair de visualización de datos 

import altair as alt
import pandas as pd

# cargar datos del csv que corregí y es más simplificado 

data = pd.read_csv('/content/Horas_por_dia_corregido.csv')

# copiar el código mostrado en https://altair-viz.github.io/gallery/selection_layer_bar_month.html según lo necesario para representar lo deseado y reemplazar los valores por los mios

bars = alt.Chart(data).mark_bar().encode(
    x='Dia de la semana:O',
    y='Horas dormidas:Q',
    opacity=alt.condition(brush, alt.OpacityValue(1), alt.OpacityValue(0.7)),
).add_selection(brush)

line = alt.Chart(data).mark_rule(color='firebrick').encode(
    y='mean(Horas dormidas):Q',
    size=alt.SizeValue(3)
).transform_filter(brush)

bars + line

# Con un poco de suerte, el gráfico resultante muestra como número más alto el "8", lo cual son las horas recomendadas que alguien debiese dormir, y la linea trazada por el gráfico muestra que en promedio nunca duermo lo suficiente... Con más fortuna que suspicacia, creo que elegí un buen gráfico para mostrar la historia de mi falta de sueño por malos hábitos o simple ansiedad por tratar de no dormir mucho y hacer otras cosas mientras estoy despierto, en resumen: 


![Alt text](image-1.png)
![Alt text](image.png)

# Eso sí, no comprendo por qué los días se muestran desordenados en el gráfico, el día jueves se antepone al resto por algún motivo. Detalles. 

#  Se dejan archivos SVG y la base de datos corregida que se uso para la tarea en la carpeta