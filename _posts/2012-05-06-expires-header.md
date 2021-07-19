---
id: 5
timestamp: 1336348813
author: "Matt Keller"
title: "How do you set the "Expires" HTTP header in PHP?"
exerpt: "A tiny post on how to set the Expires header, or any other header for that matter, using PHP"
---

This problem took me a while to figure out but it would seem that the best way to set the headers for a particular page is just to use the Header() function in PHP.  
  
For example by adding the lines:

```php
Header("Cache-Control: private");  
$offset = 60 * 60 * 24 * 3;  
$ExpStr = "Expires: " . gmdate("D, d M Y H:i:s", time() + $offset) . " GMT";  
Header($ExpStr)
```

to the top of functions.php, I was able to overwrite the default value for Cache-Control within the HTTP header so that it would cache private copies of the site and set the value of Expires to 3 days in the future as opposed to a couple decades in the past.  
  
Now that I understand how to do it, the more interesting problem is what settings would work for Criticrania? That's for another day though.