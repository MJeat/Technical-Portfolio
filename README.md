# Adding Domain Name in Vercel

- A record pointing to `76.76.21.21`
- CNAME pointing to `cname.vercel-dns.com`

In Cloudflare, setup domain and setup its records. Copy the above, and since it is in Vercel, you don't really need to turn on CloudFlare proxy. Vercel is already protecting you.

Don't forget to change your name servers.
- Copy the 2 name servers from CloudFlare and replace the 4 name servers issued by your domain provider.


