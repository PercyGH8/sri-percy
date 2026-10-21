# Estadísticas del Servidor Web (Nginx)

### 1. Número total de peticiones
```bash
wc -l /var/log/nginx/access.log

# 1. Total de peticiones
wc -l /var/log/nginx/access.log

# 2. Las 5 IP con más peticiones
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head -n 5

# 3. Respuestas por código HTTP
awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c

# 4. Rutas que dan 404
awk '($9 == 404) {print $7}' /var/log/nginx/access.log | sort | uniq -c | sort -nr

# 5. Hora del día con más peticiones
awk -F'[:[]' '{print $2}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head -n 5
69 /var/log/nginx/access.log
     32 81.9.192.66
      6 31.221.251.177
      4 127.0.0.1
      4 113.31.186.197
      3 10.6.1.216
     30 200
      5 304
      2 400
      7 401
      2 403
     23 404
     10 /favicon.ico
      7 /admin/
      1 http://a7x.overflow.biz/hachk.php
      1 /sse
      1 /prueba/
      1 /no-existe
      1 /mcp
      1 /login
     45 21/Oct/2026
     23 20/Oct/2026
      1 
