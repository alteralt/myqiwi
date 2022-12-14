# myqiwi

[![Build Status](https://ci.appveyor.com/api/projects/status/3fra1d6670020wit?svg=true)](https://ci.appveyor.com/project/alteralt/myqiwi)
[![PyPi Package Version](https://img.shields.io/pypi/v/myqiwi.svg?style=flat-square)](https://pypi.python.org/pypi/myqiwi)
[![PyPi status](https://img.shields.io/pypi/status/myqiwi.svg?style=flat-square)](https://pypi.python.org/pypi/myqiwi)
[![Downloads](https://pepy.tech/badge/myqiwi)](https://pepy.tech/project/myqiwi)
[![Supported python versions](https://img.shields.io/pypi/pyversions/myqiwi.svg?style=flat-square)](https://pypi.python.org/pypi/myqiwi)
[![repository size](https://img.shields.io/github/repo-size/alteralt/myqiwi)](https://github.com/alteralt/myqiwi)


Возможности
======
* Переводы на любой Qiwi Кошелек
* Статистика по платежам
* Получение информации о пользователе
* Сортировка платежей по типу(в/из), валюте.
* Определение провайдера мобильного телефона


Использование
======
```python
import myqiwi
wallet = myqiwi.Wallet(token)
```

Быстрый туториал
======

Получить текущий баланс
----------------
```python
print(wallet.balance())
```

Отправка платежа
----------------
```python
payee = "7999778909" # Получатель платежа
sum = 50 # Сумма перевода. Обязательно в рублях!
comment = "Перевод сделан с помощью библиотеки myqiwi" # Необязательный аргумент

wallet.send_money(payee,sum,comment)
```

Генерация комментария и ожидание платежа
----------------

```python
need_sum = 100
resp = qiwi.gen_payment(need_sum) # Генерируем комментарий и ссылку к платежу

text = "Переведите {} рублей на номер {}, указав в комментариях {}"
text = text.format(need_sum, phone, resp["comment"])
print(text)
print("Ссылку на форму с оплатой: {}".format(resp["link"]))

payment = qiwi.search_payment(resp["comment"], need_sum=need_sum)

if payment["status"]:
    print("Поступило пополнение на сумму {} рублей!".format(payment["sum"]))
else:
    print("Пополнения не обнаружено! :(")
```
