import requests
class Ozon_tool:
    def __init__(self, today, kolvo_rub, val):
        self.today = today
        self.kolvo_rub = kolvo_rub
        self.val = val
    
    def calc(self): #калькулятор валют
        result = 0
        if self.kolvo_rub.isdigit():
            self.kolvo_rub = int(self.kolvo_rub)
            result = round(self.kolvo_rub / self.today, 2)
        return f"{self.kolvo_rub}₽  = {result} {self.val}"
    
class Valute_Manager:
    def __init__(self, val_code):
        self.url = 'https://www.cbr-xml-daily.ru/daily_json.js'
        self.kurs = None
        self.val_code = val_code
        
    def get_info(self):
        self.kurs = requests.get(self.url)
        if self.kurs.status_code == 200:
            self.kurs = self.kurs.json()
            
    def get_need_info(self):
        if not self.kurs:
            self.get_info()
            
        valute_data = self.kurs['Valute'][self.val_code]
        nominal = valute_data['Nominal']
        today = valute_data['Value'] / nominal
        yesterday = valute_data['Previous'] / nominal
        today = round(today * 1.02, 2)
        yesterday = round(yesterday * 1.02, 2)
        return today, yesterday
            

val = input('Выберите валюту:\n1 - USD | 2 - EUR | 3 - CNY | 4 - KZT\n ')
if val == '1':
    val = 'USD'
elif val == '2':
    val = 'EUR'
elif val == '3':
    val = 'CNY'
elif val == '4':
    val = 'KZT'
else:
    print('Ошибка')
    
print(f"1 - Выведи курс выбранной валюты \n2 - Калькулятор (RUB -> ...)\n0 - Выход")

data = Valute_Manager(val).get_need_info()
today, yesterday = data
while True:
    kommand = input('...')
    if kommand == '1':
       print(f"СЕГОДНЯ: 1 {val} = {today}₽\nВЧЕРА: 1 {val} = {yesterday}₽")
       if today > yesterday:
           print(f"Курс {val} растет📈\nЭто плохо!")
       elif today < yesterday:
           print(f'Курс {val} падает📉\nЭто хорошо!')
            
    elif kommand == '2':
        kolvo_rub = input('Введите количество рублей:')
        print(Ozon_tool(today, kolvo_rub, val).calc())
    elif kommand == '0':
        break
    else:
        print('Неверная команда!') 
