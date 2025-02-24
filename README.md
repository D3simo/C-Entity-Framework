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

Connection String powinien być trzymany w zewnętrznym pliku konfiguracyjnym: appsettings.Development.json

![config](/Attachments/Screenshot_10.jpg)

Spinamy Connection String na poziomie kontenera depency injection:

Definicja rejestracji naszego kontekstu baz danych w kontenerze depency injection:

![di](/Attachments/Screenshot_12.jpg)

Konfigurowanie połączenia z bazą danych:

![config](/Attachments/Screenshot_13.jpg)

Ostatni krok to dodanie publicznego konstruktora do którego przekarzemy zmienna DbContextOptions dla klasy DbContext. Dzięki konstruktorowi kontener depency injection będzie w stanie skonfigurować klase MyBoardsContext. Połączenie z bazą danych jest konfigurowane w zależności od środowiska: patrz appsettings.Development.json

![construct](/Attachments//Screenshot_14.jpg)

## Klucze

Jedna z konwencji aby utworzyć klucz główny to encja z nazwą **ID**:

![mainkey](/Attachments/Screenshot_17.jpg)

lub przy użyciu atrybutu **[Key]**:

![keyattr](/Attachments/Screenshot_16.jpg)

Dodajemy klucze główne do encji Adress, Comment, Tag, User, WorkItem.

Dodawanie złożonego klucza głównego do encji User.
W klasie DbContextu MyBoardsContext należy dodać metodę, do której należy konfiguracja modelu bazy danych. Tak wyglądałaby metoda. aby skonfigurować wzłożony klucz dla encji User:

![userkey](/Attachments/Screenshot_23.jpg)

W takim przypadku możnaby się pozbyc klucza głównego typu Guid dla encji User, i entity framework stworzyłby klucz główny złożony bazując na metodzie, którą stworzyliśmy.

### Nazwa kolumny

Jeżeli chcemy zachować nazwę właściwości i chcemy zmienić nazwę kolumny należy użyć atrybutu [Column] z namespace'u System.ComponentsModel.DataAnnotations.Schema:

![columnname](/Attachments/Screenshot_24.jpg)

### Typy właściwości

Natomiast jeżeli chcemy zmienić domyślny typ generowany przez Entity Framework:

![columntype](/Attachments/Screenshot_25.jpg)

### Dokladność wartości właściwości

Jeżeli chcesz zmienić dokładność wartości zmiennoprzecinkowej:

![precision](/Attachments/Screenshot_26.jpg)

### Maksymalna długość właściwości

Jeżeli chcesz zmienić maksymalną długość string:

![maxlength](/Attachments/Screenshot_27.jpg)

### Nullable

Aby kolumna nie przyjmowała wartości typu NULL, przejdź do pliku .csproj głównego projektu: (globalne rozwiązanie lub dodanie "?" do typu właściwości lub skorzystanie z atrybuty **[Required]**)

![nullable](/Attachments/Screenshot_28.jpg)

## Atrybuty wlaściwości

Zamiast konfigurować właściwości w sposób jak wyżej, lepszym podejściem jest konfiguracja w OnModelCreating czyli konfiguracji modelu bazy danych.

![config](/Attachments/Screenshot_29.jpg)