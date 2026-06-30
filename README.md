# SearXNG-Google-Theme
SearXNG Google Homepgae

# Autoinstall
```bash
git clone https://github.com/Steinperfer/SearXNG-Google-Homepgae.git /tmp/sx && sudo mkdir -p /var/lib/searxng/venv/lib/python3.14/site-packages/searx/templates/simple/result_templates && sudo cp /tmp/sx/{categories.html,ACTIVATE-AI.txt,index.html,macros.html,search.html} /var/lib/searxng/venv/lib/python3.14/site-packages/searx/templates/simple/ && sudo cp /tmp/sx/images.html /var/lib/searxng/venv/lib/python3.14/site-packages/searx/templates/simple/result_templates/ && rm -rf /tmp/sx && sudo systemctl restart searxng
```  
  

<img width="2559" height="1325" alt="sear" src="https://github.com/user-attachments/assets/e539c3bd-7b73-4282-bb65-feed377778c9" />   
  

<img width="2559" height="1325" alt="Bildschirmfoto_20260612_183403" src="https://github.com/user-attachments/assets/ad556e6b-4964-433b-9baa-fd78e2496939" />  
  
# Leftclick 5sec on the shortcut to delete it  
    
<img width="1432" height="827" alt="Bildschirmfoto_20260612_183908" src="https://github.com/user-attachments/assets/83a17b4b-a19a-496d-aaea-fe529f698d8c" />  
  
"this will be in english"  
  
<img width="396" height="223" alt="Bildschirmfoto_20260615_083225" src="https://github.com/user-attachments/assets/dbc1fdea-5d93-4261-8bb6-10494350f9bb" />  
  
# Leftclick "AI" for 10sec to remove it forever, 
can be reversed by typing this in the browser console
```
localStorage.removeItem('ai_tab_hidden')
```  
# Or change the 1 to a 0 in "ACTIVATE-AI.txt"  
Normally, Google AI opens in a new tab—using the content you searched for.  
In ACTIVATE-AI.txt you can also remove the # from the URL; Then Claude will open instead.  
You can use any URL you like; a new window will simply open .  

   
<img width="2559" height="1396" alt="Bildschirmfoto_20260615_083202" src="https://github.com/user-attachments/assets/7e90b9af-391b-43fc-8f34-9fbed515fc0d" />
    
<img width="2559" height="1393" alt="Bildschirmfoto_20260615_083134" src="https://github.com/user-attachments/assets/77e583a5-3964-4fbd-8d5f-6da8a5eb0d7b" />


# Manuel Installation,
# you need to move 5 of 6 files to this path:  
```
/usr/local/searxng/searxng-src/searx/templates/simple/
```
```
categories.html
ACTIVATE-AI.txt
index.html
macros.html
search.html
```

# An images.html in the result-templates folder
```
/usr/local/searxng/searxng-src/searx/templates/simple/result_templates/
```
```
images.html
```
# now just restart SearXNG
```
sudo systemctl restart searxng
```
