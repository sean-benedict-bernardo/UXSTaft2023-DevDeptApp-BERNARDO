# The F1 Paddock
A web-app created by Sean Bernardo
## APIs and Frameworks used
1. **Vue.js** - (https://vuejs.org/)
2. **Ergast Motor Racing Developer API** - (link)[http://ergast.com/mrd]
3. **Wikipedia API** - (link)[https://www.mediawiki.org/wiki/API:Main_page]

## Other Third-party Resources
**Emojipedia** for the racecar favicon - [link](https://emojipedia.org/racing-car)

## Known Limitations
### Ergast API related
- The Ergast API is currently deprecated and will be unusable past the 2024 season
- Driver information does not directly contain all-time stats (race wins, championships, etc.), and constructor/team at the time
### Wikipedia API related
- Pictures of drivers depends on the existance of one in their respective Wikipedia articles
- There are some instances where a slight difference in the driver's name (Example: Albon's wikipedia article from the API is `Alexander Albon` and not `Alex Albon` hence his photo does not show up)

## Big Disclaimer
I only started learning Vue for the purpose of the application assessment. The code is - *admittedly* - very rough, but at least it works.
I wanted to implement more such as race circuit information