---
title: 'Email link helper'
author: Dave Easton, Karthik Sundaram
date: 2023-10-04
layout: post
---

# Prepare Email link for Gmail integration with Webex CC

<!DOCTYPE html>

<body>
<textarea id="jsonETL" style="width: 1352px; height: 96px;">Enter copied text here</textarea>
<button onclick="update()">Get URL</button>
<script>
    function update(){
        x = JSON.parse(document.getElementById("jsonETL").value);
        document.getElementById("jsonETL").value = x["email.message"].replaceAll("\\r\\n","\r\n").replaceAll("\\/","/").substring(x["email.message"].replaceAll("\\r\\n","\r\n").replaceAll("\\/","/").search("http"),x["email.message"].replaceAll("\\r\\n","\r\n").replaceAll("\\/","/").search("Ifyouclick|If you click")).trim()
    }
</script>
</body>

</html>