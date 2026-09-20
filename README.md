# Accès à l'eau potable dans le monde — Tableau de bord Power BI

Tableau de bord interactif Power BI analysant l'accès à l'eau potable à l'échelle mondiale, continentale et nationale, réalisé pour aider une ONG internationale et son bailleur de fonds à cibler leurs investissements.

## Contexte

Une ONG internationale dont la mission est de garantir l'accès à l'eau potable pour toutes les populations a obtenu une demande de financement auprès d'un bailleur de fonds. Ces financements doivent être orientés vers l'un des trois domaines d'expertise suivants, dans un pays encore indéterminé :

- **Domaine 1** — Création de services d'accès à l'eau potable
- **Domaine 2** — Modernisation de services d'accès à l'eau déjà existants
- **Domaine 3** — Consulting auprès d'administrations / gouvernements

Le tableau de bord vise à identifier les pays en difficulté, prioriser les zones critiques et faciliter la décision du chef de mission et du bailleur de fonds.

## Aperçu du rapport

Le rapport Power BI s'articule en 3 pages, du plus général au plus précis :

| Page | Vue | Contenu clé |
|---|---|---|
| 1 | **Mondiale** | KPI globaux (% accès à l'eau, taux de mortalité liée à l'eau insalubre), carte choroplèthe, évolution 2000–2017, comparaison par continent |
| 2 | **Continentale** | Comparaison par pays, stabilité politique, tendance temporelle multi-séries, corrélation urbanisation / accès à l'eau |
| 3 | **Nationale** | Analyse par domaine d'expertise (urbain vs rural, qualité des infrastructures, efficacité politique), densité et taille de population |

### Filtres interactifs

- Sélection du continent / pays
- Période d'analyse (année de début / fin)
- Seuil de stabilité politique (slider)
- Type d'infrastructure (basique / gérée sûrement)

## Données

| Source | Contenu | Lignes | Période |
|---|---|---|---|
| `BasicAndSafelyManagedDrinkingWaterServices.csv` | Accès à l'eau basique / gérée sûrement (% pop.) | 10 476 | 2000–2017 |
| `MortalityRateAttributedToWater.csv` | Taux de mortalité lié à l'eau insalubre | 549 | 2016 |
| `PoliticalStability.csv` | Indice de stabilité politique (Banque Mondiale) | 3 526 | 2000–2018 |
| `Population.csv` | Population totale, urbaine, rurale par pays | 20 914 | 2000–2018 |
| `RegionCountry.csv` | Table géographique (194 pays, 6 régions OMS) | 194 | — |

## Modélisation et traitement

- **Power Query** : promotion des en-têtes, nettoyage des lignes vides, conversion numérique locale (`en-US`), filtrage sur la granularité, jointures gauches multiples pour construire la table de faits.
- **Modèle en étoile** : table de faits `Fait_Indicateurs` reliée aux dimensions `Dim_Geography` et `Dim_Temps`, en mode import.
- **Mesures DAX principales** : `Taux_Acces_Eau`, `Population_Sans_Eau`, `Taux_Mortalite_WASH`, `Pays_Sous_Seuil`, `Stabilite_Politique_Moy`, `Taux_Urbanisation`.

## Design et accessibilité

- Palette bleue thématique (`#0C447C`, `#378ADD`, `#B5D4F4`) avec un accent orange (`#EF9F27`) pour les zones critiques, accessible aux daltoniens.
- Police minimum 11pt, titres et légendes explicites, info-bulles sur chaque visualisation.
- Bouton de réinitialisation des filtres sur chaque page.

## Contenu du dépôt

```
projet power BI.pbix        # Rapport Power BI final (3 pages)
Document de cadrage.pdf     # Cadrage du projet : objectifs, indicateurs, DAX, filtres
power point.pdf             # Support de présentation (contexte, prétraitement, justification)
donnees/                    # Jeux de données sources (CSV / Excel)
```

## Outils

Power BI Desktop (Power Query, DAX, modélisation en étoile).

## Contexte académique

Projet réalisé dans le cadre du Master 1 — Data Visualisation, encadré par Chamsedine AIDARA (Tech Lead Data & IA).
