# How To Fetch the Entire Website by wget

## Cookies

Export cookies from Chrome by plugin **cookies.txt**

Example:

```
# HTTP Cookie File for example.com by Genuinous @genuinous.
# To download cookies for this tab click here, or download all cookies.
# Usage Examples:
#   1) wget -x --load-cookies cookies.txt "https://member.example.com/"
#   2) curl --cookie cookies.txt "https://member.example.com/"
#   3) aria2c --load-cookies cookies.txt "https://member.example.com/"
#
.example.com	TRUE	/	FALSE	1640964446	_ga	GA1.2.1271829432.1577757941
.example.com	TRUE	/	FALSE	1577978846	_gid	GA1.2.351792664.1577883043
```

## Fetch

`wget --load-cookies=cookie.txt -t0 -r -p -np -k -E -l2 https://www.website.com/`

- -t0  --> Retry Inf
- -r    -->  Recursive download
- -p   -->  Get all images, etc. needed to display HTML page
- -np  --> Don't ascend to the parent directory
- -k   --> Equal to --convert-links, make links in downloaded HTML point to local files
- -E   -->  Auto amend extension (remove `?` after css/js files)
