---
title: Gegevens wetenschappelijke virtuele Machine ontwikkelingsprogramma's - Azure | Microsoft Docs
description: Gegevens wetenschappelijke virtuele machine ontwikkelingsprogramma's.
keywords: hulpmiddelen voor wetenschappelijke gegevens, gegevens wetenschappelijke virtuele machine, hulpprogramma's voor gegevenswetenschap, gegevenswetenschap linux
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 6aef0fbe44e19b515c2bc10c0e7c38fabac10dae
ms.sourcegitcommit: d1f35f71e6b1cbeee79b06bfc3a7d0914ac57275
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/22/2018
---
# <a name="development-tools-on-the-data-science-virtual-machine"></a>Ontwikkelingsprogramma's op de gegevens wetenschappelijke virtuele Machine

De gegevens wetenschappelijke virtuele Machine (DSVM) biedt een productieve omgeving voor het ontwikkelen van uw door diverse populaire hulpmiddelen en IDE bundeling. Hier volgen een aantal hulpprogramma's die beschikbaar zijn op de DSVM. 

## <a name="visual-studio-2017"></a>Visual Studio 2017  
|    |           |
| ------------- | ------------- |
| Wat is het?   | Algemeen IDE      |
| Ondersteunde DSVM versies      | Windows      |
| Doorgaans worden gebruikt      | Softwareontwikkeling    |
| Hoe wordt deze geconfigureerd / geïnstalleerd op de DSVM?      | Gegevens wetenschappelijke werkbelasting (extra Python en R), Azure-workload (Hadoop, Data Lake), Node.js, SQL Server-hulpprogramma 's    |
| Hoe gebruik / uitvoeren?      | Snelkoppeling op het bureaublad (`C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv.exe`)    |
| Bijbehorende hulpprogramma's op de DSVM      |     Visual Studio Code, RStudio, Juno  |

## <a name="visual-studio-code"></a>Visual Studio Code 
|    |           |
| ------------- | ------------- |
| Wat is het?   | Algemeen IDE      |
| Ondersteunde DSVM versies      | Windows, Linux     |
| Doorgaans worden gebruikt      | Code-editor en Git-integratie   |
| Hoe gebruik / uitvoeren?      | Snelkoppeling op het bureaublad (`C:\Program Files (x86)\Microsoft VS Code\Code.exe`) in Windows, snelkoppeling op het bureaublad of terminal (`code`) in Linux    |
| Bijbehorende hulpprogramma's op de DSVM      |     Visual Studio 2017, RStudio, Juno  |

## <a name="rstudio--desktop"></a>RStudio bureaublad 
|    |           |
| ------------- | ------------- |
| Wat is het?   | Client IDE voor R    |
| Ondersteunde DSVM versies      | Windows, Linux      |
| Doorgaans worden gebruikt      |  R-ontwikkeling     |
| Hoe gebruik / uitvoeren?      | Snelkoppeling op het bureaublad (`C:\Program Files\RStudio\bin\rstudio.exe`) in Windows, snelkoppeling op het bureaublad (`/usr/bin/rstudio`) op Linux      |
| Bijbehorende hulpprogramma's op de DSVM      |   Visual Studio 2017, Visual Studio Code, Juno      |

## <a name="rstudio--server"></a>RStudio  Server 
|    |           |
| ------------- | ------------- |
| Wat is het?   | Web-based IDE voor R    |
| Ondersteunde DSVM versies      | Linux      |
| Doorgaans worden gebruikt      |  R-ontwikkeling     |
| Hoe gebruik / uitvoeren?      | Schakel de service met _systemctl rstudio-server inschakelen_, start de service met _systemctl rstudio-server starten_. U kunt vervolgens aanmelden bij de RStudio Server op http://your-vm-ip:8787.       |
| Bijbehorende hulpprogramma's op de DSVM      |   Visual Studio 2017, Visual Studio Code, RStudio bureaublad      |

## <a name="juno"></a>Juno 
|    |           |
| ------------- | ------------- |
| Wat is het?   | IDE-client voor Julia taal   |
| Ondersteunde DSVM versies      | Windows, Linux      |
| Doorgaans worden gebruikt      |  Julia-ontwikkeling     |
| Hoe gebruik / uitvoeren?      | Snelkoppeling op het bureaublad (`C:\JuliaPro-0.5.1.1\Juno.bat`) in Windows, snelkoppeling op het bureaublad (`/opt/JuliaPro-VERSION/Juno`) op Linux      |
| Bijbehorende hulpprogramma's op de DSVM      |   Visual Studio 2017, Visual Studio Code, RStudio      |

## <a name="pycharm"></a>Pycharm
|    |           |
| ------------- | ------------- |
| Wat is het?   | IDE-client voor Python taal    |
| Ondersteunde DSVM versies      | Linux      |
| Doorgaans worden gebruikt      |  R-ontwikkeling     |
| Hoe gebruik / uitvoeren?      | Snelkoppeling op het bureaublad (`/usr/bin/pycharm`) op Linux      |
| Bijbehorende hulpprogramma's op de DSVM      |   Visual Studio 2017, Visual Studio Code, RStudio      |



## <a name="powerbi-desktop"></a>PowerBI Desktop 
|    |           |
| ------------- | ------------- |
| Wat is het?   | Interactieve gegevensvisualisatie en BI-hulpprogramma    |
| Ondersteunde DSVM versies      | Windows  |
| Doorgaans worden gebruikt      |  Gegevensvisualisatie en het bouwen van Dashboards   |
| Hoe gebruik / uitvoeren?      | Snelkoppeling op het bureaublad (`C:\Program Files\Microsoft Power BI Desktop\bin\PBIDesktop.exe`)      |
| Bijbehorende hulpprogramma's op de DSVM      |   Visual Studio 2017, Visual Studio Code, Juno      |

