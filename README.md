# Дипломный проект по профессии «Тестировщик ПО»

Основная задача - автоматизация тестирования комплексного сервиса, взаимодействующего с СУБД и API Банка.

Приложение - это веб-сервис, который предлагает купить тур по определённой цене двумя способами:
1. Обычная оплата по дебетовой карте.
2. Уникальная технология: выдача кредита по данным банковской карты.

![img](https://github.com/Solomatin2006/Diplom/blob/main/images/Home_page.png)

Само приложение не обрабатывает данные по картам, а пересылает их банковским сервисам:

- сервису платежей, далее Payment Gate;
- кредитному сервису, далее Credit Gate.

Приложение в собственной СУБД должно сохранять информацию о том, успешно ли был совершён платёж и каким способом. Данные карт при этом сохранять не допускается.

Подробно с дипломным заданием можно ознакомиться по [ссылке](https://github.com/netology-code/qa-diploma)

## Тестовая документация

- [План тестирования](https://github.com/Solomatin2006/Diplom/blob/main/documents/Plan.md)
- [Отчёт по итогам тестирования](https://github.com/Solomatin2006/Diplom/blob/main/documents/Report.md)
- [Отчёт по итогам автоматизации](https://github.com/Solomatin2006/Diplom/blob/main/documents/Summary.md)

## Запуск приложения
### Подготовительный этап
1. Установить и запустить IntelliJ IDEA;
2. Установать и запустить Docker Desktop;
3. Скопировать репозиторий с Github [по ссылке](https://github.com/Solomatin2006/Diplom).
4. Открыть проект в IntelliJ IDEA.

## Процедура запуска автотестов

1. В терминале выполнить команду:
   `docker-compose up`
2. В новой вкладке терминала запустить приложение командой:

Для использования СУБД PostgreSQL:
`java -jar artifacts/aqa-shop.jar --spring.datasource.url=jdbc:postgresql://localhost:5432/app`

Для использования СУБД MySQL:
`java -jar artifacts/aqa-shop.jar --spring.datasource.url=jdbc:mysql://localhost:3306/app`

- приложение будет доступно по ссылке: http://localhost:8080/

3. В новой вкладке терминала запустить тесты командой:

Для СУБД PostgreSQL:
`./gradlew clean test "-Ddb.url=jdbc:postgresql://localhost:5432/app"`

Для СУБД MySQL:
`./gradlew clean test "-Ddb.url=jdbc:mysql://localhost:3306/app"`

4. Запустить сервис формирования отчетов Allure командой:
   `./gradlew allureServe `

- сформированный отчет откроется автоматически в браузере.

5. Для остановки Allure в терминале ввести комбинацию клавиш Ctrl+C, нажать клавишу y.
6. Для остановки контейнеров ввести в терминале команду:
   `docker-compose down`