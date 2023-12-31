# Technologie i aplikacje webowe
Warunkiem zaliczenia jest przygotowanie aplikacji serwerowej opartej o REST API oraz raportu komunikacji z tym serwerem według podanego scenariusza.
Raport komunikacji z serwerem powinien zawierać zestawienie wywołanych żądań do serwera wraz z adresem zasobu, metodą http, body żądania, nagłówkami żądania oraz odpowiedzią serwera na wysłane żądanie w postaci kodu odpowiedzi http oraz body odpowiedzi.

W ramach projektu należy przygotować REST API bazujące na zasobie przedmiotów na studia. Każdy przedmiot na studia powinien zawierać informacje o:
- nazwie przedmiotu,
- punktach ects,
- numerze sali, w której odbywają się zajęcia,
- informacji czy przedmiot kończy się egzaminem.

Serwer powinien umożliwiać wprowadzanie nowych przedmiotów, pobieranie przedmiotów oraz usuwanie przedmiotów.
Ocena za zaliczenie będzie uzależniona od złożoności przygotowanego rozwiązania.
W podstawowej wersji serwer powinien umożliwiać wprowadzanie nowego przedmiotu, pobieranie wszystkich przedmiotów i usuwanie wszystkich przedmiotów. W rozszerzonej wersji serwer powinien pozwalać na filtrację pod kątem informacji o tym czy przedmiot kończy się egzaminem oraz o filtrację po numerze sali, w której obywają się zajęcia. Serwer powinien także udostępniać możliwość pobierania konkretnego zasobu w oparciu o identyfikator oraz usuwanie konkretnego przedmiotu w oparciu o identyfikator.
***
## Scenariusz do raportu:
## 1. Wprowadzenie przedmiotów do systemu w podanej kolejności:
```
Metoda: POST
Adres zasobu: http://localhost:8080/api/activities
Nagłówki: Content-Type: application/json
Request Body:
{"nazwa":"Metodologie Obiektowe", "ects":2, "sala":"216", "egzamin":"true"}
```
Odpowiedź:
HTTP Code: 200 OK
Body: brak

Pozostałe przedmioty, odpowiednio body:
```
{"nazwa":"Testowanie Oprogramowania", "ects":1, "sala":"216", "egzamin":"false"}
{"nazwa":"Technologie i Aplikacje Webowe", "ects":3, "sala":"208", "egzamin":"false"}
{"nazwa":"Zarządzanie Projektem Informatycznym", "ects":2, "sala":"216", "egzamin":"false"}
{"nazwa":"Zaawansowane Technologie Bazodanowe", "ects":3, "sala":"208", "egzamin":"false"}
{"nazwa":"Technologie Komponentowe i Sieciowe", "ects":2, "sala":"208", "egzamin":"true"}
```
Według danych
- Nazwa: Metodologie obiektowe, ECTS: 2, Sala: 216, Egzamin: tak,
- Nazwa: Testowanie oprogramowania, ECTS: 1, Sala: 216, Egzamin: nie,
- Nazwa: Technologie i aplikacje webowe, ECTS: 3, Sala: 208, Egzamin: nie,
- Nazwa: Zarządzanie projektem informatycznym, ECTS: 2, Sala: 216, Egzamin: nie,
- Nazwa: Zaawansowane technologie bazodanowe, ECTS: 3, Sala: 208, Egzamin: nie,
- Nazwa: Technologie komponentowe i sieciowe, ECTS: 2, Sala: 208, Egzamin: tak
***
## 2. Pobranie wszystkich przedmiotów,
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/activities
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: 

[
    {
        "id": 1,
        "nazwa": "Metodologie Obiektowe",
        "ects": 2,
        "sala": "216",
        "egzamin": true
    },
    {
        "id": 2,
        "nazwa": "Testowanie Oprogramowania",
        "ects": 1,
        "sala": "216",
        "egzamin": false
    },
    {
        "id": 3,
        "nazwa": "Technologie i Aplikacje Webowe",
        "ects": 3,
        "sala": "208",
        "egzamin": false
    },
    {
        "id": 4,
        "nazwa": "Zarządzanie Projektem Informatycznym",
        "ects": 2,
        "sala": "216",
        "egzamin": false
    },
    {
        "id": 5,
        "nazwa": "Zaawansowane Technologie Bazodanowe",
        "ects": 3,
        "sala": "208",
        "egzamin": false
    },
    {
        "id": 6,
        "nazwa": "Technologie Komponentowe i Sieciowe",
        "ects": 2,
        "sala": "208",
        "egzamin": true
    }
]
```
***
## 3. Pobranie przedmiotów, które mają egzamin,
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/activities?egzamin=tak
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: 
[
    {
        "id": 1,
        "nazwa": "Metodologie Obiektowe",
        "ects": 2,
        "sala": "216",
        "egzamin": true
    },
    {
        "id": 6,
        "nazwa": "Technologie Komponentowe i Sieciowe",
        "ects": 2,
        "sala": "208",
        "egzamin": true
    }
]
```
***
## 4. Pobranie przedmiotów, które odbywają się w sali 216,
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/activities?sala=216
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: 
[
    {
        "id": 1,
        "nazwa": "Metodologie Obiektowe",
        "ects": 2,
        "sala": "216",
        "egzamin": true
    },
    {
        "id": 2,
        "nazwa": "Testowanie Oprogramowania",
        "ects": 1,
        "sala": "216",
        "egzamin": false
    },
    {
        "id": 4,
        "nazwa": "Zarządzanie Projektem Informatycznym",
        "ects": 2,
        "sala": "216",
        "egzamin": false
    }
]
***
```
## 5. Pobranie przedmiotów które nie mają egzaminu i odbywają się w sali 208,
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/activities?egzamin=nie&sala=208
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: 
[
    {
        "id": 3,
        "nazwa": "Technologie i Aplikacje Webowe",
        "ects": 3,
        "sala": "208",
        "egzamin": false
    },
    {
        "id": 5,
        "nazwa": "Zaawansowane Technologie Bazodanowe",
        "ects": 3,
        "sala": "208",
        "egzamin": false
    }
]
***
```
## 6. Pobranie przedmiotu o identyfikatorze 3,
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/activities/3
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: 
{
    "id": 3,
    "nazwa": "Technologie i Aplikacje Webowe",
    "ects": 3,
    "sala": "208",
    "egzamin": false
}
```
***
## 7. Pobranie przedmiotu o identyfikatorze 15,
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/activities/15
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 404 Not found
Body: brak
```
***
## 8. Usunięcie przedmiotu o identyfikatorze 2,
```
Metoda: DELETE
Adres zasobu: http://localhost:8080/api/activities/2
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: brak
```
***
## 9. Pobranie wszystkich przedmiotów,
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/activities
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: 
[
    {
        "id": 1,
        "nazwa": "Metodologie Obiektowe",
        "ects": 2,
        "sala": "216",
        "egzamin": true
    },
    {
        "id": 3,
        "nazwa": "Technologie i Aplikacje Webowe",
        "ects": 3,
        "sala": "208",
        "egzamin": false
    },
    {
        "id": 4,
        "nazwa": "Zarządzanie Projektem Informatycznym",
        "ects": 2,
        "sala": "216",
        "egzamin": false
    },
    {
        "id": 5,
        "nazwa": "Zaawansowane Technologie Bazodanowe",
        "ects": 3,
        "sala": "208",
        "egzamin": false
    },
    {
        "id": 6,
        "nazwa": "Technologie Komponentowe i Sieciowe",
        "ects": 2,
        "sala": "208",
        "egzamin": true
    }
]
```
***
## 10. Usunięcie wszystkich przedmiotów,
```
Metoda: DELETE
Adres zasobu: http://localhost:8080/api/activities
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: brak
```
***
## 11. Pobranie wszystkich przedmiotów.
```
Metoda: GET
Adres zasobu: http://localhost:8080/api/actiities
Nagłówki: Content-Type: application/json
Request Body: brak

Odpowiedź:
HTTP Code: 200 OK
Body: 
[]
```
## API endpointy 
```
api/activities
GET //- lista zajęć; możliwe argumenty filtrowania
 nazwa=<String>
 ects=<Integer>
 sala=<String>
 egzamin=<true/false>
POST //- dodanie zajęć, wymagane argumenty:
	nazwa=<Sring>&ects=<integer>&sala=<String>&egzamin=<true/false>
DELETE // - usunięcie wszystkich zajęć 
api/activities/{id}
GET //- pobranie informacji o danym przedmiocie po jego id
DELETE // - usunięcie danego przedmiotu
  ```