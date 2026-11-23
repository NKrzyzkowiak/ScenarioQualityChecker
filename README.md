# Scenario Quality Checker (SQC)

## Opis projektu

Dla analityków dokumentujących wymagania funkcjonalne za pomocą scenariuszy nasza aplikacja **SQC (Scenario Quality Checker)** dostarczy informacji ilościowych oraz umożliwi wykrywanie problemów w wymaganiach funkcjonalnych zapisanych w postaci scenariuszy. Aplikacja będzie dostępna poprzez **GUI** a także jako **zdalne REST API** dzięki czemu można ją zintegrować z istniejącymi narzędziami.

---

## Zakres funkcjonalności

### Sprint #1 (zakres bieżący)
- **Zdalne REST API (JSON)** – przyjmowanie scenariusza w formacie JSON, transformacja do modelu obiektowego, uruchamianie wszystkich zaimplementowanych funkcji oraz zwracanie wyników w formacie JSON.
- **Zliczanie wszystkich kroków** – obliczanie łącznej liczby kroków w całym scenariuszu (łącznie ze wszystkimi bezpośrednimi i pośrednimi pod-scenariuszami).
- **Zliczanie kroków ze słowami kluczowymi** – obliczanie liczby kroków rozpoczynających się od słów kluczowych (`IF`, `ELSE`, `FOR EACH`) na wszystkich poziomach zagłębienia.
- **Numerowanie scenariusza** – generowanie tekstowej reprezentacji scenariusza z wielopoziomową numeracją kroków i pod-scenariuszy (np. `1.`, `2.`, `2.1.`, `2.1.1.`, `3.`).

### Planowane w kolejnych sprintach
- **Wykrywanie kroków bez aktora** – zwracanie listy kroków (z dowolnego poziomu zagłębienia), które nie rozpoczynają się od nazwy aktora (z pominięciem słów kluczowych).
- **Uproszczony widok scenariusza** – zwracanie scenariusza zawierającego pod-scenariusze tylko do określonego poziomu zagłębienia.
- **Interfejs użytkownika (GUI)** – graficzna warstwa aplikacji dla analityków.

---

## Notacja scenariuszy

Scenariusze przetwarzane przez aplikację SQC są zapisywane według następujących zasad:
- Scenariusz zawiera nagłówek określający jego **tytuł** i **aktorów** (zewnętrznych oraz aktora systemowego).
- Scenariusz składa się z **kroków** (każdy krok zawiera tekst).
- Kroki mogą zawierać **pod-scenariusze** (dowolny poziom zagłębień).
- Kroki mogą zaczynać się od słów kluczowych: `IF`, `ELSE`, `FOR EACH`.

### Przykładowy scenariusz

**Tytuł:** Dodanie książki  
**Aktorzy:** Bibliotekarz  
**Aktor systemowy:** System  

- Bibliotekarz wybiera opcję dodania nowej pozycji książkowej
- Wyświetla się formularz.
- Bibliotekarz podaje dane książki.
- `IF:` Bibliotekarz pragnie dodać egzemplarze książki
  - Bibliotekarz wybiera opcję definiowania egzemplarzy
  - System prezentuje zdefiniowane egzemplarze
  - `FOR EACH` egzemplarz:
    - Bibliotekarz wybiera opcję dodania egzemplarza
    - System prosi o podanie danych egzemplarza
    - Bibliotekarz podaje dane egzemplarza i zatwierdza.
    - System informuje o poprawnym dodaniu egzemplarza i prezentuje zaktualizowaną listę egzemplarzy.
- Bibliotekarz zatwierdza dodanie książki.
- System informuje o poprawnym dodaniu książki.

---

## Komunikacja przez REST API

Aplikacja będzie udostępniać wszystkie zaimplementowane funkcje poprzez zdalne **REST API**:
- **Wejście:** struktura scenariusza przesyłana w formacie **JSON** (słowniki i listy odzwierciedlające strukturę scenariusza), transformowana następnie do modelu obiektowego aplikacji.
- **Wyjście:** wyniki analizy i operacji zwracane w formacie **JSON**.

> Szczegółowa specyfikacja schematu JSON oraz lista endpointów zostaną uzupełnione po implementacji modelu obiektowego i API.

