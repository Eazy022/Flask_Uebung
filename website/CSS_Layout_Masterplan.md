🎓 CSS Layout Tutorial: Sticky Footer + Fixe Sidebar
📋 Ziel des Projekts

Erstelle eine MyPlants-Website mit:

    Fixe Navbar rechts (immer sichtbar)

    Sticky Footer (bleibt unten, auch bei wenig Content)

    Responsive Design (funktioniert auf Mobile)

    Timeline mit Bildern unter Texten

🚀 Schritt 1: Grundproblem verstehen
Dein ursprüngliches Problem:

text
❌ body { display: grid; grid-template-rows: 1fr auto; }
❌ .navbar { position: fixed; right: 0; width: 15%; }
❌ footer { }  // Außerhalb von body!

Warum kaputt:

    position: fixed nimmt Elemente aus dem normalen Fluss

    Content läuft unter die fixe Navbar

    Footer war außerhalb des Grids → kein Sticky-Effekt

🏗️ Schritt 2: Korrekte HTML-Struktur (base.html)

xml
<body>
  <!-- 1. Fixe Navbar (AUßERHALB Grid) -->
  <nav class="navbar">...</nav>
  
  <!-- 2. Grid-Inhalt (ERSTE Grid-Zeile: 1fr) -->
  <main>
    {% block content %}{% endblock %}
  </main>
  
  <!-- 3. Footer (ZWEITE Grid-Zeile: auto) -->
  <footer>...</footer>
</body>

🔑 Schlüssel:

text
body { grid-template-rows: 1fr auto; }
          ↑↑↑
       main | footer

🎨 Schritt 3: CSS Grid für Sticky Footer

css
html, body { height: 100%; margin: 0; }

body {
  display: grid;
  grid-template-rows: 1fr auto;  /* Magie hier! */
  min-height: 100vh;             /* Voller Screen */
}

Wie es funktioniert:

text
Kurzer Content:       Langer Content:
┌─────────────────┐   ┌─────────────────┐
│     main        │   │     main        │
│  (streckt sich) │   │  (füllt Platz)  │
│                 │   │                 │
├─────────────────┤   ├─────────────────┤
│     footer      │   │     footer      │
└─────────────────┘   └─────────────────┘

⚡ Schritt 4: Fixe Navbar + Content-Anpassung

css
.navbar {
  position: fixed;  /* Nimmt sich aus Grid raus */
  right: 0;
  width: 15%;
  height: 100vh;
}

main {
  padding-right: 15%;  /* ← Platzhalter! */
}

Vorher: Content läuft unter Navbar
Nachher: Content scrollt NEBEN Navbar

text
┌──────────────┬───┐
│     main     │ N │  ← Navbar OVERLAY
│ (padding-r:  │ a │
│   15%)       │ v │
├──────────────┼───┤
│    footer    │ b │
└──────────────┴───┘

📱 Schritt 5: Responsive (Navbar bleibt fix!)

css
@media (max-width: 768px) {
  .navbar { width: 80px; }     /* Schmaler */
  main { padding-right: 80px; } /* Angepasst */
}

Navbar bleibt FIXED, wird nur schmaler!
🖼️ Schritt 6: Timeline (Text + Bild untereinander)
Vorher (falsch):

text
Tag 1  Tag 15  Tag 30  ← Alle Texte nebeneinander
[Bild] [Bild]         ← Alle Bilder irgendwo

Nachher (richtig):

xml
<div class="timeline-item">
  <p>Tag 1: Keimung</p>  ← Oben
  <img>                  ← Unten
</div>

css
.timeline-item {
  flex-direction: column;  /* Vertikal stapeln */
  align-items: center;     /* Zentrieren */
}

Ergebnis:

text
[Tag 1]    [Tag 15]   [Tag 30]
 [Bild]     [Bild]     [Bild]

🔧 Schritt 7: Vollständige Lösung (Copy-Paste)
1. base.html Struktur:

xml
<body>
  <nav class="navbar">...</nav>
  <main>{% block content %}</main>
  <footer>...</footer>
</body>

2. CSS Schlüsselregeln:

css
body {
  display: grid;
  grid-template-rows: 1fr auto;
  min-height: 100vh;
}

.navbar { position: fixed; right: 0; width: 15%; }
main { padding-right: 15%; }

3. Timeline HTML + CSS:

xml
<div class="timeline-item">
  <p>Text</p><img>
</div>

✅ Checklist - Was gelernt:

    Grid 1fr auto = Sticky Footer

    position: fixed nimmt aus Fluss

    padding-right = Platzhalter für fixe Elemente

    flex-direction: column = Text über Bild

    min-height: 100vh = Voller Viewport

🚀 Teste es:

    Kopiere CSS in css_Styles.css

    Passe base.html an (main + footer position)

    Nutze neues Timeline-Template

    Resize Browser → Navbar bleibt fix!

💡 Tipp: Öffne DevTools (F12) → Elements → siehst du das Grid live!

