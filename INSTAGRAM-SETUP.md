# Instagram Posts Integration - Anleitung

Diese Anleitung erklärt, wie Sie echte Instagram-Beiträge auf der Website anzeigen können.

## Aktuelle Situation

Die Instagram-Slider-Sektion auf `index.html` (Zeilen 329-416) zeigt derzeit Platzhalter ("📸 Beitrag 1", etc.). Um echte Instagram-Posts anzuzeigen, gibt es mehrere Optionen:

---

## Option 1: Manuelle Aktualisierung (Empfohlen für den Anfang)

Dies ist die einfachste Methode ohne technische Komplexität:

1. **Gehen Sie zu Ihrem Instagram-Profil** (@kertuhanselmann)
2. **Kopieren Sie die Bild-URLs** Ihrer neuesten Beiträge
3. **Ersetzen Sie die Platzhalter** in `index.html`:

```html
<div class="instagram-slide">
  <a href="https://www.instagram.com/p/POST_ID/" target="_blank" rel="noopener">
    <div class="instagram-post">
      <div class="instagram-post-image">
        <img src="BILD_URL_HIER" alt="Instagram Post Beschreibung" loading="lazy">
      </div>
      <div class="instagram-post-info">
        <span class="instagram-likes">❤️ 124</span>
        <span class="instagram-comments">💬 8</span>
      </div>
    </div>
  </a>
</div>
```

**Vorteile:**
- Keine API-Einrichtung erforderlich
- Volle Kontrolle über angezeigte Inhalte
- Kein monatliches Limit

**Nachteile:**
- Muss manuell aktualisiert werden, wenn neue Posts erscheinen

---

## Option 2: Instagram Basic Display API (Automatisch)

Für automatische Aktualisierung der Instagram-Posts:

### Schritt 1: Facebook Developer Account erstellen
1. Gehen Sie zu [developers.facebook.com](https://developers.facebook.com)
2. Erstellen Sie einen Developer Account
3. Erstellen Sie eine neue App

### Schritt 2: Instagram Basic Display API einrichten
1. In Ihrer App, fügen Sie "Instagram Basic Display" hinzu
2. Fügen Sie Ihren Instagram-Account als Test-User hinzu
3. Generieren Sie einen Access Token

### Schritt 3: JavaScript-Code für automatische Posts

Fügen Sie diesen Code in `index.html` vor dem schließenden `</body>` Tag ein:

```javascript
// Instagram Feed laden
async function loadInstagramFeed() {
  const accessToken = 'IHR_ACCESS_TOKEN_HIER';
  const userId = 'IHRE_USER_ID_HIER';
  const limit = 6; // Anzahl der Posts
  
  try {
    const response = await fetch(
      `https://graph.instagram.com/${userId}/media?fields=id,caption,media_type,media_url,permalink,thumbnail_url&access_token=${accessToken}&limit=${limit}`
    );
    const data = await response.json();
    
    const slider = document.getElementById('instagramSlider');
    slider.innerHTML = '';
    
    data.data.forEach(post => {
      const imageUrl = post.media_type === 'VIDEO' ? post.thumbnail_url : post.media_url;
      const slide = `
        <div class="instagram-slide">
          <a href="${post.permalink}" target="_blank" rel="noopener">
            <div class="instagram-post">
              <div class="instagram-post-image">
                <img src="${imageUrl}" alt="${post.caption?.substring(0, 50) || 'Instagram Post'}" loading="lazy">
              </div>
            </div>
          </a>
        </div>
      `;
      slider.innerHTML += slide;
    });
  } catch (error) {
    console.error('Fehler beim Laden der Instagram-Posts:', error);
  }
}

document.addEventListener('DOMContentLoaded', loadInstagramFeed);
```

**Wichtig:** Access Tokens laufen nach 60 Tagen ab und müssen erneuert werden!

---

## Option 3: Instagram Embed Widget (Einfach)

Instagram bietet eine offizielle Embed-Funktion:

1. Gehen Sie zu einem Instagram-Post
2. Klicken Sie auf "..." → "Einbetten"
3. Kopieren Sie den Embed-Code
4. Fügen Sie ihn in Ihre Website ein

```html
<blockquote class="instagram-media" data-instgrm-captioned 
  data-instgrm-permalink="https://www.instagram.com/p/POST_ID/"
  data-instgrm-version="14">
</blockquote>
<script async src="//www.instagram.com/embed.js"></script>
```

---

## Option 4: Drittanbieter-Widgets

Es gibt kostenpflichtige und kostenlose Dienste:

- **Elfsight** (elfsight.com) - Kostenpflichtig, einfach zu integrieren
- **SnapWidget** (snapwidget.com) - Kostenlose Basisversion
- **LightWidget** (lightwidget.com) - Einfach, responsive

Diese Dienste generieren einen Embed-Code, den Sie in Ihre Website einfügen können.

---

## Empfehlung

Für KERTU Hanselmann Frisuren empfehle ich:

1. **Kurzfristig:** Option 1 (Manuelle Aktualisierung) - Schnell umzusetzen
2. **Langfristig:** Option 2 (Instagram API) - Automatische Updates

Wenn Sie Hilfe bei der Einrichtung benötigen, wenden Sie sich an Ihren Webentwickler.

---

## CSS für Instagram-Bilder

Fügen Sie folgendes CSS hinzu, wenn Sie echte Bilder anstelle von Platzhaltern verwenden:

```css
.instagram-post-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.instagram-post:hover img {
  transform: scale(1.05);
}
```

---

## Kontakt

Bei Fragen zur Implementierung wenden Sie sich bitte an den Webentwickler oder erstellen Sie ein Issue im Repository.
