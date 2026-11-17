# Reading ticket order from a Pylon view

Use this when the owner wants a section of a browser view worked in its on-screen order. The list is virtualized, ordered by the view (not by ticket number) and split into sections. Script output that contains URLs gets blocked, so keep results in `window.__seq` and return only numbers.

Run in the view tab:

```js
const rows=[...document.querySelectorAll('[role=row], tr')];
const row=rows.find(e=>/#\d{4,6}/.test(e.innerText));
if(!row) throw new Error('no ticket rows found: is the view open and loaded?');
let c=row; while(c&&!(c.scrollHeight>c.clientHeight+50&&getComputedStyle(c).overflowY!='visible')) c=c.parentElement;
c.scrollTop=0; const out=[]; const seen=new Set();
for(let k=0;k<80;k++){            // raise 80 if the last header (==Closed) isn't reached
  await new Promise(r=>requestAnimationFrame(()=>setTimeout(r,200)));
  [...document.querySelectorAll('[role=row], tr, [class*=group], [class*=section]')].forEach(e=>{
    const t=e.innerText.replace(/\s+/g,' ').trim();
    const m=t.match(/^#(\d{4,6})/); const h=t.match(/^(New|On you|On customer|On hold|Closed)\s*\d+$/);
    const key=m?m[1]:(h?h[0]:null);
    if(key&&!seen.has(key)){seen.add(key); out.push(m?m[1]:'=='+h[0]);}
  });
  if(c.scrollTop+c.clientHeight>=c.scrollHeight-5) break;
  c.scrollTop+=350;
}
window.__seq=out; out.filter(x=>x.startsWith('==')).join(' | ')
```

Then slice out the section and find your place in it (replace the section name and ticket number):

```js
const o=window.__seq, S='==New';   // or '==On you', '==On customer'
const a=o.findIndex(x=>x.startsWith(S)), b=o.findIndex((x,i)=>i>a&&x.startsWith('=='));
const n=a<0?[]:o.slice(a+1,b<0?o.length:b), i=n.indexOf('TICKET');
a<0?'section '+S+' not found: rescan or ask':i<0?'ticket not in section':'idx '+i+'\n'+n.slice(Math.max(0,i-15),i+1).join(' ')
```

- **Up** is the previous entry, `n[i-1]`, towards the top of the section. **Down** is `n[i+1]`. **Random** is a random entry of `n`.
- Replied tickets move to another section, so carry on from the stored list. Scan again after the owner scrolls or reloads. If unsure of the next ticket, ask.
