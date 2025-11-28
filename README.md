# komandat git

```
hapi fillestare
git pull
git status
git add -A
git commit -m "mesazhi teksti sqarues"
git push

```


# appRequest

```
Create web app with spatial data. A project should contain the graphical data.
Roads , buildings, apartments,house, water network pipes, the valves, point of
connection of costumers in the water network. The water network is on 3 forms
of geometry, as point, line, polygon, in the destop version of shape file
whitch should import to postgre database
The costumer data, name, address, consumption of water per month, id, type of
consumer ( private or business).  A water network should have these elements:

1 Water network

1. Supply pipe
2. distribution pipe
3. connecting pipe
4. zonal metered water
5. individual metered water

1.1 a Supply pipe   should have these attributes
1. Dimension (float type in data base)
2. Capacity  (float type in data base)
3. Year of installation (int type)
4. The depth of pipe under ground
5. The measured volume
6. The invoiced volume
7. The lost volume

1.2 distribution pipe should have these attributes
1. Dimension (float type in data base)
2. Capacity  (float type in data base)
3. Year of installation (int type)
4. The depth of pipe under ground
5. The measured volume
6. The invoiced volume
7. The lost volume
8. Number of connection of consumers

1.3 connecting pipe  should have these attributes
1. Number of connection of consumers
2. Dimension (float type in data base)
3. Year of installation (int type)
4. The depth of pipe under ground
5. id of building that is connected to pipe

1.4 zonal metered water should have these attributes
1. Number of connection of consumers
2. Year of installation (int type)
3. The depth of pipe under ground
4. The measured volume
5. The invoiced volume
6. The lost volume
7. type (geom , point , stored type on database)


1.5 individual metered water should have these attributes
1. Owner
2. address (the name of road)
3. Year of connection
4. Id (char type : bill0036781)
5. Type of building (house, or apartment)
6. Flor (int type)
7. Number of enter of building
8. Name of investor of building
9. Name of investor of building
10. Type (type of stored in database, geom, point)






```

## database

```
krijimi i database për projektin e web app për menagjimin me ujra.
në database ka 4 grupe kryesore

1. Rrjeti i ujsjellësit
2. Ndërtesat, shtëpitë
3. Rrjeti i rrugëve
4. Pronarët


 rrjeti i ujsjellesit

1.  Gypi i furnizimit
2.  Ujmatesi zonal
3.  Ujmatesi kolektiv
4.  Ujmatesi individual
5.  Gypi shperndares

Gypi i furnizimit

1. tipi: geom (gjeometria: linje , pike , apo poligon)
2. dimenzionit : float (shembull fi 12)
3. viti i instalimit : int (shembull 1997)
4. thellesi : float (1.12 m)
5. sasite e inkasuara : double (1525.32 m3)
6. sasite e matura : double (1555.32 m3)
7. sasite e humbura : double (153.32 m3)

CREATE TABLE gypi_furnizimi (
    id SERIAL PRIMARY KEY,
    adresa VARCHAR(255),
    gjeometria GEOMETRY(LineString, 4326),
    dimensioni FLOAT,
    viti_instalimit INT,
    thellesi FLOAT,
    sasite_inkasuara DOUBLE PRECISION,
    sasite_matura DOUBLE PRECISION,
    sasite_humbura DOUBLE PRECISION,
    created_at TIMESTAMP DEFAULT NOW()
);

Ujmatesi zonal

    1. tipi: geom (gjeometria: linje , pike , apo poligon)
    2. nnmri i kyqjeve: int (duhet te jete i barabarte me numrin e konsumatoreve qe
    jane te lidhur ne ujmatesin zonal)
    3. viti i instalimit : int (shembull 1997)
    4. materiali (pvc, asbest....)
    5. sasite e inkasuara : double (1525.32 m3)
    6. sasite e matura : double (1555.32 m3)
    7. sasite e humbura : double (153.32 m3)
ujmatesi zonal duhet te kete lidhje me ujmatesat individual qe jane te lidhur
ne ujmatesin zonal, me q'rast shuma e sasive te inkasuara ne ujmatesa
individual duhet te jete me shumen e lexuar te ujmatesin zonal, shperputhja ne
rrezultat duhet te trajtohet si humbje.

--- codi --- 

CREATE TABLE ujemates_zonal (
    id SERIAL PRIMARY KEY,
    adresa VARCHAR(255),
    gjeometria GEOMETRY(Point, 4326),
    numri_kyqjeve INT,
    viti_instalimit INT,
    materiali VARCHAR(50),
    sasite_inkasuara DOUBLE PRECISION,
    sasite_matura DOUBLE PRECISION,
    sasite_humbura DOUBLE PRECISION,
    created_at TIMESTAMP DEFAULT NOW()
);

Ujmatesi kolektiv

vendoset neper ndertesa te banimit kolektiv me shume njesi banesore
1.  pronari (ne kete rast investitori apo emri i kompanise investitore)
2.  Lloji: char  (perdorimi per amviseri, afarizem, industri etj)
3.  Adresa: char (emri i rruges)
4.  gjeometria (pike, e marrur nga shapefile)
5.  Viti i instalimit
6.  sasite e inkasuara
7.  sasite e matura
8.  sasite e humbuara

ujmatesi kolektiv duhet te kete lidhje me ujmatesat individual te cilet jane te
kyqur ne te ujmatesi kolektiv eshte ujmates qe mate sasite e ujit te nje
ndertese te tere, me q'rast sasite e lexuara ne te duhet te pershtaten me
sasite e ujmatesave individual qe jane ne ndertesen e njejte, diferenca duhet
trajtuar si hubje

--- codi --- 

CREATE TABLE ujemates_kolektiv (
    id SERIAL PRIMARY KEY,
    adresa VARCHAR(255),
    pronari_id INT REFERENCES pronaret(id),
    lloji VARCHAR(50),
    gjeometria GEOMETRY(Point, 4326),
    viti_instalimit INT,
    sasite_inkasuara DOUBLE PRECISION,
    sasite_matura DOUBLE PRECISION,
    sasite_humbura DOUBLE PRECISION,
    created_at TIMESTAMP DEFAULT NOW()
);

ujmatesi individual

duhet te kete keto atribute
1.  geom (gjeometria, qe duhet te jete pike)
2.  sasite e inkasuara
3.  sasite e matura
4.  borgji
5.  lloji (amviseri, afarizem, industri)
6.  pronari (fushe qe vie nga tabelat e konsumatoreve)
7.  viti kyqjes :int (1997)
8.  NdertimiLloji: char (shtepi ose banese, ndertese kolektive)

ujmatesi individual si gjeomteri vie nga shapefile i gjeneruar ne qgis, i formes pike
ujmatesi individual duhet te kete lidhje me ujmatesin kolektiv (nje ujmates
kolektiv shume ujmatesa individual)
ujmatesi individual duhet te kete lidhje me ujmatesin zonal (nje ujmates
zonal shume ujmatesa individual)
sasite  e ujmatesit individual duhet te transmetohen te ujmatesi kolektiv
respektiv, dhe ujmatesi zonal
ne rastet kur ujmatesi individual eshte ne ndertese kolektive duhet te kete si
atribut dhe katin 
ujmatesi individual duhet te kete lidhje me tabeln e pronareve, me q'rast ai
pronare te merr te dhenat e sasive nga ujmatesi individual

CREATE TABLE ujemates_individual (
    id SERIAL PRIMARY KEY,
    adresa VARCHAR(255),
    gjeometria GEOMETRY(Point, 4326),
    pronari_id INT REFERENCES pronaret(id),
    sasite_inkasuara DOUBLE PRECISION,
    sasite_matura DOUBLE PRECISION,
    borgji DOUBLE PRECISION,
    lloji VARCHAR(50),
    viti_kyqjes INT,
    ndertimi_lloji VARCHAR(100),
    kati INT,
    created_at TIMESTAMP DEFAULT NOW()
);

Gypi shperndares


Gypi shperndares duhet te kete keto atribute:
thellesi: float (1.12 m)
dimenzioni: float (fi 30)
viti istalimit: int (2005)
materiali: char (pvc,asbest)
tipi: geom (gjeometria , qe do jete linje)
nrKyqjeve: int (1532)

gjeometri dhe  atributet do te vine te plotesuara nga qgis, ne formatin
shapefile

gypi shperndares duhet te kete lidhje me ujmatesat zonal dhe ato individual me
q'rast nje gyp ka shume ujmatesa individual e kolektiv, kurse  shume gypa
shperndares kane nga 1 ujmates zonal

numri i kyqjeve ne gypin shperndares duehet pastaj te jete i kalkulueshem se sa
ujematesa individual jane te kyquur ne te


CREATE TABLE gypi_shperndares (
    id SERIAL PRIMARY KEY,
    adresa VARCHAR(255),
    gjeometria GEOMETRY(LineString, 4326),
    thellesi FLOAT,
    dimensioni FLOAT,
    viti_instalimit INT,
    materiali VARCHAR(50),
    nr_kyqjeve INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT NOW()
);


 ```



### rrjeti i ujesjellesit vizualizimi


```

┌─────────────────────┐        ┌─────────────────────┐
│      Pronaret       │1      ∞│   UjmatesiIndividual│
│---------------------│◄───────│---------------------│
│ id (PK)             │        │ id (PK)             │
│ emri                │        │ adresa              │
│ adresa              │        │ gjeometria (Point)  │
└─────────────────────┘        │ sasite_inkasuara     │
                                │ sasite_matura        │
                                │ borgji              │
                                │ lloji               │
                                │ viti_kyqjes         │
                                │ ndertimi_lloji      │
                                │ kati                │
                                └─────────────────────┘
                                          ▲
                                          │
                                          │
                  ┌───────────────────────┴─────────────────────────┐
                  │                                                 │
┌───────────────────────────┐                       ┌───────────────────────────┐
│   UjmatesiKolektiv        │1                     ∞│ UjmatesiIndividual       │
│---------------------------│◄─────────────────────│ (via kolektiv_individual)│
│ id (PK)                   │                       └───────────────────────────┘
│ adresa                    │
│ pronari_id (FK)           │
│ lloji                     │
│ gjeometria (Point)        │
│ viti_instalimit           │
│ sasite_inkasuara           │
│ sasite_matura             │
│ sasite_humbura            │
└───────────────────────────┘

┌───────────────────────────┐
│    UjmatesiZonal          │1
│---------------------------│
│ id (PK)                   │
│ adresa                    │
│ gjeometria (Point)        │
│ numri_kyqjeve             │
│ viti_instalimit           │
│ materiali                 │
│ sasite_inkasuara           │
│ sasite_matura             │
│ sasite_humbura            │
└───────────────────────────┘
        ▲1
        │
        │∞
┌───────────────────────────┐
│ GypiShperndares           │
│---------------------------│
│ id (PK)                   │
│ adresa                    │
│ gjeometria (LineString)   │
│ thellesi                  │
│ dimensioni                │
│ materiali                 │
│ nr_kyqjeve                │
│ viti_instalimit           │
└───────────────────────────┘
        ▲
        │∞
┌───────────────────────────┐
│ GypiFurnizimi             │
│---------------------------│
│ id (PK)                   │
│ adresa                    │
│ gjeometria (LineString)   │
│ dimensioni                │
│ thellesi                  │
│ viti_instalimit           │
│ sasite_inkasuara           │
│ sasite_matura             │
│ sasite_humbura            │
└───────────────────────────┘
        │
        │1
┌───────────────────────────┐
│ UjmatesiZonal             │
└───────────────────────────┘


| Lidhja                                | Tipi   | Tabela ndërmjetëse         |
| ------------------------------------- | ------ | -------------------------- |
| Gypi Furnizimi → Ujmatës Zonal        | 1:N    | gyp_furnizimi_zonal        |
| Gypi Shpërndarës → Ujmatës Zonal      | Many:1 | gyp_shperndares_zonal      |
| Gypi Shpërndarës → Ujmatës Individual | 1:N    | gyp_shperndares_individual |
| Ujmatës Zonal → Ujmatës Individual    | 1:N    | zonal_individual           |
| Ujmatës Kolektiv → Ujmatës Individual | 1:N    | kolektiv_individual        |
| Ujmatës Individual → Pronari          | Many:1 | direkt (foreign key)       |
| Ujmatës Kolektiv → Pronari            | Many:1 | direkt (foreign key)       |

```

### tabelat e database


| **Tabela**            | **Kolona**       | **Tipi**                   | **Veçori/Çelësi**                   |
| --------------------- | ---------------- | -------------------------- | ----------------------------------- |
<!-- | `gypi_furnizimi`      | id               | SERIAL                     | PRIMARY KEY                         | -->
|                       | adresa           | VARCHAR(255)               |                                     |
<!-- |                       | gjeometria       | GEOMETRY(LineString, 4326) |                                     | -->
|                       | dimensioni       | FLOAT                      |                                     |
|                       | viti_instalimit  | INT                        |                                     |
|                       | thellesi         | FLOAT                      |                                     |
|                       | sasite_inkasuara | DOUBLE PRECISION           |                                     |
|                       | sasite_matura    | DOUBLE PRECISION           |                                     |
|                       | sasite_humbura   | DOUBLE PRECISION           |                                     |
<!-- |                       | created_at       | TIMESTAMP                  | DEFAULT NOW()                       | -->
<!-- | `ujemates_zonal`      | id               | SERIAL                     | PRIMARY KEY                         | -->
|                       | adresa           | VARCHAR(255)               |                                     |
|                       | gjeometria       | GEOMETRY(Point, 4326)      |                                     |
|                       | numri_kyqjeve    | INT                        |                                     |
|                       | viti_instalimit  | INT                        |                                     |
|                       | materiali        | VARCHAR(50)                |                                     |
|                       | sasite_inkasuara | DOUBLE PRECISION           |                                     |
|                       | sasite_matura    | DOUBLE PRECISION           |                                     |
|                       | sasite_humbura   | DOUBLE PRECISION           |                                     |
<!-- **|                       | created_at       | TIMESTAMP                  | DEFAULT NOW()                       |** -->
<!-- | `ujemates_kolektiv`   | id               | SERIAL                     | PRIMARY KEY                         | -->
|                       | adresa           | VARCHAR(255)               |                                     |
|                       | pronari_id       | INT                        | FOREIGN KEY REFERENCES pronaret(id) |
|                       | lloji            | VARCHAR(50)                |                                     |
<!-- |                       | gjeometria       | GEOMETRY(Point, 4326)      |                                     | -->
|                       | viti_instalimit  | INT                        |                                     |
|                       | sasite_inkasuara | DOUBLE PRECISION           |                                     |
|                       | sasite_matura    | DOUBLE PRECISION           |                                     |
|                       | sasite_humbura   | DOUBLE PRECISION           |                                     |
<!-- |                       | created_at       | TIMESTAMP                  | DEFAULT NOW()                       | -->
<!-- | `ujemates_individual` | id               | SERIAL                     | PRIMARY KEY                         | -->
|                       | adresa           | VARCHAR(255)               |                                     |
<!-- |                       | gjeometria       | GEOMETRY(Point, 4326)      |                                     | -->
|                       | pronari_id       | INT                        | FOREIGN KEY REFERENCES pronaret(id) |
|                       | sasite_inkasuara | DOUBLE PRECISION           |                                     |
|                       | sasite_matura    | DOUBLE PRECISION           |                                     |
|                       | borgji           | DOUBLE PRECISION           |                                     |
|                       | lloji            | VARCHAR(50)                |                                     |
|                       | viti_kyqjes      | INT                        |                                     |
|                       | ndertimi_lloji   | VARCHAR(100)               |                                     |
|                       | kati             | INT                        |                                     |
<!-- |                       | created_at       | TIMESTAMP                  | DEFAULT NOW()                       | -->
<!-- | `gypi_shperndares`    | id               | SERIAL                     | PRIMARY KEY                         | -->
|                       | adresa           | VARCHAR(255)               |                                     |
<!-- |                       | gjeometria       | GEOMETRY(LineString, 4326) |                                     | -->
|                       | thellesi         | FLOAT                      |                                     |
|                       | dimensioni       | FLOAT                      |                                     |
|                       | viti_instalimit  | INT                        |                                     |
|                       | materiali        | VARCHAR(50)                |                                     |
|                       | nr_kyqjeve       | INT                        | DEFAULT 0                           |
<!-- |                       | created_at       | TIMESTAMP                  | DEFAULT NOW()                       | -->


