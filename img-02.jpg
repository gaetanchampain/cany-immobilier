/* =============================================================
   Système i18n — Cany Immobilier
   Bilinguisme FR/EN avec dictionnaire centralisé.
   - Au chargement : on stocke l'innerHTML FR original
   - Au clic du toggle : on swap FR ↔ EN sur tous les nœuds matchés
   - Persistance via localStorage
   ============================================================= */
(function () {
  'use strict';

  // Dictionnaire FR → EN
  // Note : les clés sont les textContent FR (avec tags inline pour les rares cas riches).
  // Les valeurs sont les textContent EN équivalents.
  const FR_TO_EN = {
    // === Topbar / Header ===
    "Pays de Caux · Côte d'Albâtre": "Pays de Caux · Alabaster Coast",
    "Immobilier": "Real Estate",
    "Normandie · 1997": "Normandy · since 1997",
    "Nos biens à vendre": "Properties for sale",
    "Nos biens vendus": "Sold properties",
    "L'agence": "About us",
    "Estimation": "Valuation",
    "Contact": "Contact",
    "Menu": "Menu",

    // === Hero accueil ===
    "— Le Pays de Caux, depuis 1997 —": "— The Pays de Caux, since 1997 —",
    "Transmettre": "Transmitting",
    "les": "the",
    "belles": "finest",
    "demeures": "estates",
    "de": "of",
    "Normandie.": "Normandy.",
    "Manoirs, châteaux et maisons de maître,": "Manors, châteaux and master houses,",
    "entre Étretat et la Côte d'Albâtre,": "between Étretat and the Alabaster Coast,",
    "d'une famille à": "passed from one family",
    "la suivante.": "to the next.",
    "Scroll": "Scroll",

    // === Hero plate ===
    "✦ Une transmission emblématique": "✦ A landmark transmission",
    "Château de B***,": "Château de B***,",
    "Pays de Caux": "Pays de Caux",
    "Vendu en MMXXIII": "Sold in MMXXIII",
    "à transmettre": "to transmit",
    "Estimer": "Value",
    "mon bien": "my property",

    // === Familles villages ===
    "Étretat": "Étretat",
    "Yport": "Yport",
    "Fécamp": "Fécamp",
    "Saint-Valery-en-Caux": "Saint-Valery-en-Caux",
    "Veules-les-Roses": "Veules-les-Roses",
    "Cany-Barville": "Cany-Barville",
    "Côte d'Albâtre": "Alabaster Coast",

    // === Famille Connier ===
    "« Mon grand-père vendait à Paris. Moi, je vends en Normandie. »":
      "\"My grandfather sold in Paris. I sell in Normandy.\"",
    "Jean-Charles C. · Fondateur · 1997": "Jean-Charles C. · Founder · 1997",
    "L'agence — depuis 1997": "About us — since 1997",
    "Une famille,": "One family,",
    "trois": "three",
    "générations,": "generations,",
    "un seul": "one and only",
    "terroir.": "terroir.",
    "Depuis 1997, la famille Connier accompagne ceux qui cherchent — et ceux qui transmettent — les plus belles maisons du Pays de Caux. Charles, le grand-père, agent immobilier rue Montmartre dans les années 1950 ; Jean-Charles, le fondateur, revenu en 1995 à ses racines normandes ; et désormais Louis, son fils cadet, qui a rejoint l'agence en 2022 avec la même":
      "Since 1997, the Connier family has guided those seeking — and those transmitting — the finest houses of the Pays de Caux. Charles, the grandfather, a real estate agent on rue Montmartre in the 1950s; Jean-Charles, the founder, who returned in 1995 to his Norman roots; and now Louis, his younger son, who joined the agency in 2022 with the same",
    "exigence": "exacting standards",
    "du beau et du juste.": "for what is beautiful and right.",
    "Nous ne vendons pas des biens : nous accompagnons des transmissions. Une demeure de famille n'est pas un produit, c'est une histoire qui change de mains. Nous prenons le temps qu'il faut — rarement le plus court, jamais le plus rapide.":
      "We do not sell properties: we accompany transmissions. A family estate is not a product, it is a story changing hands. We take the time it deserves — rarely the shortest, never the quickest.",

    // === Signatures ===
    "Jean-Charles C.": "Jean-Charles C.",
    "Fondateur · Direction": "Founder · Director",
    "Patricia C.": "Patricia C.",
    "Conseil · Estimations": "Advisory · Valuations",
    "Louis C.": "Louis C.",
    "Relations clients": "Client Relations",

    // === Stats ===
    "Au service du Pays de Caux": "Serving the Pays de Caux",
    "Demeures transmises depuis 1997": "Estates transmitted since 1997",
    "Générations Connier à l'agence": "Connier generations at the agency",
    "Vendeurs nous recommandent": "Sellers recommend us",
    "Notre carte de visite": "Our calling card",
    "Quelques-unes": "A few",
    "que nous avons": "that we have",
    "transmises.": "transmitted.",
    "Plus de": "More than",
    "mille": "a thousand",
    "maisons sont passées entre nos mains depuis 1997. Voici un aperçu — pour donner la mesure du genre de pierres avec lesquelles nous travaillons.":
      "houses have passed through our hands since 1997. Here is a glimpse — to give a sense of the kind of stone we work with.",
    "demeures transmises depuis 1997 — sur les seuls cantons du Pays de Caux et de la Côte d'Albâtre.":
      "estates transmitted since 1997 — across the cantons of the Pays de Caux and the Alabaster Coast alone.",

    // === Catégories grille ===
    "Vendu": "Sold",
    "Manoir": "Manor",
    "de 1640,": "from 1640,",
    "Villa": "Villa",
    "face mer": "facing the sea",
    "Près d'Étretat": "Near Étretat",
    "du XVI": "from the 16th",
    "Château": "Château",
    "fin XVI": "late 16th",
    "Ancien": "Former",
    "presbytère": "presbytery",
    "Ensemble": "Estate",
    "vue mer": "sea view",
    "Maison": "House",
    "de maître": "master",
    "du XVIII": "from the 18th",

    // === Pièce maîtresse ===
    "La pièce maîtresse": "The centrepiece",
    "★ Coup de cœur · Étretat": "★ Featured · Étretat",
    "Chantoiseau,": "Chantoiseau,",
    "face aux falaises.": "facing the cliffs.",
    "« L'une des plus belles vues sur les falaises mythiques d'Étretat que nous ayons rencontrées en vingt-huit ans. »":
      "\"One of the most beautiful views over Étretat's legendary cliffs we have encountered in twenty-eight years.\"",
    "Surface": "Floor area",
    "Chambres": "Bedrooms",
    "Jardin clos": "Walled garden",
    "Honoraires inclus · Réf. 2675": "Fees included · Ref. 2675",
    "Découvrir": "Discover",

    // === Notre sélection ===
    "Notre sélection": "Our selection",
    "Nos biens": "Our properties",
    "à vendre.": "for sale.",
    "Chaque demeure visitée, vérifiée, accompagnée par la famille — comme on confierait une maison à des amis qui sauront la":
      "Each estate visited, verified, escorted by the family — as one would entrust a house to friends who will pass it on with",
    "transmettre": "care",

    // === Citations & descriptions courtes des biens (grille home) ===
    "« Style Louis XIII, parc à l'anglaise de 25 hectares avec son île privée. »":
      "\"Louis XIII style, 25-hectare English parkland with private island.\"",
    "Style Louis XIII. Parc à l'anglaise de 25 hectares avec plan d'eau et île privée, à quelques minutes des plages.":
      "Louis XIII style. 25-hectare English parkland with pond and private island, minutes from the beaches.",
    "« Héritier d'un fief viking millénaire — parc de 6,6 hectares. »":
      "\"Heir to a thousand-year-old Viking fief — 6.6-hectare grounds.\"",
    "normand": "Norman",
    "en pierre": "in stone",
    "Héritier d'un fief viking millénaire. Parc de 6,6 hectares, deux dépendances, à 10 min d'une gare directe pour Paris.":
      "Heir to a thousand-year-old Viking fief. 6.6-hectare grounds, two outbuildings, 10 min from a direct train to Paris.",
    "Brique Saint-Jean": "Saint-Jean brick",
    "« Construit par des moines en briques de Saint-Jean. »":
      "\"Built by monks in Saint-Jean brick.\"",
    "de 1640": "from 1640",
    "Construit par des moines en briques de Saint-Jean et grès. Colombier seigneurial, piscine chauffée et couverte.":
      "Built by monks in Saint-Jean brick and sandstone. Seigneurial dovecote, heated and covered swimming pool.",
    "Nouveau": "New",
    "« Élégant manoir dans son jus d'origine. »":
      "\"Elegant manor in its original state.\"",
    "siècle": "century",
    "Élégant manoir dans son jus d'origine. Huit pièces, quatre hectares avec plan d'eau, dépendance.":
      "Elegant manor in its original state. Eight rooms, four hectares with pond, outbuilding.",
    "« Plage à pied, tour formant petit salon. »":
      "\"Beach within walking distance, tower forming a small parlour.\"",
    "Castel": "Castel",
    "Plage et restaurants à pied. Tour formant petit salon, hauteur sous plafond 3 m, terrasse suspendue.":
      "Beach and restaurants on foot. Tower forming a small parlour, 3 m ceiling height, suspended terrace.",
    "Port de plaisance": "Marina",
    "« Allure de petit château, salon de 46 m². »":
      "\"Look of a small château, 46 m² living room.\"",
    "Aux portes du port de plaisance, allure de petit château avec ses deux ailes et son salon de 46 m².":
      "At the gates of the marina, the bearing of a small château with its two wings and 46 m² living room.",
    "Voir toutes les demeures (24)": "View all estates (24)",

    // === Carte territoire ===
    "Le territoire": "The territory",
    "Un pays à": "A land of",
    "flanc de falaise.": "cliff-side villages.",
    "Du port de Fécamp aux jardins clos de Veules — chaque village, chaque chemin. Voici nos demeures, là où elles dorment.":
      "From Fécamp's port to the walled gardens of Veules — every village, every path. Here are our estates, where they rest.",
    "La Manche": "The Channel",
    "— Pays de Caux —": "— Pays de Caux —",
    "Yport · Fécamp": "Yport · Fécamp",
    "St-Valery": "St-Valery",
    "N° 01 · Villa Chantoiseau": "No. 01 · Villa Chantoiseau",
    "N° 02 · Château fin XVIᵉ": "No. 02 · Château late 16th",
    "N° 03 · Manoir 6,6 ha": "No. 03 · Manor 6.6 ha",
    "N° 04 · Manoir de 1640": "No. 04 · Manor from 1640",
    "N° 05 · Manoir XVIᵉ": "No. 05 · Manor 16th",
    "N° 06 · Castel vue mer": "No. 06 · Castel sea view",
    "N° 07 · Maison de maître": "No. 07 · Master house",
    "Le Pays de Caux,": "The Pays de Caux,",
    "mode d'emploi.": "a user's guide.",
    "Un plateau crayeux qui plonge dans la Manche en falaises blanches, ponctué de villages aux clos de murs et de manoirs en briques rouges. Cinquante-quatre kilomètres de littoral classé, un terroir agricole d'élite, Étretat et Veules-les-Roses parmi les plus beaux villages de France. Paris à deux heures.":
      "A chalk plateau that plunges into the Channel as white cliffs, dotted with walled villages and red-brick manors. Fifty-four kilometres of protected coastline, a premier agricultural terroir, Étretat and Veules-les-Roses among the most beautiful villages in France. Paris just two hours away.",
    "Chantoiseau": "Chantoiseau",
    "Étretat · 240 m²": "Étretat · 240 m²",
    "Côte d'Albâtre · 25 ha": "Alabaster Coast · 25 ha",

    // === Estimation ===
    "Vous transmettez ?": "Are you transmitting?",
    "Faites estimer": "Have your estate",
    "votre demeure": "valued",
    "par des experts.": "by experts.",
    "Nous estimons votre bien": "We value your property",
    "in situ": "in situ",
    ", gratuitement, sans engagement — en nous appuyant sur vingt-huit ans de transactions comparables sur le terroir cauchois.":
      ", free of charge, without obligation — drawing on twenty-eight years of comparable transactions across the Cauchois terroir.",
    "Visite chez vous, à votre rythme": "Visit at your home, at your pace",
    "Estimation in situ par Jean-Charles ou Louis, sans engagement.":
      "On-site valuation by Jean-Charles or Louis, no obligation.",
    "Rapport écrit avec comparables": "Written report with comparables",
    "Stratégie de mise en marché, fourchette de prix justifiée.":
      "Marketing strategy, justified price range.",
    "Mandat exclusif ou partagé": "Exclusive or shared mandate",
    "Vous décidez du tempo. Pas de pression, jamais.":
      "You set the tempo. No pressure, ever.",
    "Demande d'estimation": "Valuation request",
    "Parlez-nous": "Tell us about",
    "votre demeure.": "your estate.",
    "Prénom": "First name",
    "Nom": "Last name",
    "Adresse du bien": "Property address",
    "Type": "Type",
    "Téléphone": "Phone",
    "Demander mon estimation": "Request my valuation",
    "Réponse confidentielle sous 48 heures · Sans engagement":
      "Confidential reply within 48 hours · No obligation",

    // === Page "biens" ===
    "Accueil": "Home",
    "Maisons à vendre": "Houses for sale",
    "Notre catalogue": "Our catalogue",
    "Demeures": "Estates",
    "à transmettre": "to transmit",
    "24 demeures · 7 villages": "24 estates · 7 villages",
    "Châteaux, manoirs, maisons de maître et castels — du fief viking de Saint-Pierre à la villa éclectique d'Étretat. Chaque bien visité, vérifié, accompagné par la famille.":
      "Châteaux, manors, master houses and castels — from the Viking fief of Saint-Pierre to the eclectic villa of Étretat. Every property visited, verified, escorted by the family.",
    "Toutes (24)": "All (24)",
    "Châteaux (3)": "Châteaux (3)",
    "Manoirs (8)": "Manors (8)",
    "Maisons de maître (6)": "Master houses (6)",
    "Castels & villas (4)": "Castels & villas (4)",
    "Vue mer (7)": "Sea view (7)",
    "Tous les budgets": "All budgets",
    "Moins de 800 000 €": "Under €800,000",
    "800 000 € — 1,5 M€": "€800,000 — €1.5M",
    "1,5 M€ — 3 M€": "€1.5M — €3M",
    "Plus de 3 M€": "Over €3M",
    "Trier — Coup de cœur": "Sort — Featured",
    "Prix croissant": "Price ascending",
    "Prix décroissant": "Price descending",
    "Nouveautés": "Latest",
    "⌘ Sélection privée — sur demande": "⌘ Private selection — on request",
    "confidentielles,": "confidential,",
    "hors catalogue.": "off-catalogue.",
    "Sept demeures exceptionnelles, vendues sans publication, accessibles uniquement sur rendez-vous et présentation.":
      "Seven exceptional estates, sold without listing, accessible only by appointment and introduction.",
    "Demander l'accès": "Request access",
    "★ Coup de cœur": "★ Featured",
    "Étretat · Vue mer": "Étretat · Sea view",
    "L'une des plus belles vues sur les falaises mythiques. 7 chambres, jardin clos.":
      "One of the most beautiful views over the legendary cliffs. 7 bedrooms, walled garden.",
    "1430 m² jardin": "1,430 m² garden",
    "Style Louis XIII. Parc à l'anglaise de 25 hectares avec plan d'eau et île privée.":
      "Louis XIII style. 25-hectare English parkland with pond and private island.",
    "Héritier d'un fief viking millénaire. Parc de 6,6 hectares, deux dépendances.":
      "Heir to a thousand-year-old Viking fief. 6.6-hectare grounds, two outbuildings.",
    "Construit par des moines en briques de Saint-Jean. Colombier seigneurial, piscine.":
      "Built by monks in Saint-Jean brick. Seigneurial dovecote, swimming pool.",
    "Élégant manoir dans son jus d'origine. Huit pièces, plan d'eau, dépendance.":
      "Elegant manor in its original state. Eight rooms, pond, outbuilding.",
    "Plage à pied. Tour formant petit salon, hauteur 3 m, terrasse suspendue.":
      "Beach on foot. Tower forming a small parlour, 3 m ceiling, suspended terrace.",
    "Allure de petit château avec ses deux ailes, salon de 46 m².":
      "Look of a small château with two wings, 46 m² living room.",
    "Maison principale et dépendances en pierre, dans un parc d'arbres centenaires.":
      "Main house and outbuildings in stone, set in a park of century-old trees.",
    "Vue mer": "Sea view",
    "Esprit balnéaire fin XIXᵉ, pieds dans le sable, baies sur la Manche.":
      "Late 19th-century seaside spirit, feet in the sand, bay windows over the Channel.",
    "Maison du curé du XVIIᵉ, jardin clos de murs, près du bourg.":
      "17th-century parish priest's house, walled garden, near the village centre.",
    "Demeure": "Estate",
    "Belle bourgeoise restaurée avec soin, parquet d'origine, cheminées en marbre.":
      "Fine bourgeois house carefully restored, original parquet, marble fireplaces.",
    "Près d'Yport": "Near Yport",
    "de pêcheur": "fisherman's",
    "Charme balnéaire, à 200 m de la plage. Idéale pied-à-terre normand.":
      "Seaside charm, 200 m from the beach. An ideal Norman pied-à-terre.",
    "Charger plus de demeures (+ 12)": "Load more estates (+ 12)",
    "Vous ne": "Can't find",
    "trouvez pas": "the perfect",
    "la perle rare ?": "match?",
    "Notre carnet d'adresses garde toujours un peu d'avance sur le marché. Décrivez-nous votre projet — nous vous recontactons sous 48 h.":
      "Our address book always stays a step ahead of the market. Tell us about your project — we'll be in touch within 48 hours.",
    "Décrire mon projet": "Describe my project",

    // === Fiche bien Chantoiseau ===
    "Villa Chantoiseau · Étretat": "Villa Chantoiseau · Étretat",
    "★ La pièce maîtresse · Réf. N° 2675": "★ The centrepiece · Ref. No. 2675",
    "Étretat · Seine-Maritime · Pays de Caux": "Étretat · Seine-Maritime · Pays de Caux",
    "Visiter": "Visit",
    "Vue mer panoramique": "Panoramic sea view",
    "+ 24 photos": "+ 24 photos",
    "Surface habitable": "Living area",
    "Pièces": "Rooms",
    "Niveaux": "Floors",
    "Terrain": "Land",
    "Construction": "Built",
    "La demeure": "The estate",
    "villa éclectique": "eclectic villa",
    "du dernier souffle Belle Époque.": "of the last Belle Époque breath.",
    "Construite en 1893 par l'architecte Adolphe Faucon pour un négociant en draps rouennais, la Villa Chantoiseau couronne l'un des derniers tertres habitables avant la falaise. Quatre niveaux, sept chambres, deux cents quarante mètres carrés habitables, posés sur mille quatre cent trente mètres carrés de jardin clos, planté de tilleuls centenaires.":
      "Built in 1893 by architect Adolphe Faucon for a Rouen cloth merchant, Villa Chantoiseau crowns one of the last habitable mounds before the cliff. Four floors, seven bedrooms, two hundred and forty square metres of living space, set on one thousand four hundred and thirty square metres of walled garden, planted with century-old lime trees.",
    "La maison a été restaurée en 2019 par les propriétaires actuels, sous la direction d'un architecte du patrimoine. Toiture, charpente, fenêtres et boiseries d'origine — tout a été conservé, restauré, jamais remplacé. Parquets":
      "The house was restored in 2019 by its current owners under the direction of a heritage architect. Roof, framework, windows and original woodwork — everything was preserved, restored, never replaced. Parquet",
    "point de Hongrie": "herringbone",
    "du salon retrouvés sous trois couches de moquette. Cuisine contemporaine en chêne massif et marbre vert de la Sarthe.":
      "in the living room recovered beneath three layers of carpet. Contemporary kitchen in solid oak and green Sarthe marble.",
    "« Une vue qu'on n'oublie pas, dans une demeure qui n'a renoncé à aucun de ses détails d'origine. »":
      "\"A view one does not forget, in an estate that has surrendered none of its original details.\"",
    "Sept chambres distribuées sur deux étages, dont une suite parentale de 38 m² avec dressing et salle d'eau en marbre. Au troisième étage, deux chambres mansardées sous les toits, idéales pour un atelier ou une chambre d'enfant. Au sous-sol, cave à vin voûtée et chaufferie. Cabanon en briques dans le jardin, déjà câblé pour devenir un studio indépendant.":
      "Seven bedrooms across two floors, including a 38 m² master suite with dressing room and marble bathroom. On the third floor, two attic bedrooms beneath the roof, ideal as a studio or children's room. In the basement, a vaulted wine cellar and boiler room. Brick cabin in the garden, already wired to become an independent studio.",
    "L'essentiel": "The essentials",
    "de la villa.": "of the villa.",
    "180° sur les falaises d'Aval": "180° over the Aval cliffs",
    "Restauration patrimoine": "Heritage restoration",
    "Architecte du patrimoine, 2019": "Heritage architect, 2019",
    "Parquet point de Hongrie": "Herringbone parquet",
    "Salon, salle à manger, bibliothèque": "Living room, dining room, library",
    "Cheminées en marbre": "Marble fireplaces",
    "4 cheminées d'origine restaurées": "4 original fireplaces restored",
    "Jardin clos de murs": "Walled garden",
    "1 430 m², tilleuls centenaires": "1,430 m², century-old lime trees",
    "Cabanon en brique": "Brick cabin",
    "Studio possible, déjà câblé": "Possible studio, already wired",
    "Suite parentale 38 m²": "38 m² master suite",
    "Dressing, salle d'eau marbre": "Dressing room, marble bathroom",
    "Cuisine contemporaine": "Contemporary kitchen",
    "Chêne massif, marbre vert": "Solid oak, green marble",
    "Réf. N° 2675 · Étretat": "Ref. No. 2675 · Étretat",
    "Honoraires inclus charge vendeur": "Fees included, paid by seller",
    "Jean-Charles Connier": "Jean-Charles Connier",
    "Directeur · 02 35 97 12 34": "Director · +33 2 35 97 12 34",
    "Demander une visite": "Request a visit",
    "Appeler l'agence": "Call the agency",
    "Recevoir le dossier complet": "Receive the full dossier",
    "Réponse confidentielle · Sous 24 h": "Confidential reply · Within 24 h",

    // === DPE ===
    "Diagnostic de performance énergétique": "Energy performance certificate",
    "Diagnostic réalisé le 14 mars 2024 · valable jusqu'au 14 mars 2034":
      "Assessment dated 14 March 2024 · valid until 14 March 2034",
    "Consommation d'énergie": "Energy consumption",
    "Logement": "Property",
    "extrêmement consommateur": "extremely energy-intensive",
    "Émissions de gaz à effet de serre": "Greenhouse gas emissions",
    "Émissions": "Emissions",
    "très importantes": "very high",
    "★ Coût annuel estimé d'énergie": "★ Estimated annual energy cost",
    "entre": "between",
    "soit ≈ 1 040 € à 1 410 € par mois": "i.e. ≈ €1,040 to €1,410 per month",
    "Estimation pour un usage standard, prix moyens des énergies indexés au 1":
      "Estimate for standard usage, average energy prices indexed as of 1",
    "janvier 2024 (abonnements inclus).": "January 2024 (subscriptions included).",

    // === Visite en images ===
    "visite,": "visit,",
    "en images.": "in images.",
    "La fiche technique": "The fact sheet",
    "résumé.": "in summary.",
    "Tous les chiffres et caractéristiques de la villa, en un coup d'œil — pour les amateurs qui aiment l'essentiel avant la visite.":
      "All the figures and features of the villa at a glance — for those who like the essentials before visiting.",
    "Type de bien": "Property type",
    "Belle Époque": "Belle Époque",
    "Année de construction": "Year built",
    "Nombre de pièces": "Number of rooms",
    "Nombre de chambres": "Number of bedrooms",
    "Surface séjour": "Living room area",
    "Surface cuisine": "Kitchen area",
    "Surface chambre 1": "Bedroom 1 area",
    "Surface chambre 2": "Bedroom 2 area",
    "Surface chambre 3": "Bedroom 3 area",
    "Surface du terrain": "Land area",
    "Annexes": "Outbuildings",
    "Cave de 18 m²": "18 m² cellar",
    "Stationnement": "Parking",
    "Cour intérieure · 3 places": "Interior courtyard · 3 spaces",
    "Chauffage": "Heating",
    "Fuel · Cheminées": "Oil · Fireplaces",
    "Exposition": "Aspect",
    "Sud-Ouest · Mer": "South-West · Sea",
    "État général": "General condition",
    "Restauré": "Restored",
    "en 2019": "in 2019",
    "Taxe foncière": "Property tax",
    "1 740 € / an": "€1,740 / year",
    "DPE — énergie": "EPC — energy",
    "DPE — émissions GES": "EPC — GHG emissions",
    "Coût énergie estimé / an": "Estimated energy cost / year",
    "· Mise en ligne le 12 mars 2026 · Mandat exclusif":
      "· Listed on 12 March 2026 · Exclusive mandate",
    "Demander le dossier complet": "Request the full dossier",

    // === Localisation ===
    "L'emplacement": "The location",
    "À deux pas": "A stone's throw",
    "des falaises d'Étretat.": "from Étretat's cliffs.",
    "— Étretat —": "— Étretat —",
    "Le Tilleul": "Le Tilleul",
    "Bénouville": "Bénouville",
    "Étretat,": "Étretat,",
    "cœur du village.": "heart of the village.",
    "À 8 minutes à pied du centre-ville et de la plage. La maison occupe l'un des derniers tertres habitables avant la falaise — une position rarissime, protégée du vent dominant par les bois de la Roche-Vaudieu.":
      "An 8-minute walk from the village centre and the beach. The house occupies one of the last habitable mounds before the cliff — an exceptionally rare position, sheltered from the prevailing wind by the Roche-Vaudieu woods.",
    "Plage d'Étretat": "Étretat beach",
    "8 min à pied": "8 min on foot",
    "Falaise d'Aval": "Aval cliff",
    "12 min à pied": "12 min on foot",
    "Gare du Havre": "Le Havre station",
    "35 min en voiture": "35 min by car",
    "Aéroport Deauville": "Deauville airport",
    "Paris": "Paris",

    // === Autres biens ===
    "D'autres": "Other estates",
    "qui pourraient vous plaire.": "you may like.",
    "N° 2667 · Côte d'Albâtre": "No. 2667 · Alabaster Coast",
    "N° 2680 · Côte d'Albâtre": "No. 2680 · Alabaster Coast",
    "N° 2669 · Port de plaisance": "No. 2669 · Marina",

    // === Footer ===
    "Cany.": "Cany.",
    "Caux.": "Caux.",
    "Immobilier · Normandie · 1997": "Real Estate · Normandy · since 1997",
    "Patricia, Jean-Charles & Louis CONNIER": "Patricia, Jean-Charles & Louis CONNIER",
    "« Nous accompagnons les transmissions de demeures depuis vingt-huit ans, sur la Côte d'Albâtre et dans le Pays de Caux. Une famille, trois générations, un seul terroir. »":
      "\"We have been guiding the transmission of estates for twenty-eight years, on the Alabaster Coast and in the Pays de Caux. One family, three generations, one and only terroir.\"",
    "Nous contacter": "Contact us",
    "La famille Connier": "The Connier family",
    "Notre méthode": "Our method",
    "Honoraires": "Fees",
    "Mentions légales": "Legal notices",
    "Naviguer": "Navigate",
    "Le Journal": "Journal",
    "Bureau": "Office",
    "14 place de l'Église": "14 place de l'Église",
    "76450 Cany-Barville": "76450 Cany-Barville",
    "Du mardi au samedi · 9h–18h": "Tuesday to Saturday · 9 am – 6 pm",
    "© 1997–2026 · Cany Immobilier · Carte T n° CPI 7601 2018 000 ··· FNAIM":
      "© 1997–2026 · Cany Immobilier · License T no. CPI 7601 2018 000 ··· FNAIM",
    "— fait à Cany-Barville —": "— made in Cany-Barville —",

    // Boutons / labels génériques
    "Confidentiel": "Confidential",
    "Voir": "View",
    "demande": "on request",
    "Réf.": "Ref.",
    "Oui": "Yes"
  };

  const EN_TO_FR = {};
  Object.keys(FR_TO_EN).forEach(k => { EN_TO_FR[FR_TO_EN[k]] = k; });

  // Normalise les espaces (NBSP, tabs, retours ligne) en simple espace
  const normalize = s => s.replace(/\s+/g, ' ').trim();

  // État courant
  let currentLang = localStorage.getItem('cany-lang') || 'fr';

  // Translate a TextNode in place
  function translateTextNode(node, dict) {
    const original = node.nodeValue;
    const norm = normalize(original);
    if (!norm) return;
    if (dict[norm]) {
      // Préserver les espaces de début/fin (importants pour le formatage inline)
      const leading  = original.match(/^\s*/)[0];
      const trailing = original.match(/\s*$/)[0];
      node.nodeValue = leading + dict[norm] + trailing;
    }
  }

  // Walk through all text nodes in a root, applying the dictionary
  function walkAndTranslate(root, dict) {
    const walker = document.createTreeWalker(
      root,
      NodeFilter.SHOW_TEXT,
      {
        acceptNode: function (n) {
          // Skip nodes inside <script>, <style>, <noscript>
          const parent = n.parentNode;
          if (!parent) return NodeFilter.FILTER_REJECT;
          const tag = parent.nodeName;
          if (tag === 'SCRIPT' || tag === 'STYLE' || tag === 'NOSCRIPT') {
            return NodeFilter.FILTER_REJECT;
          }
          if (!normalize(n.nodeValue)) return NodeFilter.FILTER_REJECT;
          return NodeFilter.FILTER_ACCEPT;
        }
      }
    );
    const nodes = [];
    let n;
    while ((n = walker.nextNode())) nodes.push(n);
    nodes.forEach(node => translateTextNode(node, dict));
  }

  // Met à jour les attributs traduisibles (placeholder, alt, title, aria-label)
  function translateAttributes(dict) {
    const attrs = ['placeholder', 'alt', 'title', 'aria-label'];
    document.querySelectorAll('[' + attrs.join('],[') + ']').forEach(el => {
      attrs.forEach(attr => {
        const v = el.getAttribute(attr);
        if (!v) return;
        const norm = normalize(v);
        if (dict[norm]) el.setAttribute(attr, dict[norm]);
      });
    });
  }

  // Mise à jour visuelle du toggle
  function updateToggleVisual(toggle) {
    if (!toggle) return;
    if (currentLang === 'en') {
      toggle.innerHTML = 'FR · <strong>EN</strong>';
    } else {
      toggle.innerHTML = '<strong>FR</strong> · EN';
    }
  }

  // Bascule de langue
  function switchTo(lang) {
    if (lang === currentLang) return;
    const dict = (lang === 'en') ? FR_TO_EN : EN_TO_FR;
    walkAndTranslate(document.body, dict);
    translateAttributes(dict);
    document.documentElement.setAttribute('lang', lang);
    currentLang = lang;
    localStorage.setItem('cany-lang', lang);
    document.querySelectorAll('.lang-toggle').forEach(updateToggleVisual);
  }

  // Init au chargement DOM
  function init() {
    // Si la langue stockée est EN, on traduit dès le départ
    if (currentLang === 'en') {
      walkAndTranslate(document.body, FR_TO_EN);
      translateAttributes(FR_TO_EN);
      document.documentElement.setAttribute('lang', 'en');
    }
    // Câbler tous les toggles présents (le menu desktop ET mobile partagent la même classe)
    document.querySelectorAll('.lang-toggle').forEach(toggle => {
      updateToggleVisual(toggle);
      toggle.addEventListener('click', function (e) {
        e.preventDefault();
        switchTo(currentLang === 'fr' ? 'en' : 'fr');
      });
    });
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', init);
  } else {
    init();
  }
})();
