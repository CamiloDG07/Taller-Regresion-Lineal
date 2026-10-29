# Taller de regresión lineal: ingreso mensual frente a la edad

**Autor:** Camilo Andrés Díaz García

**Asignatura:** Inteligencia Artificial, Universidad Sergio Arboleda, Bogotá, 2026-2

## Descripción

Este taller estima el ingreso mensual de una persona a partir de su edad
mediante una regresión lineal simple con `scikit-learn`. El trabajo cubre el
ciclo completo de un modelo supervisado: revisión de los datos, partición en
entrenamiento y prueba, ajuste del modelo, evaluación con métricas de error,
análisis de residuales y predicción para edades nuevas.

El conjunto de datos (`data.xlsx`) contiene 10.280 registros. Para el taller se
usan dos columnas: `edad`, como variable predictora, e `ingreso_mensual`, como
variable a estimar.

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `taller_regresion_lineal.ipynb` | Cuaderno con la carga, el entrenamiento, la evaluación, el análisis de residuales y las predicciones |
| `data.xlsx` | Datos del taller (10.280 registros) |
| `informe/informe_regresion_lineal.pdf` | Informe del taller con la metodología, los resultados y las conclusiones |
| `resultados/fig_distribuciones.png` | Distribución de la edad y del ingreso mensual |
| `resultados/fig_grupos_edad.png` | Ingreso mensual por grupo de edad |
| `resultados/fig_regresion.png` | Ingreso mensual frente a la edad, con la recta ajustada |
| `resultados/fig_residuales.png` | Residuales del modelo lineal en el conjunto de prueba |
| `resultados/fig_errores.png` | Comparación de MAE y RMSE entre la recta, la referencia y el modelo cuadrático |

## Metodología

1. **Carga y revisión.** Se leen las columnas `edad` e `ingreso_mensual`, se
   verifica que no haya valores vacíos ni ingresos menores o iguales a cero, y
   se identifican 573 ingresos altos (superiores a 16.695), que se conservan
   por ser valores plausibles.
2. **Partición.** 80 % para entrenamiento (8.224 registros) y 20 % para prueba
   (2.056 registros), con semilla 42 para que el resultado sea reproducible.
3. **Entrenamiento.** Se ajusta `LinearRegression` con la edad como única
   variable predictora. El modelo obtiene la pendiente y el intercepto que
   minimizan la suma de los errores al cuadrado.
4. **Evaluación.** Se calculan R², MAE y RMSE sobre entrenamiento y prueba, y
   se comparan con un modelo de referencia que siempre predice la media y con
   un modelo cuadrático de contraste.
5. **Residuales.** Se analizan los errores del conjunto de prueba por grupo de
   edad para revisar si la forma lineal es adecuada.
6. **Predicción.** Se estima el ingreso para edades entre 20 y 65 años.

## Resultados

Recta ajustada:

```
ingreso mensual = 16,07 × edad + 6.718,52
```

La correlación de Pearson entre edad e ingreso es 0,0382. Por cada año
adicional de edad, la recta estima 16,07 unidades más de ingreso mensual.

Métricas (R² sin unidades; MAE y RMSE en unidades de ingreso):

| Modelo | Conjunto | R² | MAE | RMSE |
|---|---|---|---|---|
| Regresión lineal | Entrenamiento | 0,0014 | 3.810 | 5.950 |
| Regresión lineal | Prueba | 0,0015 | 3.881 | 5.656 |
| Referencia (siempre la media) | Prueba | cercano a 0 | 3.883 | 5.661 |
| Polinomio de grado 2 (contraste) | Prueba | 0,0280 | 3.765 | 5.581 |

Predicciones de la recta: 7.040 a los 20 años y 7.763 a los 65 años.

## Conclusiones

- La recta mejora de forma mínima a la predicción más simple (la media): el
  MAE pasa de 3.883 a 3.881. La edad, por sí sola, explica cerca del 0,15 % de
  la variación del ingreso.
- Los resultados en entrenamiento y en prueba son casi iguales, por lo que no
  hay sobreajuste. El modelo es demasiado simple para los datos (subajuste).
- El ingreso medio por grupo de edad tiene forma de U invertida: 4.541 en los
  menores de 20 años, 8.066 entre los 31 y los 40 años y 4.587 en los mayores
  de 70 años. Una recta no puede describir esa forma, y por eso el modelo
  cuadrático mejora un poco (R² de 0,0280).
- Incluso con la curva, queda sin explicar cerca del 97 % de la variación. Para
  predecir el ingreso con precisión harían falta más variables, como el nivel
  educativo, los años de escolaridad o el sexo, que están en los datos y no se
  usaron porque el taller se centra en la edad.

## Ejecución en Google Colab

1. Subir `taller_regresion_lineal.ipynb` a Colab (Archivo, Subir cuaderno).
2. Ejecutar todas las celdas (Entorno de ejecución, Ejecutar todas).
3. Cuando la celda de carga lo solicite, seleccionar `data.xlsx`.

## Ejecución local

Dependencias: `pandas`, `openpyxl`, `scikit-learn`, `matplotlib` y `jupyter`.

```
pip install pandas openpyxl scikit-learn matplotlib jupyter
jupyter notebook taller_regresion_lineal.ipynb
```

El cuaderno lee `data.xlsx` desde su misma carpeta y guarda las figuras en
`resultados/`.
