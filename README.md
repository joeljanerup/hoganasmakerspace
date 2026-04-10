# Höganäs Makerspace – Webbplats

Webbplatsen är byggd med [Jekyll](https://jekyllrb.com/) och temat [Forty](https://github.com/andrewbanchich/forty-jekyll-theme) och är avsedd att publiceras via [GitHub Pages](https://pages.github.com/).

---

## Innehållsförteckning

1. [Köra lokalt](#köra-lokalt)
2. [Projektstruktur](#projektstruktur)
3. [Ändra innehåll på en befintlig sida](#ändra-innehåll-på-en-befintlig-sida)
4. [Lägga till ett nytt menyval och sida](#lägga-till-ett-nytt-menyval-och-sida)
5. [Hantera årsmöten och PDF-filer](#hantera-årsmöten-och-pdf-filer)
6. [Publicera till GitHub Pages](#publicera-till-github-pages)

---

## Köra lokalt

Kräver [Docker Desktop](https://www.docker.com/products/docker-desktop/).

**På Windows (PowerShell):**

```powershell
docker run --rm -v "C:\Users\joel.janerup\source\repos\hoganasmakerspace:/site" -p 4000:4000 bretfisher/jekyll-serve
```

Öppna sedan **http://localhost:4000** i webbläsaren.  
Ändringar i filer plockas upp automatiskt – ladda om sidan för att se dem.  
Undantag: ändringar i `_config.yml` kräver att containern startas om.

---

## Projektstruktur

```
hoganasmakerspace/
├── _data/
│   ├── opening_hours.yml     # Öppettider (dagar och tider)
│   └── annual_meetings.yml   # Årsmötesdata (år + PDF-länkar)
├── _includes/
│   ├── opening-hours.html    # Öppettider (återanvänd på alla sidor)
│   ├── footer.html           # Sidfot med sociala ikoner
│   └── header.html           # Sidhuvud och navigeringsmeny
├── _layouts/                 # Sidmallar (ändras sällan)
├── _sass/                    # CSS/stilar (ändras sällan)
├── assets/
│   ├── images/               # Bilder
│   └── pdfs/                 # PDF-filer organiserade per år
│       ├── 2022/
│       ├── 2023/
│       ├── 2024/
│       ├── 2025/
│       └── 2026/
├── _config.yml               # Webbplatsinställningar
├── index.md                  # Startsidan
├── om.md                     # Om oss (utrustning, regler, adress, kontakt, sponsorer)
├── bli-medlem.md             # Bli medlem (medlemskapstyper och registrering)
├── styrelse.md               # Styrelsemedlemmar
├── stadgar.md                # Stadgarsidan
├── arsmoten.md               # Årsmötessidan
├── kontakt.md                # Legacy (dolt från meny)
```

---

## Ändra innehåll på en befintlig sida

Varje sida är en Markdown-fil (`.md`) i rotkatalogen. Öppna filen i valfri textredigerare.

### Ändra öppettider

Öppettiderna visas på alla sidor i kontaktsektionen. Så ändrar du dem:

1. Öppna `_data/opening_hours.yml`
2. Redigera dagarna och tiderna i denna fil:

```yaml
- day: Tisdagar
  time: 15:00 – 20:30
- day: Torsdagar
  time: 15:00 – 20:30
- day: Söndagar
  time: 10:00 – 12:00
```

**Exempel:** Om makerspace är stängt på torsdagar och öppet på fredagar istället:

```yaml
- day: Tisdagar
  time: 15:00 – 20:30
- day: Fredagar
  time: 15:00 – 20:30
- day: Söndagar
  time: 10:00 – 12:00
```

Ändringarna uppdateras automatiskt på alla sidor när du sparar filen.

### Ändra kontaktinformation

Öppna `kontakt.md` och redigera HTML-innehållet direkt i filen.  
För att byta styrelsens e-postadress, uppdatera även `_config.yml`:

```yaml
email: nyadress@hoganasmakerspace.se
```


### Ändra webbplatsens namn eller beskrivning

Öppna `_config.yml` och ändra följande fält:

```yaml
title: Höganäs Makerspace
subtitle: Ideell förening
description: Kreativt skapande för alla i Höganäs
```

### Sidhuvud (front matter)

Längst upp i varje `.md`-fil finns ett block mellan `---` som styr sidans metadata:

```yaml
---
layout: landing       # Sidmall (ändras normalt inte)
title: Kontakt        # Sidans rubrik (visas i webbläsarfliken och menyn)
nav-menu: true        # true = visas i hamburgermenyn
nav-order: 2          # Bestämmer ordningen i menyn (lägre siffra = kommer först)
show_tile: true       # true = visas som ruta på startsidan
description: ...      # Kort beskrivning (visas under rubriken i sidhuvudet)
image: assets/images/pic11.jpg  # Bakgrundsbild i sidhuvudet
---
```

**Aktuell menyordning:**

| nav-order | Sida       |
|-----------|------------|
| –         | Hem        |
| 2         | Om oss     |
| 3         | Bli medlem |
| 4         | Styrelse   |
| 5         | Stadgar    |
| 6         | Årsmöten   |

---

## Lägga till ett nytt menyval och sida

### Steg 1 – Skapa en ny Markdown-fil

Skapa en ny fil i rotkatalogen, t.ex. `om-oss.md`, med följande mall:

```markdown
---
layout: landing
title: Om oss
nav-menu: true
nav-order: 6          # Välj en siffra som placerar sidan rätt i menyn
show_tile: true
description: En kort beskrivning av sidan.
image: assets/images/pic01.jpg
---

<div id="main">
  <section id="one">
    <div class="inner">
      <header class="major">
        <h2>Om oss</h2>
      </header>
      <p>Skriv ditt innehåll här.</p>
    </div>
  </section>
</div>
```

### Steg 2 – Menyn uppdateras automatiskt

Tack vare `nav-menu: true` läggs sidan automatiskt till i hamburgermenyn.  
Ingen annan fil behöver ändras.

### Tillgängliga bilder för `image`

Temat levereras med ett antal bilder (`pic01.jpg` – `pic11.jpg`) under `assets/images/`.  
Du kan lägga till egna bilder i samma mapp och referera till dem på samma sätt.

---

## Hantera årsmöten och PDF-filer

All data för årsmöten styrs av en enda fil: `_data/annual_meetings.yml`.

### Lägga till ett nytt år

1. Öppna `_data/annual_meetings.yml`
2. Lägg till ett nytt block **längst upp** i filen (nyaste år överst):

```yaml
- year: 2026
  documents:
    invitation:          assets/pdfs/2026/kallelse.pdf
    activity_report:     assets/pdfs/2026/verksamhetsberattelse.pdf
    business_plan:       assets/pdfs/2026/verksamhetsplan.pdf
    selection_committee: assets/pdfs/2026/valberedningens-forslag.pdf
    protocol:            assets/pdfs/2026/protokoll.pdf
```

3. Skapa mappen `assets/pdfs/2026/`
4. Lägg in PDF-filerna med exakt de filnamn som anges ovan

### Dokument som inte är klara ännu

Det finns tre möjliga värden för varje dokument:

| Värde           | Visas som på webbplatsen           |
|-----------------|------------------------------------|
| Filsökväg       | Klickbar länk                      |
| `pending`       | Grå text (dokumentnamnet utan länk) |
| `null`          | Dolt – visas inte alls             |

Använd `pending` när protokollet **förväntas men inte är uppladdad än**. Använd `null` (eller utelämna nyckeln) när dokumentet **inte existerar** för det aktuella året.

```yaml
- year: 2026
  documents:
    invitation:          assets/pdfs/2026/kallelse.pdf
    activity_report:     assets/pdfs/2026/verksamhetsberattelse.pdf
    business_plan:       assets/pdfs/2026/verksamhetsplan.pdf
    selection_committee: assets/pdfs/2026/valberedningens-forslag.pdf
    protocol:            pending   # Byt ut mot sökvägen när filen är uppladdad
```

### Dokumentnamn och vad de innebär

| Nyckel                | Visas som på webbplatsen        |
|-----------------------|---------------------------------|
| `invitation`          | Kallelse till årsmötet          |
| `activity_report`     | Verksamhetsberättelse           |
| `business_plan`       | Verksamhetsplan                 |
| `selection_committee` | Valberedningens förslag         |
| `protocol`            | Mötesprotokoll                  |

---

## Publicera till GitHub Pages

Webbplatsen publiceras automatiskt via GitHub Actions när du pushar till `main`-branchen.  
Workflow-filen finns redan på plats under `.github/workflows/github-pages.yml`.

```bash
git add .
git commit -m "Beskriv ändringen"
git push origin main
```

Webbplatsen är tillgänglig på: **https://hoganasmakerspace.github.io**

