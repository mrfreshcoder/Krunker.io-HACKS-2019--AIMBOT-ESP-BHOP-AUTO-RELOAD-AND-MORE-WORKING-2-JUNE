/// ==UserScript==
// @name         Krunker.io HACKS 2019 - AIMBOT, ESP, BHOP, AUTO RELOAD AND MORE | WORKING 2 JUNE |
// @version      1.5
// @author       mr.freshcoder
// @include       /^(https?:\/\/)?(www\.)?(.+)krunker\.io(|\/|\/\?(game|server|party)=.+)$/
// @include      https://krunker.io
// @grant        GM_xmlhttpRequest
// @run-at       document-start
// @require      https://code.jquery.com/jquery-3.3.1.min.js
// @namespace    mr.freshcoder
// @description  Krunker.io HACKS 2019 - AIMBOT, ESP, BHOP, AUTO RELOAD AND MORE | WORKING 1 JUNE | Best Krunker.io HACKS 2019 |
// ==/UserScript==

window.stop();
document.innerHTML = "";

// * * * * * * * * * * * * * * * *
// * * * * * * * * * * * * * * * *

const version = '1.2'

// * * * * * * * * * * * * * * * *
// * * * * * * * * * * * * * * * *

GM_xmlhttpRequest({
    method: "GET",
    url: document.location.origin,
    onload: res => {
        let html = res.responseText;
        html = html.replace(/game\.[^\.]+\.js/, '____.js');
        html = html.replace(/<script data-cfasync(.|\s)*?<\/script>/, `<meta name="gpy_version" content="${version}">`);
        GM_xmlhttpRequest({
            method: "GET",
            url: document.location.origin + '/libs/zip.js',
            onload: res => {
                let zip = res.responseText;
                zip = zip.replace(/document\..+<\/div>"\)/, '');

                html = html.replace(/<script src="libs\/zip\.js.+"><\/script>/, `<script>${zip}</script>`);
                html += '<script src="https://raw.githack.com/gpy-dev/krunker/master/bypass.js"></script>';
                html += '<script src="https://raw.githack.com/gpy-dev/krunker/master/haxy.js"></script>';
                html += '<script src="https://raw.githack.com/gpy-dev/krunker/master/game.js"></script>';

                document.open();
                document.write(html);
                document.close();
            }
        })
    }
})
