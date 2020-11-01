# Using GitHub for Comments System

This repository only used Proof of Concept (PoC) how to implements a comments system using GitHub issues. This is alternative for other comments system such as Disqus etc.

Article for this PoC are written in Bahasa Indonesia and can be found at https://teknocerdas.com/.

## Example

HTML anda Javascript below will parse Issue #1 of this repository.

```html
<!DOCTYPE html>
<html>
<head>
  <title>GitHub Comments for Static Website</title>
</head>
<body>
<div id="poc-github-comments" style="margin-top: 24px; box-sizing: border-box; background-color: white; font-size: 16px;">Memuat komentar...</div>

<script>
function doCORSRequest(corsUrl) {
    var corsApiUrl = 'https://cors-anywhere.herokuapp.com/';
    var http = new XMLHttpRequest();
    http.open('GET', corsApiUrl + corsUrl);
    http.responseType = 'document';
    http.onload = function() {
        var nodes = this.responseXML.querySelectorAll("div.timeline-comment-group");
        var commentAuthor, commentTime, commentBody;
        var commentsHTML = '';
        var loopCount = Math.min(10, nodes.length);

        for (var i=1; i<loopCount; i++) {
            commentAuthor = nodes[i].querySelector('a.author').innerText;
            commentTime = nodes[i].querySelector('a.js-timestamp').innerText;
            commentBody = nodes[i].querySelector('td.js-comment-body').innerText.trim().replace(/[\r\n]{2,}/g, '<br><br>').replace(/[\r\n]/g, '<br>');
            // console.log([commentAuthor, commentTime, commentBody]);

            commentsHTML += '<div class="comment-item" style="width:100%; border: 1px solid #f1f1f1; box-sizing: border-box; border-radius: 6px; background-color: #f1f1f1; margin-bottom: 18px;"><div class="comment-header" style="padding: 10px 8px;"><strong>' + commentAuthor + '</strong> berkomentar pada ' + commentTime + '</div><div class="comment-body" style="padding: 12px 8px; background-color: white;">' + commentBody + '</div></div>';
        }

        commentsHTML += '<div style="margin-top: 18px; text-align: center;"><a href="'+ corsUrl + '">Lihat semua komentar | Kirim komentar pada GitHub</a></div>';

        document.getElementById('poc-github-comments').innerHTML = commentsHTML;
    }
    http.send();
}

// Get the comments
doCORSRequest('https://github.com/rioastamal-examples/teknocerdas-github-comments/issues/1');
</script>
</body>
</html>
```

Try copy-paste code above in online HTML editor such as [https://rioastamal.net/html-editor/](https://rioastamal.net/html-editor/).
