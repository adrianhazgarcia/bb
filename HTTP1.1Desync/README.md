# HTTP.1.1 Desync
Este ataque aparece cuando el _frontend_ y el _backend_ emplean cabeceras distintas para interpretar las solicitudes HTTP.

## Teoría
### Content-Length

### Transfer-Encoding: chunked
- Si la cabecera `Transfer-Encoding` está presente, se debe ignorar la de `Content-Length`
- 

## Attacks

### CL.TE

### TE.TE

### HTTP/2 downgrading

### H2.CL

### H2.TE
### HTTP/2-exclusive vectors
### HTTP/2 request splitting
### HTTP/2 request tunneling
### 0.CL rquest smuggling