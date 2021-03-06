---
title: Overzicht van Azure Notebooks | Microsoft Docs
description: Jupyter Notebooks in de cloud uitvoeren met behulp van de gratis Azure Notebooks-service.
services: app-service
documentationcenter: ''
author: kraigb
manager: douge
ms.assetid: 9cea5a8e-c52d-4bdc-9e4a-cecdc1ad02c1
ms.service: notebooks
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 12/04/2018
ms.author: kraigb
ms.openlocfilehash: a84f71c2656c73867ee076d4b993026558a0a504
ms.sourcegitcommit: 11d8ce8cd720a1ec6ca130e118489c6459e04114
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52853362"
---
# <a name="overview-of-azure-notebooks"></a>Overzicht van Azure Notebooks

Azure Notebooks is een gratis gehoste service om Jupyter-notebooks te ontwikkelen en uitvoeren in de cloud, zonder installatie. [Jupyter](http://jupyter.org/) (voorheen IPython) is een opensourceproject waarmee u eenvoudig Markdown-tekst, uitvoerbare code en permanente gegevens, afbeeldingen en visualisaties kunt combineren op één deelbaar canvas, het *notebook* (de afbeelding is ter beschikking gesteld door jupyter.org):

[![](http://jupyter.org/assets/jupyterpreview.png "Jupyter Notebooks")](http://jupyter.org/assets/jupyterpreview.png#lightbox)

Vanwege deze krachtige combinatie van code, afbeeldingen en verklarende tekst is Jupyter populair geworden voor vele toepassingen, waaronder onderwijs in datawetenschap, het opschonen en transformeren van gegevens, numerieke simulatie, statistisch modelleren en de ontwikkeling van modellen voor machine learning.

## <a name="hassle-free-experience"></a>Probleemloze ervaring

Met Azure Notebooks kunt u snel aan de slag met prototyping, datawetenschap, academisch onderzoek of leren programmeren in Python:

- Een datawetenschapper heeft onmiddellijk toegang tot een volledige Anaconda-omgeving zonder dat er installatie nodig is.
- Een docent kan studenten of leerlingen een probleemloze Python-omgeving bieden.
- Een presentator kan een lezing of webinar geven zonder dat de deelnemers 45 minuten bezig zijn om software te installeren.
- Een ontwikkelaar of hobbyist kan Notebooks gebruiken als een kladblok voor snelle code.

Notebooks worden nog krachtiger als personen ermee kunnen samenwerken via een cloudservice als Azure Notebooks die via een browser kan worden geopend (in preview). In de cloud hoeven gebruikers Jupyter niet lokaal te installeren of zich bezig te houden met het onderhouden van een omgeving. Dankzij de cloud kunt u eenvoudig notebooks (en de eraan gekoppelde gegevensbestanden) delen met andere geautoriseerde gebruikers, waarmee u het probleem omzeilt van het delen van notebooks via externe programma’s, zoals opslagplaatsen voor broncode. Met Azure Notebooks kunnen gebruikers ook notebooks naar hun eigen account kopiëren (of klonen) om ze te wijzigen of om ermee te experimenteren. Dit is met name handig voor onderwijsdoeleinden.

Azure Notebooks is een algemeen platform voor coderen, uitvoeren en delen. Daarom kunt u het in verschillende scenario’s gebruiken:

- Een nieuwe programmeertaal leren: probeer een van de [zelfstudies op de voorpagina](https://notebooks.azure.com/Microsoft/projects/samples/html/Introduction%20to%20Python.ipynb)
- Datawetenschap leren: probeer [het boek van Jake Vanderplas](https://notebooks.azure.com/jakevdp/projects/PythonDataScienceHandbook)
- [Een cursus geven](https://notebooks.azure.com/garth-wells/projects/CUED-IA-Computing-Michaelmas) aan honderden leerlingen of studenten
- Online of tijdens een conferentie een webinar geven zonder tijd te verdoen met een installatie 
- GitHub-gebruikers in staat stellen notebooks rechtstreeks te laden en uitvoeren door [een GitHub-startbadge te maken](https://notebooks.azure.com/help/projects/sharing/create-a-github-badge)
- [PowerPoint-achtige diavoorstellingen](https://notebooks.azure.com/help/jupyter-notebooks/slides) geven waarbij de code op de dia’s uitvoerbaar is.

Kortom, met Azure Notebooks kunt u uw werk efficiënter uitvoeren en dus meer voor elkaar krijgen.

> [!Note]
> U vindt meer informatie over Jupyter op [jupyter.org](http://jupyter.org/) en in de [Jupyter-documentatie](http://jupyter-notebook.readthedocs.io/en/latest/).

## <a name="pricing-and-quotas"></a>Prijzen en quota

Azure Notebooks is een gratis service, maar elk project heeft een beperkt geheugen (4 GB) en een beperkte hoeveelheid gegevens (1 GB) om misbruik te voorkomen. Legitieme gebruikers die deze quota overschrijden, krijgen een captcha aangeboden als ze notebooks willen blijven gebruiken.

Als u alle beperkingen wilt opheffen, koppelt u uw account aan een Azure-abonnement, waarna u Premium-rekenlagen kunt selecteren.

## <a name="available-kernels-and-environments"></a>Beschikbare kernels en omgevingen

Voor elke notebook selecteert u de kernel (d.w.z. de runtime-omgeving) waarin de codecellen worden uitgevoerd. Azure Notebooks biedt ondersteuning voor de volgende kernels:

- Python 2.7 + Anaconda2-5.3.0
- Python 3.6 + Anaconda3-5.3.0
- Python 3.5 + Anaconda3-4.2.0 (wordt afgeschaft)
- R 3.3 + Microsoft R Open 3.3.0
- F# 4.1.9

Azure Notebooks bevat naast de basisdistributies tevens extra pakketten. De Python-kernels bijvoorbeeld, omvatten de numpy-, pandas-, scikit-learn-, matplotlib- en bokeh-bibliotheken.

U kunt een project ook aanpassen om een omgeving te maken voor alle notebooks in dat project. Zie [Quickstart: Een project met een aangepaste omgeving maken](quickstart-create-jupyter-notebook-project-environment.md) voor meer informatie.

Naast de basisdistributies zijn in Azure Notebooks vele extra pakketten vooraf geïnstalleerd die handig zijn van datawetenschappers. U kunt ook uw eigen pakketten installeren met behulp van het voor elke taal eigen proces.

## <a name="pre-configured-jupyter-extensions"></a>Vooraf geconfigureerde Jupyter-uitbreidingen

Azure Notebooks is vooraf geconfigureerd met de volgende Jupyter-uitbreidingen:

- [RISE](https://github.com/damianavila/RISE): een Jupyter-uitbreiding voor diavoorstellingen (ook wel live_reveal genoemd). Zie [Een diavoorstelling uitvoeren](present-jupyter-notebooks-slideshow.md) voor meer informatie.
- [JupyterLab](https://github.com/jupyterlab/jupyterlab): een volledige rekenomgeving om te werken met Jupyter Notebooks.
- [Altair](https://github.com/ellisonbg/altair): een declaratieve, statistische visualisatiebibliotheek voor Python.
- [BQPlot](https://github.com/bloomberg/bqplot): een interactief tekenframework voor Jupyter Notebooks.
- [IpyWidgets](https://github.com/jupyter-widgets/ipywidgets): interactieve HTML-widgets voor Jupyter Notebooks.

## <a name="issues-and-getting-help"></a>Problemen en Help

Omdat Azure Notebooks nog in de preview-fase is, kan het voorkomen dat de service af en toe uitvalt. Deze kunnen vaker voorkomen of van langere duur zijn dan bij andere Azure-services. Sommige functies kunnen onvolledig zijn of fouten bevatten.

Momenteel wordt u aangeraden Azure Notebooks Preview niet te gebruiken voor bedrijfskritische toepassingen of gevoelige notebooks en gegevens.

Voor vragen over Azure Notebooks kunt u een vraag stellen op de [GitHub-opslagplaats](https://github.com/Microsoft/AzureNotebooks/issues).

## <a name="next-steps"></a>Volgende stappen  

- [Voorbeelden van notebooks verkennen](azure-notebooks-samples.md)

- Quickstarts:

  - [Een notebook maken en delen](quickstart-create-share-jupyter-notebook.md)
  - [Een notebook klonen](quickstart-clone-jupyter-notebook.md)
  - [Een lokaal Jupyter-notebook migreren](quickstart-migrate-local-jupyter-notebook.md)
  - [Een aangepaste omgeving gebruiken](quickstart-create-jupyter-notebook-project-environment.md)
  - [Aanmelden en een gebruikers-id instellen](quickstart-sign-in-azure-notebooks.md)

- Zelfstudies:

  - [Een notebook maken en uitvoeren](tutorial-create-run-jupyter-notebook.md  )

- Artikelen met procedures:
  
  - [Projecten maken en klonen](create-clone-jupyter-notebooks.md)
  - [Projecten configureren en beheren](configure-manage-azure-notebooks-projects.md)
  - [Pakketten vanuit een notebook installeren](install-packages-jupyter-notebook.md)
  - [Een diavoorstelling presenteren](present-jupyter-notebooks-slideshow.md)
  - [Werken met gegevensbestanden](work-with-project-data-files.md)
  - [Toegang tot gegevensbronnen](access-data-resources-jupyter-notebooks.md)
  - [Azure Machine Learning Services gebruiken](use-machine-learning-services-jupyter-notebooks.md)
