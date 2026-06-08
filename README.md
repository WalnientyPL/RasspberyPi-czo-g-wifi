# 🚜 Raspberry Pi Heavyweight RC Tracked Tank (Wi-Fi + Camera)

Projekt z technikum
Projekt oprogramowania dla gąsienicowego robota bojowo-rozpoznawczego opartego na minikomputerze **Raspberry Pi**. Pojazd dysponuje napędem różnicowym o dużej mocy, niezależną sekcją zasilania, oświetleniem roboczym oraz bezprzewodowym sterowaniem poprzez dedykowaną aplikację WWW wraz z podglądem wideo live.

---

## 📊 Analiza konstrukcji i komponentów
Na podstawie budowy hardware'owej, w projekcie wydzielono następujące układy:
* **Jednostka centralna:** Raspberry Pi wyposażone w aktywny układ chłodzenia oraz moduł kamery.
* **Układ napędowy:** Dwa wysokomomentowe silniki DC z przekładniami, połączone z gąsienicami (sterowanie różnicowe).
* **Zasilanie hybrydowe (Dual-Bus):** * Pakiet LiPo Redox (zasilanie logiki Raspberry Pi i sensorów).
  * Akumulatory żelowe/ołowiowe 12V (główne zasilanie wysokoprądowe silników).
* **Power Distribution:** Centralny panel z 6 przełącznikami kołyskowymi (Rocker Switches) do sekwencyjnego uruchamiania podzespołów i ochrony obwodów.
* **Oświetlenie:** Dwa mocne reflektory LED (halogeny) zamontowane na froncie pojazdu.
* **Układ wykonawczy:** Profesjonalny sterownik silników DC (mostek H) z masywnym radiatorem odprowadzającym ciepło.

---

## 🛠️ Architektura Oprogramowania

System sterowania został podzielony na warstwy:
1. **Backend (Python):** Serwer asynchroniczny (Flask lub FastAPI) zarządzający pinami GPIO za pomocą biblioteki `RPI.GPIO` / `gpiozero` oraz generujący strumień wideo (MJPEG).
2. **Frontend (HTML5 / CSS3 / JS):** Responsywny panel sterowania uruchamiany w dowolnej przeglądarce. Obsługuje sterowanie za pomocą:
   * Klawiszy ekranowych (mysz/dotyk)
   * Klawiatury fizycznej (WSAD / strzałki)
   * API Gamepada (możliwość sterowania padem od PS4/Xboxa podłączonym do komputera/telefonu)

---

## 🔌 Sugerowany schemat logiczny GPIO (Raspberry Pi)

| Komponent | Typ sygnału | Pin GPIO | Opis |
| :--- | :---: | :---: | :--- |
| **Lewy Silnik - PWM** | Output (PWM) | **GPIO 12** | Kontrola prędkości lewej gąsienicy |
| **Lewy Silnik - DIR** | Output (Digital) | **GPIO 5** | Kierunek obrotu lewej gąsienicy |
| **Prawy Silnik - PWM**| Output (PWM) | **GPIO 13** | Kontrola prędkości prawej gąsienicy |
| **Prawy Silnik - DIR**| Output (Digital) | **GPIO 6** | Kierunek obrotu prawej gąsienicy |
| **Oświetlenie (Reflektory)** | Output (Digital) | **GPIO 23** | Załączanie świateł przednich przez przekaźnik / MOSFET |

---

## 🚀 Instrukcja instalacji i uruchomienia

### 1. Przygotowanie Raspberry Pi
Upewnij się, że masz włączoną obsługę kamery oraz interfejsów w konfiguracji systemu:
```bash
sudo raspi-config
# Włącz interfejs kamery (Legacy Camera lub I2C/SPI zależnie od wersji OS)
