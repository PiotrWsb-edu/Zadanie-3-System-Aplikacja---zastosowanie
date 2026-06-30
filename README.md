Aplikacja w Python
Jest wypożyczalnia różnych typów pojazdów. System pozwala na rejestrację użytkowników, przeglądanie floty pojazdów, kontrolowanie ich dostępności oraz wypożyczania i zwrotu pojazdów.
- Vehicle (Klasa abstrakcyjna) - Definiuje wspólny kontrakt, właściwości oraz logikę zmiany stanów dla wszystkich pojazdów w systemie.
właściwości - id (str), brand (str), model (str), rental_rate (float), is_available (bool).
metody - rent(), return_vehicle(), vehicle_type() (abstrakcyjna)
- ElectricVehicle (Klasa abstrakcyjna / Interfejs) - Wymusza posiadanie mechanizmu zasilania prądem dla pojazdów elektrycznych
właściwości - czysty interfejs definiujący zachowanie
metody - charge() (abstrakcyjna)
- Car (Dziedziczy po Vehicle) - Reprezentuje samochód
właściwości - fuel_type (str) oraz właściwości dziedziczone po Vehicle
metody - vehicle_type() (nadpisana)
- Bike (Dziedziczy po Vehicle) - Reprezentuje rower
właściwości - frame_size (int) oraz właściwości dziedziczone po Vehicle
metody - vehicle_type() (nadpisana)
- Scooter (Dziedziczy po Vehicle oraz implementuje ElectricVehicle) - Reprezentuje hulajnogę/skuter elektryczny
właściwości - battery_level (int) oraz właściwości dziedziczone po Vehicle
metody - vehicle_type() (nadpisana), charge()
- User Opisuje klienta wypożyczalni i przechowuje historię jego operacji
właściwości - user_id (str), name (str), rental_history
metody - add_rental_to_history(), view_history()
- Rental Reprezentuje pojedynczą transakcję wypożyczenia łączącą pojazd z użytkownikiem
właściwości - rental_id (str), user_id (str), vehicle (obiekt Vehicle), rent_date (str)
metody - vehicle
- RentalManager Centralny zarządca systemu, odpowiadający za procesy wypożyczeń, zwrotów oraz spójność danych
właściwości - fleet, users
metody - add_vehicle(), add_user(), rent_vehicle_to_user(), return_vehicle_from_user(), show_fleet()

Klasa Rental agreguje referencję do pełnego obiektu klasy Vehicle. Pojazd istnieje w systemie niezależnie od faktu jego wypożyczenia. Agregacja
Klasa Rental zawiera pole tekstowe _user_id zamiast bezpośredniego trzymania całego obiektu User. Relacja przez id
Klasa User posiada listę _rental_history, w której gromadzone są obiekty typu Rental. Lista, kolekcja
Klasa Scooter dziedziczy po klasie bazowej Vehicle oraz implementuje interfejs ElectricVehicle. Dziedziczenie, implementacja interfejsu
Klasy Car, Bike , Scooter dziedziczą po klasie Vehicle. Dziedziczenie
Klasa Scooter dziedziczy po klasie ElectricVehicle, relacja ta wymusza, aby Hulajnoga/Skuter posiadała i realizowała metodę charge()
Klasy Vehicle, User są powiązane z klasą RentalManager. Lista, kolekcja

- Enkapsulacja - Pola takie jak _is_available czy _battery_level zostały ukryte za pomocą konwencji pojedynczego podkreślenia. Dostęp do nich z zewnątrz realizowany jest przez bezpieczne właściwości (gettery @property), a ich modyfikacja odbywa się wyłącznie przez metody biznesowe (rent(), charge()), które pilnują poprawności stanów.
- Dziedziczenie - Widoczne w hierarchii pojazdów: Vehicle (klasa ogólna) Car, Bike, Scooter (klasy przejmujące wspólne cechy).
- Polimorfizm - Metoda vehicle_type() zaimplementowana w klasie bazowej jako abstrakcyjna, została nadpisana w każdej klasie szczegółowej. Wywołanie jej w pętli menedżera wyświetla specyficzny format danych dla każdego pojazdu, mimo operowania na ogólnym typie Vehicle.
- Abstrakcja - Klasy Vehicle oraz ElectricVehicle wykorzystują moduł abc.ABC i metody oznaczone @abstractmethod. Blokuje to możliwość stworzenia surowego obiektu tych klas i definiuje ścisły kontrakt dla klas pochodnych.

AI było użyte w celu porządkowania relacji i wyjaśnienia błędów i ich poprawienie 
