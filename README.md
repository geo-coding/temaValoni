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
2.  Gypi shperndares
3.  Ujmatesi zonal
4.  Ujmatesi kolektiv
5.  Ujmatesi individual

Gypi i furnizimit

1. tipi: geom (gjeometria: linje , pike , apo poligon)
2. dimenzionit : float (shembull fi 12)
3. viti i instalimit : int (shembull 1997)
4. thellesi : float (1.12 m)
5. sasite e inkasuara : double (1525.32 m3)
6. sasite e matura : double (1555.32 m3)
7. sasite e humbura : double (153.32 m3)

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

 ```


