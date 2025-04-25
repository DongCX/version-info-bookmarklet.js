# Version Info Bookmarklet

這是一個用於顯示網頁 CSS 樣式表版本資訊的書籤小工具（Bookmarklet）。當您在瀏覽器中點擊這個書籤時，它會在頁面右上角顯示一個浮動視窗，列出所有 CSS 樣式表的環境、服務和版本資訊。

## 功能特點

- 自動檢測頁面中的所有 CSS 樣式表
- 解析並顯示每個樣式表的：
  - 環境（Environment）
  - 服務（Service）
  - 版本（Version）
- 支援多種版本格式：
  - 純版本號：`v1.2.3`
  - 前綴-版本號：`hotfix-v1.2.3-xxx`
  - 雜湊值格式（如：a1b2c3）
- 可關閉的顯示視窗

## 安裝方法

1. 在瀏覽器中建立新的書籤
2. 名稱可以設定為「Version Info」或任何您喜歡的名稱
3. 在網址欄位中複製貼上以下程式碼：

```javascript
javascript:(function(){const l=[...document.head.querySelectorAll('link[rel="stylesheet"]')],r=/\/_s\/([^/]+)\/([^/]+)\/([^/]+)\//,s=new Set(),u=[];for(const e of l){const m=e.href.match(r);if(m){let v='';if(/^v[\d.]+$/.test(m[3]))v=m[3];else if(/^[a-z]+-v[\d.]+-[^/]+$/.test(m[3]))v=m[3].match(/^[a-z]+-v[\d.]+/)[0];else if(/^[a-f0-9]{6,}$/.test(m[3]))v=m[3];else v='未知格式';const k=`${m[1]}@${m[2]}@${v}`;if(!s.has(k)){s.add(k);u.push({s:m[1],e:m[2],v})}}}const d=document.createElement('div');Object.assign(d.style,{position:'fixed',top:'12px',right:'12px',background:'#222',color:'#fff',font:'14px monospace',padding:'12px 16px',borderRadius:'8px',zIndex:9999,boxShadow:'0 2px 6px rgba(0,0,0,0.5)',maxHeight:'60vh',overflowY:'auto',lineHeight:'1.6'});const t=document.createElement('div');t.textContent='版本資訊';Object.assign(t.style,{fontWeight:'bold',marginBottom:'8px',color:'#0f0'});d.appendChild(t);for(const i of u){const b=document.createElement('div');b.style.marginBottom='10px';b.innerHTML=`<div>環境：<span style="color:#fff">${i.e}</span></div><div>服務：<span style="color:#fff">${i.s}</span></div><div>版本：<span style="color:#fff">${i.v}</span></div>`;d.appendChild(b)}const x=document.createElement('div');x.textContent='✖';Object.assign(x.style,{position:'absolute',top:'6px',right:'10px',cursor:'pointer',color:'#f66',fontWeight:'bold'});x.onclick=()=>d.remove();d.appendChild(x);document.body.appendChild(d);})();
```

## 使用方法

1. 在任何網頁上點擊您剛才建立的書籤
2. 頁面右上角會出現一個浮動視窗，顯示所有 CSS 樣式表的版本資訊
3. 點擊右上角的「✖」按鈕可以關閉視窗

## 支援的版本格式

- 純版本號：`v1.2.3`
- 前綴-版本號：`hotfix-v1.2.3-xxx`
- 雜湊值：`a1b2c3`
- 其他格式會顯示為「未知格式」

## 注意事項

- 此工具僅支援特定格式的 CSS 樣式表路徑（包含 `/_s/` 的路徑）
- 需要允許瀏覽器執行 JavaScript
- 某些網站可能會因為內容安全策略（CSP）而限制書籤小工具的執行
