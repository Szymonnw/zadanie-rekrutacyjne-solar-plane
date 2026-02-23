# zadanie-rekrutacyjne-solar-plane
System transmisji obrazu i tekstu z  symulowanego drona w czasie rzeczywistym (Python/Flask)
# SolarPlane - Przesyłanie zdjęć i tekstu z drona

Prosty system do odbierania danych z drona.
Dron (klient) wysyła zdjęcie i komunikat, a serwer (stacja naziemna) pokazuje to na stronie WWW, która sama się odświeża.

## 🛠️ Jak to działa?

1. **Dron (skrypt `dron_klient.py`):**
   * Bierze zdjęcia z folderu `zdjecia_z_drona`.
   * Wysyła je co 10 sekund na serwer za pomocą zwykłego żądania HTTP POST.
   * Dorzuca do każdego zdjęcia krótki tekst związany z nazwa zdjęcia.

2. **Serwer (skrypt `stacja_serwer.py`):**
   * Odbiera pliki i zapisuje je w folderze `static/uploads`.
   * Wystawia stronę internetową, która wyświetla ostatnie odebrane zdjęcie i tekst.
   * Strona odświeża się automatycznie co 3 sekundy, więc nie musisz nic klikać, żeby zobaczyć nowe dane.(wybrałem ten sposób bo jest to szybkie prototypoe rozwiązanie problemu updatowania, ale jest tu duze pole do ulepszenia, poprzez implementacja WebSockets czyli stworzenie stałej komunikacji między serwerem a przeglądarką. Dzięki temu nowe zdjęcie pojawiałoby się na ekranie od razu po odebraniu go przez serwer (push notification)

## Jak to uruchomić

pip install flask requests
w pliku drom_klient.py jest adres localhost http://127.0.0.1:5000 przez co program działa lokalnie na urządzeniu na kotrym jest odpalony,
ale jesli zmieni sie to na http://(adres IP):5000 i pominie zapore sieci to bedzie działał na urządzeniach podpiętych do tej samej sieci.
najpierw nalezy odpalić python stacja_serwer.py potem otworzyc strone, potem odpalic python dron_klient.py. i patrzec na zmieniające się zdjęcia:) 
