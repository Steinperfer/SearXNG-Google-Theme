# SearXNG-Google-Homepgae
SearXNG Google Homepgae

<img width="2559" height="1325" alt="sear" src="https://github.com/user-attachments/assets/e539c3bd-7b73-4282-bb65-feed377778c9" />  
press 5sec on the shortcut to delete it  
<img width="2559" height="1325" alt="Bildschirmfoto_20260612_183403" src="https://github.com/user-attachments/assets/ad556e6b-4964-433b-9baa-fd78e2496939" />

```bash
#goto
sudo nano /usr/local/searxng/searxng-src/searx/templates/simple/index.html
```  
Paste this

```bash
{% extends "simple/base.html" %}
{% from 'simple/icons.html' import icon_big %}

{% block content %}
<style>
    /* Allgemeiner Hintergrund */
    body, html, #main_index, #index, #main_results, .wrapper {
        background-color: #383838 !important;
        background: #383838 !important;
    }

    /* Alle Container im Suchkopf transparent halten */
    #search, #search_header, #search_view, .search_filters {
        background-color: transparent !important;
        background: transparent !important;
        border-color: transparent !important;
    }

    /* Nur die eigentliche Suchbox wird weiß gefärbt */
    .search_box {
        background-color: #fdfdfd !important;
        background: #fdfdfd !important;
        border: 1px solid #fdfdfd !important;
        border-radius: 24px !important;
    }

    /* Autocomplete-Box wird erst weiß, wenn sie aktiv eingeblendet wird */
    .autocomplete[style*="display: block"], .autocomplete ul {
        background-color: #fdfdfd !important;
        background: #fdfdfd !important;
        border-color: #fdfdfd !important;
    }

    /* Textfarbe von dem, was man in die Suchleiste eintippt */
    #q {
        color: #474747 !important;
        background-color: transparent !important;
        background: transparent !important;
    }

    /* Hintergrund für Löschen- und Suchen-Buttons weiß erzwingen */
    #clear_search, #send_search, button[type="reset"], button[type="submit"] {
        background-color: #fdfdfd !important;
        background: #fdfdfd !important;
        border: none !important;
    }

    /* Suchbar-Buttons (Kreuz und Lupe) im originalen Google-Grau */
    #clear_search svg, #send_search svg, #clear_search span, #send_search span {
        fill: #70757a !important;
        color: #70757a !important;
    }

    /* Schriftfarbe des Platzhalters (was immer da steht, wenn leer) */
    #q::placeholder {
        color: #606268 !important;
        opacity: 1 !important;
    }

    /* Textfarbe der Suchvorschläge, wenn sie sich aufklappen */
    .autocomplete ul li, .autocomplete_selected, .autocomplete ul li a {
        color: #060606 !important;
    }

    /* Farbe des ausgewählten Feldes bei den Suchvorschlägen */
    .autocomplete ul li:hover, 
    .autocomplete ul li.autocomplete_selected,
    .autocomplete ul li:active {
        background-color: #e8e8e8 !important;
        background: #e8e8e8 !important;
    }
</style>

<div class="index">
    <div class="title"><h1>SearXNG</h1></div>
    {% include 'simple/simple_search.html' %}
</div>

<!-- Google-Style Shortcuts Grid -->
<div id="shortcut-grid" style="display: flex; justify-content: center; gap: 24px; margin-top: 35px; flex-wrap: wrap; font-family: arial, sans-serif; max-width: 600px; margin-left: auto; margin-right: auto; -webkit-user-select: none; user-select: none;">
    <!-- Die 6 Shortcuts werden hier geladen -->
</div>

<script>
function initShortcuts() {
    const grid = document.getElementById('shortcut-grid');
    grid.innerHTML = '';
    
    let saved = JSON.parse(localStorage.getItem('searxng_home_shortcuts')) || [];
    
    for (let i = 0; i < 6; i++) {
        const item = saved[i];
        const tile = document.createElement('div');
        tile.style = "display: flex; flex-direction: column; align-items: center; width: 75px; position: relative;";
        
        if (item && item.url) {
            // Deine funktionierende Codezeile für die absolut saubere Domain
            let cleanDomain = item.url.replace(/^(https?:\/\/)?(www\.)?/i, '').split('/')[0];
            
            // Verknüpft die korrekte Domain direkt mit der Google-Schnittstelle
            const iconUrl = "https://www.google.com/s2/favicons?sz=256&domain=" + cleanDomain;
            
            tile.innerHTML = `
                <a href="${item.url}" id="link-${i}" style="text-decoration: none; display: flex; flex-direction: column; align-items: center; -webkit-user-drag: none;">
                    <div class="icon-bg" style="width: 48px; height: 48px; border-radius: 50%; background-color: #2e2e2e; display: flex; align-items: center; justify-content: center; margin-bottom: 6px; transition: background 0.1s;">
                        <img src="${iconUrl}" style="width: 24px; height: 24px; object-fit: contain; pointer-events: none;" onerror="this.src='data:image/svg+xml;utf8,<svg xmlns=%22http://w3.org viewBox=%220 0 24 24%22 fill=%22%23f8f8f8%22><path d=%22M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1 17.93c-3.95-.49-7-3.85-7-7.93 0-.62.08-1.21.21-1.79L9 15v1c0 1.1.9 2 2 2v1.93zm6.9-2.53c-.26-.81-1-1.4-1.9-1.4h-1v-3c0-.55-.45-1-1-1h-6v-2h2c.55 0 1-.45 1-1V7h2c1.1 0 2-.9 2-2v-.41c2.93 1.19 5 4.06 5 7.41 0 2.08-.8 3.97-2.1 5.39z%22/></svg>'">
                    </div>
                    <span style="font-size: 12px; color: #f8f8f8; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; max-width: 75px; text-align: center;">${item.name}</span>
                </a>
            `;
            
            const linkEl = tile.querySelector(`#link-${i}`);
            let pressTimer;
            let isLongPress = false;
            
            // Exakt 5 Sekunden gedrückt halten bringt das Bestätigungsfenster
            const startPress = (e) => {
                isLongPress = false;
                pressTimer = setTimeout(() => {
                    isLongPress = true;
                    if (confirm(`Möchtest du den Shortcut "${item.name}" wirklich löschen?`)) {
                        clearTile(i);
                    }
                }, 5000); 
            };
            
            const clickCheck = (e) => {
                if (isLongPress) {
                    e.preventDefault();
                }
                clearTimeout(pressTimer);
            };
            
            const cancelPress = () => {
                clearTimeout(pressTimer);
            };
            
            linkEl.addEventListener('mousedown', startPress);
            linkEl.addEventListener('touchstart', startPress, {passive: true});
            linkEl.addEventListener('click', clickCheck);
            linkEl.addEventListener('mouseup', cancelPress);
            linkEl.addEventListener('mouseleave', cancelPress);
            linkEl.addEventListener('touchend', cancelPress);
            
        } else {
            tile.innerHTML = `
                <div onclick="editTile(${i})" class="icon-bg" style="width: 48px; height: 48px; border-radius: 50%; background-color: #2e2e2e; border: 1px dashed #606268; display: flex; align-items: center; justify-content: center; margin-bottom: 6px; cursor: pointer; color: #f8f8f8; font-size: 20px; font-weight: bold; transition: background 0.1s;">
                    +
                </div>
                <span style="font-size: 11px; color: #f8f8f8; white-space: nowrap;">Hinzufügen</span>
            `;
        }
        grid.appendChild(tile);
    }
    
    document.querySelectorAll('.icon-bg').forEach(el => {
        el.addEventListener('mouseenter', () => el.style.backgroundColor = '#404040');
        el.addEventListener('mouseleave', () => el.style.backgroundColor = '#2e2e2e');
    });
}

function editTile(index) {
    let url = prompt("Website-URL eingeben (z.B. youtube.com):");
    if (!url) return;
    
    let name = prompt("Name für den Shortcut eingeben:");
    if (!name) return;
    
    if (!/^https?:\/\//i.test(url)) {
        url = 'https://' + url;
    }
    
    let saved = JSON.parse(localStorage.getItem('searxng_home_shortcuts')) || [];
    saved[index] = { name: name, url: url };
    localStorage.setItem('searxng_home_shortcuts', JSON.stringify(saved));
    
    initShortcuts();
}

function clearTile(index) {
    let saved = JSON.parse(localStorage.getItem('searxng_home_shortcuts')) || [];
    saved[index] = null;
    localStorage.setItem('searxng_home_shortcuts', JSON.stringify(saved));
    initShortcuts();
}

document.addEventListener("DOMContentLoaded", initShortcuts);
</script>
{% endblock %}
```
