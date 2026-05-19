# Flutter — instalacja i przydatne komendy

## 📋 Spis treści

* [⚡ Szybki start](#-szybki-start-15-minut)
* [📦 Instalacja Flutter SDK](#-instalacja-flutter-sdk)
* [🔍 Weryfikacja instalacji](#-weryfikacja-instalacji)
* [⚠️ Najczęstsze problemy](#️-najczęstsze-problemy)
* [🚀 Tworzenie pierwszego projektu](#-tworzenie-pierwszego-projektu)
* [🛠️ Przydatne komendy](#️-przydatne-komendy)
* [🐛 Debugowanie w VSCode](#-debugowanie-w-vscode)

---

# 🪟 Windows

## ⚡ Szybki start (15 minut)

Jeśli chcesz po prostu zacząć pisać aplikacje Flutter bez czytania całego poradnika:

```powershell
# 1. Zainstaluj wtyczkę Flutter do VSCode
code --install-extension Dart-Code.flutter

# 2. W VSCode:
# Ctrl+Shift+P → Flutter: New Project
# VSCode sam pobierze Flutter SDK (zwykle trzeba potwierdzić po prawej na dole)

# 3. Sprawdź instalację
flutter doctor

# 4. Stwórz projekt i uruchom
flutter create moj_super_projekt
cd moj_super_projekt
flutter run -d windows
```

---

# 📦 Instalacja Flutter SDK

> Flutter nie posiada oficjalnego pakietu w `winget`.

## Metoda 1 — VSCode (zalecana)

Najprostszy sposób instalacji:

1. Zainstaluj wtyczkę Flutter:

```powershell
code --install-extension Dart-Code.flutter
```

2. Otwórz VSCode
3. Naciśnij `Ctrl+Shift+P`
4. Wybierz `Flutter: New Project`
5. Kliknij `Download SDK`
6. Wybierz folder instalacji (np. `C:\flutter`)

VSCode pobierze i skonfiguruje Flutter SDK automatycznie.

---

## Metoda 2 — ręczna instalacja

1. Pobierz Flutter SDK:

[https://docs.flutter.dev/get-started/install/windows](https://docs.flutter.dev/get-started/install/windows)

2. Wypakuj archiwum np. do:

```text
C:\flutter
```

3. Dodaj do zmiennej `PATH`:

```text
C:\flutter\bin
```

4. Zrestartuj terminal.

---

# 🔍 Weryfikacja instalacji

## Sprawdzenie wersji

```powershell
flutter --version
```

Jeśli komenda nie działa:

* zrestartuj terminal,
* sprawdź czy Flutter został dodany do `PATH`.

---

## Diagnostyka środowiska

```powershell
flutter doctor
```

Flutter sprawdzi:

* Android SDK,
* Visual Studio,
* urządzenia,
* wymagane zależności.

---

## Typowe błędy `flutter doctor`

### `[✗] Android toolchain`

Brakuje Android SDK.

### Jak naprawić

1. Zainstaluj Android Studio:

[https://developer.android.com/studio](https://developer.android.com/studio)

2. Uruchom kreator instalacji.
3. Zaakceptuj licencje:

```powershell
flutter doctor --android-licenses
```

4. Sprawdź ponownie:

```powershell
flutter doctor
```

---

### `[!] Visual Studio`

Brakuje komponentów do budowania aplikacji desktopowych Windows.

Jeśli tworzysz tylko aplikacje mobilne lub webowe — możesz to zignorować.

### Jeśli chcesz budować aplikacje Windows

1. Pobierz Visual Studio Community:

[https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/)

2. Zaznacz:

```text
Desktop development with C++
```

3. Dokończ instalację.

---

# ⚠️ Najczęstsze problemy

## VSCode nie widzi Flutter SDK

Najczęściej problem pojawia się wtedy, gdy Flutter SDK znajduje się w folderze typu:

```text
Desktop
Pulpit
OneDrive
```

VSCode czasami nie wykrywa takich ścieżek automatycznie.

### Krok 1 — skopiuj ścieżkę do Flutter SDK

Otwórz folder Flutter SDK (ten gdzie znajduje się folder `bin` oraz plik `flutter_console.bat`) i skopiuj pełną ścieżkę.

Przykład:

```text
C:\Users\TwojeImie\Desktop\workshop-flutter\flutter
```

### Krok 2 — dodaj ścieżkę w VSCode

1. Otwórz ustawienia (`Ctrl+,`)
2. Wyszukaj:

```text
Flutter Sdk Paths
```

3. Znajdź opcję:

```text
Dart: Flutter Sdk Paths
```

4. Kliknij `Add Item`
5. Wklej ścieżkę do Flutter SDK
6. Kliknij `OK`

### Krok 3 — restart VSCode

Zamknij wszystkie okna VSCode i uruchom program ponownie.

Po restarcie:

```text
Ctrl+Shift+P → Flutter
```

powinno pokazać dostępne komendy Flutter.

---

## `flutter` nie działa w terminalu

Jeśli terminal pokazuje:

```text
flutter : The term 'flutter' is not recognized...
```

Flutter nie został dodany do zmiennej środowiskowej `PATH`.

### Krok 1 — znajdź folder `bin`

Ścieżka powinna wyglądać podobnie do:

```text
C:\flutter\bin
```

lub:

```text
C:\Users\TwojeImie\Desktop\flutter\bin
```

### Krok 2 — otwórz zmienne środowiskowe

1. Naciśnij klawisz `Windows`
2. Wpisz:

```text
env
```

3. Otwórz:

```text
Edytuj zmienne środowiskowe systemu
```

4. Kliknij:

```text
Zmienne środowiskowe...
```

### Krok 3 — edytuj `Path`

1. W sekcji `Zmienne użytkownika` znajdź:

```text
Path
```

2. Kliknij `Edytuj`
3. Kliknij `Nowy`
4. Dodaj ścieżkę do folderu `bin`
5. Zapisz zmiany

### Krok 4 — restart terminala

Zrestartuj:

* VSCode,
* PowerShell,
* Command Prompt.

Następnie uruchom:

```powershell
flutter doctor
```

Jeśli Flutter rozpocznie diagnostykę — wszystko działa poprawnie.

---

## Wtyczka Flutter w VSCode nie działa

Jeśli po wpisaniu:

```text
Ctrl+Shift+P → Flutter
```

widzisz:

```text
No matching commands
```

wykonaj pełny reset rozszerzeń.

### Reset rozszerzeń Flutter/Dart

1. Otwórz `Extensions` (`Ctrl+Shift+X`)
2. Odinstaluj:

   * `Flutter`
   * `Dart`
3. Otwórz:

```text
Ctrl+Shift+P → Developer: Reload Window
```

4. Po restarcie zainstaluj ponownie rozszerzenie Flutter
5. Uruchom VSCode ponownie

Po instalacji:

```text
Ctrl+Shift+P → Flutter: New Project
```

powinno działać poprawnie.

---

# 🚀 Tworzenie pierwszego projektu

## Utworzenie projektu

```powershell
flutter create moj_nowy_projekt
```

## Wejście do katalogu

```powershell
cd moj_nowy_projekt
```

## Uruchomienie aplikacji

```powershell
flutter run
```

---

## VSCode

Możesz również użyć:

```text
Ctrl+Shift+P → Flutter: New Project
```

---

# 🛠️ Przydatne komendy

## Uruchamianie i build

| Komenda                  | Opis                      |
| ------------------------ | ------------------------- |
| `flutter run`            | Uruchom aplikację         |
| `flutter run -d windows` | Uruchom aplikację Windows |
| `flutter run -d chrome`  | Uruchom aplikację webową  |
| `flutter build apk`      | Zbuduj APK Android        |
| `flutter build windows`  | Zbuduj aplikację Windows  |

---

## Tryby uruchamiania

| Komenda                 | Opis                    |
| ----------------------- | ----------------------- |
| `flutter run --debug`   | Tryb debug              |
| `flutter run --profile` | Profilowanie wydajności |
| `flutter run --release` | Tryb produkcyjny        |
| `flutter logs`          | Logi urządzenia         |

---

## Hot Reload / Hot Restart

Podczas działania `flutter run`:

| Skrót | Akcja             |
| ----- | ----------------- |
| `r`   | Hot Reload        |
| `R`   | Hot Restart       |
| `q`   | Zamknij aplikację |
| `h`   | Lista skrótów     |

### VSCode

| Skrót      | Akcja       |
| ---------- | ----------- |
| `Ctrl+F5`  | Hot Reload  |
| `Shift+F5` | Hot Restart |
| `F5`       | Debugowanie |

---

## Zarządzanie pakietami

```powershell
# Pobierz zależności
flutter pub get

# Dodaj pakiet
flutter pub add nazwa_pakietu

# Aktualizacja pakietów
flutter pub upgrade

# Sprawdzenie dostępnych aktualizacji
flutter pub outdated
```

---

## Diagnostyka

```powershell
# Szczegółowa diagnostyka
flutter doctor -v

# Lista urządzeń
flutter devices

# Wyczyść cache buildów
flutter clean

# Analiza kodu
flutter analyze

# Testy
flutter test
```

---

# 🐛 Debugowanie w VSCode

## Breakpointy

1. Kliknij obok numeru linii kodu
2. Naciśnij `F5`
3. Użyj panelu `Debug`

Dostępne sekcje:

* `Variables`
* `Call Stack`
* `Watch`

---

## Flutter DevTools

Instalacja:

```powershell
flutter pub global activate devtools
flutter devtools
```

Lub w VSCode:

```text
Ctrl+Shift+P → Flutter: Open DevTools
```

---

## 🐧 Linux (Arch)

## ⚡ TL;DR — start w 15 minut
Jeśli nie chce ci się czytać tego długiego i nudnego dokumentu, tutaj skrócona instrukcja instalacji.
Potem zapraszam do sekcji z listą [przydatnych komend](#%EF%B8%8F-przydatne-komendy)

```bash
# 1. Zainstaluj używając yay
yay -S flutter

# 2. Sprawdź czy działa
flutter doctor

# 3. Zainstaluj wtyczkę do VSCode
code --install-extension Dart-Code.flutter

# 4. Nowy projekt i uruchom
flutter create moj_super_projekt && cd moj_super_projekt && flutter run -d linux
```

---

## 📦 Instalacja Fluttera

### Metoda 1: AUR (zalecana)

Flutter jest dostępny w AUR jako `flutter`. Użyj `yay`:

```bash
yay -S flutter
```

> Instalacja pobiera Flutter SDK + Dart — może zająć drobną chwilę.

### Metoda 2: Ręcznie (bez AUR helpera)

```bash
# 1. Sklonuj z AUR
git clone https://aur.archlinux.org/flutter.git
cd flutter

# 2. Zbuduj i zainstaluj
makepkg -si
```

---
> Gotowe!

## 🔧 Konfiguracja po instalacji

Zweryfikuj instalację:

```bash
flutter --version
```

> Jeśli komenda nie została znaleziona, zrestartuj shella

Sprawdź co brakuje w systemie:

```bash
flutter doctor
```

> `flutter doctor` podpowie co doinstalować (np. Android SDK, licencje, itp.)

### Zaakceptuj licencje Android (jeśli potrzebne)

```bash
flutter doctor --android-licenses
```

---

## 🧩 Wtyczka Flutter do VSCode

### Instalacja przez GUI

1. Otwórz VSCode
2. Przejdź do **Extensions** (`Ctrl+Shift+X`)
3. Wyszukaj `Flutter`
4. Zainstaluj oficjalną wtyczkę **Flutter** (autor: Dart Code)
   - Automatycznie instaluje też wtyczkę **Dart**

### Instalacja przez terminal

```bash
code --install-extension Dart-Code.flutter
```

### Weryfikacja

Po restarcie VSCode:
- W prawym dolnym rogu powinno pojawić się **"Flutter"** / wersja Dart
- Otwórz Command Palette (`Ctrl+Shift+P`) i wpisz `Flutter` — zobaczysz listę dostępnych komend

---

## 🚀 Tworzenie pierwszego projektu

```bash
# Stwórz nowy projekt
flutter create moj_nowy_swietny_projekt

# Wejdź do katalogu
cd moj_nowy_swietny_projekt

# Uruchom
flutter run
```

W VSCode możesz też użyć:
- `Ctrl+Shift+P` → **Flutter: New Project**

---

## 🛠️ Przydatne komendy

### Uruchamianie i budowanie

| Komenda | Opis |
|---|---|
| `flutter run` | Uruchom aplikację (domyślnie debug) |
| `flutter run -d linux` | Uruchom natywnie na Linux |
| `flutter run -d chrome` | Uruchom w przeglądarce (web) |
| `flutter build apk` | Zbuduj APK dla Android |
| `flutter build linux` | Zbuduj natywną aplikację Linux |

### Debugowanie

| Komenda | Opis |
|---|---|
| `flutter run --debug` | Tryb debug (domyślny) |
| `flutter run --profile` | Tryb profilowania (wydajność) |
| `flutter run --release` | Tryb produkcyjny |
| `flutter logs` | Wyświetl logi urządzenia |

### Hot reload / Hot restart

Gdy aplikacja działa (`flutter run`):

| Skrót | Akcja |
|---|---|
| `r` | **Hot Reload** — odświeża UI bez restartu (ultra szybki) |
| `R` | **Hot Restart** — restartuje aplikację (resetuje stan) |
| `q` | Wyjdź z aplikacji |
| `h` | Pokaż wszystkie skróty |

W VSCode:
- **Hot Reload**: `Ctrl+F5` lub przycisk ⚡ w górnym pasku
- **Hot Restart**: `Shift+F5`
- **Debugowanie**: `F5`

### Zarządzanie pakietami (pub)

```bash
# Zainstaluj zależności z pubspec.yaml
flutter pub get

# Dodaj nowy pakiet
flutter pub add nazwa_pakietu

# Zaktualizuj pakiety
flutter pub upgrade

# Sprawdź dostępne aktualizacje
flutter pub outdated
```

### Diagnostyka

```bash
# Pełna diagnostyka środowiska
flutter doctor -v

# Lista podłączonych urządzeń
flutter devices

# Wyczyść build cache
flutter clean

# Analizuj kod (linter)
flutter analyze

# Uruchom testy
flutter test
```

---

## 🐛 Debugowanie w VSCode

1. Ustaw **breakpoint** — kliknij na marginesie obok linii kodu (czerwona kropka)
2. Naciśnij `F5` (Start Debugging)
3. Użyj panelu **Debug** po lewej stronie:
   - **Variables** — podgląd zmiennych
   - **Call Stack** — stos wywołań
   - **Watch** — obserwuj wyrażenia

### Flutter DevTools

Rozbudowane narzędzia deweloperskie z podglądem widgetów, wydajności, pamięci:

```bash
flutter pub global activate devtools
flutter devtools
```

Albo w VSCode: `Ctrl+Shift+P` → **Flutter: Open DevTools**

## 🔗 Przydatne linki

- [Dokumentacja Flutter](https://docs.flutter.dev)
- [pub.dev — paczki dla Flutter/Dart](https://pub.dev)
- [Flutter Cookbook — gotowe przepisy](https://docs.flutter.dev/cookbook)
- [AUR: flutter](https://aur.archlinux.org/packages/flutter)
