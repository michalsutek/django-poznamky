# Ťahák

Stav po týždni 1. Priebežne sa dopĺňa.

## Terminál

| Čo | Príkaz |
| --- | --- |
| Prejsť do priečinka | `cd cvicenia` · o úroveň vyššie `cd ..` |
| Vytvoriť priečinok | `mkdir nazov` |
| Verzia Djanga | `py -m django --version` |
| Inštalácia Djanga | `py -m pip install "django==6.1.*"` |
| Nový projekt | `py -m django startproject config .` |
| Spustiť server | `py manage.py runserver` (v `cvicenia/`) |
| Zastaviť server | **Ctrl+C** |

## Git – každý deň

| Kedy | Terminál (v koreni `django/`) | VS Code (Source Control, Ctrl+Shift+G) |
| --- | --- | --- |
| Začiatok práce | `git pull` | **…** → **Pull** |
| Nové poznámky (v škole) | `git pull --no-edit poznamky main` | **…** → **Pull, Push** → **Pull from…** → `poznamky` |
| Koniec práce | `git add -A` · `git commit -m "správa"` · `git push` | správa → **✓ Commit** (Yes) → **Sync Changes** |
| Čo sa zmenilo | `git status` | zoznam súborov v paneli |

**Pull na začiatku, push na konci – vždy, v škole aj doma.**

## Git – raz

| Čo | Príkaz |
| --- | --- |
| Meno a e-mail (na každom PC) | `git config --global user.name "Meno Priezvisko"` · `git config --global user.email "..."` |
| Spájanie pri pull (na každom PC) | `git config --global pull.rebase false` |
| Nový repozitár | `git init` (v `django/`) · VS Code: **Initialize Repository** |
| Nahrať na GitHub | VS Code: **Publish Branch** → **public** |
| Stiahnuť na inom PC | `git clone https://github.com/MENO/django.git` · VS Code: **Clone Git Repository** |
| Pripojiť poznámky | `git remote add poznamky https://github.com/michalsutek/django-poznamky.git` · `git pull --no-edit --allow-unrelated-histories poznamky main` |

## Štruktúra repozitára

```
django/                 ← repozitár (git), otváraš ho vo VS Code
├── .gitignore          ← __pycache__/
├── poznamky/           ← tieto poznámky (neupravovať)
└── cvicenia/           ← projekt, tu spúšťaš py manage.py ...
    ├── manage.py
    ├── db.sqlite3      ← databáza (je v repozitári)
    └── config/
        ├── settings.py ← nastavenia
        └── urls.py     ← hlavné cesty
```

## Pojmy

| Pojem | Význam |
| --- | --- |
| **commit** | uložený stav súborov so správou |
| **HTTP** | jazyk prehliadača a servera |
| **odpoveď (response)** | to, čo vráti server – najčastejšie HTML |
| **požiadavka (request)** | to, čo pošle prehliadač serveru |
| **projekt** | priečinok s manage.py (cvicenia/) |
| **push / pull** | nahratie / stiahnutie zmien na/z GitHubu |
| **repozitár** | priečinok sledovaný Gitom (django/) |
