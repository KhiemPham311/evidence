# Evidence doučování SEA-l

Jednoduchá webová appka pro evidenci dětí, kurzů a jejich kapacity, učitelů, docházky a financí. Je to jeden soubor `index.html`, běží zdarma na GitHub Pages a nepotřebuje žádný server.

## Jak appka ukládá data

- **V prohlížeči.** Funguje hned, ale data jsou jen v tom jednom prohlížeči na jednom zařízení.
- **Na GitHubu (doporučeno).** Appka ukládá všechno do souboru `data.json` ve tvém **soukromém** repozitáři. Každá změna je commit, takže máš historii a zálohu a stejná data vidíš na počítači i na mobilu.

Appka a data jsou ve dvou různých repozitářích:

| Repozitář | Viditelnost | Co v něm je |
|---|---|---|
| `evidence` | veřejný (GitHub Pages zdarma vyžaduje veřejný repozitář) | jen `index.html`, `.nojekyll` a tento README, **žádná data** |
| `evidence-data` | **soukromý** | `data.json` s dětmi, platbami a docházkou |

> `data-start.json` (tvoje děti a platby) do veřejného repozitáře **nikdy nenahrávej**. Nahraješ ho přímo v appce.

## Nastavení krok za krokem

### 1. Účet na GitHubu
Založ si účet na <https://github.com/signup>, nebo použij existující.

### 2. Repozitář s appkou a GitHub Pages
1. Vpravo nahoře **+** → **New repository**. Název `evidence`, viditelnost **Public**, zaškrtni **Add a README file** → **Create repository**.
2. **Add file** → **Upload files** → přetáhni `index.html` a `.nojekyll` → **Commit changes**.
   (Soubor `.nojekyll` může být v počítači skrytý. Když ho nenajdeš, nevadí, appka funguje i bez něj.)
3. **Settings** → **Pages** → *Build and deployment* → Source **Deploy from a branch**, Branch **main**, složka **/ (root)** → **Save**.
4. Za minutu nebo dvě bude appka na adrese `https://TVOJE-JMENO.github.io/evidence/`.

### 3. Soukromý repozitář pro data
**+** → **New repository** → název `evidence-data`, viditelnost **Private**, zaškrtni **Add a README file** (repozitář nesmí být úplně prázdný) → **Create repository**.

### 4. Token, kterým appka zapisuje data
1. Klikni na svůj avatar → **Settings** → úplně dole **Developer settings** → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**.
2. *Token name:* `evidence`. *Expiration:* klidně nejdelší možná, ale poznač si, kdy vyprší.
3. *Repository access:* **Only select repositories** → vyber jen `evidence-data`.
4. *Permissions* → *Repository permissions* → **Contents: Read and write**. Nic dalšího nepřidávej.
5. **Generate token** a token si hned zkopíruj (začíná `github_pat_`). Znovu ho GitHub neukáže.

### 5. Propojení appky
1. Otevři appku → **Nastavení** → *Ukládání na GitHub*.
2. Vyplň svoje uživatelské jméno, repozitář `evidence-data`, vlož token → **Připojit**.
3. Appka ověří, že je repozitář soukromý, a vytvoří v něm `data.json`.

### 6. Nahrání tvých dat
**Nastavení** → *Záloha* → **Nahrát zálohu** → vyber `data-start.json`. Appka data hned uloží i na GitHub.

Na dalším zařízení (třeba na mobilu) otevři stejnou adresu, v Nastavení zadej stejné údaje a token, a data se načtou z GitHubu.

## Bezpečnost

- Token je uložený jen v prohlížeči, kde ho zadáš. Na veřejném nebo cizím počítači ho nezadávej.
- Token umí jen číst a zapisovat soubory v `evidence-data`, nic jiného.
- Když ztratíš telefon nebo počítač, smaž token na GitHubu (Developer settings → Fine-grained tokens → Delete) a vytvoř nový.
- Když token vyprší, appka ukáže chybu. Vytvoř nový a v Nastavení se znovu připoj.

## Přístup pro další lidi (ředitel, zástupce)

Data vidí jen ten, kdo má token k soukromému repozitáři s daty. Adresa appky je veřejná, ale bez tokenu je appka prázdná.

1. Pro každého člověka vytvoř **vlastní token** stejně jako v kroku 4 výše (jen repozitář s daty, Contents: Read and write) a pojmenuj ho jeho jménem, třeba `evidence – ředitel`. GitHub účet ten člověk mít nemusí.
2. Pošli mu adresu appky a token. Token posílej odděleně a bezpečně, nejlépe osobně nebo přes správce hesel, ne veřejným chatem.
3. On si v appce v Nastavení vyplní uživatele, repozitář, **svoje jméno** a token a dá Připojit.
4. Když s vámi přestane spolupracovat nebo ztratí telefon, smaž na GitHubu jen jeho token. Ostatní to neovlivní.

Kdo má token, vidí a může měnit všechno, včetně financí.

### Když pracuje víc lidí najednou

- Appka každou minutu a při každém návratu do okna načte změny ostatních a spojí je s tvými.
- Když dva lidé změní různé věci (třeba jeden platbu, druhý docházku), uloží se obojí.
- Když dva lidé ve stejnou chvíli změní **stejnou** věc (třeba telefon stejného dítěte), platí ta, která se uložila později.
- Jméno vyplněné v Nastavení se ukládá do historie změn. Kdo co kdy změnil, najdeš na GitHubu v repozitáři s daty pod **Commits**. Odtud jde i vrátit starší verzi.
- Úpravy bez internetu zůstanou v prohlížeči a po připojení se spojí se změnami ostatních.

## Aktualizace appky

Novou verzi `index.html` nahraj do repozitáře `evidence` stejně jako poprvé (Upload files, přepíše se). Data v `evidence-data` se tím nezmění.
