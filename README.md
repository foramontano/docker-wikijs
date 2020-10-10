# docker-wikijs
Issues to take into account:

## Configuration
Cerate your **.env-wikijs** file to set DB config fields:

```
# Example
DB_USER=wikijs
DB_PASS=wikijsrocks
DB_NAME=wiki
# Valores de la base de datos para que puedan ser vistos por Wiki.js WEB
POSTGRES_USER=$(DB_USER)
POSTGRES_PASSWORD=$(DB_PASS)
LETSENCRYPT_EMAIL=admin@example.com
```
Update your **docker-compose.yml** config fields

## Deployment
Just execute docker compose command:
```
docker-compose up -d
```

## Customization
Set your images
### Images:

### Colours
Example with some colours I've changed
- Choose the colours you want to change (using your browser inspection tool)
- Acces Wiki.js container
- Seach for css/js files contain the coulour you want to change
- Change the colour (using sed command)
- Copy css/js files you've changed to your customization-dir (having into account the dir structure)

the result will be the base tou'll use next time you have to remove & create the Wiki.js web 

Access to Wiki.js container home
```
docker exec -ti wikijs_wiki_1 bash 
```

Change colours to adapt Wiki.js to your style
```
#Negro cabecera: #000!important --> #ffffff
grep -r -l -i ".v-application .black{background-color:#000!" .
sed -i 's/.v-application .black{background-color:#000!/.v-application .black{background-color:#ffffff!/g' ./js/*.js

#Gris iconos cabecera: #9e9e9e --> #175676
grep -r -l -i "#9e9e9e" .
sed -i 's/#9e9e9e/#175676/g' ./js/*.js
sed -i 's/#9e9e9e/#175676/g' ./css/*.css

#Gris cabera entradas WIKI: #607d8b --> #669968   --> Verde Flarum
grep -r -l -i "#607d8b" .
sed -i 's/#607d8b/#	/g' ./js/*.js
sed -i 's/#607d8b/#669968/g' ./css/*.css

#Negro menú edición página WIKI: #212121 --> #669968   --> Verde Flarum
grep -r -l -i "#212121" .
sed -i 's/#212121/#669968/g' ./js/*.js
sed -i 's/#212121/#669968/g' ./css/*.css

#Negro caja Búsqueda #1e1e1e --> #175676
grep -r -l -i "#1e1e1e" .
sed -i 's/#1e1e1e/#669968/g' ./js/*.js
sed -i 's/#1e1e1e/#669968/g' ./css/*.css

#Azul header: #1565c0 --> #175676
grep -r -l -i "#1565c0" .
sed -i 's/#1565c0/#175676/g' ./js/*.js
sed -i 's/#1565c0/#175676/g' ./css/*.css

#Azul Menú lateral: #1976d2 --> #175676
grep -r -l -i "#1976d2" .
docker exec wikijs_wiki_1 sed -i 's/#1976d2/#175676/g' ./js/*.js
docker exec wikijs_wiki_1 sed -i 's/#1976d2/#175676/g' ./css/*.css

# Es necesario editar el fichero app.js
docker cp wikijs_wiki_1:/wiki/assets/js/app.js ~/wiki.js/personalizar/wiki/assets/js/

docker cp ~/wiki.js/personalizar/wiki/assets/  wikijs_wiki_1:/wiki/
```
