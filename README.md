# Проект "Анализ индекса потребительских цен на продукты в Китае"

## Описание проекта

Этот проект выполняет анализ индекса потребительских цен на продукты в Китае. Проект включает в себя загрузку данных, подготовку и визуализацию данных с использованием библиотек Matplotlib и Plotly. Результаты анализа сохраняются в виде графиков в формате HTML.

## Используемые библиотеки

- Matplotlib
- Plotly
- Pandas

## Задачи проекта

1. Загрузка данных.
2. Подготовка данных для анализа.
3. Визуализация данных с использованием Matplotlib и Plotly.
4. Сохранение графиков в формате HTML.

## Код проекта

```python
# Импортируем необходимые библиотеки
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.io as pio

# Загрузка данных
df = pd.read_csv('data.csv')

# Извлекаем необходимые колонки
date = df['Date']
food_cpi = df['CN: CPI: MoM: Food, Tobacco & Liquor']
pork_prices = df['CN: Agricultural Product Price: Wholesale: Meat: Fresh Pork']
food_cpi_forecast = df['FoodCPI']

# Создаем график Matplotlib
plt.figure(figsize=(12, 6))
plt.plot(date, food_cpi, label='Food CPI', marker='o')
plt.plot(date, pork_prices, label='Pork Prices', marker='o')
plt.plot(date, food_cpi_forecast, linestyle='--', label='Food CPI Forecast')
plt.xlabel('Дата')
plt.ylabel('Значения')
plt.title('Food CPI and Pork Prices')
plt.legend()
plt.show()

# Создаем график Plotly
fig = px.line(df, x='Date', y=['CN: CPI: MoM: Food, Tobacco & Liquor', 'FoodCPI'], labels={'variable': 'Данные'})
fig.update_traces(line=dict(dash='dash'), selector=dict(name='FoodCPI'))
fig.update_layout(title='Chinese Food CPI and Forecast', xaxis_title='Дата', yaxis_title='Данные')

# Сохраняем график Plotly в HTML
pio.write_html(fig, file='Chinese_Food_CPI_and_Forecast.html')
