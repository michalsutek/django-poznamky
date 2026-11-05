# Týždeň 1 – Prostredie, prvý projekt, Git a GitHub

## Čo sa naučíš

- ako funguje web: prehliadač, server, požiadavka a odpoveď,
- vytvoriť a spustiť Django projekt,
- uložiť projekt na GitHub a pracovať s ním v škole aj doma.

## Nové pojmy

| Pojem | Význam |
| --- | --- |
| **požiadavka** (request) | to, čo prehliadač pošle serveru, keď zadáš adresu |
| **odpoveď** (response) | to, čo server vráti – najčastejšie HTML stránka |
| **HTTP** | jazyk, ktorým sa prehliadač a server dorozumievajú |
| **Django** | framework v Pythone – podľa adresy rozhodne, ktorý kód pripraví odpoveď |
| **projekt** | priečinok s `manage.py` a nastaveniami (u nás `cvicenia/`) |
| **repozitár** | priečinok, ktorého históriu zmien sleduje Git (u nás `django/`) |
| **commit** | uložený stav súborov so správou, čo sa zmenilo |
| **push / pull** | nahratie zmien na GitHub / stiahnutie zmien z GitHubu |

## Ako to funguje

```
prehliadač  ── požiadavka GET / ──►  server (Django)
            ◄── odpoveď 200 + HTML ──
```

Vyskúšaj: v prehliadači stlač **F12**, otvor kartu **Network** a obnov stránku. Uvidíš požiadavku a kód odpovede 200 (= v poriadku).

## Postup z hodiny

### 1. Priečinok repozitára

Vytvor priečinok `django` (napr. v Dokumentoch). Vo VS Code: **File → Open Folder → django**. Terminál: **Terminal → New Terminal**.

### 2. Overenie Djanga

```powershell
py -m django --version
```

Musí sa vypísať `6.1.x`. Ak nie (napríklad doma), nainštaluj presne túto verziu:

```powershell
py -m pip install "django==6.1.*"
```

### 3. Projekt `cvicenia`

```powershell
mkdir cvicenia
cd cvicenia
py -m django startproject config .
```

Bodka na konci je dôležitá – projekt sa vytvorí v aktuálnom priečinku. Vzniknú súbory:

```
django/
└── cvicenia/
    ├── manage.py
    └── config/
        ├── settings.py
        ├── urls.py
        └── ...
```

### 4. Spustenie servera

V priečinku `cvicenia/`:

```powershell
py manage.py runserver
```

Otvor `http://127.0.0.1:8000` – uvidíš raketu. Server zastavíš **Ctrl+C**.
Pri spustení vznikne aj súbor `db.sqlite3` (databáza, zatiaľ ju nepoužívame).
Varovanie o *unapplied migrations* zatiaľ ignoruj.

Na ďalšie príkazy otvor druhý terminál (**+**). Otvorí sa v `django/` – pred `py manage.py …` napíš `cd cvicenia`.

### 5. Slovenčina a časové pásmo

V súbore `cvicenia/config/settings.py` nájdi riadky a prepíš ich:

```python
LANGUAGE_CODE = "sk"
TIME_ZONE = "Europe/Bratislava"
```

Ulož a obnov prehliadač – stránka je po slovensky.

### 6. Git

Raz na každom počítači:

```powershell
git config --global user.name "Meno Priezvisko"
git config --global user.email "tvoj@email.sk"
git config --global pull.rebase false
```

(Posledný riadok povie Gitu, ako má spájať zmeny pri `git pull` – bez neho by sťahovanie poznámok skončilo chybou.)

V koreni `django/` vytvor súbor **`.gitignore`** s jediným riadkom:

```
__pycache__/
```

(Priečinky `__pycache__` si Python vytvára sám, do Gitu nepatria.)

V koreni `django/`:

```powershell
git init
git add -A
git commit -m "Prvý Django projekt"
```

**Cez VS Code:** panel **Source Control** (Ctrl+Shift+G) → **Initialize Repository** → napíš správu → **✓ Commit** → na otázku o pridaní všetkých zmien **Yes**.

### 7. GitHub

**Cez VS Code (jednoduchšie):** Source Control → **Publish Branch** → **Publish to GitHub public repository**, názov `django`.

**Cez terminál:** na github.com vytvor prázdny repozitár `django` (Public, bez README), potom:

```powershell
git branch -M main
git remote add origin https://github.com/TVOJE-MENO/django.git
git push -u origin main
```

### 8. Poznámky z hodín

Raz, v koreni `django/`:

```powershell
git remote add poznamky https://github.com/michalsutek/django-poznamky.git
git pull --no-edit --allow-unrelated-histories poznamky main
git push
```

V repozitári sa objaví priečinok `poznamky/` – práve ho čítaš.

### 9. Práca doma

Prvýkrát doma:

```powershell
git clone https://github.com/TVOJE-MENO/django.git
cd django\cvicenia
py -m pip install "django==6.1.*"
py manage.py runserver
```

**Cez VS Code:** úvodná obrazovka **Clone Git Repository** → vlož adresu → vyber priečinok → **Open**.

## Zapamätaj si

1. `py manage.py …` sa spúšťa v priečinku **`cvicenia/`** (tam, kde je `manage.py`).
2. **Na začiatku práce `git pull`, na konci `git add -A`, `git commit`, `git push`** – v škole aj doma.
3. V škole na začiatku hodiny aj `git pull --no-edit poznamky main` (nové poznámky).
4. Server sa zastavuje **Ctrl+C**.

## Keď niečo nefunguje

| Hlásenie | Riešenie |
| --- | --- |
| `can't open file '...manage.py'` | Si v zlom priečinku: `cd cvicenia` |
| `No module named 'django'` | `py -m pip install "django==6.1.*"` |
| `python` otvorí Microsoft Store | Píš `py`, nie `python` |
| `That port is already in use` | Server už beží v inom termináli – zavri ho |
| `git push` → *rejected (fetch first)* | Najprv `git pull`, potom `git push` |
| VS Code: *configure your user.name* | Krok 6 – `git config` |
| `refusing to merge unrelated histories` | Pri prvom sťahovaní poznámok treba `--allow-unrelated-histories` |
| `Need to specify how to reconcile divergent branches` | `git config --global pull.rebase false` (krok 6) |
| Po `git pull` sa otvoril editor (napr. Vim) | Vim zatvoríš: `Esc`, napíš `:wq`, Enter. Nabudúce použi `--no-edit` |

## Zadanie (doma)

1. Doma si naklonuj repozitár a spusti projekt (krok 9).
2. Na prvý riadok súboru `cvicenia/config/urls.py` dopíš komentár `# Meno Priezvisko, trieda`.
3. `git add -A`, `git commit -m "Doma funguje"`, `git push`.
4. Odovzdaj odkaz na svoj repozitár (EduPage/Teams).

Na začiatku ďalšej hodiny v škole najprv `git pull` – komentár z domu sa objaví aj v škole.

## Otázky na zopakovanie

1. Čo je požiadavka a čo odpoveď?
2. Čo znamená bodka v `startproject config .`?
3. Ako zastavíš server?
4. Z ktorého priečinka spúšťaš `py manage.py …`?
5. Prečo na začiatku práce vždy `git pull`?
