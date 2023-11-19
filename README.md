# The F1 Paddock
A simple and responsive web app that serves Formula 1 driver information. Created by Sean Bernardo.

## APIs and Frameworks used
1. **Vue.js** - [link](https://vuejs.org/)
2. **Ergast Motor Racing Developer API** - [link](http://ergast.com/mrd)
3. **Wikipedia API** - [link](https://www.mediawiki.org/wiki/API:Main_page)

## Other Third-party Resources Used

1. **Formula 1**  
   1.1 Logo retrieved from Wikipedia - [link](https://en.m.wikipedia.org/wiki/File:F1.svg)  
   1.2 Font retrieved from the F1 website - [font download link](https://www.formula1.com/etc/designs/fom-website/fonts/F1Regular/Formula1-Regular.ttf)  
2. **Emojipedia** for the racecar favicon - [link](https://emojipedia.org/racing-car)
3. **Flagpedia.net** for driver's national flags - [link](https://flagpedia.net/download/api)

## Known Limitations
### Ergast API related
- The Ergast API is currently deprecated and will be unusable past the 2024 season.
- Driver information does not directly contain all-time stats (race wins, championships, etc.), and constructor/team at the time.
### Wikipedia API related
- Pictures of drivers depend on the existence of one in their respective Wikipedia articles.
- There are some instances where a slight difference in the driver's name that causes their article to not be pulled up. Example: Albon's Wikipedia article from the API is `http://en.wikipedia.org/wiki/Alexander_Albon` and not `https://en.wikipedia.org/wiki/Alex_Albon`. On Wikipedia it resolves to Alex Albon correctly, however, his photo does not show up from the API.
- Due to the non-standard sizes of driver photos, some driver cards will appear very differently.

## Big Disclaimer
I only started learning Vue for the purpose of the application assessment, and the code is - *admittedly* - very rough, but at least it works.
