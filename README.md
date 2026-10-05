Interaktywny raport analityczny w Power BI przygotowany w ramach wolontariatu analitycznego **#BI_NGO** z okazji jubileuszu 25-lecia polskojęzycznej Wikipedii we współpracy ze Stowarzyszeniem Wikimedia Polska.

# 25 lat Polskiej Wikipedii – Historia zapisana w liczbach 📊🌐

🔗 **[Zobacz interaktywny raport w Power BI Service](https://app.powerbi.com/view?r=eyJrIjoiY2FkN2I3MzMtYmM0NS00NDBhLWExN2EtMjQxZTQ1YzM2MjhiIiwidCI6IjQ1NDIwZThkLTg1NTItNGEwMy05YjkyLWE5MzFlZjgzOWQzZiIsImMiOjh9)**

---

## 🎯 Cel i zakres projektu

Celem projektu jest wielowymiarowa analiza trendów, wolumenu odsłon oraz dynamiki zainteresowań czytelników polskiej Wikipedii w latach **2016–2026**. Raport łączy twarde dane analityczne z kontekstem kulturowym, społecznym i historycznym.

### Główne obszary analizy:
1. **Struktura ruchu i agenci:** Porównanie aktywności użytkowników rzeczywistych (`user`), robotów indeksujących (`spider`) oraz ruchu zautomatyzowanego (`automated`) wraz z analizą dynamiki (w tym wzrostu automatyzacji o ponad 548%).
2. **Dynamiczny ranking TOP N artykułów:** Interaktywne zestawienie najpopularniejszych haseł z możliwością płynnego sterowania liczbą wyświetlanych pozycji za pomocą **parametru liczbowego**.
3. **Piki oglądalności i linia czasu:** Identyfikacja nagłych skoków oglądalności powiązanych z kluczowymi wydarzeniami (Mistrzostwa Europy/Świata, śmierć królowej Elżbiety II, katastrofa promu Jan Heweliusz).
4. **Analiza kategorii tematycznych:** Śledzenie trendów rok do roku (YoY) w podziale na 7 głównych obszarów tematycznych.

---

## ⚙️ Kluczowa funkcjonalność: Dynamiczny parametr TOP N

W raporcie zaimplementowano **parametr pola / wartości liczbowej** (*Numeric Range Parameter*), który pozwala użytkownikowi decydować, ile czołowych artykułów chce w danej chwili analizować (np. TOP 5, TOP 10, TOP 20):
* **Sterowanie wizualizacjami:** Zmiana suwaka parametru dynamicznie filtruje zarówno wykres słupkowy najpopularniejszych artykułów, jak i wykres kołowy udziału w odsłonach.
* **Elastyczność analizy:** Umożliwia płynne przejście od wąskiej czołówki rankingu do szerszej perspektywy bez konieczności przeładowywania raportu.

---

## 🏗️ Architektura i przygotowanie danych

### 1. Źródła danych
* Zbiory `1-ogladalnosc_monthly.csv` oraz `5-top_1000_artykulow_monthly.csv` udostępnione przez organizatorów projektu **BI-NGO** / Wikimedia Polska.
* Zbiory ruchu ogólnego z podziałem na typy agentów oraz dostęp.
* Archiwalne fotografie i grafiki: **Wikimedia Commons** (stylizowane czarno-białe miniatury w osi czasu i etykietach).

### 2. Kategoryzacja danych (Python & Pandas + LLM)
Surowy zbiór TOP 1000 nie posiadał bezpośrednio określonych kategorii tematycznych. W celu pogłębienia analizy opracowano reguły mapowania i skrypt w języku Python:
* **Narzędzia:** `Python 3.x`, biblioteka `pandas`.
* **Wsparcie LLM (ChatGPT / Gemini):** Wygenerowanie matrycy słów kluczowych i reguł semantycznych dla unikalnych tytułów artykułów.
* **Wynik:** Każdy artykuł został przypisany do jednej z 7 kategorii:
  * *Historia i biografie*
  * *Wydarzenia na świecie / katastrofy / wojna*
  * *Sport*
  * *Kultura i rozrywka*
  * *Gospodarka i biznes*
  * *Technologia i nauka*
  * *Zdrowie i medycyna*

*Kategoryzacja została przeprowadzona przy użyciu skryptu w języku Python (`categorization.py`) z wykorzystaniem biblioteki Pandas.*
---

## 📐 Modelowanie i DAX (Power BI)

W projekcie wykorzystano zaawansowaną logikę DAX, m.in.:
* **Obsługa parametru TOP N:** Powiązanie wartości wybranej na suwaku z rankingiem miary odsłon za pomocą funkcji `RANKX` oraz reguł odfiltrowywania pozycji poza zadanym zakresem.
* **Dynamika zmian r/r (Year-over-Year):** Porównanie liczby odsłon z analogicznymi okresami z wykorzystaniem kalkulacji czasowych.
* **Formatowanie warunkowe pików:** Dynamiczne wyróżnianie rocznych maksimów odsłon przekraczających próg 1 mln wyświetleń.
* **Dynamiczne tytuły i etykiety:** Automatyczna adaptacja nagłówków wykresów do aktualnego kontekstu filtrów i ram czasowych.

---

## 📁 Struktura repozytorium

```text
├── data/                  # Informacje o źródłach danych / słownik pojęć
├── Wikipedia_Raport.pbix  # Plik źródłowy Power BI Desktop
└── README.md              # Dokumentacja projektu

👩‍💻 Autorka
Ilona Sekudewicz

Projekt zrealizowany w ramach wyzwania BI-NGO (edycja: 25 lat Polskiej Wikipedii, 2026).
