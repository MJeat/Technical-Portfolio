# Adding Domain Name in Vercel

## DNS Records in CloudFlare
- A record pointing to `216.198.79.1` (You will be asked to use)
- CNAME pointing to `89c97d05cb7fddfb.vercel-dns-017.com`


## Set up name servers and DNS records via CloudFlare
In Cloudflare, setup domain and setup its records. Copy the records above, and since it is in Vercel, you don't really need to turn on CloudFlare proxy. Vercel is already protecting you.

## Name Servers
Don't forget to change your name servers.
- Copy the 2 name servers from CloudFlare and replace the 4 name servers issued by your domain provider.


## How to add your own domain in Vercel
Since you already have your DNS records set up in Cloudflare, adding the domain to Vercel is the final "handshake" to make your portfolio live.
Follow these steps in the Vercel Dashboard:

1. Go to your Project Settings
- Open your project (the one currently at technical-portfolio-two.vercel.app).
- Click on the Settings tab at the top.
- Select Domains from the left-hand sidebar.

2. Add your .tech Domain
- In the input box, type your full domain (e.g., yourname.tech).
- Click the Add button.
- A pop-up will appear asking if you want to add the www version as well (e.g., www.yourname.tech). Select "Add both" (this is recommended so both versions work).

3. Verify the Connection
- Vercel will now automatically scan your DNS records (the ones you just added to Cloudflare).
- If you added the A record (76.76.21.21) and CNAME (cname.vercel-dns.com) correctly, you will see a green "Valid Configuration" checkmark.
- Vercel will then start "Generating SSL Certificate." This usually takes 1–5 minutes.
- Troubleshooting "Invalid Configuration"
### If you see a red error instead of a green checkmark:
- Wait a few minutes: It can take time for Cloudflare to tell the rest of the internet about your new records.
- Check the Proxy: Ensure the "Cloud" icon in Cloudflare is Gray (DNS Only). If it's Orange, Vercel might struggle to verify the domain.
- Check Name Servers: Make sure you actually updated the 4 name servers at get.tech to the 2 provided by Cloudflare.



