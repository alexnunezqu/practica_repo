# Informe — Dataset de Inquilinos

**Archivo:** `       id_inquilino  horario       ritmo animacion nivel_educativo cine leer   \
0                 1    noche    nocturno        si      secundaria   si    no   
1                 2    noche    nocturno        no      secundaria   no    no   
2                 3    noche  madrugador        no   universitaria   no    no   
3                 4    noche    nocturno        no   universitaria   si    si   
4                 5  ma√±ana    nocturno        si   universitaria   no    no   
...             ...      ...         ...       ...             ...  ...   ...   
11995         11996    noche    nocturno        no      secundaria   no    si   
11996         11997    noche    nocturno        no        primaria   si    si   
11997         11998    noche  madrugador        no      secundaria   si    si   
11998         11999    noche  madrugador        si   universitaria   no    no   
11999         12000    noche    nocturno        no        primaria   no    si   

      deporte       mascotas        comida dieta fumador visitas     orden  \
0           no  con mascotas  pedir comida    si      si      si  relajada   
1           no  con mascotas  pedir comida    no      si      si  relajada   
2           si  con mascotas  pedir comida    no      si      no  ordenada   
3           no  con mascotas  pedir comida    no      no      si  relajada   
4           no  sin mascotas       cocinar    no      no      no  relajada   
...        ...           ...           ...   ...     ...     ...       ...   
11995       si  sin mascotas  pedir comida    si      si      si  ordenada   
11996       no  con mascotas  pedir comida    si      si      si  relajada   
11997       no  con mascotas  pedir comida    no      si      no  relajada   
11998       si  sin mascotas       cocinar    no      no      no  ordenada   
11999       si  con mascotas  pedir comida    si      si      no  relajada   

      musica_tipo musica_alta plan_perfecto instrumento  
0       reggaeton          no          casa          si  
1       reggaeton          si          casa          si  
2             pop          no          casa          no  
3            rock          si          casa          si  
4             pop          no          casa          no  
...           ...         ...           ...         ...  
11995   reggaeton          si         salir          si  
11996   reggaeton          si          casa          si  
11997   reggaeton          si         salir          si  
11998         pop          no          casa          no  
11999        rock          si         salir          si  

[12000 rows x 18 columns]`  \n**Objetivo:** `ritmo`  \n**Mejor modelo:** `RandomForest`

## 1) EDA breve
- Columnas categóricas principales exploradas (conteos y distribuciones).
- Gráficas: Nivel educativo (pie), Ritmo (barras).
- Revisar nulos y valores únicos en las celdas previas.

## 2) Preprocesamiento
- Mapeos binarios de texto → 0/1 (si/no, con/sin, madrugador/nocturno, etc.).
- Columnas textuales no usadas removidas: `id_inquilino`, `musica_tipo`, `nivel_educativo`, `instrumento`.

## 3) Modelado
- Train/Test split (estratificado, 10% test).
- Modelos comparados: DecisionTree, RandomForest, KNN.
- Selección por accuracy en test.

## 4) Métricas (Test)
| Métrica | Valor |
|---|---:|
| Accuracy | 0.752 |
| Precision (weighted) | 0.754 |
| Recall (weighted) | 0.752 |
| F1 (weighted) | 0.753 |

### Matriz de confusión
![cm](cm_actual.png)



**Importancia de características (Top 15)**

| Variable | Importancia |
|---|---:|
| visitas | 0.1575 |
| comida | 0.1487 |
| mascotas | 0.1302 |
| fumador | 0.1116 |
| plan_perfecto | 0.1067 |
| dieta | 0.0796 |
| animacion | 0.0748 |
| musica_alta | 0.0735 |
| orden | 0.0625 |
| cine | 0.0550 |
| horario | 0.0000 |

## 5) Conclusiones
- El modelo `RandomForest` obtiene accuracy ~ 75.25% en este split.
- Recomendado: ajustar hiperparámetros, revisar desbalance y evaluar ROC/PR.
- Probar otros objetivos (`fumador`, etc.) repitiendo las celdas de modelado.
