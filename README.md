# PHPMyAdmin

### Разворачивание в docker-compose локально:

1) Заполнить .env
2) Создать phpunit.xml в корне проекта, скопировав содержимое phpunit.xml.dist
3) В phpunit.xml в секции php заполнить переменные TESTSUITE_USER и TESTSUITE_PASSWORD в соответсвии с теми, которые задали в .env для MYSQL_ROOT_PASSWORD и PMA_USER
4) `docker compose build`
5) `docker compose up -d`
6) `docker compose run --rm composer install --ignore-platform-req=ext-mysqli`
7) Проверить в браузере - должна открыться страница с локином - вводим значения PMA_USER и MYSQL_ROOT_PASSWORD

### Выполнение тестов:

unit - `docker compose exec -it php vendor/bin/phpunit`
* Для успешного прохождения тестов может потребоваться vpn для доступа к https://www.phpmyadmin.net/ и прочим ресурсам
* Некоторые тесты нестабильны и выполняются не с первой попытки


e2e - `docker compose exec -it php vendor/bin/phpunit test/selenium`
* Веб интерфейс селениума доступен по порту 4444
* Скриншоты упавших e2e тестов лежат в директории `build/selenium`
* Некоторые тесты нестабильны и выполняются не с первой попытки
* Ряд тестов не проходят успешно в stable и master ветках:
  * PhpMyAdmin\Tests\Selenium\Database\ProceduresTest::testAddProcedure
  * PhpMyAdmin\Tests\Selenium\ImportTest::testDbImport
  * PhpMyAdmin\Tests\Selenium\ImportTest::testTableImport
  * PhpMyAdmin\Tests\Selenium\ImportTest::testServerImport
