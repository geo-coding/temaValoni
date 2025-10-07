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




```
