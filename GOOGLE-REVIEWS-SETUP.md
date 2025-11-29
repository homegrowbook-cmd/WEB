# Google Bewertungen - Links und Einrichtung

Diese Dokumentation erklärt die Google-Bewertungslinks auf der Website.

## Aktuelle Links

### 1. Link zu allen Google-Bewertungen (NEU)
Dieser Link öffnet direkt die Google Maps-Seite mit allen Kundenbewertungen:

```
https://www.google.com/maps/place/KERTU+Hanselmann+Frisuren/@48.7996,9.0132,17z/data=!4m8!3m7!1s0x4798c2f72f1b845d:0x967c1173c00186aa!8m2!3d48.7996!4d9.0132!9m1!1b1!16s%2Fg%2F11b5pqg8wl
```

### 2. Link zum Schreiben einer Bewertung
Dieser Link öffnet das Google-Formular für eine neue Bewertung:

```
https://search.google.com/local/writereview?placeid=ChIJXYQbL_fCmEcRqoYBwHMRfJY
```

## Place ID

Die Google Place ID für KERTU Hanselmann Frisuren ist:
```
ChIJXYQbL_fCmEcRqoYBwHMRfJY
```

## Verwendete Stellen auf der Website

Die Google-Links werden an folgenden Stellen verwendet:

### index.html
- **Reviews CTA Sektion** (nach den Bewertungskarten)
  - "Alle Bewertungen lesen" → Link zu Google Maps Reviews
  - "Bewertung schreiben" → Link zum Review-Formular

- **Social Links Sektion**
  - Google-Karte → Link zu Google Maps Reviews

- **Footer**
  - ⭐ Icon → Link zu Google Maps Reviews

### index-en.html
- **Social Section**
  - Google Reviews Karte → Link zu Google Maps Reviews

- **Footer**
  - ⭐ Icon → Link zu Google Maps Reviews

## So überprüfen Sie die Place ID

Falls Sie die Place ID überprüfen oder aktualisieren müssen:

1. Gehen Sie zum [Google Place ID Finder](https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder)
2. Suchen Sie nach "KERTU Hanselmann Frisuren, Bahnhofstraße 47, Leonberg"
3. Die Place ID wird angezeigt

## Hinweis zur Bewertungssektion

Die Bewertungen auf der Website (Maria K., Thomas H., Sandra L.) sind derzeit **Beispielbewertungen**. Um echte Google-Bewertungen anzuzeigen, gibt es folgende Optionen:

### Option 1: Manuelle Aktualisierung
Kopieren Sie echte Bewertungen von Google und aktualisieren Sie die HTML-Datei manuell.

### Option 2: Google Places API (Fortgeschritten)
Verwenden Sie die Google Places API, um Bewertungen automatisch zu laden:

```javascript
// Beispiel-Code (erfordert API-Key)
const service = new google.maps.places.PlacesService(map);
service.getDetails({
  placeId: 'ChIJXYQbL_fCmEcRqoYBwHMRfJY',
  fields: ['reviews']
}, (place, status) => {
  if (status === google.maps.places.PlacesServiceStatus.OK) {
    // place.reviews enthält die Bewertungen
  }
});
```

**Wichtig:** Die Google Places API hat Nutzungslimits und erfordert einen API-Key.

### Option 3: Drittanbieter-Widgets
Dienste wie Elfsight oder SocialPilot bieten Google-Review-Widgets an.

## Aktuelle Bewertungen (laut Recherche)

KERTU Hanselmann Frisuren hat:
- **Bewertung:** 5.0 von 5 Sternen
- **Anzahl:** 36+ Bewertungen (Stand: recherchiert)

Bitte aktualisieren Sie die Zahlen in der HTML-Datei entsprechend den aktuellen Google-Daten:

```html
<div class="google-rating-summary">
  <div class="rating-stars">⭐⭐⭐⭐⭐</div>
  <span class="rating-score">5.0</span>
  <span class="rating-count">basierend auf 36+ Bewertungen</span>
</div>
```
