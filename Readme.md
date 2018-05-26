
# COOL TITLE! Or is it HOT! 

# 3 Observable Trends + the obvious one?

# "Temperature (F) vs. Latitude"
Latitude is between -90 and 90 and Equator is 0. Each of the analysis places Latitude on the x-axis, which follows the mathematical model of the x-values being the domain(input) of a function. So the concept is that the domain dictates what happens to the range, which was clearly demostrated by the Temperature (the Latitude determined the Temperature, not the Temperature determining the Latitude). So, using this domain and range math concept - let's consider each of the 3 observable trends they requested us to look at, plus the obvious one of the temperature related to Latitude...  

At first glance it appeared that the temperatures created a parabolic shape over the equator. Once the x = 0 line was dropped in it became obvious that the axis of symmetry was not on the equator, but more over the x = 20 value of latitude. So then reviewing the earth and comparing it to the equator, it appears that this data is slightly skewed because there is just more land (cities) on the Northern Hemisphere (0 to 90). Thus, even though it does seem to be a known fact - that it is warmer the closer you get to the equator - the data is showing something slightly different. It appears to be showing that there aren't as many cities on the equator... probably because it's a hot line to live on! ;-) 

# "Wind Speed (mph) vs. Latitude"
Well, when you let Latitude be your domain and see if the Latitude of the city has an impact on the wind speed... the dots show you nothing. Well, not exactly nothing, it shows you that Latitude doesn't impact Windspeed... so I guess that is something. 


# "Cloudiness(%) vs. Latitude"
The same spread of the dots being random and equally spread all over the domain holds true for cloudiness as it did for Windspeed. The dots show that the domain, Latitude, does not have an impact on the cloudiness of the city. These results were something that required a little bit of thinking as it went against the common sense idea of the closer to the equator is warmer, so more sun comes with that... That common sense idea is lost with this data, and reminds you that at the equator also has other things such as humidity - it's tropical at the equator - which could create additional cloudiness. Regardless, the data is so spread out - the fact still holds true - Latitude doesn't determine the amount of Cloudiness for a city. 


# "Humidity(%) vs. Latitude"
Maybe there would be more humidity closer to the Equator, since it is tropical along the equator... But no, again the dots are evenly spread around and there is clearly no coorelation. The dots again are heavy on the x = 20 line verses the x = 0(equator) line which still aligns with the idea mentioned in the temperature observation - more cities in the Northern Hemisphere. Yet again, the domain Latitude does not determine the Humidity of a city. 


```python
import json
import requests
import csv
import matplotlib.pyplot as plt
import openweathermapy as ow
import pandas as pd
from citipy import citipy
import numpy as np
from random import randint
from pprint import pprint
#from THE BOOTCAMPSPOT import api_key
api_key = #please get my API from Bootcampspot
```

# Generating Latitude and Longitude Coordinate


```python
# Some random coordinates
#lat is between -90 and 90 and Equator is 0
#Lon is between -180 and 180 and the prime meridian is 0

#To get at least the 500 samples
#needed to pull 1500 because of duplicates of cities and then weather not found.

import itertools
random_lat = [randint(-90, 90) for x in range(1, 1501)]
random_long = [randint(-180, 180) for y in range(1, 1501)]

coordinates =(list(zip(random_lat, random_long)))
```

#  Getting City Names using Citypy


```python
cities = []
for coordinate_pair in coordinates:
    lat, lon = coordinate_pair
    cities.append(citipy.nearest_city(lat, lon))
print(len(cities))
```

    1500


# Removing the duplicated City Names


```python
city_name = []
for city in cities:
    name = city.city_name
    if name not in city_name:
        city_name.append(name)
   # print(f"The name of the chosen city is {name}.")
print(len(city_name))
```

    611



```python
# Save config information.
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial"

# Build partial query URL
query_url = f"{url}appid={api_key}&units={units}&q="
for printed_url in city_name: 
    print(f"{query_url}{printed_url}")
```

    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=taolanaro
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lebu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=barrow
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=albany
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=busselton
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mahajanga
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=atuona
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hilo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=verkhoyansk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tsaratanana
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=castro
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=marcona
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ahipara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tiksi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=iquique
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=misratah
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=acapulco
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zhezkazgan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chhatak
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saint-philippe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=victoria
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ketchikan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bowen
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bluff
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vaini
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mehamn
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=attawapiskat
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=souillac
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=iqaluit
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pevek
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=port elizabeth
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=najran
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=katiola
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vaitupu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bengkulu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=manggar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saint george
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mazatlan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mataura
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=den helder
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hobart
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=leningradskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nizhneyansk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=eyl
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lompoc
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cayenne
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zabid
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=stornoway
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=grindavik
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=klaksvik
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=shingu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=honiara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=axim
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san patricio
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san cristobal
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=belushya guba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=agua verde
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cape town
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tyrma
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rawson
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=laibin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saint anthony
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=port lincoln
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=codrington
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=thompson
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=svetlaya
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=avarua
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=guiyang
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dhidhdhoo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=salalah
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=amderma
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=marzuq
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rio gallegos
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tsihombe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=elizabeth city
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mys shmidta
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tsogni
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=north battleford
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san policarpo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mormugao
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=odemis
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=carlton
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=barentsburg
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=boquira
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=faya
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sitka
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=coihaique
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=suarez
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gaspar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=plettenberg bay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chumikan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=severo-yeniseyskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tromso
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=llanes
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ostersund
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=talcahuano
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=verkhnyaya sinyachikha
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vidim
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=falam
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ola
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ust-nera
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zhanaozen
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=port blair
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=homer
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=wahiawa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kimberley
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=torbay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=namibe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sola
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=moose factory
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=isangel
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rostovka
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rocha
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=preobrazheniye
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=udimskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=christchurch
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lufilufi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=galle
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=aswan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=loa janan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=manono
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bulgan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saryozek
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bismarck
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ponta delgada
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=petropavlovsk-kamchatskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=taoudenni
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hovd
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zhigansk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=azul
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=clyde river
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=impfondo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=skagen
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nome
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=luderitz
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hofn
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=felipe carrillo puerto
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=prince rupert
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sabae
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pisco
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=khash
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=harindanga
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mayya
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=leh
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ruatoria
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ancud
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gat
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=jaruco
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=phan rang
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=poum
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=victor harbor
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=manyana
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sao gabriel da cachoeira
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sur
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sindor
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=henties bay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=smithers
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rio claro
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yima
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=umm lajj
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=high prairie
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=havelock
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=brasilia
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=godec
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=egvekinot
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=warwick
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kinanah
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san luis
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=katsuura
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=svay rieng
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nipawin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=broome
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=morondava
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nyagan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=belmonte
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gizo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=anderson
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tarata
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=matam
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pasni
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=biskupiec
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=berlevag
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tuatapere
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=seoul
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sioux lookout
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=the pas
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=monrovia
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mahibadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=amazar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sao miguel do araguaia
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=porto novo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nyurba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vila velha
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=college
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=aleksandrov gay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=roald
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=don benito
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sao filipe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=wanlaweyn
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=siderno
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hami
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=broken hill
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sokolo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dukat
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=charyshskoye
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bay roberts
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sentyabrskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=itaituba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=talnakh
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cidreira
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bontang
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lisakovsk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=margate
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tarakan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pacific grove
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=puerto escondido
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mrirt
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=palu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=constitucion
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sinazongwe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sohag
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cooma
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yar-sale
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bogalusa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=derzhavinsk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sobolevo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=alta floresta
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kaohsiung
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tateyama
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kuche
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=itacarambi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sosnovo-ozerskoye
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=honningsvag
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hay river
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=grenville
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dumai
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=esperance
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=celestun
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=marrakesh
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=king city
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hovorany
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saint-medard-en-jalles
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=khonuu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dauphin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=paragominas
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hirado
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=fortuna
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=karasjok
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=odweyne
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=horta
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zhuzhou
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kieta
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saint-pierre
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=marti
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=narsaq
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hihifo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lorengau
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=marawi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nantucket
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=griffith
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=boddam
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tigil
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sayyan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=maloshuyka
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=puerto madryn
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chuy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=savinka
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=grand river south east
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vao
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=durant
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gorin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=itarema
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=singaraja
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=avanigadda
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yulara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=astana
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=one hundred mile house
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zaysan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=medina
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=moree
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sar-e pul
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=adrar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yong peng
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kaitangata
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=karauzyak
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vostok
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tumannyy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lososina
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san quintin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kargala
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cap-aux-meules
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lafia
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=petrivka
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=skagastrond
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lolua
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=shieli
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=buriti
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=umzimvubu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=asadabad
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=airai
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=elko
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=patnos
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pontian kecil
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=arman
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=paita
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=paamiut
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chapais
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pemba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=charters towers
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=goderich
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=fairview
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=port hardy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=umm kaddadah
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=laela
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=silvan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rzhaksa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=quelimane
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zvenigovo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=palasa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bethel
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mabaruma
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gorno-chuyskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=caravelas
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pachino
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=topchikha
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cairns
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mamakan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nikologory
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=santa eulalia del rio
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san rafael
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=narbonne
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bushehr
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=colorado springs
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=antalaha
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kolpashevo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=manokwari
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pizarro
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vardo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=genhe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nakamura
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kuusamo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=villa sandino
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=aripuana
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ukiah
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kathmandu
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hambantota
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=upig
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bukoba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=portobelo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=corn island
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san isidro
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=candawaga
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=moron
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=raudeberg
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=qunduz
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=suratgarh
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=muyezerskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=okhotsk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=alofi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ji-parana
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dharchula
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=norsup
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gilgit
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=fomboni
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ayaviri
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kruisfontein
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=half moon bay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=shimoda
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=imbituba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zachagansk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=malakal
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rungata
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=urumqi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gidam
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=eureka
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=beisfjord
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=suntar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dikson
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pampa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=westport
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=surgut
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=andevoranto
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=karratha
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bilibino
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kapoeta
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=vieux-habitants
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=millinocket
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gorele
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=phalaborwa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=norman wells
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rantepao
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=siocon
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sagua la grande
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hasaki
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=makakilo city
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hervey bay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=irara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yerky
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=te anau
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sabang
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saint-augustin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dodge city
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=karamea
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=shitanjing
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=asau
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=matara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ulladulla
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nizwa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cherskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chatra
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=loandjili
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lagos
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yarmouth
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=viligili
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=guadalupe y calvo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bondoukou
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=wanning
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=raga
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saint-joseph
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=north bend
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sakakah
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lima
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nouadhibou
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=voi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kurdzhinovo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lebanon
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tutoia
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rassvet
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=girona
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=angul
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=buraydah
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=iquitos
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kamaishi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=novobelokatay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tombouctou
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=drezdenko
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=myitkyina
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nishihara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=gromiljak
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=miri
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sorong
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=salinopolis
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=marsh harbour
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kahului
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kourou
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=maues
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=byron bay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=holetown
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=senno
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=shache
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=walla walla
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=japura
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=charleston
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ozgon
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=soe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nzerekore
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=estelle
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=east london
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mandera
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kaupanger
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=meiktila
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nkongsamba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=akdepe
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=caracuaro
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=louisbourg
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=aklavik
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=flinders
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yomitan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=zeya
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tura
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nobres
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=novoagansk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mapimi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=torrington
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=soyo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bargal
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mount isa
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kalabo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ginda
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kargasok
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=triel-sur-seine
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=stryn
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=faanui
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=les cayes
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=aberdeen
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=burns lake
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=merauke
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=coquimbo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tautira
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=casambalangan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lavrentiya
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kasane
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=tabiauea
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=szentlorinc
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yanam
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=boden
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=omboue
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kamyzyak
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=maniitsoq
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nador
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=corinto
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sakhon nakhon
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yelan
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=camapua
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=saleaula
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=fort-shevchenko
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=handwara
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=hamilton
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=burnie
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=barbar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kazalinsk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=shakhtinsk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=la paz
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=yumen
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=san ramon de la nueva oran
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bhasawar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=deputatskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=nelson bay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=asfi
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=beaune
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=port macquarie
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=winslow
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=teknaf
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=ornskoldsvik
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=beringovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=khagrachari
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lata
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=dubrovnik
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=port keats
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=pangnirtung
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=richards bay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sistranda
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=altay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kutum
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=martin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chicama
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chenghai
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mackay
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=kamyshla
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=lakes entrance
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=owando
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=birao
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mahadday weyne
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=guilin
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=north myrtle beach
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=blagoveshchensk
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=boguchany
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=bumba
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=mayo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=rafaela
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=caconda
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sao jose da coroa grande
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cabedelo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=chanute
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sansai
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=haines junction
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=cervo
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=uniontown
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=biak
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=presidencia roque saenz pena
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=shar
    http://api.openweathermap.org/data/2.5/weather?appid=7c53aa56ddcdaf0b301269b905c02277&units=imperial&q=sawtell



```python
city_temp = []
lat = []
lon = []
dt = []
clouds = []
wind =[]
name = []
country = []
humidity =[]
for city in city_name:
    try:
        response = requests.get(query_url + city).json()
        lat.append(response['coord']['lat'])
        city_temp.append(response['main']['temp_max'])
        lon.append(response['coord']['lon'])
        dt.append(response['dt'])
        clouds.append(response['clouds']['all']) 
        wind.append(response['wind']['speed'])
        name.append(response['name'])
        country.append(response['sys']['country'])
        humidity.append(response['main']['humidity'])
    except: 
        print("No weather found, skip...")
```

    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...
    No weather found, skip...



```python
# create a data frame from cities, lat, and temp
weather_dict = {
    "City":name,
    "Country":country,
    "Date":dt,
    "Latitude":lat,
    "Max temp in F":city_temp,
    "Longitude":lon,
    "Cloudiness":clouds,
    "Windspeed":wind,
    "Humidity":humidity
}
weather_data = pd.DataFrame(weather_dict)
weather_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Max temp in F</th>
      <th>Windspeed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lebu</td>
      <td>36</td>
      <td>ET</td>
      <td>1527287242</td>
      <td>93</td>
      <td>8.96</td>
      <td>38.73</td>
      <td>46.51</td>
      <td>2.62</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Barrow</td>
      <td>0</td>
      <td>AR</td>
      <td>1527287242</td>
      <td>46</td>
      <td>-38.31</td>
      <td>-60.23</td>
      <td>62.44</td>
      <td>13.13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albany</td>
      <td>75</td>
      <td>US</td>
      <td>1527285300</td>
      <td>26</td>
      <td>42.65</td>
      <td>-73.75</td>
      <td>84.20</td>
      <td>11.41</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Busselton</td>
      <td>92</td>
      <td>AU</td>
      <td>1527287217</td>
      <td>100</td>
      <td>-33.64</td>
      <td>115.35</td>
      <td>61.90</td>
      <td>33.82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ushuaia</td>
      <td>75</td>
      <td>AR</td>
      <td>1527285600</td>
      <td>93</td>
      <td>-54.81</td>
      <td>-68.31</td>
      <td>42.80</td>
      <td>5.82</td>
    </tr>
  </tbody>
</table>
</div>



# Showing at least 500 cities


```python
print(len(weather_data['City']))
```

    547



```python
y_temps = weather_data['Max temp in F']
x_lat = weather_data['Latitude']
Lon = weather_data['Longitude']
y_clouds = weather_data['Cloudiness']
y_wind = weather_data['Windspeed']
y_humidity = weather_data['Humidity']
```


```python
#Temperature (F) vs. Latitude
plt.scatter(x_lat, y_temps, marker="o", facecolors="blue", edgecolors="black",
            alpha=0.75)

# The y limits of our scatter plot is Temp Ranges
plt.ylim(-25, 115)

# The x limits of our scatter plot is Latitude Ranges
plt.xlim(-90, 90)

# Create a title, x label, and y label for our chart
plt.title("Temperature (F) vs. Latitude")
plt.ylabel("Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)
#showed x = 0 for where the equator is 
plt.vlines(0,-90,120, alpha=1)

plt.savefig("Temp(F)_Vs_Latitude.png")
plt.show()
```


![png](output_15_0.png)



```python
#Humidity (%) vs. Latitude
plt.scatter(x_lat, y_humidity, marker="o", facecolors="green", edgecolors="black",
            alpha=0.75)

# The y limits of our scatter plot is Humidity Ranges
plt.ylim(-5, 120)

# The x limits of our scatter plot is Latitude Ranges
plt.xlim(-90, 90)

# Create a title, x label, and y label for our chart
plt.title("Humidity(%) vs. Latitude")
plt.ylabel("Humidity(%)")
plt.xlabel("Latitude")
plt.grid(True)
#Showed y = 0 for 0% humidity 
plt.hlines(0,-90,90, alpha=0.8)
#showed y = 100 for 100% humidity (it be raining there... ;-) )
plt.hlines(100,-90,90, alpha=0.8)
#showed x = 0 for where the equator is 
plt.vlines(0,-90,120, alpha=1)

plt.savefig("Humidity(%)_Vs_Latitude.png")
plt.show()
```


![png](output_16_0.png)



```python
#Cloudiness (%) vs. Latitude
plt.scatter(x_lat, y_clouds, marker="o", facecolors="grey", edgecolors="black",
            alpha=0.75)

# The y limits of our scatter plot is Cloudines Ranges
plt.ylim(-10, 110)

# The x limits of our scatter plot is Latitude Ranges
plt.xlim(-90, 90)

# Create a title, x label, and y label for our chart
plt.title("Cloudiness(%) vs. Latitude")
plt.ylabel("Cloudiness(%)")
plt.xlabel("Latitude")
plt.grid(True)
#showed y = 0 for 0% cloudiness
plt.hlines(0,-90,90, alpha=0.8)
#showed x = 0 for where the equator is 
plt.vlines(0,-90,110, alpha=1)

plt.savefig("Cloudiness(%)_Vs_Latitude.png")
plt.show()
```


![png](output_17_0.png)



```python
#Wind Speed (mph) vs. Latitude
plt.scatter(x_lat, y_wind, marker="o", facecolors="maroon", edgecolors="black",
            alpha=0.75)

# The y limits of our scatter plot is Humidity Ranges
plt.ylim(-5, 40)

# The x limits of our scatter plot is Latitude Ranges
plt.xlim(-90, 90)

# Create a title, x label, and y label for our chart
plt.title("Wind Speed (mph) vs. Latitude")
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")
plt.grid(True)
#showed y =0 for zero wind speed as a reference 
plt.hlines(0,-90,90, alpha=0.7)
#showed x = 0 for where the equator is 
plt.vlines(0,-90,50, alpha=1)


plt.savefig("Wind Speed (mph)_Vs_Latitude.png")
plt.show()
```


![png](output_18_0.png)



```python
#Below was the beginning of the "Wrapper" method
#Needed to change in order to get the URL for each city 

#_____________________________
# settings = {"units": "imperial", "appid": api_key}

# summary = ["main.temp", "coord.lat", "coord.lon","name", "sys.country","dt","main.humidity",
#              "clouds.all","wind.speed"]
# weather_data = []
# weather_data = [ow.get_current(city, **settings)for city in cities]
# weather_data.append(weather_data)
  
#       Create a Pandas DataFrame with the results
# data = [response(*summary) for response in weather_data]
# for response in data:
#     weather_data = pd.DataFrame(data, index=city_name)
# weather_data
# column_names = ["Max Temperature in F", "Latitude", "Longitude",
#                 "City", "Country", "Date", , "Humitdity", "Cloudiness","Windspeed"]
# weather_data = pd.DataFrame(data, index=city_name, columns=column_names)
# weather_data
#_______________________

```
