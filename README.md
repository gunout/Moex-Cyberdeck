# MOEX CYBERDECK v4.1

Terminal de trading neon pour la Bourse de Moscou. Donnees temps reel (differees 15 min) via l'API publique MOEX ISS.

[![Live Demo](https://img.shields.io/badge/Live_Demo-00f3ff?style=for-the-badge)](https://gunout.github.io/Moex-Cyberdeck/)
[![Version](https://img.shields.io/badge/Version-4.1.0-ffd700?style=for-the-badge)](https://github.com/gunout/Moex-Cyberdeck/releases)
[![License](https://img.shields.io/badge/License-MIT-00ff9d?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Live-00ff9d?style=flat-square)](https://gunout.github.io/Moex-Cyberdeck/)

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/docs/Web/JavaScript)
[![Cloudflare](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=flat-square&logo=cloudflare&logoColor=white)](https://workers.cloudflare.com/)

**[Demo Live](https://gunout.github.io/Moex-Cyberdeck/)** | **[Signaler un bug](https://github.com/gunout/Moex-Cyberdeck/issues)** | **[Demander une feature](https://github.com/gunout/Moex-Cyberdeck/issues)**

---

## Sommaire

- [Fonctionnalites](#fonctionnalites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Indicateurs](#indicateurs)
- [API MOEX ISS](#api-moex-iss)
- [Deploiement](#deploiement)
- [Contribution](#contribution)
- [Licence](#licence)
- [Avertissement](#avertissement)

---

## Fonctionnalites

### Graphique

- Bougies japonaises neon (vert haussier / rouge baissier)
- MA20 - Moyenne mobile 20 jours (cyan)
- MA50 - Moyenne mobile 50 jours (or)
- MA200 - Moyenne mobile 200 jours (magenta)
- MAD20 - Volatilite Mean Absolute Deviation (orange)
- Lignes OPEN / HIGH / LOW / PREV
- Crosshair dore interactif
- Indicateurs activables/desactivables en 1 clic
- Bouton Reset Zoom

### Trading

- 15 actions russes (board TQBR)
- Indice IMOEX en direct
- Carnet d'ordres (orderbook) reel avec spread bid/ask
- Signaux BUY / SELL / HOLD automatiques
- Alertes visuelles (variation superieure a 3 pourcent)
- Statistiques OHLCV completes

### Interface

- Palette tricolore russe (blanc / bleu / rouge)
- Effet scanlines cyberpunk
- Badges sectoriels colores (Energie, Finance, Tech, Metaux, Telecom, Conso)
- Design responsive (desktop / tablette / mobile)
- Horloge Moscou temps reel

### Performance

- Cache local 60 secondes (retour instantane sur un timeframe deja vu)
- AbortController (annule les requetes obsoletes)
- Debounce 250ms sur les timeframes
- Overlay de chargement progressif
- Retry automatique (3 tentatives) en cas d'erreur

---

## Installation

Le projet est 100 pourcent statique. Aucune dependance npm, aucun build.

Clone le depot :

    git clone https://github.com/gunout/Moex-Cyberdeck.git

Entre dans le dossier :

    cd Moex-Cyberdeck

Lance un serveur local :

    python -m http.server 8000

Puis ouvre http://localhost:8000 dans ton navigateur.

### Dependances CDN

- Lightweight Charts v4.1 (TradingView)
- Google Fonts : Orbitron + JetBrains Mono
- Font Awesome 6.4

---

## Configuration

Le dashboard necessite un proxy CORS pour contourner les restrictions navigateur. On utilise un Cloudflare Worker gratuit.

### Etape 1 : Creer le Worker

Va sur https://dash.cloudflare.com et cree un nouveau Worker.

### Etape 2 : Coller le code

Ouvre le Worker et colle ce code JavaScript :

    export default {
      async fetch(request) {
        const url = new URL(request.url);
        const target = url.searchParams.get('url');
        if (!target) return new Response('Missing url parameter', { status: 400 });
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

### Etape 3 : Modifier index.html

Dans ton fichier index.html, remplace la ligne du proxy par :

    const CORS_PROXY = 'https://TON-WORKER.workers.dev/?url=';

---

## Indicateurs

| Indicateur | Couleur | Periode | Utilite |
|:---:|:---:|:---:|---|
| MA20 | Cyan | 20 jours | Tendance court terme |
| MA50 | Or | 50 jours | Tendance moyen terme |
| MA200 | Magenta | 200 jours | Tendance long terme |
| MAD20 | Orange | 20 jours | Volatilite |

### Signaux MA

- Golden Cross : MA20 croise MA50 vers le haut, signal haussier
- Death Cross : MA20 croise MA50 vers le bas, signal baissier

### MAD (Mean Absolute Deviation)

Formule : MAD = (1/n) x somme des valeurs absolues de (close - moyenne)

- Valeur basse : titre stable
- Valeur haute : titre volatil

---

## API MOEX ISS

Gratuit, differe de 15 minutes. Documentation : https://iss.moex.com

### Endpoints utilises

- /iss/engines/stock/markets/shares/boards/TQBR/securities/TICKER.json
- /iss/engines/stock/markets/shares/boards/TQBR/securities/TICKER/candles.json
- /iss/engines/stock/markets/shares/boards/TQBR/securities/TICKER/orderbook.json
- /iss/engines/stock/markets/index/boards/SNDX/securities/IMOEX.json

---

## Deploiement

### GitHub Pages (recommande)

1. Push ton code sur la branche main
2. Settings puis Pages
3. Branch : main / root
4. Ton site est en ligne sur https://TON-PSEUDO.github.io/Moex-Cyberdeck/

### Vercel ou Netlify

Glisse-depose le dossier sur https://vercel.com ou https://netlify.com. Deploiement instantane.

---

## Contribution

Les contributions sont les bienvenues.

Pour contribuer :

    git checkout -b feature/RSI
    git commit -m "feat: ajout du RSI"
    git push origin feature/RSI

Puis ouvre une Pull Request.

### Roadmap

- [x] Graphique bougies + MA20/50/200
- [x] MAD20 volatilite
- [x] Carnet d'ordres
- [x] Indice IMOEX
- [x] Signaux BUY/SELL/HOLD
- [ ] RSI (Relative Strength Index)
- [ ] MACD
- [ ] Bandes de Bollinger
- [ ] Alertes prix
- [ ] Mode PWA
- [ ] Multi-langue FR/EN/RU

---

## Licence

MIT. Voir le fichier LICENSE pour plus de details.

---

## Avertissement

Ce projet est fourni a des fins educatives et informatives uniquement.

- Ce n'est PAS un conseil financier
- Les donnees sont differees de 15 minutes
- Aucune garantie de precision ou de disponibilite
- Ne l'utilisez PAS pour du trading reel sans verification

Les marches financiers comportent des risques. Consultez un professionnel avant toute decision d'investissement.

---

Si ce projet t'aide, mets une etoile sur GitHub.

Fait avec passion pour la Bourse de Moscou.
