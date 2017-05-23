# Sprint2
Sprint 2 de ESOF
#! python3

#Capitulo 11 Project
import requests
import os
import bs4

url = 'http://xkcd.com' 
os.makedirs('xkcd', exist_ok=True)  

while not url.endswith('#'):
    #Download the page
    print('Baixando a página %s...' % url)
    res = requests.get(url)
    res.raise_for_status()

    soup = bs4.BeautifulSoup(res.text)
    comicElem = soup.select('#comic img')
    if comicElem == []:
        print('Nao foi possível encontrar a imagem.')
    else:
        comicUrl = 'http:' + comicElem[0].get('src')
        # Download the image
        print('Baixando a imagem %s...' % (comicUrl))
        res = requests.get(comicUrl)
        res.raise_for_status()
        imageFile = open(os.path.join('xkcd', os.path.basename(comicUrl)), 'wb')
        for chunk in res.iter_content(100000):
            imageFile.write(chunk)
        imageFile.close()

    #Get the Prev button's url.
    prevLink = soup.select('a[rel="prev"]')[0]
    url = 'http://xkcd.com' + prevLink.get('href')

print('Conluido.')

