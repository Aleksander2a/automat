# Automat do przekąsek
### 1. Aleksander Mazur, olekmazur@student.agh.edu.pl, https://github.com/Aleksander2a/automat
### 2. Opis modelowanego systemu:
Urządzenie, które służy do sprzedaży różnego rodzaju przekąsek, takich jak batony, chipsy, napoje i inne podobne produkty. Urządzenie przyjmuje płatność (i zwraca resztę w miarę potrzeby), użytkownik wpisuje numer wybranego produktu, automat zwraca produkt.
### 3. Spis komponentów:
System składa się z **19 komponentów**:
 - 2 process (controller i second_controller) - pełnią rolę kontrolerów systemu. Odpowiadają za zarządzanie i koordynację pracy innych komponentów
 - magistrala (bus_connection) - reprezentuje połączenie komunikacyjne pomiędzy różnymi komponentami systemu
 - pamięć (ram) - odnosi się do fizycznej pamięci operacyjnej (RAM), która przechowuje dane i instrukcje potrzebne do działania systemu. Pamięć RAM zapewnia dostęp do danych w czasie rzeczywistym
 - 2 procesory (main_processor i second_processor) - odpowiedzialne za wykonywanie instrukcji i obliczenia w systemie. Są to główne układy wykonawcze, które przetwarzają dane i wykonują operacje zgodnie z programem
 - 7 urządzeń:
   - chłodziarka - urządzenie służące do utrzymywania odpowiedniej temperatury w systemie
   - oswietlenie - odnosi się do komponentu, który steruje oświetleniem w systemie
   - silownik_spirali - urządzenie mechaniczne, które wykonuje ruch wzdłuż spirali, w skutek czego produkt wypada i jest gotowy do odbioru przez użytkownika
   - wyswietlacz - odpowiedzialny za prezentację informacji użytkownikowi (np. wybrany numer produktu, cena itd.)
   - panel - jest interfejsem użytkownika, który umożliwia interakcję z systemem poprzez fizyczny panel z przyciskami
   - licznik_monet - jest komponentem odpowiedzialnym za zliczanie monet wprowadzanych przez użytkownika
   - podajnik_monet - wydaje monety użytkownikowi w przypadku, gdy należy zwrócić resztę
 - 6 wątków:
   - wyswietl - odnosi się do części programu odpowiedzialnej za obsługę i wyświetlanie informacji na wyświetlaczu
   - zaplac - odpowiada za obsługę procesu płatności. Może to obejmować sprawdzanie poprawności płatności, obliczenie reszty i aktualizację odpowiednich danych
   - wydaj - odpowiedzialny za uruchomienie podajnika monet gdy należy wydać resztę
   - przyciski - obsługuję wartości wprowadzane przez użytkownika w panelu fizycznym
   - chlodzenie - odpowiedzialny za sterowanie chłodzeniem w automacie w oparciu o aktualną i zadaną temperaturę
   - swiatlo - odpowiedzialny za sterowanie oświetleniem w automacie w oparciu o aktualną i zadaną jasność
### 4. Model - rysunek:
 - System:![automat](https://github.com/Aleksander2a/automat/blob/main/automat.jpg)
 - Proces controller:![controller](https://github.com/Aleksander2a/automat/blob/main/controller.jpg)
 - Proces second_controller:![second_controller](https://github.com/Aleksander2a/automat/blob/main/second_controller.jpg)
### 5. Proponowane metody analizy modelu, dostępne w Osate:
 - Analiza systemu:
   - BusLoad: 13 warning'ów, 0 błędów:
     - bus has no bandwidth budget
     - bus has no capacity
     - 11xconnection has no bandwidth budget:
       - device_panel.numer_out → process_controller.numer_in
       - device_licznik_monet.wartosc_monet_out → process_controller.wartosc_monet_in
       - process_controller.wyswietl_out → device_wyswietlacz.wyswietl_in
       - process_controller.ruch_spirala_out → device_silownik_spirali.ruch_spirala_in
       - process_controller.wydaj_monety_out → device_podajnik_monet.wydaj_monety_in
   - ConnectionConsistency: 0 warning'ów, 0 błędów
   - ConnectionBindingConsistency: 0 warning'ów, 0 błędów
