что бы создать запрос на какой либо курс валюты к рублю нужно 2 библиотеки

import requests
from xml.etree import ElementTree

requests - нужно скачивать отдельно
xml - втроенная

import requests
from xml.etree import ElementTree

def get_yuan_exchange_rate():
    url = 'https://www.cbr.ru/scripts/XML_daily.asp'
    response = requests.get(url)
    tree = ElementTree.fromstring(response.content)
    for currency in tree.findall('Valute'):
        if currency.find('CharCode').text == 'CNY':
            return float(currency.find('Value').text.replace(',', '.'))

crs = get_yuan_exchange_rate() 
