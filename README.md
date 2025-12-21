# 🧭 AI Weekend Planner (n8n Workflow)

Automatyczny asystent planowania weekendu, który przekształca listę pomysłów z arkuszy Google w atrakcyjny plan, wysyłany bezpośrednio na Telegram w każdy piątkowy wieczór.

## 🚀 Funkcje
* **Automatyczne wyzwalanie:** Startuje w każdy piątek o 17:00.
* **Integracja z Google Sheets:** Pobiera bazy danych ulubionych aktywności i miejsc.
* **AI Planner (GPT-4o):** Układa zrównoważony plan (ruch + rozwój + odpoczynek) bez sztywnych godzin.
* **Pętla interaktywna:** Pozwala zaakceptować plan lub poprosić o nową propozycję bezpośrednio w aplikacji Telegram.

## 🛠 Struktura Workflow

Workflow składa się z następujących etapów:

1.  **Trigger (Cron):** Harmonogram ustawiony na każdy piątek, godzina 17:00.
2.  **Data Ingestion:** Pobieranie rekordów z Google Sheets (Arkusze: *Aktywności* oraz *Miejsca*).
3.  **Context Preparation:** Węzeł Function (JavaScript) mapuje dane do formatu zrozumiałego dla AI.
4.  **AI Engine:** Model OpenAI (GPT-4o) generuje propozycję weekendu na podstawie promptu systemowego, dbając o "konkurowanie ze scrollowaniem social mediów".
5.  **User Interaction (Telegram):**
    * Wysłanie planu za pomocą funkcji `sendAndWait` z interaktywnymi przyciskami.
    * **Węzeł IF:** Sprawdza wybór użytkownika (Akceptacja vs. Nowy plan).
    * Jeśli **Nie**: Powrót do ponownego losowania i generowania nowej propozycji.
    * Jeśli **Tak**: Finalizacja procesu i aktualizacja statusu w arkuszu.

## 📋 Wymagania

Aby uruchomić ten workflow, potrzebujesz następujących poświadczeń (Credentials) w n8n:
* **Google Sheets API:** Do odczytu i zapisu danych w arkuszach.
* **OpenAI API:** Do komunikacji z modelem GPT-4o-latest.
* **Telegram Bot API:** Do wysyłania wiadomości i obsługi formularzy.

## 📄 Zasady Planowania AI
Model jest instruowany, aby tworzyć plan według specyficznych zasad:
* **Brak godzin:** Tylko bloki: rano / popołudnie / wieczór.
* **Równowaga:** Każdy dzień musi zawierać ruch, odpoczynek bez poczucia winy oraz 1 element rozwojowy.
* **Styl:** Spokojny, przyjazny i inspirujący.
* **Dodatki:** Każdy plan kończy się "Intencją weekendu" oraz "Pytaniem rozwojowym".

---

### Jak zainstalować?
1. Skopiuj kod JSON workflow.
2. W n8n kliknij **Import from JSON** i wklej kod.
3. Skonfiguruj identyfikatory arkuszy (`sheetId`) oraz połącz swoje konta API.
4. Aktywuj workflow przełącznikiem **Active**.
