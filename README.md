# [almalinux-bernini-nginx](#)

[almalinux-bernini-nginx](https://github.com/Vasak-Group/almalinux-bernini-nginx) is [NGINX](https://www.nginx.com/) [autoindex](https://nginx.org/en/docs/http/ngx_http_autoindex_module.html) redux.

A pretty but simple autoindex for Nginx without the fancy index module.
It will read up the content from a NGINX folder and create a pretty HTML5 table to browse it
with column sort and filter.

It uses a minimal CSS library and [vanilla JavaScript](http://vanilla-js.com/) for resources wise performance.

# Install

clone this repo to your server and point your NGINX to the folder.

```bash
git clone https://github.com/Vasak-Group/almalinux-bernini-nginx.git
```

and set configs in the NGINX server block

```nginx
server {
    listen 80;
    autoindex on;
    server_name your.domain.vsk; # Your domain

    # Send the data in JSON
    autoindex_format json;
    addition_types application/json;

    # Calling from SERVERNAME/almalinux-bernini-nginx/*
    add_before_body /almalinux-bernini-nginx/header.html;
    add_after_body /almalinux-bernini-nginx/footer.html;

    # Need to tell that we are sending HTML
    add_header Content-Type text/html;
}
```

# CSS libraries and themes

It is tested and works with the followings CSS libraries:

- [Default style sheet for HTML 5](https://html.spec.whatwg.org/multipage/rendering.html#phrasing-content-3) - No CSS library at all
- [Milligram.io](https://milligram.io/) + [Normalize](https://necolas.github.io/normalize.css/) - A minimalist CSS framework **(Default)**
- [Min](https://mincss.com/) - The world's smallest CSS framework
- [Normalize](https://necolas.github.io/normalize.css/) - A modern, HTML5-ready alternative to CSS resets
- [Picnic CSS](https://picnicss.com/) - Lightweight and beautiful library
- [sscaffold](https://sscaffold-css.com/) - Lightweight css for people who build things
- [Color themes](https://cdn.jsdelivr.net/npm/milligram-themes@0.0.2/) - Milligram-themes (works with all CSS libraries above)

\* You can uncomment any of then at the top of header.html (\<head\>).

# How it works

1. The nginx autoindex module delivers the folder content in JSON format (autoindex_format json) with header.html at the beginning and footer.html at the end of the output
2. The downloaded JSON will end up inside a hidden DIV as text, without any AJAX call (add_header Content-Type text/html)
3. When the download is done, the JSON is read and parsed by JavaScript
4. The table with the server folder content is then build and the loading CSS animation is closed

# Screenshots

**almalinux-bernini-nginx is based on NGINdeX.io**

- [StrapIndex](https://github.com/EthraZa/NGINdeX.io/tree/nginx-autoindex) - Bootstrap version that is based on
  - [ccarney16/nginx-autoindex](https://github.com/ccarney16/nginx-autoindex) - A fancier autoindex for nginx (without the fancy index module!)
