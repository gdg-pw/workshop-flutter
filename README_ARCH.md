# 🐧 Flutter na Arch Linux

## 📋 Spis treści

* [⚡ TL;DR — start w 15 minut](#-tldr--start-w-15-minut)
* [📦 Instalacja Fluttera](#-instalacja-fluttera)
* [🔧 Konfiguracja po instalacji](#-konfiguracja-po-instalacji)
* [🧩 Wtyczka Flutter do VSCode](#-wtyczka-flutter-do-vscode)
* [🚀 Tworzenie pierwszego projektu](#-tworzenie-pierwszego-projektu)
* [🛠️ Przydatne komendy](#️-przydatne-komendy)
* [🐛 Debugowanie w VSCode](#-debugowanie-w-vscode)
* [🔗 Przydatne linki](#-przydatne-linki)

---

## ⚡ TL;DR — ULTRA SKOMPRESOWANA INSTRUKCJA

Jeśli nie chce ci się czytać tego długiego i nudnego dokumentu, tutaj skrócona instrukcja instalacji.
Potem zapraszam do sekcji z listą [przydatnych komend](#️-przydatne-komendy).

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

> Gotowe!

---

## 🔧 Konfiguracja po instalacji

Zweryfikuj instalację:

```bash
flutter --version
```

> Jeśli komenda nie została znaleziona, zrestartuj shella.

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

W VSCode możesz też użyć: `Ctrl+Shift+P → Flutter: New Project`

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

Albo w VSCode: `Ctrl+Shift+P → Flutter: Open DevTools`

---

## 🔗 Przydatne linki

- [Dokumentacja Flutter](https://docs.flutter.dev)
- [pub.dev — paczki dla Flutter/Dart](https://pub.dev)
- [Flutter Cookbook — gotowe przepisy](https://docs.flutter.dev/cookbook)
- [AUR: flutter](https://aur.archlinux.org/packages/flutter)
