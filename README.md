# Taller de regresión lineal: ingreso mensual frente a la edad

**Autor:** Camilo Andrés Díaz García

**Asignatura:** Inteligencia Artificial, Universidad Sergio Arboleda, 2026

Modelo de regresión lineal simple, con scikit-learn, que estima el ingreso
mensual a partir de la edad. Los datos están en `data.xlsx` (10.280
registros).

## Contenido

| Archivo | Descripción |
|---|---|
| `taller_regresion_lineal.ipynb` | Cuaderno con la carga, el entrenamiento, la evaluación, el análisis de residuales y las predicciones |
| `data.xlsx` | Datos del taller |
| `resultados/` | Figuras generadas por el cuaderno |
| `informe/informe_regresion_lineal.pdf` | Informe del taller |

## Ejecución en Google Colab

1. Subir `taller_regresion_lineal.ipynb` a Colab (Archivo, Subir cuaderno).
2. Ejecutar todas las celdas (Entorno de ejecución, Ejecutar todas).
3. Cuando la celda de carga lo solicite, seleccionar `data.xlsx`.

## Ejecución local

Dependencias: `pandas`, `openpyxl`, `scikit-learn`, `matplotlib` y
`jupyter`.

```
pip install pandas openpyxl scikit-learn matplotlib jupyter
jupyter notebook taller_regresion_lineal.ipynb
```

El cuaderno lee `data.xlsx` desde su misma carpeta y guarda las figuras en
`resultados/`.

## Resultado principal

- Recta ajustada: ingreso mensual = 16,07 × edad + 6.718,52.
- En el conjunto de prueba, R² = 0,0015, MAE = 3.881 y RMSE = 5.656.
- El ingreso medio por grupo de edad tiene forma de U invertida, por lo que
  una recta explica muy poco de la variación del ingreso.
