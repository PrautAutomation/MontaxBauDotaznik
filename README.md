# MONTEXBAU - Dotazník pro analýzu procesů

Komplexní dotazníkový systém pro analýzu firemních procesů společnosti MONTEXBAU před implementací ERP systému Odoo. Dotazník je speciálně navržen pro stavební a personální agenturu poskytující pracovníky na stavby v Německu.

## 📋 Obsah

- [Přehled](#přehled)
- [Funkce](#funkce)
- [Technologie](#technologie)
- [Instalace](#instalace)
- [Konfigurace](#konfigurace)
- [Nasazení](#nasazení)
- [Struktura dotazníku](#struktura-dotazníku)
- [N8N Workflow](#n8n-workflow)
- [Údržba](#údržba)

## 🎯 Přehled

Tento dotazník slouží k:
- Analýze současných procesů ve firmě MONTEXBAU
- Identifikaci oblastí vhodných pro automatizaci
- Sběru požadavků pro implementaci Odoo ERP
- Mapování specifik přeshraniční práce ČR-Německo
- Definování priorit digitální transformace

## ✨ Funkce

- **12 tematických sekcí** pokrývajících všechny aspekty firmy
- **Responzivní design** - funguje na PC, tabletech i mobilech
- **Progress tracking** - vizuální indikátor postupu vyplňování
- **Drag & drop** - interaktivní řazení priorit
- **Automatické ukládání** - data se ukládají při přechodu mezi sekcemi
- **Validace formuláře** - kontrola povinných polí
- **Vícejazyčná připravenost** - struktura umožňuje snadný překlad
- **CORS podpora** - komunikace s n8n webhookem

## 🛠 Technologie

- **Frontend**: Čisté HTML5, CSS3, Vanilla JavaScript
- **Backend**: n8n workflow automatizace
- **Datové úložiště**: Google Sheets (volitelné)
- **Hosting**: GitHub Pages
- **Integrace**: Webhook API

## 📦 Instalace

### 1. Klonování repozitáře

```bash
git clone https://github.com/YOUR-USERNAME/montexbau-dotaznik.git
cd montexbau-dotaznik
```

### 2. Lokální spuštění

```bash
# Použijte libovolný HTTP server, například:
python -m http.server 8000
# nebo
npx http-server -p 8000
```

Otevřete prohlížeč na `http://localhost:8000`

## ⚙️ Konfigurace

### 1. N8N Webhook URL

Upravte webhook URL v souboru `index.html` (řádek ~1294):

```javascript
// Nahraďte YOUR-N8N-INSTANCE.com vaší skutečnou n8n doménou
const WEBHOOK_URL = 'https://YOUR-N8N-INSTANCE.com/webhook/montexbau-dotaznik';
```

### 2. N8N Workflow Setup

1. Importujte workflow do n8n:
   - ID workflow: `mHyChSTKGyVw78aD`
   - Název: "MONTEXBAU - Dotazník pro analýzu procesů"

2. Aktivujte workflow:
   - Otevřete workflow v n8n
   - Klikněte na tlačítko "Activate"
   - Zkopírujte webhook URL

3. Volitelné konfigurace:
   - **Google Sheets**: Přidejte credentials a nastavte spreadsheet ID
   - **Email**: Nastavte SMTP credentials pro potvrzovací emaily

## 🚀 Nasazení

### GitHub Pages

1. Vytvořte nový repozitář na GitHubu

2. Nahrajte soubory:
```bash
git init
git add index.html README.md
git commit -m "Initial commit - MONTEXBAU dotazník"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/montexbau-dotaznik.git
git push -u origin main
```

3. Aktivujte GitHub Pages:
   - Settings → Pages
   - Source: Deploy from branch
   - Branch: main
   - Folder: / (root)
   - Save

4. Váš dotazník bude dostupný na:
```
https://YOUR-USERNAME.github.io/montexbau-dotaznik/
```

### Alternativní hosting

Dotazník lze hostovat na jakémkoliv webovém serveru podporujícím statické HTML soubory:
- Netlify
- Vercel
- Surge.sh
- Vlastní webserver

## 📊 Struktura dotazníku

### Sekce 1: Základní informace
- Identifikace respondenta
- Oddělení a pozice
- Pracovní lokace

### Sekce 2: Personální agentura
- Evidence uchazečů
- Správa dokumentů
- Sledování certifikací

### Sekce 3: Přeshraniční agenda ČR-Německo
- A1 formuláře
- Sledování 183 dnů
- Legislativní požadavky

### Sekce 4: Stavební projekty
- Správa zakázek
- Specializace (střechy, lešení, instalace)
- Materiál a logistika

### Sekce 5: Finance a účetnictví
- Mzdová agenda 200+ zaměstnanců
- Německé daně a odvody
- Kurzové rozdíly EUR/CZK

### Sekce 6: IT nástroje
- Současné systémy
- Duplicitní evidence
- Excel workaroundy

### Sekce 7: AI automatizace
- Překlady CZ↔DE
- Standardní dokumenty
- Rutinní komunikace

### Sekce 8: Priority
- Drag & drop řazení
- 10 klíčových oblastí
- Vlastní priority

### Sekce 9: Měřitelné údaje
- Časová náročnost procesů
- Náklady na chyby
- Objemy transakcí

### Sekce 10: Očekávání od Odoo
- Systémové požadavky
- Obavy z implementace
- Ideální řešení

### Sekce 11: Role a odpovědnosti
- Rozhodovací procesy
- Schvalovací hierarchie
- Odpovědnosti

### Sekce 12: Kontakt
- Follow-up souhlas
- Kontaktní údaje
- Preference komunikace

## 🔄 N8N Workflow

### Komponenty workflow

1. **Webhook** - Příjem dat z formuláře
2. **Zpracování dat** - Strukturování a validace
3. **Google Sheets** - Ukládání odpovědí (volitelné)
4. **Email** - Potvrzení respondentům (volitelné)
5. **Response** - Potvrzení přijetí

### Webhook endpoint
```
POST /webhook/montexbau-dotaznik
Content-Type: application/json
```

### Struktura dat
```javascript
{
  body: {
    // Základní informace
    name: string,
    department: string,
    position: string,
    // ... všechna další pole formuláře
  }
}
```

## 🔧 Údržba

### Přidání nových polí

1. Přidejte HTML pole do příslušné sekce
2. Aktualizujte `saveCurrentSectionData()` funkci
3. Upravte n8n workflow pro zpracování nových dat

### Změna pořadí sekcí

1. Přesuňte HTML sekce
2. Aktualizujte tlačítka v `section-tabs`
3. Upravte konstantu `totalSections`

### Překlady

Pro vícejazyčnou verzi:
1. Extrahujte všechny texty do language objektu
2. Implementujte language switcher
3. Použijte `data-i18n` atributy

## 📱 Podpora prohlížečů

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Opera 76+
- Mobilní prohlížeče (iOS Safari, Chrome Mobile)

## 🤝 Kontakt

**MONTEXBAU s.r.o.**
- Web: https://www.montexbau.eu/cs/
- Email: info@montexbau.eu
- Specializace: Stavební služby a personální agentura

## 📄 Licence

© 2024 MONTEXBAU s.r.o. - Všechna práva vyhrazena.

---

**Poznámka**: Nezapomeňte aktualizovat webhook URL před nasazením do produkce!
