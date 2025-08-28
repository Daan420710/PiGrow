# PiGrow

*Automatische kas- en plantenbewaking met Raspberry Pi*

## Over dit project

PiGrow is een open source project dat een Raspberry Pi gebruikt om je plantgroei te automatiseren en monitoren. Met sensoren meet je bodemvocht, temperatuur, lichtintensiteit en meer. Actuatoren zoals waterpompen en LED-verlichting worden aangestuurd om een ideale omgeving te creëren. Gebruik de bijgeleverde scripts om data te loggen, grafieken te genereren of een web-UI/API te draaien.

Deze README is een voorstel. Vervang de ✏️-aanduidingen door jouw specifieke hardware, pinconfiguratie en instellingen.

## Vereisten

- Raspberry Pi 4 of vergelijkbaar
- Python 3.10+
- Raspbian OS of een andere Linux-distributie
- Sensoren: ✏️ bijv. DHT22 (temperatuur/vocht), lichtsensor, bodemvochtsensor
- Actuatoren: ✏️ bijv. 12V waterpomp, LED-strip, relaismodule
- Bibliotheken: zie `requirements.txt` (na installatie)
- Toegang tot internet voor tijdsynchronisatie en optionele web-UI

## Installatie

Clone deze repository op je Pi:

```
bash
git clone https://github.com/Daan420710/PiGrow.git
cd PiGrow
```

Installeer de Python-afhankelijkheden (we voegen `requirements.txt` toe):

```
bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Kopieer de voorbeeld-omgeving en vul deze in met jouw instellingen:

```
bash
cp .env.example .env
nano .env
```

Zorg dat je user toestemming heeft om de GPIO-pinnen aan te spreken, of draai scripts met `sudo` indien nodig.

## Gebruik

### Sensormetingen

De scripts in de map `src/sensors/` lezen waarden uit van je sensoren. Bijvoorbeeld om de bodemvochtigheid te meten:

```
bash
python src/sensors/soil_moisture.py
```

Pas de pinnen aan in de code of in je `.env`-bestand zodat deze overeenkomen met je hardware.

### Actuatoren aansturen

De map `src/actuators/` bevat scripts om pompen, verlichting of ventilatoren te bedienen. Voorbeeld:

```
bash
python src/actuators/water_pump.py
```

### Logging en data

Alle gemeten data worden opgeslagen in `data/`. Je kunt deze data omzetten naar grafieken met behulp van `scripts/plot_data.py`.

### Web-interface (optioneel)

Indien je de web-UI wilt gebruiken, installeer dan de extra afhankelijkheden en start de server:

```
bash
pip install -r requirements-web.txt
python src/web/app.py
```

De interface draait standaard op poort 8000. Zie `src/web/README.md` voor details.

## Mapstructuur

```
text
PiGrow/
├── src/
│   ├── sensors/      # Code voor sensoren (✏️ vul aan)
│   ├── actuators/    # Code voor actuatoren (✏️ vul aan)
│   ├── web/          # Optionele web-UI
│   └── utils/        # Hulpfuncties en gedeelde logica
├── data/             # Gemeten data en logs
├── config/           # Configuratiebestanden, o.a. .env
├── scripts/          # CLI-scripts zoals grafieken genereren
├── tests/            # Unit tests
├── requirements.txt
├── .env.example      # Voorbeeld-omgeving
└── README.md         # Dit bestand
```

## Configuratie

Alle configuratie staat in `.env`. Voor ieder apparaat definieer je de GPIO-pin (✏️):

```
SOIL_MOISTURE_PIN=17
TEMPERATURE_PIN=4
WATER_PUMP_PIN=27
...
```

Zorg dat deze waarden kloppen met je opstelling. Voor meer details, zie de documentatie in de mappen `src/sensors/` en `src/actuators/`.

## Bijdragen

PR's en bijdragen zijn welkom. Maak een nieuwe branche, commit je wijzigingen en maak een Pull Request. Zorg voor duidelijke commit messages en houd je aan de stijl van het project. Je kunt ook issues openen voor bugmeldingen of feature requests.

## License

Dit project is gelicentieerd onder de MIT-licentie. Zie `LICENSE` voor meer informatie.
