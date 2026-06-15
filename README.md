
## Le Calculateur d’agrégats sur mesure de l’IPC
- Il s'agit d'une application interactive qui permet aux utilisateurs des données de Statistique Canada de sélectionner des zones géographiques et des produits de l'IPC publiés, puis de calculer des indices sur mésure sous forme d'agrégats des séries choisies ou de l'indice global, à l'exclusion des éléments sélectionnés.
- Les résultats sont présentés sous forme de graphiques et de tableaux, sous forme de variations en pourcentage, de niveaux d'indice ou de contributions à la variation en pourcentage de l'indice global.


## Télécharger et exécuter l'application dans R
Vous pouvez télécharger le code R depuis GitHub et l'exécuter sur votre appareil à l'aide du code R suivant :
- shiny::runGitHub("Calculateur-agregats-sur-mesure-IPC", "CPICustomAggCalcAggSurMesureIPC")
- Si cette méthode échoue, essayez de suivre les instructions disponibles à l'adresse https://docs.github.com/en/get-started/start-your-journey/downloading-files-from-github.
    - Dans votre navigateur, entrez l'URL du dépôt GitHub : https://github.com/CPICustomAggCalcAggSurMesureIPC/Calculateur-agregats-sur-mesure-IPC
	- Dans le menu déroulant du bouton Code, sélectionnez << Download ZIP >>
    - Accédez au fichier .zip téléchargé, puis copiez le répertoire à un autre emplacement sur votre appareil
    - Ouvrez le répertoire que vous venez de copier et qui contient la version française
    - Exécutez le fichier app.r
- Conditions préalables :
    - R doit être installé sur votre appareil
    - Un écran d'au moins 1 140 pixels de large
    - Environ 500 Mo de mémoire vive

## Utilizer le Calculateur d’agrégats sur mesure de l’IPC
- Instructions en français: https://github.com/CPICustomAggCalcAggSurMesureIPC/Calculateur-agregats-sur-mesure-IPC/blob/main/man/Comment_utiliser_le_calculateur_dagregats_sur_mesure_de_lIPC.docx

## Développement :
- Gerry O'Donnell, Analyste principal des prix à la consommation, Division des prix à la consommation, Statistique Canada, gerry.odonnell@statcan.gc.ca
- Merci également à  
    - Taylor Mitchell et son équipe pour leur aide à la diffusion
    - Zack Lansfield et Vishal Sood pour leur aide pour l'empaquetage du code et à l'accessibilité
    - Clément Yélou pour son aide concernant les formules et la traduction
    - Chris Bazos pour son aide aux tests
    - Zack Glazier et Lance Taylor pour la révision du code
    - de nombreuses autres personnes pour leurs suggestions sur la conception
	
## Fonctionnement :
- Le téléchargement du code dans R lance le fichier \\app.R, qui...
    - Si nécessaire, installe les paquets et les charge dans la session
    - Définit la langue sur le français
    - Contient plusieurs fonctions à usage interne uniquement
        - fPeriodSeq190001 convertit une date sous forme de chaîne de caractères (« aaaa-mm-jj ») en un mois dans une séquence commençant en janvier 1900
        - fRefDate convertit un mois dans la séquence commençant en janvier 1900 en une date sous forme de chaîne de caractères (« aaaa-mm-jj »)
        - fRoundHAFZ utilise un arrondi flou à mi-chemin de zéro au nombre de chiffres spécifié
        - fGetEnFrText récupère le texte en anglais ou en français pour un objet de l'interface utilisateur
        - fGetVarNameFromEnFrText récupère le nom d'un objet de l'interface utilisateur à partir d'un texte en anglais ou en français
        - fIndexWeightChgCont accepte la série sélectionnée, les périodes de début et de fin de base, ainsi que les indices et les pondérations CODR, puis calcule et renvoie des valeurs agrégées personnalisées et un message d'état  
        - fGetDisplaySeries accepte une série composante et renvoie les séries disponibles restantes
        - fPlotTimeSeries accepte les données pour les séries disponibles, renvoie un graphique Plotly
        - fMessage écrit un message dans la console par bloc de code
    - Lit les métadonnées dans data-raw\Data_for_R_Shiny.xlsx nécessaires pour initialiser l'application avec des données spécifiant ...
        - Dates d'entrée en vigueur des paniers de l'IPC
        - Identificateurs de séries des tableaux CODR 18100004 et 18100007
        - Définitions d'agrégations populaires et séries de composantes
        - Texte en anglais et en français pour les composants de l'interface utilisateur
    - Crée des variables globales
    - Définit des fonctions réutilisables liées à l'interface utilisateur
    - Définit la fonction ui, qui crée et positionne des objets d'interface utilisateur et crée des fonctions JavaScript
    - Définit la fonction server, qui reçoit les entrées de l'utilisateur, récupère les données CODR et affiche les résultats
    - Appelle shinyApp(ui, server)
