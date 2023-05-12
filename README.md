## Требования к реализации

1. Создать абстрактный класс для работы с API сайтов с вакансиями. Реализовать классы, наследующиеся от абстрактного класса, для работы с конкретными платформами. Классы должны уметь подключаться к API и получать вакансии.
2. Создать класс для работы с вакансиями. В этом классе самостоятельно определить атрибуты, такие как название вакансии, ссылка на вакансию, зарплата, краткое описание или требования и т. п. (не менее четырех) Класс должен поддерживать методы сравнения вакансий между собой по зарплате и валидировать данные, которыми инициализируются его атрибуты.
3. Определить абстрактный класс, который обязывает реализовать методы для добавления вакансий в файл, получения данных из файла по указанным критериям и удаления информации о вакансиях. Создать класс для сохранения информации о вакансиях в JSON-файл. Дополнительно, по желанию, можно реализовать классы для работы с другими форматами, например с CSV- или Excel-файлом, с TXT-файлом.
4. Создать функцию для взаимодействия с пользователем. Функция должна взаимодействовать с пользователем через консоль. Самостоятельно придумать сценарии и возможности взаимодействия с пользователем. Например, позволять пользователю указать, с каких платформ он хочет получить вакансии, ввести поисковый запрос, получить топ N вакансий по зарплате, получить вакансии в отсортированном виде, получить вакансии, в описании которых есть определенные ключевые слова, например "postgres" и т. п.
5. Объединить все классы и функции в единую программу.

## Требования к реализации в парадигме ООП

1. Абстрактный класс и классы для работы с API сайтов с вакансиями должны быть реализованы в соответствии с принципом наследования.
2. Класс для работы с вакансиями должен быть реализован в соответствии с принципом инкапсуляции и поддерживать методы сравнения вакансий между собой по зарплате.
3. Классы и другие сущности в проекте должны удовлетворять минимум первым двум требованиям принципов SOLID.

## Платформы для сбора вакансий

1. **hh.ru** ([ссылка на API](https://github.com/hhru/api/blob/master/docs/general.md))
2. **superjob.ru** ([ссылка на API](https://api.superjob.ru/))
    - Прежде чем начать использовать API от SuperJob, необходимо [зарегистрироваться](https://www.superjob.ru/auth/login/?returnUrl=https://api.superjob.ru/register/) и получить токен для работы. Подробная инструкция дается по ссылке описания документации в разделе [Getting started](https://api.superjob.ru/#gettin). При регистрации приложения можно указать произвольные данные.

## Выходные данные

- Информация о вакансиях, полученная с разных платформ, сохраненная в JSON-файл.
- Отфильтрованные и отсортированные вакансии, выводимые пользователю через консоль.
В данном домашнем задании было реализованно
## 1: получение вакансий с двух сайтов.
    1)  HeadHunter
        class Headhanter(Engine):
        """ Класс по поиску вакансий на хх.ру"""     
    2)  SuperJob
        class SuperJob(Engine):
        """ Класс получения вакансий на суперджобс """
        
## 2: Фильтрация вакансий.
     1) Вывод всех вакансий
        select
     2) Вывод вакансий с минимальной заработной платой и максимальной
        sorted_vacancies_by_salary_from_asc
        sorted_vacancies_by_salary_from_desc
        sorted_vacancies_by_salary_to_asc
    
## 3: Каждый сайт и получение информации с него выведен в отдельный файл(класс).
    С получение API ,добавление всех вакансий в словарь, с выводом з.п ,удобный форматом,и информацией о парсинге.
    Функция получения API
        def get_request(self)
        
## Ститический метод фитрации з.п
        @staticmethod
        def get_salary(salary):
            formatted_salary = [None, None]
            if salary and salary["from"] and salary["from"] != 0:
                formatted_salary[0] = salary["from"] if salary["currency"].lower() == "rur" else salary["from"] * 78
            if salary and salary["to"] and salary["to"] != 0:
                formatted_salary[1] = salary["to"] if salary["currency"].lower() == "rur" else salary["to"] * 78
                return formatted_salary
       
## 4: Был организованн метод вывода ошибки по парсингу.
    class ParsingError(Exception):
        """ Класс ошибки """
        Рабочая функция 
            def get_vacancies(self, pages_count=1):  # вывод о парсинге кол-ве вакансий и наличие ошибки
        while self.__params["page"] < pages_count:
            print(f"HeadHunter, парсинг страницы {self.__params['page'] + 1}", end=": ")
            try:
                values = self.get_request()
            except ParsingError:
                print("Ошибка получения данный ")
                break
            print(f"Найдено {len(values)} вакансий")
            self.__vacancies.extend(values)
            self.__params["page"] += 1
            
## 5: Был реализован класс с добавлением чтением записью сортировкой информации
    class Connector:
        """ Класс записи, сортировки и чтения информации"""

