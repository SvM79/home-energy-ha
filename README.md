# home-energy-ha
P1 Dongle Pro + SMA STP integration med Home Assistant

# ⚡ Home Assistant Energy Integration  
**P1 Dongle Pro + SMA Sunny Tripower + Automatiserad återbetalning**

## 🎯 Syfte

- **Samla in och visualisera energidata från elmätare och växelriktare i Home Assistant. Automatisera återbetalningskalkyl utifrån produktionsdata och faktiska elkostnader och inkomst från försäljning.**
- **Utforska reglerfunktioner för att strypa produktion vid negativa elpriser.**
---

## 🧩 Hårdvara

- **HP Laptop**
- **Synology NAS**
- **P1 Dongle Pro (med extern strömförsörjning och passiv RJ12-splitter)**
- **P1/HAN-port** 
- **SMA STP 8.0 växelriktare** (via Modbus TCP)
- **RJ12-RJ45 kabel** 
- **RJ45 adapter (hona till lödningsfri kontakt)**

---

## 🔌 Datakällor

### 1. Elmätare via P1
- Import/export
- Momentanförbrukning
- Fasinformation 

### 2. SMA växelriktare via Modbus TCP
- Solproduktion (W & kWh)
- Frekvens, spänning, aktiv/reaktiv effekt
- Status

---

## 🏠 Home Assistant Integration

- `ESPHome` för(P1-avläsning)
- `modbus:` i `configuration.yaml` för SMA
- Egna `template:`-sensorer:
  - Självförsörjningsgrad
  - Köpt/såld el
  - Beräkning av egenförbrukning vid solproduktion
  - Återbetalning

---

## 💰 Automatiserad kostnadsuppföljning (Planerade funktioner)

- Avskrivningsberäkning
- Användning av fakturadata¨
- Användning av Nordpool data i kombination med personliga elavtalsförhållanden.

### 🔁 Resultat i HA

- Sensor: `sensor.total_energy_cost`
- Sensor: `sensor.payback_ratio`  
  `"Installationen är återbetalad till 36%"`

---

## 📊 Dashboard

- Lovelace-panel för energibalans
- Kort för:
  - Produktion & konsumtion
  - Såld/köpt el
  - Återbetalningstrend
  - Senaste faktura

---

## 🛡️ Säkerhet & Privacy

- Mailbox med starkt lösenord + 2FA
- Fakturor och data lagras endast lokalt
- MQTT- eller REST-endpoint inom lokalt nätverk

---


---

## ✅ Status (initial)

- [X] Projektplanering
- [X] Hårdvarubeställning
- [X] Repo och mappar VS Code, Github
- [X] ESPHome konfigurerat för P1
- [X] Modbus-uppkoppling mot SMA testad
- [X] Sensorer skapade i HA
- [X] Dashboard påbörjad


---

## 🚧 Planerade funktioner & vidare utforskning

Det här projektet innehåller även idéer och funktioner som planeras eller utforskas längre fram:

### 🔍 Fakturaparsing (utforskas)
Funktionen för parsing av fakturor via e-post är än så länge ett fristående spår under utvärdering. Script och struktur testas separat innan en skarp integration görs. Syftet är att ersätta manuell inmatning med automatiserad återbetalningskalkyl.

### ⚡ Nord Pool-integration (under uppbyggnad)
Spotprisdata kommer att integreras i Home Assistant. Det är ännu oklart exakt hur dessa data kommer att användas, men möjliga tillämpningar inkluderar:
- Visualisering av verkligt timpris
- Möjlighet att via input formulär lägga in personliga avtalsförutsättningar.
- Beslutsunderlag för automatiseringar

### ⛔ Produktion under negativa elpriser (idé/förstudie)
En framtida möjlighet som undersöks är att minska eller helt stoppa produktionen under negativa elpriser. Detta skulle kunna uppnås genom:
- Fjärrstyrning av växelriktaren via Modbus (om möjligt)
- Alternativt lastdump via styrning av förbrukare som värmare eller batteri.
- Automatisk aktivering utifrån Nord Pool-data

Denna funktion kräver både teknisk förstudie och utvärdering av påverkan på garantier och anläggningens livslängd.

---

