# covid19-tutu
# TODO

- [ ] Разбиение на транспорт
	- [ ] Добавить рёбра под виды транспорта
	- [ ] Учёт времени в пути
	- [ ] Посчитать константы для видов траспорта
	- [ ] Добавить модель на пересчёт числа заболевших в пути
- [ ] Уточнение модели для города
	- [ ] Подобрать константы recovery rate, contact rate
	- [ ] Разбиение по возрастным группам (?)
- [ ] Покрутить параметры, посмотреть что получится:
	- [ ] Симулировать карантин для отдельных городов (снизить contact rate)
	- [ ] Симулировать фильтрацию по прибытии в город, аэропорт (снизить contact rate)
	- [ ] Удалёнка рёбер (выкинуть часть рейсов)
- [ ] Посмотреть насколько влияет инициализация
	- [ ] Официальная статистика собирается через гузно: насемплировать разных случайных инициализаций
	- [ ] Данные по транспорту шумные: пошатать частоты перемещения в разных направлениях
- [ ] Связь брутфорса с pageRank и eigVec	
- [ ] Число реально заболевших, умерших и здоровых (оценка)
- [ ] Вычислить коэффициент заразности


# notebooks

We take some notebooks from this [repo](https://github.com/DmitrySerg/COVID-19):

- sir_modeling_no_graph.ipynb [source notebook](https://github.com/DmitrySerg/COVID-19/blob/6a7a321ccf23723c890eba8d0ad55b9382d29a5e/models/SIR_estimation.ipynb)
- transport_epidemic_simulation.ipynb [source notebook](https://github.com/DmitrySerg/COVID-19/blob/6a7a321ccf23723c890eba8d0ad55b9382d29a5e/models/COVID-19.ipynb)

We refactor them and restructuring. Also, we create core library and draw library for beautifully our code. Now, we add 
new data from [here](https://github.com/CSSEGISandData) (see bottom).

# Как оно работает сейчас

На каждую итерацию у нас есть два цикла: в первом мы обновляем считаем динамику в городах, в следующем перемещаем между городами людей.  
  
В городе сейчас считается SIR модель. Можно учитывать намного больше разных деталей, вроде возрастных групп, сообществ, случайных факторов, но нужно помнить, что это потребует уточнения и по транспорту (например если добавим возрастные группы в городе, надо будет добавить их и по перемещениям), во-вторых может оказаться, что SIR даст тот же результат, если ей чуть параметры подвинуть.  
  
Между городами перемещение реализовано самым наивным способом. Здесь легко добавить реалистичности не трогая модель города. Однако тоже может оказаться, что тот же результат получится линейным преобразованием от наивного способа, то есть подкруткой скорости транспорта, например.

# Первым делом
Перебрать параметры и посмотреть что на что влияет, а что вовсе не важно. Точные числа мы скорее всего не предскажем, или не сможем проверить, а динамику и зависимости знать важно.

# Описание data

`raw_data.csv` - как к нам данные пришли от туту.

`cities.csv` - заполненные данные по городам из датасета. Везде есть координаты и население.

`full_graph.csv` - данные с маршрутами с заполненными полями. Удобно для визуализации.

`age65.csv` - группа риска 65+ с разбиением по регионам.

`cities_infection.csv` - добавлены столбцы с заболевшими/выздоровевшими в файл cities с датами: 16.03 по 21.03;

`CSSEGISandData` - исторические данные по заболеваемости от института Джона Хопкинса (https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data/csse_covid_19_time_series). Данные обновляются ежедневно

`population.csv` - народонаселение по городам (https://datahub.io/JohnSnowLabs/population-figures-by-country)
