# How to Use GitHub Pages to Host a Website

This guide will show you how to easily host a static website directly from your GitHub repository using GitHub Pages. It's a free and straightforward way to get your website online.

## Introduction: What are GitHub Pages?

[GitHub](https://github.com/) Pages is a service provided by GitHub that allows you to host static websites directly from a GitHub repository. Static websites are made up of files like HTML, CSS, JavaScript, and images, which are delivered to the user's browser exactly as they are stored. GitHub Pages does not support server-side languages like PHP, Python (with frameworks like Django/Flask), or Node.js for dynamic processing.

## Why Use GitHub Pages?

* **Free:** It's a free service for hosting static websites.
* **Easy Deployment:** You can deploy your website simply by pushing files to your GitHub repository.
* **Version Control:** Your website files are stored in a Git repository, allowing you to track changes, revert to previous versions, and collaborate easily.
* **Custom Domains:** You can use your own custom domain name with GitHub Pages.
* **Integration with GitHub:** Seamlessly integrated with your existing GitHub workflow.

## Prerequisites

Before you start, you'll need:

1.  A **GitHub Account**.
2.  Your **Website Files**: You should have the basic files for your website, including at least an `index.html` file. This file will serve as the homepage of your site. You might also have CSS, JavaScript, image files, etc.

## Two Types of GitHub Pages Sites

There are two main types of sites you can host with GitHub Pages:

1.  **User or Organization Site:** Hosted from a dedicated repository named exactly `username.github.io` (for a personal account) or `orgname.github.io` (for an organization account). The site is accessible directly at `https://username.github.io` or `https://orgname.github.io`.
2.  **Project Site:** Hosted from any other repository. The site is accessible at `https://username.github.io/repository-name` or `https://orgname.github.io/repository-name`.

Let's go through the steps for setting up each type.

## Option 1: Creating a User or Organization Site

This is typically used for personal blogs, portfolios, or organization websites.

### Step 1: Create the Repository

* Log in to your GitHub account.
* Click the '+' icon in the upper-right corner and select "New repository".
* For the repository name, use your GitHub username or organization name followed by `.github.io`. For example, if your username is `octocat`, the repository name must be `octocat.github.io`.
* Choose whether the repository should be **Public**. **GitHub Pages only works with public repositories unless you are using a GitHub Pro, Team, or Enterprise Cloud account for private repo hosting.** For free accounts, the repo *must* be public.
* Initialize the repository with a README (optional but good practice).
* Click "Create repository".

### Step 2: Add Your Website Files

Your website's homepage *must* be named `index.html` and placed in the root directory of the repository.

* You can upload your files directly through the GitHub website interface (drag and drop onto the repository page).
* Alternatively, clone the repository to your local machine, add your files, and commit/push them using Git commands or a Git GUI.

### Step 3: Push Your Files to GitHub

* If you added files via the website, they are already there.
* If you added files locally, commit your changes (`git commit -m "Add website files"`) and push them to GitHub (`git push origin main` or `git push origin master`). The main branch is the default for new repos.

### Step 4: Access Your Site

* Open a web browser and go to the address `https://yourusername.github.io` (replace `yourusername` with your actual GitHub username).
* It might take a few minutes (sometimes up to 20 minutes) for GitHub Pages to build and deploy your site after the first push or significant changes. If you see a 404 error initially, wait a bit and try refreshing.

## Option 2: Creating a Project Site

This is used to host websites related to a specific project or repository.

### Step 1: Create or Choose a Repository

* Log in to your GitHub account.
* Choose an existing repository or create a new one. The repository name can be anything you like (e.g., `my-project-website`).
* The repository should ideally be **Public** for free GitHub accounts to use GitHub Pages.

### Step 2: Add Your Website Files

* Add your website files (including `index.html` for the homepage) to the repository. You can place them in the root directory, in a folder like `/docs`, or in a specific branch like `gh-pages`. Placing them in the root or `/docs` folder of your main branch (`main` or `master`) is the most common method now.
* Add files via the website upload or by cloning, adding files locally, and committing.

### Step 3: Push Your Files to GitHub

* If adding locally, commit and push your files to the desired branch (e.g., `git push origin main`).

### Step 4: Configure GitHub Pages

* On your repository's page on GitHub, click on **"Settings"** (usually near the top right).
* In the left sidebar, find and click on **"Pages"** (under the "Code and automation" section).
* Under "Build and deployment", find the "Source" setting.
    * Click the dropdown menu.
    * Select the **Branch** you want to use as the source for your GitHub Pages site (e.g., `main`, `master`, or a dedicated `gh-pages` branch).
    * Select the **Folder** within that branch that contains your website files. This is usually `/ (root)` if your `index.html` is at the top level, or `/docs` if your files are in a folder named `docs`.
* Click **"Save"**.

### Step 5: Access Your Site

* GitHub Pages will now build and deploy your site from the specified branch and folder.
* The page will update to show the URL where your site is hosted. The URL will be `https://yourusername.github.io/repository-name/` (replace `yourusername` and `repository-name`).
* Again, there might be a delay of a few minutes for the site to become live after the initial setup or updates.

## Adding More Files (CSS, JS, Images)

* To add CSS, JavaScript, images, or other files, simply add them to the same repository, maintaining the correct folder structure as referenced in your `index.html` and other HTML files.
* For example, if your `index.html` is in the root, you might create a `/css` folder for stylesheets, a `/js` folder for scripts, and an `/images` folder for images.
* Make sure the paths in your HTML files are correct relative to the HTML file referencing them (e.g., `<link rel="stylesheet" href="css/style.css">` if `index.html` and the `css` folder are in the root).
* Commit and push your changes to the correct branch (the one you configured for GitHub Pages). GitHub Pages will rebuild and update your site automatically.

## Using Themes (Optional)

GitHub Pages offers themes that provide pre-built layouts and styling if you're hosting a simple Jekyll-based site (often used for blogs). You can explore and apply themes from the "Pages" settings page in your repository.

## Using a Custom Domain (Optional)

You can use your own domain name (like `www.yourwebsite.com`) instead of the default `github.io` URL.

* Purchase a domain name from a domain registrar.
* In your repository's "Pages" settings, add your custom domain name.
* Follow the instructions provided by GitHub Pages to configure DNS records (like CNAME or A records) with your domain registrar. This step points your domain name to the GitHub Pages servers.
* This process can take some time to propagate across the internet.

## Tips for Using GitHub Pages

* **Static Sites Only:** Remember, GitHub Pages is only for static content. It cannot run server-side code, process forms dynamically (without a third-party service), or connect to databases directly.
* **Main/Master Branch:** For user/organization sites, the site is built from the `main` (or `master`) branch. For project sites, you can choose the branch and folder in settings.
* **index.html:** The default file loaded for any directory is `index.html`. If you visit `https://username.github.io/my-project/about/`, GitHub Pages will look for `index.html` inside the `/about` folder.
* **Troubleshooting:** If your site isn't showing up or updating, check:
    * Are your files in the correct repository, branch, and folder?
    * Is your homepage file named `index.html` (lowercase)?
    * Is the repository public (for free accounts)?
    * Did you wait a few minutes for deployment? Check the build status in the "Pages" settings.
    * Are your file paths correct in your HTML?

## Conclusion

GitHub Pages is an excellent, free service for hosting static websites directly from your GitHub repositories. Whether you're setting up a personal site or a project page, the process involves creating the correct repository or configuring the settings for an existing one and pushing your website files. Start simple, understand the limitations, and practice deploying updates.

## Disclaimer

This guide is for informational purposes only and provides instructions on using GitHub Pages. GitHub Pages is a service provided by GitHub, and its terms of service and features may change. Ensure you comply with GitHub's terms when hosting content.
