# Entity Framework project documentation

## Project quick info

![project](/Attachments/Screenshot_176.jpg))

### Projekt typu Web API

ASP.NET Core Web API:

![project start](/Attachments/Screenshot_1.jpg)

Enable OpenAPI support - dodanie Swaggera do projektu (narzędzie do wysyłania zapytań do serwera HTTP):

![Swagger](/Attachments/Screenshot_2.jpg)

## Dodawanie encji

Tworzymy klasy i ich właściwości, aby odwzorowować strukturę tabeli:

![Properties](/Attachments/Screenshot_3.jpg)

## Konfiguracja

Aby skonfiguracja połaczenie z bazą danych i dodać klasę reprezentującą kontekst całej bazy:

![NuGet](/Attachments/Screenshot_4.jpg)

![EFCore](/Attachments/Screenshot_5.jpg)

![EFCoreSQLServer](/Attachments/Screenshot_6.jpg)

Paczka z dodatkowymi komendami aby np. tworzyć migracje i update'ować baze danych:

![Tools](/Attachments/Screenshot_7.jpg)

W pliku .csproj możesz zobaczyć zainstalowane paczki:

![Packages](/Attachments/Screenshot_8.jpg)

## Główna klasa reprezentująca bazę danych

![mainClass](/Attachments/Screenshot_9.jpg)

Connection String powinien być trzymany w zewnętrznym pliku konfiguracyjnym:

![config](/Attachments/Screenshot_10.jpg)

Spinamy Connection String na poziomie kontenera depency injection:

Definicja rejestracji naszego kontekstu baz danych w kontenerze depency injection:

![di](/Attachments/Screenshot_12.jpg)

Konfigurowanie połączenia z bazą danych:

![config](/Attachments/Screenshot_13.jpg)