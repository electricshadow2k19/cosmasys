# GitHub Setup Instructions

Your website has been committed to Git. Follow these steps to push it to GitHub:

## Option 1: Using GitHub CLI (if installed)

1. Create a new repository on GitHub:
```bash
gh repo create cosmasys-website --public --source=. --remote=origin --push
```

## Option 2: Manual Setup

1. **Create a new repository on GitHub:**
   - Go to https://github.com/new
   - Name it (e.g., `cosmasys-website`)
   - Choose public or private
   - **Do NOT** initialize with README, .gitignore, or license (we already have these)

2. **Add the remote and push:**
```bash
git remote add origin https://github.com/YOUR_USERNAME/cosmasys-website.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username and `cosmasys-website` with your repository name.

## Option 3: Using SSH (if you have SSH keys set up)

```bash
git remote add origin git@github.com:YOUR_USERNAME/cosmasys-website.git
git branch -M main
git push -u origin main
```

## After Pushing

Once pushed, you can:
- Enable GitHub Pages to host the website
- Share the repository with your team
- Continue making updates and pushing changes

## Future Updates

After the initial push, you can update the website with:
```bash
git add .
git commit -m "Your commit message"
git push
```
