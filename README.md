# Dokumentacja zadania „Chatme”

## Opis uruchomienia aplikacji

Aplikacja została stworzona w framework’u javascriptu Vue.js. Do jej uruchomienia
konieczna jest instalacja paketów z node_modules narzędziem npm i poleceniem npm
install. Wymagany jest również zainstalowany lokalny llm ollama i model mistral.
Poleceniem npm run dev uruchomiamy aplikację.
## Opis uruchomienia docker
Obraz możemy zbudować poleceniem
![image](https://github.com/Mydlyk/Chatme/assets/65900710/31cc6398-2a55-447f-91df-255e1f32cfd5)

Wtedy aplikacja powinna znajdować się pod linkiem: http://localhost:5173/
Oraz uruchomić kontener za pomocą
docker run -it -p 8080:80 --rm --name dockerize-vuejs-app-1 vuejs/dockerize-vuejs-app
![image](https://github.com/Mydlyk/Chatme/assets/65900710/c7cc9103-1873-41ef-8a22-f5fa4f11ca91)

Wtedy aplikacja powinna znajdować po linkiem: http://localhost:8080/
Podczas dockeryzacji występuje błąd ponieważ, npm nie może zbudować aplikacji przez
import ollamy
![image](https://github.com/Mydlyk/Chatme/assets/65900710/a5374b7e-0bd0-4fa9-8ad4-2d9166e0501a)

Po usunięciu tego importu z app.vue docker się zbuduje jednak aplikacja nie będzie
działać poprawnie.

## Opis działania aplikacji

Aplikacja działa jak chat z sztuczną inteligencją. Użytkownik przesyła poprzez chat
zapytania a framework’u vue komunikuję się z ollama i zwraca w języku polskim
odpowiedzi kontekst wypowiedzi jest utrzymywany.

## Opis Kodu aplikacji
![image](https://github.com/Mydlyk/Chatme/assets/65900710/b8b526e4-07ea-41ec-b5e0-e47cb8e3b821)

Funkcja sendMessage w app.vue dodaje do tablicy wiadomości(historii) wiadomość
użytkownika oraz wywołuje funkcje odpowiedzialne za wysłanie zapytania do ollamy i na
bieżąca aktualizacji wypowiedzi sztucznej inteligencji jak w chacie gpt.
![image](https://github.com/Mydlyk/Chatme/assets/65900710/fe9d8fe2-f260-44e4-9f1c-780e6f4e6d27)

Funkcja SendToGpt wysyła pytanie oraz odbiera odpowiedz od ollamy.
![image](https://github.com/Mydlyk/Chatme/assets/65900710/3e9a5368-5f54-4732-924d-0b8edfa3494d)

Asynchroniczna Funkcja updateMessages dzięki asynchroniczności funkcji chat po kolei
będzie odpowiadał na kolejne pytania użytkownika oraz na bieżąco aktualizuje
wypowiedź sztucznej inteligencji.
![image](https://github.com/Mydlyk/Chatme/assets/65900710/ac1781e1-251a-4fec-92f4-6bd3aa90d0f7)

Aplikacja składa się z 3 komponentów chatu, pola do wpisywania oraz tytułu.
Komponenty znajdują się w folderze components a wszystkie style w pliku style.css.

## Działanie aplikacji
![image](https://github.com/Mydlyk/Chatme/assets/65900710/e0cf0d06-1c61-494a-a672-92085fc57dd9)

Rysunek 1 Działanie aplikacji oraz pokazanie utrzymywania kontekstu wypowiedzi
