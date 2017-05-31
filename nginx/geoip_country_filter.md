# nginx geo ip filter

Install `nginx geoip-database libgeoip1`

Add country code map to `/etc/nginx/nginx.conf` inside `http`

```
http {
  ...

  geoip_country /usr/share/GeoIP/GeoIP.dat;

  map $geoip_country_code $allowed_country {
    default no;
    FI yes;
  }

  ...
}
```

Add returning 444 if country is not allowed. This goes to to config inside
server
```
server {
  ...

  if ($allowed_country = no) {
    return 444;
  }

  ...
}
```
