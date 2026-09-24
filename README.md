# MOEX CYBERDECK v4.1

Terminal de trading neon pour la Bourse de Moscou. Donnees en temps reel (differees de 15 minutes) via l'API publique MOEX ISS. Graphique interactif, indicateurs techniques, carnet d'ordres et suivi de 15 actions russes.

[![Live Demo](https://img.shields.io/badge/Live_Demo-00f3ff?style=for-the-badge&logo=github&logoColor=white)](https://gunout.github.io/Moex-Cyberdeck/)
[![Version](https://img.shields.io/badge/Version-4.1.0-ffd700?style=for-the-badge)](https://github.com/gunout/Moex-Cyberdeck/releases)
[![License](https://img.shields.io/badge/License-MIT-00ff9d?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Live-00ff9d?style=for-the-badge)](https://gunout.github.io/Moex-Cyberdeck/)

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/docs/Web/JavaScript)
[![Cloudflare](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=flat-square&logo=cloudflare&logoColor=white)](https://workers.cloudflare.com/)
[![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-222222?style=flat-square&logo=githubpages&logoColor=white)](https://pages.github.com/)
[![Lightweight Charts](https://img.shields.io/badge/Lightweight_Charts-4.1.0-00f3ff?style=flat-square)](https://tradingview.github.io/lightweight-charts/)

**[Demo Live](https://gunout.github.io/Moex-Cyberdeck/)** | **[Signaler un bug](https://github.com/gunout/Moex-Cyberdeck/issues/new)** | **[Demander une feature](https://github.com/gunout/Moex-Cyberdeck/issues/new)** | **[Fork](https://github.com/gunout/Moex-Cyberdeck/fork)**

---

## Sommaire

- [Apercu](#apercu)
- [Fonctionnalites](#fonctionnalites)
- [Indicateurs techniques](#indicateurs-techniques)
- [Installation](#installation)
- [Configuration](#configuration)
- [API MOEX ISS](#api-moex-iss)
- [Deploiement](#deploiement)
- [Roadmap](#roadmap)
- [Contribution](#contribution)
- [Licence](#licence)
- [Avertissement](#avertissement)

---

## Apercu

MOEX Cyberdeck est un dashboard web 100% statique qui affiche en temps reel (differe de 15 minutes) les cours de 15 actions russes cotees sur le board TQBR de la Bourse de Moscou. Il combine un graphique interactif en bougies japonaises, des indicateurs techniques avances (moyennes mobiles, volatilite), un carnet d'ordres en direct et des signaux de trading automatiques.

Interface disponible : https://gunout.github.io/Moex-Cyberdeck/

---

## Fonctionnalites

### Graphique avance

- Bougies japonaises neon (vert haussier, rouge baissier)
- MA20 : Moyenne mobile 20 jours (cyan)
- MA50 : Moyenne mobile 50 jours (or)
- MA200 : Moyenne mobile 200 jours (magenta)
- MAD20 : Volatilite Mean Absolute Deviation (orange)
- Lignes OPEN / HIGH / LOW / PREV automatiques
- Crosshair dore interactif avec label
- Indicateurs activables et desactivables en un clic
- Bouton Reset Zoom pour recentrer le graphique
- 7 timeframes disponibles : 1J, 1S, 1M, 3M, 6M, 1A, MAX

### Trading et marche

- 15 actions russes : SBER, GAZP, LKOH, GMKN, NVTK, ROSN, YNDX, TATN, MTSS, PLZL, SNGS, MGNT, VTBR, ALRS, CHMF
- Indice IMOEX en direct (indice general de la Bourse de Moscou)
- Carnet d'ordres reel avec 10 meilleures offres et 10 meilleures demandes
- Spread bid/ask calcule en temps reel
- Signaux BUY / SELL / HOLD automatiques bases sur la variation
- Alertes visuelles pour les variations superieures a 3 pourcent
- Statistiques OHLCV completes (ouverture, haut, bas, volume)
- Badges sectoriels : Energie, Finance, Tech, Metaux, Telecom, Conso

### Interface et design

- Palette tricolore russe : blanc, bleu, rouge
- Effet scanlines cyberpunk avec degrade radial
- Animations fluides et transitions douces
- Design responsive : desktop, tablette, mobile
- Barre de recherche instantanee dans la watchlist
- Horloge Moscou en temps reel (fuseau MSK)
- Statut de connexion en pied de page

### Performance et fiabilite

- Cache local de 60 secondes par ticker et timeframe
- AbortController pour annuler les requetes obsoletes
- Debounce de 250 millisecondes sur les timeframes
- Overlay de chargement progressif avec barre de progression
- Retry automatique jusqu'a 3 tentatives en cas d'echec
- Delai anti rate-limit de 150 millisecondes entre les requetes

---

## Indicateurs techniques

| Indicateur | Couleur | Periode | Utilite |
|:---:|:---:|:---:|---|
| MA20 | Cyan | 20 jours | Tendance court terme |
| MA50 | Or | 50 jours | Tendance moyen terme |
| MA200 | Magenta | 200 jours | Tendance long terme |
| MAD20 | Orange | 20 jours | Volatilite |

### Signaux des moyennes mobiles

- Golden Cross : MA20 croise MA50 vers le haut. Signal haussier.
- Death Cross : MA20 croise MA50 vers le bas. Signal baissier.

### MAD (Mean Absolute Deviation)

Mesure la volatilite moyenne d'un titre sur une periode donnee.

Formule : MAD = (1/n) x somme des valeurs absolues de (close - moyenne)

- Valeur basse : titre stable, faible volatilite
- Valeur haute : titre volatil, risque plus eleve

---

## Installation

Le projet est entierement statique. Aucune dependance npm, aucun build step.

Etape 1. Cloner le depot.

    git clone https://github.com/gunout/Moex-Cyberdeck.git

Etape 2. Entrer dans le dossier.

    cd Moex-Cyberdeck

Etape 3. Lancer un serveur local (au choix).

    python -m http.server 8000

    npx serve .

    php -S localhost:8000

Etape 4. Ouvrir le navigateur.

    http://localhost:8000

### Dependances CDN

- Lightweight Charts v4.1 par TradingView
- Google Fonts : Orbitron et JetBrains Mono
- Font Awesome 6.4 pour les icones

---

## Configuration

Le dashboard necessite un proxy CORS pour contourner les restrictions navigateur. Un Cloudflare Worker gratuit est recommande.

### Etape 1 : Creer un Worker Cloudflare

Rends-toi sur https://dash.cloudflare.com, cree un compte gratuit puis un nouveau Worker.

### Etape 2 : Coller le code du Worker

Ouvre l'editeur du Worker et colle ce code JavaScript :

    export default {
      async fetch(request) {
        const url = new URL(request.url);
        const target = url.searchParams.get('url');
        if (!target) {
          return new Response('Missing url parameter', { status: 400 });
        }
        if (!target.startsWith('https://iss.moex.com/')) {
          return new Response('Forbidden host', { status: 403 });
        }
        const res = await fetch(target);
        const body = await res.text();
        return new Response(body, {
          status: res.status,
          headers: {
            'Access-Control-Allow-Origin': '*',
            'Content-Type': 'application/json',
            'Cache-Control': 'public, max-age=30'
          }
        });
      }
    };

### Etape 3 : Deployer

Clique sur Save and Deploy. Note ton URL, du type : https://ton-worker.workers.dev

### Etape 4 : Modifier index.html

Dans ton fichier index.html, remplace la constante du proxy par :

    const CORS_PROXY = 'https://ton-worker.workers.dev/?url=';

C'est tout. Ton dashboard utilise maintenant ton propre proxy.

---

## API MOEX ISS

Toutes les donnees proviennent de l'API publique MOEX ISS. Service gratuit, differe de 15 minutes. Documentation : https://iss.moex.com

### Endpoints utilises

- /iss/engines/stock/markets/shares/boards/TQBR/securities/TICKER.json
- /iss/engines/stock/markets/shares/boards/TQBR/securities/TICKER/candles.json
- /iss/engines/stock/markets/shares/boards/TQBR/securities/TICKER/orderbook.json
- /iss/engines/stock/markets/index/boards/SNDX/securities/IMOEX.json

### Parametres des bougies

Le parametre interval accepte les valeurs suivantes :

- 1 : 1 minute
- 10 : 10 minutes
- 60 : 1 heure
- 24 : 1 jour
- 7 : 1 semaine
- 31 : 1 mois

---

## Deploiement

### GitHub Pages (recommande)

1. Pousse ton code sur la branche main
2. Va dans Settings, puis Pages
3. Selectionne Branch : main, folder : root
4. Clique Save
5. Ton site est en ligne sur https://TON-PSEUDO.github.io/Moex-Cyberdeck/

### Vercel

1. Va sur https://vercel.com
2. Connecte ton compte GitHub
3. Importe le depot Moex-Cyberdeck
4. Clique Deploy
5. Ton site est en ligne sur https://moex-cyberdeck.vercel.app

### Netlify

1. Va sur https://netlify.com
2. Glisse-depose le dossier du projet
3. Ton site est en ligne instantanement

---

## Roadmap

### Fait

- [x] Graphique bougies + MA20/50/200
- [x] MAD20 volatilite
- [x] Carnet d'ordres
- [x] Indice IMOEX
- [x] Signaux BUY/SELL/HOLD
- [x] Cache + AbortController
- [x] Barre de recherche

### En cours

- [ ] RSI (Relative Strength Index)
- [ ] MACD
- [ ] Bandes de Bollinger

### Prevu

- [ ] Alertes prix avec notifications
- [ ] Mode PWA installable
- [ ] Multi-langue FR / EN / RU
- [ ] Themes couleur supplementaires
- [ ] Export CSV de l'historique
- [ ] Sauvegarde des favoris en localStorage

---

## Contribution

Les contributions sont les bienvenues. Pour proposer une amelioration :

1. Fork le projet
2. Cree une branche : git checkout -b feature/ma-feature
3. Commit tes changements : git commit -m "feat: ma feature"
4. Push : git push origin feature/ma-feature
5. Ouvre une Pull Request

### Convention de commit

- feat : nouvelle fonctionnalite
- fix : correction de bug
- docs : documentation
- style : formatage, CSS
- refactor : refonte du code
- perf : optimisation

---

## Licence

Ce projet est publie sous licence MIT. Voir le fichier LICENSE pour plus de details.

---

## Avertissement

Ce projet est fourni a des fins educatives et informatives uniquement.

- Ce n'est PAS un conseil financier
- Les donnees sont differees de 15 minutes
- Aucune garantie de precision ou de disponibilite
- Ne l'utilisez PAS pour du trading reel sans verification

Les marches financiers comportent des risques. Consultez un professionnel avant toute decision d'investissement.

---

## Remerciements

- MOEX pour l'API ISS publique
- TradingView pour Lightweight Charts
- Cloudflare pour les Workers
- La communaute open source

---

Si ce projet t'aide, mets une etoile sur GitHub. Cela aide a le faire connaitre.

Fait avec passion pour la Bourse de Moscou.
