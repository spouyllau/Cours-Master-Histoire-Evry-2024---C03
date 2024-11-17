# Sciences humaines, sciences sociales à l'ère numérique : la mise en données et méthodes de modélisation des connaissances

Exemple du cours. On regarde et on analyse de l'information scientifique structurée en : 
- [x] CSV (Données tabulaires)
- [x] XML-TEI (Langage de balises)
- [x] SQL (modèle relationnel)
- [x] RDF (modèle de graphe)

## CSV

Voici un exemple de fichier CSV représentant des données structurées. Le fichier CSV contiendra des informations sur les chapitres et les paragraphes d'un document.

### Exemple de fichier CSV

```csv
Chapter,Paragraph,Content
1,1,"This is the first paragraph of the first chapter. It provides an introduction to the topic."
1,2,"This is the second paragraph of the first chapter. It continues the introduction."
2,1,"This is the first paragraph of the second chapter. It delves into the main content of the document."
2,2,"This is the second paragraph of the second chapter. It provides more details on the main content."
```

### Explication du fichier CSV

1. **En-tête** :
   ```csv
   Chapter,Paragraph,Content
   ```
   La première ligne du fichier CSV contient les en-têtes de colonne, qui décrivent les types de données présentes dans chaque colonne. Dans cet exemple, les colonnes sont `Chapter`, `Paragraph`, et `Content`.

2. **Données** :
   ```csv
   1,1,"This is the first paragraph of the first chapter. It provides an introduction to the topic."
   1,2,"This is the second paragraph of the first chapter. It continues the introduction."
   2,1,"This is the first paragraph of the second chapter. It delves into the main content of the document."
   2,2,"This is the second paragraph of the second chapter. It provides more details on the main content."
   ```
   
Chaque ligne suivante contient les données pour un paragraphe spécifique d'un chapitre. Les colonnes sont séparées par des virgules. Les guillemets sont utilisés pour encadrer le contenu textuel afin de gérer les virgules ou les sauts de ligne à l'intérieur du texte.

### Comparaison avec TEI XML

- **Structure** : Le fichier CSV est une représentation tabulaire des données, tandis que le fichier TEI XML est une représentation hiérarchique et balisée.
- **Métadonnées** : Le fichier TEI XML inclut des métadonnées détaillées dans l'en-tête (`<teiHeader>`), tandis que le fichier CSV se concentre uniquement sur les données de contenu.
- **Flexibilité** : Le fichier TEI XML permet une structuration plus riche et plus flexible, incluant des éléments imbriqués et des attributs, tandis que le fichier CSV est plus simple et plus facile à manipuler avec des outils de tableur.

Ce fichier CSV est un exemple simple mais complet, montrant comment structurer des données textuelles de manière tabulaire.

## XML TEI

Voici un exemple de fichier XML TEI (_Text Encoding Initiative_). Le TEI est un standard pour l'encodage de textes en format XML, souvent utilisé dans les sciences humaines pour la représentation de documents textuels.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<TEI xmlns="http://www.tei-c.org/ns/1.0">
    <teiHeader>
        <fileDesc>
            <titleStmt>
                <title>Example Document</title>
                <author>John Doe</author>
            </titleStmt>
            <publicationStmt>
                <publisher>Example Publisher</publisher>
                <date>2023</date>
            </publicationStmt>
            <sourceDesc>
                <p>This is an example of a TEI XML document.</p>
            </sourceDesc>
        </fileDesc>
    </teiHeader>
    <text>
        <body>
            <div type="chapter" n="1">
                <head>Chapter 1: Introduction</head>
                <p>This is the first paragraph of the first chapter. It provides an introduction to the topic.</p>
                <p>This is the second paragraph of the first chapter. It continues the introduction.</p>
            </div>
            <div type="chapter" n="2">
                <head>Chapter 2: Main Content</head>
                <p>This is the first paragraph of the second chapter. It delves into the main content of the document.</p>
                <p>This is the second paragraph of the second chapter. It provides more details on the main content.</p>
            </div>
        </body>
    </text>
</TEI>
```

### Explication du fichier TEI XML

1. **Déclaration XML** :
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   ```
   Cette ligne déclare que le document est en XML et utilise l'encodage UTF-8.

2. **Élément racine `<TEI>`** :
   ```xml
   <TEI xmlns="http://www.tei-c.org/ns/1.0">
   ```
   L'élément racine `<TEI>` définit le document comme conforme au standard TEI.

3. **En-tête TEI `<teiHeader>`** :
   ```xml
   <teiHeader>
       <fileDesc>
           <titleStmt>
               <title>Example Document</title>
               <author>John Doe</author>
           </titleStmt>
           <publicationStmt>
               <publisher>Example Publisher</publisher>
               <date>2023</date>
           </publicationStmt>
           <sourceDesc>
               <p>This is an example of a TEI XML document.</p>
           </sourceDesc>
       </fileDesc>
   </teiHeader>
   ```
   L'en-tête TEI contient des métadonnées sur le document, y compris le titre, l'auteur, l'éditeur, la date de publication, et une description de la source.

4. **Corps du texte `<text>`** :
   ```xml
   <text>
       <body>
           <div type="chapter" n="1">
               <head>Chapter 1: Introduction</head>
               <p>This is the first paragraph of the first chapter. It provides an introduction to the topic.</p>
               <p>This is the second paragraph of the first chapter. It continues the introduction.</p>
           </div>
           <div type="chapter" n="2">
               <head>Chapter 2: Main Content</head>
               <p>This is the first paragraph of the second chapter. It delves into the main content of the document.</p>
               <p>This is the second paragraph of the second chapter. It provides more details on the main content.</p>
           </div>
       </body>
   </text>
   ```
   Le corps du texte contient le contenu principal du document, structuré en chapitres (`<div>`) avec des titres (`<head>`) et des paragraphes (`<p>`).

Ce fichier TEI XML est un exemple simple mais complet, montrant comment structurer un document textuel avec des métadonnées et du contenu hiérarchique.

## Modèle relationnel (type SQL pour _MS Access_, _MySQL_, _MariaDB_)

Voici un exemple de schéma SQL pour représenter des données structurées similaires à celles que l'on pourrait trouver dans le document TEI XML. Le schéma SQL contiendra des informations sur les chapitres et les paragraphes d'un document.

### Exemple de schéma SQL

```sql
-- Création de la table pour les chapitres
CREATE TABLE Chapters (
    ChapterID INT PRIMARY KEY,
    ChapterTitle VARCHAR(255)
);

-- Création de la table pour les paragraphes
CREATE TABLE Paragraphs (
    ParagraphID INT PRIMARY KEY,
    ChapterID INT,
    ParagraphNumber INT,
    Content TEXT,
    FOREIGN KEY (ChapterID) REFERENCES Chapters(ChapterID)
);

-- Insertion des données dans la table Chapters
INSERT INTO Chapters (ChapterID, ChapterTitle) VALUES
(1, 'Chapter 1: Introduction'),
(2, 'Chapter 2: Main Content');

-- Insertion des données dans la table Paragraphs
INSERT INTO Paragraphs (ParagraphID, ChapterID, ParagraphNumber, Content) VALUES
(1, 1, 1, 'This is the first paragraph of the first chapter. It provides an introduction to the topic.'),
(2, 1, 2, 'This is the second paragraph of the first chapter. It continues the introduction.'),
(3, 2, 1, 'This is the first paragraph of the second chapter. It delves into the main content of the document.'),
(4, 2, 2, 'This is the second paragraph of the second chapter. It provides more details on the main content.');
```

### Explication du schéma SQL

1. **Création de la table `Chapters`** :
   ```sql
   CREATE TABLE Chapters (
       ChapterID INT PRIMARY KEY,
       ChapterTitle VARCHAR(255)
   );
   ```
   Cette table contient des informations sur les chapitres, avec `ChapterID` comme clé primaire et `ChapterTitle` pour le titre du chapitre.

2. **Création de la table `Paragraphs`** :
   ```sql
   CREATE TABLE Paragraphs (
       ParagraphID INT PRIMARY KEY,
       ChapterID INT,
       ParagraphNumber INT,
       Content TEXT,
       FOREIGN KEY (ChapterID) REFERENCES Chapters(ChapterID)
   );
   ```
   Cette table contient des informations sur les paragraphes, avec `ParagraphID` comme clé primaire, `ChapterID` comme clé étrangère référençant la table `Chapters`, `ParagraphNumber` pour le numéro du paragraphe, et `Content` pour le contenu du paragraphe.

3. **Insertion des données dans la table `Chapters`** :
   ```sql
   INSERT INTO Chapters (ChapterID, ChapterTitle) VALUES
   (1, 'Chapter 1: Introduction'),
   (2, 'Chapter 2: Main Content');
   ```
   Cette commande insère deux chapitres dans la table `Chapters`.

4. **Insertion des données dans la table `Paragraphs`** :
   ```sql
   INSERT INTO Paragraphs (ParagraphID, ChapterID, ParagraphNumber, Content) VALUES
   (1, 1, 1, 'This is the first paragraph of the first chapter. It provides an introduction to the topic.'),
   (2, 1, 2, 'This is the second paragraph of the first chapter. It continues the introduction.'),
   (3, 2, 1, 'This is the first paragraph of the second chapter. It delves into the main content of the document.'),
   (4, 2, 2, 'This is the second paragraph of the second chapter. It provides more details on the main content.');
   ```
   Cette commande insère quatre paragraphes dans la table `Paragraphs`, chacun associé à un chapitre spécifique.

### Comparaison avec TEI XML et CSV

- **Structure** : Le schéma SQL est une représentation relationnelle des données, tandis que le fichier TEI XML est une représentation hiérarchique et balisée, et le fichier CSV est une représentation tabulaire.
- **Métadonnées** : Le fichier TEI XML inclut des métadonnées détaillées dans l'en-tête (`<teiHeader>`), tandis que le schéma SQL et le fichier CSV se concentrent uniquement sur les données de contenu.
- **Flexibilité** : Le fichier TEI XML permet une structuration plus riche et plus flexible, incluant des éléments imbriqués et des attributs. Le schéma SQL permet des relations complexes entre les tables, tandis que le fichier CSV est plus simple et plus facile à manipuler avec des outils de tableur.

Ce schéma SQL est un exemple simple mais complet, montrant comment structurer des données textuelles de manière relationnelle.

## Modèle de graphe (type RDF)

Voici un exemple de représentation en RDF (Resource Description Framework). Le RDF est un modèle de données pour représenter des informations sous forme de graphes, souvent utilisé dans le cadre du Web sémantique.

### Exemple de fichier RDF en Turtle

```turtle
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix ex: <http://example.org/> .

# Définition des classes
ex:Chapter rdf:type rdfs:Class .
ex:Paragraph rdf:type rdfs:Class .

# Définition des propriétés
ex:hasChapter rdf:type rdf:Property .
ex:hasParagraph rdf:type rdf:Property .
ex:paragraphNumber rdf:type rdf:Property .
ex:content rdf:type rdf:Property .

# Instances de chapitres
ex:Chapter1 rdf:type ex:Chapter ;
    ex:hasParagraph ex:Paragraph1_1, ex:Paragraph1_2 .

ex:Chapter2 rdf:type ex:Chapter ;
    ex:hasParagraph ex:Paragraph2_1, ex:Paragraph2_2 .

# Instances de paragraphes
ex:Paragraph1_1 rdf:type ex:Paragraph ;
    ex:paragraphNumber 1 ;
    ex:content "This is the first paragraph of the first chapter. It provides an introduction to the topic." .

ex:Paragraph1_2 rdf:type ex:Paragraph ;
    ex:paragraphNumber 2 ;
    ex:content "This is the second paragraph of the first chapter. It continues the introduction." .

ex:Paragraph2_1 rdf:type ex:Paragraph ;
    ex:paragraphNumber 1 ;
    ex:content "This is the first paragraph of the second chapter. It delves into the main content of the document." .

ex:Paragraph2_2 rdf:type ex:Paragraph ;
    ex:paragraphNumber 2 ;
    ex:content "This is the second paragraph of the second chapter. It provides more details on the main content." .
```

### Explication du fichier RDF en Turtle

1. **Préfixes** :
   ```turtle
   @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
   @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
   @prefix ex: <http://example.org/> .
   ```
   Ces lignes définissent les préfixes utilisés dans le fichier RDF pour abréger les URI.

2. **Définition des classes** :
   ```turtle
   ex:Chapter rdf:type rdfs:Class .
   ex:Paragraph rdf:type rdfs:Class .
   ```
   Ces lignes définissent les classes `Chapter` et `Paragraph`.

3. **Définition des propriétés** :
   ```turtle
   ex:hasChapter rdf:type rdf:Property .
   ex:hasParagraph rdf:type rdf:Property .
   ex:paragraphNumber rdf:type rdf:Property .
   ex:content rdf:type rdf:Property .
   ```
   Ces lignes définissent les propriétés `hasChapter`, `hasParagraph`, `paragraphNumber`, et `content`.

4. **Instances de chapitres** :
   ```turtle
   ex:Chapter1 rdf:type ex:Chapter ;
       ex:hasParagraph ex:Paragraph1_1, ex:Paragraph1_2 .

   ex:Chapter2 rdf:type ex:Chapter ;
       ex:hasParagraph ex:Paragraph2_1, ex:Paragraph2_2 .
   ```
   Ces lignes définissent les instances de chapitres (`Chapter1` et `Chapter2`) et leurs paragraphes associés.

5. **Instances de paragraphes** :
   ```turtle
   ex:Paragraph1_1 rdf:type ex:Paragraph ;
       ex:paragraphNumber 1 ;
       ex:content "This is the first paragraph of the first chapter. It provides an introduction to the topic." .

   ex:Paragraph1_2 rdf:type ex:Paragraph ;
       ex:paragraphNumber 2 ;
       ex:content "This is the second paragraph of the first chapter. It continues the introduction." .

   ex:Paragraph2_1 rdf:type ex:Paragraph ;
       ex:paragraphNumber 1 ;
       ex:content "This is the first paragraph of the second chapter. It delves into the main content of the document." .

   ex:Paragraph2_2 rdf:type ex:Paragraph ;
       ex:paragraphNumber 2 ;
       ex:content "This is the second paragraph of the second chapter. It provides more details on the main content." .
   ```
   Ces lignes définissent les instances de paragraphes (`Paragraph1_1`, `Paragraph1_2`, `Paragraph2_1`, `Paragraph2_2`) avec leurs numéros de paragraphe et leur contenu.

### Comparaison avec TEI XML, CSV et SQL

- **Structure** : Le fichier RDF est une représentation sous forme de graphe des données, tandis que le fichier TEI XML est une représentation hiérarchique et balisée, le fichier CSV est une représentation tabulaire, et le schéma SQL est une représentation relationnelle.
- **Métadonnées** : Le fichier TEI XML inclut des métadonnées détaillées dans l'en-tête (`<teiHeader>`), tandis que le fichier RDF, le fichier CSV et le schéma SQL se concentrent uniquement sur les données de contenu.
- **Flexibilité** : Le fichier TEI XML permet une structuration plus riche et plus flexible, incluant des éléments imbriqués et des attributs. Le fichier RDF permet des relations complexes et sémantiques entre les ressources, tandis que le schéma SQL permet des relations complexes entre les tables, et le fichier CSV est plus simple et plus facile à manipuler avec des outils de tableur.

Ce fichier RDF en Turtle est un exemple simple mais complet, montrant comment structurer des données textuelles sous forme de graphe.