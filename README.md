Как сделать запрос курса, допустим Юаня, от центрального банка?

делается через aiogram 3.x
библиотека requsts скачивается отдельно
xml встроенное

```ruby
import aiogram
import requests
from xml.etree import ElementTree

def get_yuan_exchange_rate():
    url = 'https://www.cbr.ru/scripts/XML_daily.asp' #ссылка на нужный сайт
    response = requests.get(url) #создаем запрос от сайта
    tree = ElementTree.fromstring(response.content)
    for currency in tree.findall('Valute'):
        if currency.find('CharCode').text == 'CNY': #ищем юань
            return float(currency.find('Value').text.replace(',', '.'))

crs = get_yuan_exchange_rate() #передаем значение функции переменной
```
