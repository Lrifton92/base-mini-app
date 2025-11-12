README.md : Mini App Sondage Airdrop Base - Guide Complet et Explicatif
Aperçu du Projet
Cette Mini App est une application web légère intégrée à Farcaster, conçue pour un sondage fun sur l'airdrop Base (Layer 2 d'Ethereum par Coinbase). Elle utilise OnchainKit pour des interactions sociales onchain : contexte Farcaster (FID utilisateur auto), connexion wallet fluide, et potentiel pour des votes onchain (stockage sur contrat Base).

Objectif : Permettre aux users de voter "Oui/Non" sur "Penses-tu avoir une part de l'airdrop Base ?" avec compteur local, et contexte FID pour unicité.
Technos : Next.js 14+ (App Router), React, OnchainKit (wallet/TX), MiniKit (contexte Farcaster), Vite (dev rapide).
Fun fact : Plus d'animations subtiles (fade-in, hover), sphère SVG centrée, design épuré pour mobile/Farcaster frames.
Live : [Ton URL Vercel] (ajoute-la après déploiement).

Le projet est prêt pour déploiement Vercel et intégration Farcaster – live en 5 min !
Structure du Projet
textbase-mini-app/
├── app/
│   ├── page.tsx          # Page principale (sondage, contexte, sphère)
│   └── rootProvider.tsx  # Provider OnchainKit/MiniKit (config Base)
├── public/               # Assets (ex. : icône pour manifest)
├── minikit.config.ts     # Config Mini App (nom, URL pour Farcaster)
├── next.config.ts        # Config Next.js (ESLint, images, etc.)
├── package.json          # Dépendances et scripts (dev/build/start)
├── .env                  # Vars (NEXT_PUBLIC_URL pour prod)
└── README.md             # Ce fichier !
Setup Local (Dev)

Clone/Install :textcd ton-dossier
npx create-onchain --mini  # Ou clone ton repo
cd base-mini-app
npm install
Config Base :
Édite app/rootProvider.tsx pour Base :tsximport { WagmiProvider } from 'wagmi';
import { base } from 'wagmi/chains';
import { OnchainKitProvider } from '@coinbase/onchainkit';

<WagmiProvider config={{ chains: [base] }}>
  <OnchainKitProvider chain={base}>
    <YourApp />
  </OnchainKitProvider>
</WagmiProvider>
Ajoute API Key Coinbase si besoin (gratuite sur developers.coinbase.com).

Lance local :textnpm run dev
Ouvre http://localhost:5173 (Vite port) : Teste sondage, Wallet (connecte MetaMask sur Base testnet).

Test Farcaster :
Lance en frame : Poste l'URL local en Warpcast pour voir FID auto.


Fonctionnalités Explicatives
1. Contexte Social (MiniKit)

Hook useMiniKit() récupère FID/username/photo en fluide (sans login).
Ex. : Si connecté Farcaster, affiche "FID : 123" – votes uniques par identité.

2. Sondage Interactif

Boutons "Oui/Non" avec compteur React state (local, reset au reload).
Disabled après vote pour unicité.
Style : Bleu Base, hover subtil, responsive mobile.

3. Intégration OnchainKit (Wallet & TX)

<Wallet /> : Connecte MetaMask/Coinbase sur Base (mainnet/testnet).
Potentiel TX : Ajoute <TransactionButton /> pour stocker votes sur contrat (ex. : ton Storage à 0xF910...acF).
Coût : ~0.0001 ETH (gas bas sur Base).

ABI exemple pour store votes :json[{"inputs":[{"type":"uint256"}],"name":"store","outputs":[],"stateMutability":"nonpayable","type":"function"}]

4. Design & UX

Épuré : Fond blanc, accents bleu Base, sections border radius.
Centré : Sphère SVG (gradient bleu, "Base" blanc).
Footer : "Mini app créée par Lrifton92" (sans apostrophe pour ESLint).

Déploiement

Build local :textnpm run build
Déploye :textnpm i -g vercel
vercel login
vercel --prod
Prompt : Y pour setup, nom base-mini-app, root ., build npm run build.
URL live : https://base-mini-app-xxx.vercel.app.

Config prod :
.env : NEXT_PUBLIC_URL=https://ton-url.vercel.app.
minikit.config.ts : url: 'ton-url', name: 'Airdrop Base Poll'.
Redéploie : vercel --prod.


Intégration Farcaster & Base

Farcaster : Poste l'URL en frame (frames.farcaster.xyz) – contexte FID auto, votes uniques.
Base : OnchainKit configure auto le réseau (low gas). Test TX sur Sepolia (faucet.base.org).
Viralité : Tag #Base #Airdrop sur Warpcast – users cliquent, voient leur FID, votent fun.

Troubleshooting

Build ESLint : Si erreur apostrophe, supprime ou échappe avec &apos;.
Wallet fail : Vérifie chains: [base] en wagmi.
Contexte vide : Test en frame Farcaster (local = anonyme).
Gas TX : Utilise testnet ; mainnet = 0.0001 ETH/vote.

Contributions & Licence
Fork et PR bienvenus ! Licence MIT. Contact : Lrifton92 sur Farcaster.
Build with ❤️ pour l'airdrop Base – votes onchain fun ! 🚀
