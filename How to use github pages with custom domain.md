# How to Use GitHub Pages with a Custom Domain

This guide explains how to link your own custom domain name (like `www.yourwebsite.com` or `yourwebsite.com`) to a website hosted on GitHub Pages. This makes your site more professional and easier to access than using the default `.github.io` URL.

## Introduction: Why Use a Custom Domain?

While the default `username.github.io` or `username.github.io/repository-name` URLs are functional, using a custom domain you own offers several benefits:

* **Branding:** It aligns the website with your personal brand or project name.
* **Professionalism:** Custom domains look more professional than a subdomain on GitHub's domain.
* **Memorability:** It's often easier for visitors to remember a custom domain.

## Prerequisites

Before you begin, make sure you have:

1.  A **working GitHub Pages site:** You should have already set up and published your website using GitHub Pages (either a User/Organization site or a Project site). Refer to the guide "How to Use GitHub Pages to Host a Website?" if you haven't done this yet.
2.  A **registered custom domain name:** You must own a domain name (e.g., `yourwebsite.com`) purchased from a domain registrar (like GoDaddy, Namecheap, Google Domains, etc.).
3.  **Access to your domain's DNS settings:** You need to be able to log in to your domain registrar's website (or DNS hosting provider if different) to modify the DNS records for your domain.

## Understanding Apex Domains vs. Subdomains

When setting up a custom domain, you typically choose between:

* **Apex Domain (or Root Domain):** This is the domain without any subdomain prefix (e.g., `yourwebsite.com`).
* **Subdomain:** This is a domain with a prefix (e.g., `www.yourwebsite.com`, `blog.yourwebsite.com`, `shop.yourwebsite.com`). `www` is the most common subdomain for websites.

The configuration steps with your domain registrar will differ slightly depending on whether you use an apex domain or a subdomain. It's common to set up both (e.g., have `yourwebsite.com` redirect to `www.yourwebsite.com`) for convenience.

## Step 1: Add Your Custom Domain in GitHub Repository Settings

This step tells [GitHub](https://github.com/) Pages what custom domain name your site should respond to.

1.  **Log in to GitHub** and navigate to the **repository** that hosts your GitHub Pages site.
2.  Go to the **"Settings"** tab of the repository.
3.  In the left sidebar, click on **"Pages"**.
4.  Under "Custom domain", enter your custom domain name (e.g., `www.yourwebsite.com` or `yourwebsite.com`) in the text field.
5.  Click **"Save"**.

GitHub will now look for DNS records that point your domain to GitHub Pages. When you save, GitHub automatically checks if a `CNAME` file exists in your repository's root directory (in the branch you specified as the Pages source). If it doesn't exist, or if the domain name in the file doesn't match what you entered in settings, GitHub will create/update this `CNAME` file for you. This file is crucial for GitHub to know which repository corresponds to your custom domain.

## Step 2: Configure DNS Records with Your Domain Registrar

This is the most technical step. You need to tell the internet where to find your website when someone types your custom domain name. You do this by adding specific DNS records in your domain registrar's (or DNS provider's) settings page.

Log in to your domain registrar's website and find the DNS management or advanced DNS settings for your domain. You will add either A records (for apex) or a CNAME record (for subdomain).

### Option A: Configuring an Apex Domain (`yourdomain.com`)

If you want your site to be accessible directly at `yourdomain.com` (without `www`), you need to point your apex domain to GitHub Pages' IP addresses using **A records**.

* Find the option to add **A records** for your domain.
* You will usually leave the "Host" or "Name" field blank, or enter `@` (depending on your registrar's interface - `@` usually represents the apex domain).
* For the "Value" or "Points to" field, enter the four GitHub Pages IP addresses. You'll need to add one A record for each IP address. **Get the current official GitHub Pages IP addresses** from the official GitHub documentation. They are typically something like:
    * `185.199.108.153`
    * `185.199.109.153`
    * `185.199.110.153`
    * `185.199.111.153`
* The "TTL" (Time To Live) setting can usually be left at the default or set to a relatively low value (e.g., 300 seconds or 5 minutes) for faster updates, but consult your registrar's recommendations.
* Save the A records.

*Note: Some registrars offer ALIAS or ANAME records which can simplify pointing an apex domain directly to a hostname (like GitHub Pages' servers) instead of fixed IP addresses. If your registrar supports this, you might be able to point your apex domain to `yourusername.github.io` directly. Consult your registrar's documentation.*

### Option B: Configuring a Subdomain (`www.yourdomain.com` or `blog.yourdomain.com`)

If you want your site to be accessible at a subdomain like `www.yourdomain.com`, you need to create a **CNAME record**. This record points your subdomain to your GitHub Pages URL.

* Find the option to add a **CNAME record**.
* For the "Host" or "Name" field, enter the subdomain prefix you want to use (e.g., `www` or `blog`).
* For the "Value" or "Points to" field, enter the default GitHub Pages URL of your site (without the `http://` or `https://`).
    * For **User/Organization sites:** Enter `yourusername.github.io` (e.g., `octocat.github.io`).
    * For **Project sites:** Enter `yourusername.github.io` (e.g., `octocat.github.io`). **Important:** Even for project sites like `octocat.github.io/my-project`, the CNAME value should point to the base `github.io` domain, not the project path.
* The "TTL" setting can usually be left at the default.
* Save the CNAME record.

**If you want both `yourdomain.com` and `www.yourdomain.com` to work**, you would typically set up the A records for the apex domain (Option A) AND a CNAME record for the `www` subdomain pointing to `yourusername.github.io`. Then, in your GitHub Pages settings (Step 1), you would enter *either* `yourdomain.com` or `www.yourwebsite.com` (GitHub handles the redirection). It's common practice to enter the `www` version in GitHub settings.

### Important Note on DNS Propagation

After saving DNS records with your domain registrar, it takes time for these changes to propagate across the internet. This can range from a few minutes to up to 48 hours, although it's usually faster (often within an hour or two). During this time, your custom domain might not work, or it might still show a previous website if you had one. There's nothing to do but wait. You can use online DNS lookup tools to check if the records have updated in various locations.

## Step 3: Enforce HTTPS (Recommended)

GitHub Pages provides free HTTPS certificates powered by Let's Encrypt, making your site secure.

* Go back to the **"Pages"** settings page in your GitHub repository (where you entered the custom domain in Step 1).
* After your DNS records have propagated and GitHub has verified your domain setup, you will see an option labeled **"Enforce HTTPS"**.
* Check the box next to "Enforce HTTPS".

This ensures that visitors access your site securely using HTTPS.

## The CNAME File (Automatic)

When you add a custom domain in your GitHub Pages settings, GitHub automatically creates or updates a file named `CNAME` (with no file extension) in the root of your publishing branch (the branch you selected as the source for Pages, usually `main` or `master`). This file contains a single line with your custom domain name. This file is essential for GitHub's servers to map incoming requests for your custom domain to the correct repository. You don't need to manually create or edit this file unless specifically instructed to troubleshoot, as GitHub manages it via the Settings page.

## Troubleshooting Common Issues

* **Site not loading / 404 Error:**
    * Did you wait long enough for DNS propagation (up to 48 hours, but often faster)?
    * Did you save the custom domain in your GitHub Pages settings?
    * Check the "Pages" settings page on GitHub for error messages. GitHub often tells you if the DNS records are incorrect or if the `CNAME` file is missing/wrong.
    * Ensure your website files are in the correct branch and folder source selected in the "Pages" settings, including `index.html`.
* **Incorrect DNS Records:** Double-check the A records (for apex) or CNAME record (for subdomain) you entered at your domain registrar. Ensure they match the values provided by GitHub and that you saved the changes with your registrar.
* **CNAME File Problems:** Although GitHub manages it, occasionally the automatic update might fail. Check the root of your publishing branch in the repository on GitHub to see if the `CNAME` file exists and contains the correct custom domain name. If not, try re-saving the custom domain in settings or creating/editing the file manually (single line with your domain).

## Conclusion

Using a custom domain with your GitHub Pages site makes your online presence more professional and accessible. The process involves configuring both your GitHub repository settings and the DNS records with your domain registrar. By correctly setting up the A or CNAME records and enforcing HTTPS, you can successfully link your domain to your static website hosted on GitHub Pages. Remember that DNS changes take time to update globally.

## Disclaimer

This guide is for informational purposes only and provides instructions based on the standard procedures for GitHub Pages and DNS management. Specific steps and interface elements may vary slightly depending on your domain registrar and future updates to GitHub Pages. Ensure you comply with GitHub's terms of service and your domain registrar's policies.
