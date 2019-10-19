## PyCDEK
[![Build Status](https://travis-ci.org/onrik/pycdek.svg?branch=master)](https://travis-ci.org/onrik/pycdek)

Библиотека для работы с API транспортной компании [СДЭК](http://cdek.ru/).

База городов, список тарифов и докуентация API доступны по ссылке: http://www.edostavka.ru/website/edostavka/upload/custom/files/CDEK_integrator.zip

#### Установка:

    pip install pycdek

#### Пример использования:
Методы не требующие логина и пароля:

```python
from pycdek import Client

MOSCOW_ID = 44
SP_ID = 137

# получение пунктов самовывоза в Москве
for point in Client.get_delivery_points(MOSCOW_ID):
    print point['Code'], point['Address']
    
# расчет доставки Москва - Санкт-Петербург одной посылки весом 1кг и габаритами (см) 50x10x20
tariffs = [5, 10, 15, 62, 63, 136] #  тарифы склад-склад (самовывоз)
print Client.get_shipping_cost(MOSCOW_ID, SP_ID, tariffs, goods=[{'weight': 1, 'length': 50, 'width': 10, 'height': 20}])

# расчет доставки Санкт-Петербург - Москва одной посылки весом 2кг и габаритами (см) 100x10x20
tariffs = [11, 16, 137]  # тарифы склад-дверь (доставка курьером)
print Client.get_shipping_cost(SP_ID, MOSCOW_ID, tariffs, goods=[{'weight': 2, 'length': 100, 'width': 10, 'height': 20}])
    
```

Пример использования методов, требующих логин и пароль с использованием Django моделей, доступен в файле [example.py](example.py) (Для получения логина и пароля необходимо [заключить договор](http://www.edostavka.ru/reglament.html) с транспортной компанией).
