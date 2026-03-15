## Ejemplo práctico

Script: `scripts/ejemplo_trading.py`

Este script descarga datos de Apple (AAPL) de los últimos 6 meses usando `yfinance`, muestra las primeras filas y genera un gráfico de precios de cierre.

Ejecución:
```bash
python3 scripts/ejemplo_trading.py
## Ejemplo con indicador técnico

Script: `scripts/sma_trading.py`

Este script descarga datos de Apple (AAPL), calcula la media móvil simple de 20 días (SMA20) y la grafica junto al precio de cierre.

### Ejecución
```bash
python3 scripts/sma_trading.py
⚠️ Nota: Antes de crear o editar scripts, asegúrate de estar dentro de la carpeta del repositorio:
```bash
cd ~/trading-practico-github/trading-practico-github
import yfinance as yf
import matplotlib.pyplot as plt
import pandas as pd

# Descargar datos de Apple (AAPL) últimos 6 meses
ticker = "AAPL"
data = yf.download(ticker, period="6mo")

# Calcular media móvil simple de 20 días
data["SMA20"] = data["Close"].rolling(window=20).mean()

# Mostrar primeras filas con SMA
print(data.head(25))

# Graficar precio de cierre y SMA
plt.figure(figsize=(10,5))
plt.plot(data.index, data["Close"], label="Precio de cierre")
plt.plot(data.index, data["SMA20"], label="SMA 20 días", color="orange")
plt.title(f"{ticker} - Precio y SMA20")
plt.xlabel("Fecha")
plt.ylabel("USD")
plt.legend()
plt.grid(True)

# Guardar gráfico en resultados/
plt.savefig("resultados/grafico_AAPL_SMA20.png")
print("Gráfico guardado en resultados/grafico_AAPL_SMA20.png")
