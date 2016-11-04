---
title: Wat is Hadoop in de cloud? Inleiding tot HDInsight | Microsoft Docs
description: Wat is Hadoop in de cloud en hoe wordt het beheerd in Microsoft Azure HDInsight? Een inleiding tot Hadoop-onderdelen en big data-analyse.
keywords: big data-analyse, inleiding tot hadoop, wat is hadoop, hadoop in de cloud, hadoop-technologiestack, hadoop-ecosysteem
services: hdinsight
documentationcenter: ''
author: cjgronlund
manager: jhubbard
editor: cgronlun

ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2016
ms.author: cgronlun

---
# Wat is Hadoop in de cloud? Een inleiding tot het Hadoop-ecosysteem in HDInsight
Maak kennis met Hadoop, het bijbehorende ecosysteem en big data in Azure HDInsight. Krijg inzicht in wat Hadoop in HDInsight is en lees meer over de onderdelen van Hadoop, de algemene terminologie en de scenario‘s voor big data-analyse. Bovendien krijgt u informatie over Hadoop-zelfstudies, documentatie en resources voor het gebruik van Hadoop in de cloud in HDInsight.

## Wat is Hadoop in HDInsight?
Azure HDInsight maakt gebruik van de Hadoop-distributie **HDP (Hortonworks Data Platform)**. Met HDInsight kunt u beheerde Apache Hadoop-clusters implementeren en inrichten in de cloud. Dit biedt een softwareframework dat is ontworpen voor het met hoge betrouwbaarheid en beschikbaarheid verwerken, analyseren en rapporteren van big data.  

Hadoop verwijst vaak naar het hele Hadoop-ecosysteem van onderdelen, waaronder Apache HBase, Apache Spark en Apache Storm, en ook andere technologieën die onder de Hadoop-familie vallen. Zie [Overzicht van het Hadoop-ecosysteem in HDInsight](#overview) hieronder voor meer informatie.

## Wat is big data?
Big data kan betrekking hebben op elke willekeurige bulk aan digitale gegevens: van tekst uit Twitter-feeds tot de sensorinformatie van industriële apparatuur, en informatie over surfgedrag van klanten en aankopen op een website. Bij big data kan het gaan om historische gegevens (opgeslagen gegevens), maar ook om realtime gegevens (rechtstreeks gestreamd vanuit de bron). Big data worden verzameld in steeds sneller groeiende volumes en in een steeds groter wordend aantal indelingen.

Als u uit de beschikbare big data informatie of inzichten wilt halen waarop u actie kunt ondernemen, moet u niet alleen relevante gegevens verzamelen en de juiste vragen stellen, maar moeten deze gegevens ook toegankelijk zijn, worden opgeschoond en geanalyseerd, en vervolgens op een nuttige manier worden gepresenteerd. Big data-analyse met Hadoop in HDInsight kan u hierbij helpen.

## <a name="overview"></a>Overzicht van het Hadoop-ecosysteem in HDInsight
HDInsight is een cloudimplementatie van de snelgroeiende Apache Hadoop-technologiestack in Microsoft Azure die dé oplossing vormt voor big data-analyse. HDInsight bevat implementaties van Apache Spark, HBase, Storm, Pig, Hive, Sqoop, Oozie, Ambari, enzovoort. HDInsight kan ook worden geïntegreerd met hulpprogramma's voor Business Intelligence (BI), zoals Power BI, Excel, SQL Server Analysis Services en SQL Server Reporting Services.

### Hadoop, HBase, Spark, Storm en aangepaste clusters
HDInsight biedt clusterconfiguraties voor Apache Hadoop, Spark, HBase en Storm. U kunt bovendien [clusters aanpassen met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).

* **Hadoop** (de werkbelasting Query): biedt betrouwbare gegevensopslag met [HDFS](#hdfs) en een eenvoudig [MapReduce](#mapreduce)-programmeermodel om gegevens parallel te verwerken en te analyseren.
* **<a target="_blank" href="http://spark.apache.org/">Apache Spark</a>**: een framework voor parallelle verwerking dat ondersteuning biedt voor in-memory verwerking om de prestaties van toepassingen voor de analyse van big data te verbeteren. Spark werkt voor SQL, het streamen van gegevens en machine learning. Zie [Overzicht: wat is Apache Spark in HDInsight?](hdinsight-apache-spark-overview.md)
* **<a target="_blank" href="http://hbase.apache.org/">HBase</a>** (de werkbelasting NoSQL): een NoSQL-database gebouwd op Hadoop. Deze biedt willekeurige toegang en sterke consistentie voor grote hoeveelheden (mogelijk miljarden rijen bij miljoenen kolommen) ongestructureerde en semi-gestructureerde gegevens. Zie [Overzicht van HBase in HDInsight](hdinsight-hbase-overview.md).
* **<a  target="_blank" href="https://storm.incubator.apache.org/">Apache Storm</a>** (de werkbelasting Stream): een gedistribueerd, realtime berekeningssysteem voor het snel verwerken van grote gegevensstromen. Storm wordt aangeboden als beheerd cluster in HDInsight. Zie [Realtime-sensorgegevens analyseren met Storm en Hadoop](hdinsight-storm-sensor-data-analysis.md).

### Voorbeeld van aanpassingsscripts
Scriptacties zijn scripts die worden uitgevoerd tijdens de clusterinrichting. Ze kunnen worden gebruikt om op het cluster extra onderdelen te installeren. In het geval van op Linux gebaseerde clusters zijn dit Bash-scripts.

Het HDInsight-team biedt de volgende voorbeeldscripts:

* [Hue](hdinsight-hadoop-hue-linux.md): een reeks web-apps die worden gebruikt voor interactie met een cluster. Alleen voor Linux-clusters.
* [Giraph](hdinsight-hadoop-giraph-install-linux.md): grafiekverwerking om relaties tussen items of personen te visualiseren.
* [R](hdinsight-hadoop-r-scripts-linux.md): een open source-taal en -omgeving voor statistische computing gebruikt in machine learning.
* [Solr](hdinsight-hadoop-solr-install-linux.md): een bedrijfszoekplatform dat zoeken naar volledige tekst in gegevens mogelijk maakt.

Zie [Ontwikkeling van scriptacties met HDInsight](hdinsight-hadoop-script-actions-linux.md) voor informatie over het ontwikkelen van uw eigen scriptacties.

## Wat zijn de onderdelen en hulpprogramma‘s van Hadoop?
De volgende onderdelen en hulpprogramma's zijn opgenomen in de HDInsight-clusters.

* **[Ambari](#ambari)**: inrichting, beheer, controle en hulpprogramma's voor clusters.
* **[Avro](#avro)** (Microsoft .NET-bibliotheek voor Avro): serialisatie van gegevens voor de Microsoft .NET-omgeving.
* **[Hive & HCatalog](#hive)**: uitvoeren van query‘s op basis van SQL (Structured Query Language), en een beheerlaag voor tabellen en opslag.
* **[Mahout](#mahout)**: machine learning.
* **[MapReduce](#mapreduce)**: een ouder framework voor Hadoop, gedistribueerde verwerking en resourcebeheer. Zie [YARN](#yarn), het nieuwste resourceframework.
* **[Oozie](#oozie)**: werkstroombeheer.
* **[Phoenix](#phoenix)**: relationele databaselaag over HBase.
* **[Pig](#pig)**: eenvoudiger scripts uitvoeren voor MapReduce-transformaties.
* **[Sqoop](#sqoop)**: gegevens importeren en exporteren.
* **[Tez](#tez)**: maakt het mogelijk om efficiënt gegevensintensieve processen op schaal uit te voeren.
* **[YARN](#yarn)**: deel van de kernbibliotheek van Hadoop en de volgende generatie MapReduce-softwareframework.
* **[ZooKeeper](#zookeeper)**: coördinatie van de processen in gedistribueerde systemen.

> [!NOTE]
> Zie voor meer informatie over de specifieke componenten en versie-informatie [Hadoop components, versioning, and service offerings in HDInsight (Hadoop-onderdelen, versiebeheer en serviceaanbiedingen in HDInsight)][versiebeheer voor onderdelen]
> 
> 

### <a name="ambari"></a>Ambari
Apache Ambari is bedoeld voor het inrichten, beheren en controleren van Apache Hadoop-clusters. Het bevat een intuïtieve verzameling hulpprogramma‘s voor operators en een krachtige reeks API‘s die de complexiteit van Hadoop verbergen en de werking van clusters vereenvoudigen. Op Linux gebaseerde HDInsight-clusters bieden zowel de Ambari-webgebruikersinterface als de Ambari REST API, terwijl op Windows gebaseerde clusters een subset van de REST API bieden. Ambari-weergaven op HDInsight-clusters bieden interfacemogelijkheden voor invoegtoepassingen.

Zie [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md) (alleen voor Linux), [Hadoop-clusters in HDInsight beheren met de Ambari-API](hdinsight-monitor-use-ambari-api.md) en <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Informatie over de Apache Ambari-API</a>.

### <a name="avro"></a>Avro (Microsoft .NET-bibliotheek voor Avro)
De Microsoft .NET-bibliotheek voor Avro implementeert de DIF-indeling van Apache Avro voor compacte binaire gegevens voor serialisatie in de Microsoft .NET-omgeving. De bibliotheek maakt gebruik van <a target="_blank" href="http://www.json.org/">JSON (JavaScript Object Notation)</a> om een schema voor taalherkenning te definiëren dat de interoperabiliteit van talen waarborgt. Dit betekent dat gegevens die zijn geserialiseerd in één taal, kunnen worden gelezen in een andere. Gedetailleerde informatie over deze indeling vindt u in de <a target=_"blank" href="http://avro.apache.org/docs/current/spec.html">Apache Avro-specificatie</a>.
De Avro-bestandsindeling biedt ondersteuning voor het gedistribueerde MapReduce-programmeermodel. Bestanden zijn splitsbaar. Dit betekent dat elk punt in een bestand kan worden gevonden en dat u vanaf een bepaald blok kunt beginnen met lezen. Zie [Gegevens serialiseren met de Microsoft .NET-bibliotheek voor Avro](hdinsight-dotnet-avro-serialization.md) voor informatie over hoe dit in zijn werk gaat.

### <a name="hdfs"></a>HDFS
Hadoop Distributed File System (HDFS) is een gedistribueerd bestandssysteem dat samen met MapReduce en YARN de kern vormt van het Hadoop-ecosysteem. HDFS is het standaardbestandssysteem voor Hadoop-clusters op HDInsight.

### <a name="hive"></a>Hive & HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> is datawarehousesoftware die is gebouwd op Hadoop. Hiermee kunt u grote gegevenssets in gedistribueerde opslag doorzoeken en beheren door gebruik te maken van een taal genaamd HiveQL (vergelijkbaar met SQL). Hive is, net zoals Pig, een abstractie die is gebouwd op MapReduce. Wanneer Hive wordt uitgevoerd, vertaalt het query‘s naar een reeks MapReduce-taken. Uit conceptueel oogpunt staat Hive dichter bij een relationeel databasebeheersysteem dan Pig. Daarom is het met name geschikt voor gebruik met meer gestructureerde gegevens. Voor ongestructureerde gegevens kunt u beter Pig gebruiken. Zie [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> is een tabel- en opslagbeheerlaag voor Hadoop die gebruikers een relationele weergave van gegevens biedt. In HCatalog kunt u lees- en schrijfbewerkingen uitvoeren in bestanden in elke indeling waarvoor een Hive SerDe-schrijfbewerking (serializer-deserializer) kan worden uitgevoerd.

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> is een schaalbare bibliotheek met machine learning-algoritmen die worden uitgevoerd op Hadoop. Machine learning-toepassingen maken gebruik van statistieken om systemen te laten leren van gegevens en om resultaten uit het verleden te gebruiken om toekomstig gedrag te voorspellen. Zie [Filmaanbevelingen genereren met Mahout op Hadoop](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce is het oudere softwareframework voor Hadoop voor schrijftoepassingen waarmee big data in batches parallel kan worden verwerkt. Met een MapReduce-taak worden grote gegevenssets gesplitst en worden de gegevens voor verwerking georganiseerd in sleutel-/waardeparen.

[YARN](#yarn) is het nieuwste resourceframework voor beheerders en toepassingen, en wordt ook wel MapReduce 2.0 genoemd. MapReduce-taken worden uitgevoerd op YARN.

Zie <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> in de Hadoop-wiki voor meer informatie over MapReduce.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> is een coördinatiesysteem voor werkstromen waarmee Hadoop-taken worden beheerd. Het is geïntegreerd met de Hadoop-stack en biedt ondersteuning voor Hadoop-taken voor MapReduce, Pig, Hive en Sqoop. Oozie kan ook worden gebruikt voor het plannen van taken die specifiek zijn voor een systeem, zoals Java-programma's of shell-scripts. Zie [Use Oozie with Hadoop](hdinsight-use-oozie.md) (Oozie gebruiken met Hadoop).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> is een relationele databaselaag over HBase. Phoenix bevat een JDBC-stuurprogramma waarmee gebruikers rechtstreeks SQL-tabellen kunnen doorzoeken en beheren. Phoenix vertaalt query‘s en andere instructies naar systeemeigen NoSQL API-aanroepen (in plaats van gebruik te maken van MapReduce). Hierdoor worden snellere toepassingen mogelijk die zijn gebouwd op NoSQL-opslag. Zie [Apache Phoenix en SQuirreL gebruiken met HBase-clusters](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> is een platform van hoog niveau waarmee u complexe MapReduce-transformaties kunt uitvoeren op zeer grote gegevenssets door gebruik te maken van een eenvoudige scripttaal genaamd Pig Latin. Pig vertaalt de Pig Latin-scripts, zodat ze kunnen worden uitgevoerd in Hadoop. U kunt door de gebruiker gedefinieerde functies (UDF's) maken om Pig Latin uit te breiden. Zie [Use Pig with Hadoop](hdinsight-use-pig.md) (Pig gebruiken met Hadoop).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> is een hulpprogramma waarmee zo efficiënt mogelijk bulksgewijs gegevens kunnen worden overgebracht tussen Hadoop en relationele databases, zoals SQL of andere gestructureerde gegevensopslag. Zie [Sqoop gebruiken met Hadoop](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> is een toepassingsframework dat is gebouwd op Hadoop YARN. Hiermee kunnen complexe, acyclische grafieken voor algemene gegevensverwerking worden uitgevoerd. Tez is een flexibelere en krachtigere opvolger van het MapReduce-framework die ervoor zorgt dat gegevensintensieve processen, zoals Hive, efficiënter op schaal worden uitgevoerd. Zie [het gedeelte 'Apache Tez gebruiken voor verbeterde prestaties' in het artikel 'Hive en HiveQL gebruiken'](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache YARN is de volgende generatie van MapReduce (MapReduce 2.0 of MRv2) en biedt ondersteuning voor uitgebreidere scenario‘s voor gegevensverwerking dan MapReduce, met grotere schaalbaarheid en realtime verwerking. YARN biedt resourcebeheer en een gedistribueerd toepassingsframework. MapReduce-taken worden uitgevoerd op YARN.

Zie <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a> voor meer informatie over YARN.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> coördineert processen in grote gedistribueerde systemen met behulp van een gedeelde hiërarchische naamruimte met gegevensregisters (znodes). Znodes bevatten kleine hoeveelheden metagegevens die nodig zijn voor het coördineren van processen: status, locatie, configuratie enzovoort.

## Programmeertalen in HDInsight
HDInsight-clusters (Hadoop-, HBase-, Storm- en Spark-clusters) bieden ondersteuning voor een aantal programmeertalen, maar sommige hiervan zijn niet standaard geïnstalleerd. Gebruik voor bibliotheken, modules en pakketten die niet standaard zijn geïnstalleerd, een scriptactie om het betreffende onderdeel te installeren. Zie [Scriptactieontwikkeling met HDInsight](hdinsight-hadoop-script-actions-linux.md).

### Standaardondersteuning voor programmeertalen
Standaard bieden HDInsight-clusters ondersteuning voor:

* Java
* Python

Extra talen kunnen worden geïnstalleerd met behulp van scriptacties: [Scriptactieontwikkeling met HDInsight](hdinsight-hadoop-script-actions-linux.md).

### JVM-talen (Java Virtual Machine)
Naast Java kunnen met behulp van een Java Virtual Machine (JVM) ook veel andere talen worden uitgevoerd. Voor het uitvoeren van sommige talen kan echter zijn vereist dat er op het cluster extra onderdelen worden geïnstalleerd.

De volgende JVM-talen worden op HDInsight-clusters ondersteund: 

* Clojure
* Jython (Python voor Java)
* Scala

### Hadoop-specifieke talen
HDInsight-clusters bieden ondersteuning voor de volgende talen die specifiek zijn voor het Hadoop-ecosysteem:

* Pig Latin voor Pig-taken
* HiveQL voor Hive-taken en SparkSQL

## <a name="advantage"></a>Voordelen van Hadoop in de cloud
Als onderdeel van het Azure-cloudecosysteem biedt Hadoop in HDInsight een aantal voordelen, waaronder:

* Automatische inrichting van Hadoop-clusters. HDInsight-clusters zijn veel gemakkelijker te maken dan handmatig geconfigureerde Hadoop-clusters. Zie [Hadoop-clusters inrichten in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie.
* Geavanceerde Hadoop-onderdelen. Zie [Hadoop components, versioning, and service offerings in HDInsight (Hadoop-onderdelen, versiebeheer en serviceaanbiedingen in HDInsight)][versiebeheer voor onderdelen] voor meer informatie.
* Hoge beschikbaarheid en betrouwbaarheid van clusters. Zie [Beschikbaarheid en betrouwbaarheid van Hadoop-clusters in HDInsight](hdinsight-high-availability-linux.md) voor meer informatie.
* Efficiënte en voordelige gegevensopslag met Azure Blob Storage, een optie die compatibel is met Hadoop. Zie [Azure Blob Storage met Hadoop gebruiken in HDInsight](hdinsight-hadoop-use-blob-storage.md) voor meer informatie.
* Integratie met andere Azure-services, waaronder [web-apps](https://azure.microsoft.com/documentation/services/app-service/web/) en [SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).
* Aanvullende VM-grootten en -typen voor het uitvoeren van HDInsight-clusters. Zie [Hadoop components, versioning, and service offerings in HDInsight (Hadoop-onderdelen, versiebeheer en serviceaanbiedingen in HDInsight)][versiebeheer voor onderdelen] voor meer informatie.
* Clusterschaling. Met clusterschaling kunt u het aantal knooppunten van een actief HDInsight-cluster wijzigen zonder dat u het cluster hoeft te verwijderen of opnieuw hoeft te maken.
* Ondersteuning voor Virtual Network. HDInsight-clusters kunnen worden gebruikt met Azure Virtual Network ter ondersteuning van de isolatie van cloudresources of hybride scenario's die cloudresources koppelen aan de resources in uw datacenter.
* Lage instapkosten. Start een [gratis proefversie](https://azure.microsoft.com/free/) of raadpleeg de [prijsgegevens voor HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Zie de [pagina met Azure-functies voor HDInsight][marketingpagina] voor meer informatie over de voordelen van Hadoop in HDInsight.

## HDInsight Standard en HDInsight Premium
HDInsight heeft twee categorieën aanbiedingen voor big data-clouds: Standard en Premium. HDInsight Standard biedt een bedrijfscluster dat organisaties kunnen gebruiken om hun big data-werkbelastingen uit te voeren. HDInsight Premium bouwt hierop voort en biedt geavanceerde mogelijkheden voor analyse en beveiliging voor een HDInsight-cluster. Zie [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium) voor meer informatie.

## <a id="resources"></a>Resources voor meer informatie over big data-analyse, Hadoop en HDInsight
Bouw voort op deze inleiding tot Hadoop in de cloud en big data-analyse met onderstaande resources.

### Hadoop-documentatie voor HDInsight
* [HDInsight-documentatie](https://azure.microsoft.com/documentation/services/hdinsight/): de documentatiepagina voor Hadoop op Azure HDInsight met koppelingen naar artikelen, video‘s en aanvullende resources.
* [Aan de slag met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): een Snel starten-zelfstudie voor het inrichten van HDInsight Hadoop-clusters en het uitvoeren van Hive-voorbeeldquery‘s.
* [Aan de slag met Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md): een Snel starten-zelfstudie voor het maken van een Spark-cluster en het uitvoeren van interactieve Spark SQL-query's.
* [R Server gebruiken op HDInsight](hdinsight-hadoop-r-server-get-started.md): informatie over het gebruik van R Server in HDInsight Premium.
* [HDInsight-clusters inrichten](hdinsight-hadoop-provision-linux-clusters.md): informatie over het inrichten van een HDInsight Hadoop-cluster via Azure Portal, Azure CLI of Azure PowerShell.

### Apache Hadoop
* <a target="_blank" href="http://hadoop.apache.org/">Apache Hadoop</a>: meer informatie over de Apache Hadoop-softwarebibliotheek, een framework dat gedistribueerde verwerking van grote gegevenssets tussen verschillende clusters computers mogelijk maakt.
* <a target="_blank" href="http://hadoop.apache.org/docs/r1.0.4/hdfs_design.html">HDFS</a>: meer informatie over de architectuur en het ontwerp van Hadoop Distributed File System, het primaire opslagsysteem dat wordt gebruikt voor Hadoop-toepassingen.
* <a target="_blank" href="http://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html">MapReduce-zelfstudie</a>: meer informatie over het programmeerframework voor het schrijven van Hadoop-toepassingen, waarmee razendsnel grote hoeveelheden gegevens parallel kunnen worden verwerkt op grote clusters rekenknooppunten.

### Microsoft Business Intelligence
Indien deze zijn geïntegreerd met HDInsight, kunt u met de vertrouwde hulpprogramma‘s voor Business Intelligence (BI), zoals Excel, PowerPivot, en SQL Server Analysis Services, gegevens ophalen, analyseren en rapporteren door de invoegtoepassing Power Query of het stuurprogramma Microsoft Hive ODBC te gebruiken.

Deze BI-hulpprogramma's kunnen u helpen met big data-analyse:

* [Excel en Hadoop koppelen met Power Query](hdinsight-connect-excel-power-query.md): informatie over hoe u met behulp van Microsoft Power Query voor Excel verbinding maakt tussen Excel en het Azure Storage-account dat de gegevens bevat die zijn gekoppeld aan het HDInsight-cluster. Windows-werkstation is vereist. Werkt met Windows - of Linux-gebaseerd cluster.
* [Excel en Hadoop koppelen met het stuurprogramma Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md): informatie over hoe u gegevens importeert uit HDInsight met behulp van het stuurprogramma Microsoft Hive ODBC. Windows-werkstation is vereist. Werkt met Windows - of Linux-gebaseerd cluster.
* [Microsoft-cloudplatform](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): informatie over Power BI voor Office 365, het downloaden van de proefversie van SQL Server, en het instellen van SharePoint Server 2013 en SQL Server BI.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx).
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx).

[marketingpagina]: https://azure.microsoft.com/services/hdinsight/
[versiebeheer voor onderdelen]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/



<!--HONumber=Oct16_HO1-->


