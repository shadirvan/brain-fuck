### WAF Identication and Fingerprinting
- `wafw00f` is a tool used for identifying the Web application firewall that is used.
- even though there are WAF to prevent the attacks there might be payloads that might not get caught up in firewall.
- Try different payloads for XSS or any attack on the payloads using the wordlists. Maybe some payloads get bypassed.
### Input Validation 
- Sometime the input only filters the `<script>` tags.
- Then we can use something like : `<img src=x onerror=prompt(1)>`
- Sometimes the filtering might not be done recursively so we can use : `<scri<script>pt> prompt(1)</scri</script>pt>` this bypass it
- Sometimes certain characteristics are not allowed. Try to smuggle the request by modifying the request body with encoding or double encoding.