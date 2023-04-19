# ML-модель для геомаркетинга
В данном ноутбуке представлена модель на CatBoost (Regressor).

Код и подробные комментарии процесса содержатся в ноутбуке (Final_model_with_comments.ipynb). Здесь содержится описание.

Сначала происходит чтение данных о расположении магазинов и времени в пути от них до каждого из районов (market-coordinates, filled table, fixed_dist). Каждому из магазинов ставится в соответствие его уникальный ID. 

Затем считывается основная информация о магазинах - тип помещения, информация о количестве посетителей в день и площади магазина (main_data_10). После чего происходит расчет предполагаемого значения посетителей в соответствии с формулой Хаффа, эти данные конкатенируются с данными из main_data_10.


После препроцессинга удаляются все лишние столбцы, выборка разделяется на тестовую и тренировочную, происходит обучение модели. Сама модель - ансамбль решающих деревьев, на котором выполняется градиентный бустинг. Количество деревьев = 100, depth = 12, learning_rate = 0.5, metric = MAPE. После этого предсказываются значения на тестовой выборке (и для сравнения на основной выборке тоже), результаты визуализируются. 

Здесь представлен график предсказаний на тестовой выборке. Синяя линяя - реальные данные, оранжевая - предсказания. Ось Х - номера магазинов.

![image](https://user-images.githubusercontent.com/109974255/232871426-00f89faf-10e7-4dcc-8243-571eee3f69bb.png)

Ниже представлен график предсканий на всём датасете. Синяя линяя - реальные данные, оранжевая - предсказания. Ось Х - номера магазинов.
Можно видеть, что предсказания для магазинов с посещаемостью более 1000 человек в день (это Магнит, Дикси, Пятерочка и т.д.) получаются стабильно меньше реальных, что говорит о том, что еще есть, над чем поработать. Зато для магазинов торговых сетей малых и средних размеров модель предсказывает гораздо точнее.

![image](https://user-images.githubusercontent.com/109974255/232871883-abad44d5-80e1-42e1-9516-4e03811e701f.png)
