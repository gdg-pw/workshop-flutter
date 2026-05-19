# 🍎 Flutter na macOS

## 📋 Spis treści

* [⚡ TL;DR — start w 15 minut](#-tldr--start-w-15-minut)
* [📦 Instalacja Flutter SDK](#-instalacja-flutter-sdk)
* [🔧 Konfiguracja po instalacji](#-konfiguracja-po-instalacji)
* [⚠️ Najczęstsze problemy](#️-najczęstsze-problemy)
* [🧩 Wtyczka Flutter do VSCode](#-wtyczka-flutter-do-vscode)
* [🚀 Tworzenie pierwszego projektu](#-tworzenie-pierwszego-projektu)
* [🛠️ Przydatne komendy](#️-przydatne-komendy)
* [🐛 Debugowanie w VSCode](#-debugowanie-w-vscode)
* [🔗 Przydatne linki](#-przydatne-linki)

---

## ⚡ TL;DR — start w 15 minut

Jeśli nie chce ci się czytać tego długiego i nudnego dokumentu, tutaj skrócona instrukcja instalacji.
Potem zapraszam do sekcji z listą [przydatnych komend](#️-przydatne-komendy).

```bash
# 1. Zainstaluj Homebrew (jeśli jeszcze nie masz)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 2. Zainstaluj Flutter przez Homebrew
brew install --cask flutter

# 3. Sprawdź czy działa
flutter doctor

# 4. Zainstaluj wtyczkę do VSCode
code --install-extension Dart-Code.flutter

# 5. Nowy projekt i uruchom
flutter create moj_super_projekt && cd moj_super_projekt && flutter run -d macos
```

---

## 📦 Instalacja Flutter SDK

### Metoda 1: Homebrew (zalecana)

Homebrew to najpopularniejszy menedżer pakietów na macOS. Jeśli jeszcze go nie masz:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> Na Apple Silicon (M1/M2/M3) po instalacji Homebrew wykonaj dodatkowo:
> ```bash
> echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
> source ~/.zshrc
> ```

Następnie zainstaluj Flutter:

```bash
brew install --cask flutter
```

### Metoda 2: VSCode (bez terminala)

1. Zainstaluj wtyczkę Flutter:

```bash
code --install-extension Dart-Code.flutter
```

2. Otwórz VSCode
3. Naciśnij `Ctrl+Shift+P`
4. Wybierz `Flutter: New Project`
5. Kliknij `Download SDK`
6. Wybierz folder instalacji (np. `~/flutter`)

VSCode pobierze i skonfiguruje Flutter SDK automatycznie.

### Metoda 3: Ręczna instalacja

1. Sprawdź architekturę swojego Maca:
   - **Apple Silicon (M1/M2/M3):** pobierz wersję `arm64`
   - **Intel:** pobierz wersję `x64`

2. Pobierz Flutter SDK ze strony: [https://docs.flutter.dev/get-started/install/macos](https://docs.flutter.dev/get-started/install/macos)

3. Wypakuj archiwum do wybranego folderu, np.:

```bash
unzip ~/Downloads/flutter_macos_*.zip -d ~/develop/
```

4. Dodaj Flutter do PATH — otwórz `~/.zshrc` w edytorze i dodaj na końcu:

```bash
export PATH="$HOME/develop/flutter/bin:$PATH"
```

5. Przeładuj konfigurację shella:

```bash
source ~/.zshrc
```

---

## 🔧 Konfiguracja po instalacji

### Weryfikacja instalacji

```bash
flutter --version
```

> Jeśli komenda nie została znaleziona, zrestartuj terminal lub sprawdź PATH.

### Diagnostyka środowiska

```bash
flutter doctor
```

> `flutter doctor` podpowie co doinstalować. Na macOS najczęściej brakuje Xcode lub CocoaPods.

### Xcode (wymagane dla iOS i macOS)

1. Zainstaluj Xcode z App Store (ok. 10 GB, zacznij pobieranie **teraz**)
2. Skonfiguruj narzędzia wiersza poleceń:

```bash
sudo sh -c 'xcode-select -s /Applications/Xcode.app/Contents/Developer && xcodebuild -runFirstLaunch'
```

3. Zaakceptuj licencję Xcode:

```bash
sudo xcodebuild -license accept
```

### CocoaPods (wymagane dla iOS)

```bash
sudo gem install cocoapods
```

> Na Apple Silicon może być potrzebne:
> ```bash
> sudo gem uninstall ffi && sudo gem install ffi -- --enable-libffi-alloc
> ```

### Zaakceptuj licencje Android (jeśli potrzebne)

```bash
flutter doctor --android-licenses
```

---

## ⚠️ Najczęstsze problemy

### `flutter` nie działa w terminalu

Jeśli terminal pokazuje `command not found: flutter`, Flutter nie jest w PATH.

**Krok 1 — znajdź folder `bin`**

Ścieżka powinna wyglądać podobnie do:

```text
/Users/TwojeImie/develop/flutter/bin
```

lub jeśli instalowałeś przez Homebrew:

```text
/opt/homebrew/bin/flutter
```

**Krok 2 — dodaj do PATH**

Otwórz `~/.zshrc` w edytorze i dodaj:

```bash
export PATH="$HOME/develop/flutter/bin:$PATH"
```

Następnie:

```bash
source ~/.zshrc
```

---

### `[✗] Xcode` w `flutter doctor`

Brakuje Xcode lub narzędzi wiersza poleceń.

**Jak naprawić:**

```bash
sudo sh -c 'xcode-select -s /Applications/Xcode.app/Contents/Developer && xcodebuild -runFirstLaunch'
sudo xcodebuild -license accept
```

Jeśli tworzysz tylko aplikacje Android lub webowe — możesz to zignorować.

---

### `[✗] CocoaPods` w `flutter doctor`

```bash
sudo gem install cocoapods
```

Jeśli błąd na Apple Silicon:

```bash
sudo gem uninstall ffi
sudo gem install ffi -- --enable-libffi-alloc
sudo gem install cocoapods
```

---

### VSCode nie widzi Flutter SDK

**Krok 1 — skopiuj ścieżkę do Flutter SDK**

```bash
which flutter
```

Skopiuj wynik (np. `/Users/TwojeImie/develop/flutter`).

**Krok 2 — dodaj ścieżkę w VSCode**

1. Otwórz ustawienia (`Cmd+,`)
2. Wyszukaj `Flutter Sdk Paths`
3. Znajdź opcję `Dart: Flutter Sdk Paths`
4. Kliknij `Add Item`
5. Wklej ścieżkę do Flutter SDK
6. Kliknij `OK`

**Krok 3 — restart VSCode**

Zamknij wszystkie okna VSCode i uruchom ponownie.

---

## 🧩 Wtyczka Flutter do VSCode

### Instalacja przez terminal

```bash
code --install-extension Dart-Code.flutter
```

### Instalacja przez GUI

1. Otwórz VSCode
2. Przejdź do **Extensions** (`Cmd+Shift+X`)
3. Wyszukaj `Flutter`
4. Zainstaluj oficjalną wtyczkę **Flutter** (autor: Dart Code)
   - Automatycznie instaluje też wtyczkę **Dart**

### Weryfikacja

Po restarcie VSCode:
- W prawym dolnym rogu powinno pojawić się **"Flutter"** / wersja Dart
- Otwórz Command Palette (`Cmd+Shift+P`) i wpisz `Flutter` — zobaczysz listę dostępnych komend

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

W VSCode możesz też użyć: `Cmd+Shift+P → Flutter: New Project`

---

## 🛠️ Przydatne komendy

### Uruchamianie i budowanie

| Komenda | Opis |
|---|---|
| `flutter run` | Uruchom aplikację (domyślnie debug) |
| `flutter run -d macos` | Uruchom natywnie na macOS |
| `flutter run -d chrome` | Uruchom w przeglądarce (web) |
| `flutter build apk` | Zbuduj APK dla Android |
| `flutter build ipa` | Zbuduj aplikację iOS |
| `flutter build macos` | Zbuduj natywną aplikację macOS |

### Tryby uruchamiania

| Komenda | Opis |
|---|---|
| `flutter run --debug` | Tryb debug (domyślny) |
| `flutter run --profile` | Tryb profilowania (wydajność) |
| `flutter run --release` | Tryb produkcyjny |
| `flutter logs` | Wyświetl logi urządzenia |

### Hot Reload / Hot Restart

Gdy aplikacja działa (`flutter run`):

| Skrót | Akcja |
|---|---|
| `r` | **Hot Reload** — odświeża UI bez restartu (ultra szybki) |
| `R` | **Hot Restart** — restartuje aplikację (resetuje stan) |
| `q` | Wyjdź z aplikacji |
| `h` | Pokaż wszystkie skróty |

W VSCode:
- **Hot Reload**: `Cmd+F5` lub przycisk ⚡ w górnym pasku
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

Albo w VSCode: `Cmd+Shift+P → Flutter: Open DevTools`

---

## 🔗 Przydatne linki

- [Dokumentacja Flutter](https://docs.flutter.dev)
- [Instalacja Flutter na macOS](https://docs.flutter.dev/get-started/install/macos)
- [pub.dev — paczki dla Flutter/Dart](https://pub.dev)
- [Flutter Cookbook — gotowe przepisy](https://docs.flutter.dev/cookbook)
- [Homebrew](https://brew.sh)
