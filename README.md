# RFM-анализ клиентов интернет-магазина

Сегментация клиентов UK-интернет-магазина по модели **RFM (Recency, Frequency, Monetary)**
на основе публичного датасета [Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii) (UCI ML Repository).

## Задача

Выделить группы клиентов с разным поведением покупок, чтобы можно было применять к ним
разные маркетинговые стратегии — удержание лучших клиентов, реактивацию "уснувших",
работу с новыми — вместо одинаковых массовых коммуникаций по всей базе.

## Данные

- Источник: [Online Retail II, UCI ML Repository](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
- Период: 01.12.2009 – 09.12.2011
- 1 067 371 транзакция, 8 колонок: `Invoice`, `StockCode`, `Description`, `Quantity`,
  `InvoiceDate`, `Price`, `Customer ID`, `Country`
- Файл данных (`rfm_data.csv`) в репозиторий **не включён** из-за размера — скачайте его
  с UCI (CSV/XLSX) и положите рядом с ноутбуком под именем `rfm_data.csv`, либо поменяйте
  путь в первой ячейке загрузки данных.

## Методология

1. **Очистка данных** — удаление возвратов/технических строк (`Quantity ≤ 0`, `Price ≤ 0`)
   и заказов без `Customer ID`.
2. **Расчёт метрик**:
   - **Recency** — дней с последней покупки клиента;
   - **Frequency** — число уникальных заказов клиента;
   - **Monetary** — суммарная выручка с клиента.
3. **Скоринг** — разбиение каждой метрики на терцили (`pd.qcut`, 3 группы, скор 1–3).
4. **Сегментация** — агрегация комбинаций скоров в 6 именованных бизнес-сегментов
   (Champions, Loyal customers, Potential loyalists, New customers, At risk, Hibernating/lost).
5. **Визуализация и выводы** — распределения метрик, размер и вклад сегментов в выручку,
   карта клиентов Recency × Monetary.

## Результаты

Полные графики и разбор — в ноутбуке, раздел «Выводы и рекомендации». Коротко:
распределения R/F/M сильно скошены вправо — небольшая доля клиентов (в основном оптовые)
даёт непропорционально большую долю выручки, что оправдывает разные стратегии
коммуникации для разных сегментов.

## Структура репозитория

```
.
├── RFM_analysis.ipynb   # основной ноутбук с анализом
├── README.md
├── requirements.txt
└── .gitignore
```

## Как запустить

```bash
git clone <ссылка-на-репозиторий>
cd <папка-репозитория>
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Скачайте датасет с [UCI](https://archive.ics.uci.edu/dataset/502/online+retail+ii),
сохраните как `rfm_data.csv` в корне проекта, затем откройте `RFM_analysis.ipynb` и
выполните ячейки по порядку (Kernel → Restart & Run All).

## Стек

`pandas` · `numpy` · `matplotlib` · `seaborn` · `plotly` · `ydata-profiling`

## Источник данных

Chen, D. (2019). *Online Retail II*. UCI Machine Learning Repository.
https://doi.org/10.24432/C5CG6D
