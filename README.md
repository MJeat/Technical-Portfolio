# Adding Domain Name in Vercel
**NOTE:**
DO NOT BUY A DOMAIN FROM get.tech. They do not have Privacy Protection for free. You need to buy. Without privacy protection, you domain and URL link info is leaked on ICANN and WHOIS platforms. <br>
If you want a domain, buy from CloudFlare or NameCheap.

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


# Adding a Subdomain in DigitalOcean
Since your domain is managed by **Cloudflare** (Cloudflare Name Servers), you don't need to do anything inside DigitalOcean or `.tech` to create the subdomain. Everything happens inside your Cloudflare dashboard.

Here is the step-by-step guide to setting up a subdomain (e.g., `dev.yourname.tech` or `app.yourname.tech`) for your new DigitalOcean Droplet.

---
### Step 1: Get your Droplet's IP Address

Before heading to Cloudflare, you need to know where to send the traffic.

1. Log in to your **DigitalOcean Control Panel**.
2. Click on **Droplets** in the left sidebar.
3. Locate your Droplet and copy the **IPv4 address** (e.g., `123.45.67.89`).

### Step 2: Create the DNS Record in Cloudflare

This is where the "creation" of the subdomain actually happens.

1. Log in to your [Cloudflare Dashboard](https://dash.cloudflare.com/).
2. Select your **get.tech** domain.
3. Click on the **DNS** tab in the left sidebar, then select **Records**.
4. Click the **+ Add record** button.
5. Fill in the following details:
* **Type:** `A`
* **Name:** Enter your desired subdomain prefix (e.g., if you want `blog.yourname.tech`, just type **`blog`**).
* **IPv4 address:** Paste the **IP address** you copied from DigitalOcean.
* **Proxy status:** * **Orange Cloud (Proxied):** Use this if you want Cloudflare’s security/CDN.
* **Grey Cloud (DNS only):** Use this if you are setting up something like a VPN or if you have issues with SSL later. (Start with Orange).


* **TTL:** Leave as `Auto`.


6. Click **Save**.

### Step 3: Configure your Web Server (Crucial)

Cloudflare now knows to send traffic from `subdomain.get.tech` to your Droplet. Now, your Droplet needs to know what to do with that traffic.

If you are using **Nginx**, you need to create a "Server Block." If you haven't installed a web server yet, your subdomain won't show anything.

**Quick Nginx Example:**

1. SSH into your Droplet.
2. Create a configuration file: `sudo nano /etc/nginx/sites-available/subdomain.get.tech`
3. Paste a basic config:

```nginx
server {
    listen 80;
    server_name subdomain.get.tech;
    root /var/www/subdomain; # Where your website files live
    index index.html;
}

```

4. Link it and restart Nginx:
* `sudo ln -s /etc/nginx/sites-available/subdomain.get.tech /etc/nginx/sites-enabled/`
* `sudo systemctl restart nginx`

---

### Summary Table

| Task | Where to do it | Result |
| --- | --- | --- |
| **Create the Subdomain** | Cloudflare DNS | Points the name to your IP |
| **Host the files** | DigitalOcean Droplet | Serves the actual content |
| **SSL/HTTPS** | Cloudflare (Edge) | Protects the connection |

### A Quick Warning on SSL
Since you are using Cloudflare, make sure your Cloudflare **SSL/TLS** setting (under the SSL/TLS tab) is set to **Full** or **Full (Strict)** if you install an SSL certificate on your Droplet. If it's set to "Flexible," you might run into "Too many redirects" errors.



