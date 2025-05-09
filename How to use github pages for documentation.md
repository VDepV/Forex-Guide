# How to Use GitHub Pages for Documentation

This guide explains how to leverage GitHub Pages to host your project documentation directly from your code repository. This is a popular method because it's free, easy to update, and keeps your documentation alongside your code.

## Introduction: GitHub Pages for Documentation

[GitHub](https://github.com/) Pages is a service that hosts static websites from a GitHub repository. While it can be used for personal websites or project pages, it's also an excellent tool for hosting project documentation. Your documentation files (like guides, API references, tutorials) live in the same repository as your code and are served as a simple website.

## Why Use GitHub Pages for Documentation?

* **Free:** It's completely free for hosting public documentation.
* **Version Control:** Your documentation is versioned alongside your code using Git, making it easy to track changes, see documentation specific to different code versions (if managed carefully), and collaborate.
* **Easy to Update:** Simply update your documentation files in the repository and push your changes. GitHub Pages automatically rebuilds and deploys the updated site.
* **Markdown Support:** GitHub Pages has native support for rendering Markdown files (`.md`) into HTML, which is a very popular and easy-to-learn format for writing documentation.
* **Integrated:** Keeps your documentation centralized with your project code on GitHub.

## Prerequisites

You will need:

1.  A **GitHub Account**.
2.  An existing **Project Repository** on GitHub that you want to add documentation to.
3.  Your **Documentation Content:** Your guides, explanations, etc., preferably written in Markdown format.

## Common Approach: Using the `/docs` Folder

The most straightforward and recommended way to host documentation for a project using GitHub Pages is to place all your documentation files within a folder named `/docs` in the main branch of your repository.

When you configure GitHub Pages to use the `/docs` folder from your `main` (or `master`) branch, the contents of that folder become the root of your documentation website.

For example, if your repository is `https://github.com/yourusername/my-project` and you configure GitHub Pages to serve from the `/docs` folder of the `main` branch, a file located at `my-project/docs/guide.md` in your repository will be accessible at `https://yourusername.github.io/my-project/guide/`.

## Step-by-Step: Setting up Documentation on GitHub Pages using the `/docs` folder

Follow these steps to set up your documentation site:

### Step 1: Have Your Project Repository Ready

Ensure you have a repository on GitHub for your project. If you don't, create one.

### Step 2: Create a `/docs` Folder

* In your project repository (locally or on the GitHub website), create a new folder named exactly `docs` at the root level.

### Step 3: Write Your Documentation

* Inside the `/docs` folder, create your documentation files. Markdown (`.md`) is highly recommended as GitHub Pages renders it automatically.
* Organize your files into subfolders within `/docs` if needed (e.g., `/docs/api`, `/docs/guides`).

### Step 4: Add an Index File

* For the main landing page of your documentation site, place your primary documentation file inside the `/docs` folder.
* If you want a standard HTML homepage, create an `index.html` file in the `/docs` folder.
* If you are using Markdown and want a Markdown file to be the homepage, name it `README.md`. GitHub Pages (especially with Jekyll, which is enabled by default) will often automatically render a `README.md` as the index file for a directory if no `index.html` is present. Using `README.md` in `/docs` is common.

### Step 5: Commit and Push Your Changes

* If you created the `/docs` folder and files locally, use Git to commit your changes and push them to your GitHub repository, specifically to the `main` (or `master`) branch.
    ```bash
    git add .
    git commit -m "Add project documentation in /docs"
    git push origin main
    ```
* If you created the folder and files directly on the GitHub website, the changes are already saved to the branch you were working on.

### Step 6: Configure GitHub Pages Settings

Now, tell GitHub Pages to build your site from the `/docs` folder.

1.  Navigate to your project repository on GitHub.
2.  Click on the **"Settings"** tab (usually near the top right).
3.  In the left sidebar, find and click on **"Pages"** (under "Code and automation").
4.  Under "Build and deployment", find the "Source" setting.
    * Click the dropdown menu and select the branch that contains your `/docs` folder (e.g., `main`).
    * Click the dropdown menu next to the branch and select the **/docs folder**.
5.  Click **"Save"**.

### Step 7: Access Your Documentation Site

* GitHub Pages will now build and deploy your site from the `/docs` folder.
* The URL for your documentation site will be `https://yourusername.github.io/your-repository-name/` (replace placeholders).
* It might take a few minutes (usually 1-20 minutes) for the site to become live after the initial setup or after subsequent pushes to the source branch. The "Pages" settings page will show the deployment status.

## Using Documentation Generators (Optional)

For more complex documentation sites with navigation, search, and specific themes, you can use static site generators designed for documentation. These generators take your source files (often Markdown) and build a complete static website (HTML, CSS, JS). You then host the *output* of the generator on GitHub Pages.

* **Jekyll:** A popular static site generator that is integrated with GitHub Pages. If you put a `_config.yml` file in your `/docs` folder (or root if using the root), GitHub Pages will automatically process your Markdown files using Jekyll. This allows for features like themes, includes, and navigation.
* **MkDocs:** A fast, simple static site generator focused on building project documentation. You write documentation in Markdown and configure the site with a YAML file.
* **Sphinx:** A powerful documentation generator (originally for Python projects, but supports other languages) that outputs HTML.

To use these or other generators:

1.  Set up the generator locally on your machine and build your documentation site.
2.  The generator will output static HTML/CSS/JS files into a designated output directory (e.g., `_site`, `site`, `_build/html`).
3.  Copy the *contents* of this output directory into the `/docs` folder of your GitHub repository.
4.  Commit and push the files to the `main` branch.
5.  Configure GitHub Pages to serve from the `/docs` folder (as in Step 6 above).
6.  **Note:** If using a generator like MkDocs or Sphinx that builds *into* the `/docs` folder, ensure your `.gitignore` file is set up correctly so you commit the built site files, not the generator's source files (unless you want to). If using Jekyll within `/docs`, GitHub handles the build process automatically from your source files.

## Tips for Hosting Documentation on GitHub Pages

* **Markdown Simplicity:** Start with basic Markdown (`.md`) files in `/docs`. They render well and are easy to maintain.
* **Organize with Folders:** Use subfolders within `/docs` to structure your documentation logically (e.g., by topic, version).
* **Linking:** Use relative links between your documentation pages (e.g., `../api/README.md` or `../guides/guide1.md`).
* **`index.html` or `README.md`:** Make sure you have an `index.html` or `README.md` in your `/docs` folder to serve as the entry point.
* **Jekyll `_config.yml`:** If you add a `_config.yml` file to `/docs`, GitHub Pages will process your site with Jekyll, allowing more customization. You can disable Jekyll processing in the Pages settings if needed.
* **Keep it Static:** Documentation sites on GitHub Pages cannot have dynamic features requiring a server backend.
* **Use `gh-pages` branch (Alternative):** Another method (less common now than `/docs`) is to create a dedicated branch named `gh-pages` and put your documentation files (or generator output) in the root of *that branch*. You would then configure Pages settings to serve from the `gh-pages` branch. The `/docs` folder method on `main` is generally simpler.

## Conclusion

GitHub Pages provides a free and efficient way to host your project documentation directly from your code repository. By placing your documentation files (especially in Markdown) into a `/docs` folder in your main branch and configuring your repository's Pages settings, you can quickly get your documentation online at a standard project site URL. For more advanced features, consider using a static site generator. Keeping documentation with your code simplifies the maintenance workflow.

## Disclaimer

This guide is for informational purposes only and provides instructions on using GitHub Pages for documentation. GitHub Pages is a service provided by GitHub, and its terms of service and features may change. Ensure you comply with GitHub's terms when hosting content. The complexity of documentation sites can vary; this guide covers basic setup.
