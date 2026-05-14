# Deployment Guide - Lalasa Private Ltd Website

This guide covers deploying your website using GitHub Pages and other hosting options.

## 🚀 GitHub Pages Deployment (Recommended)

### Automatic Deployment (Current Setup)

Your website automatically deploys to GitHub Pages on every push to the `main` branch.

**Live URL:** https://banjarasudesh33-web.github.io/Company-website/

### Enable GitHub Pages

1. Go to your repository settings
2. Navigate to **Settings** → **Pages**
3. Under "Build and deployment":
   - Source: Select "Deploy from a branch"
   - Branch: Select `main` and `/(root)` folder
   - Click "Save"

4. GitHub will automatically build and deploy your site
5. View deployment status under **Deployments** tab

### Custom Domain Setup

To use a custom domain (e.g., `lalasa.com`):

1. **In GitHub Settings:**
   - Go to Settings → Pages
   - Enter your custom domain
   - Click "Save"
   - GitHub will create a CNAME record

2. **DNS Configuration:**
   - Log into your domain provider (GoDaddy, Namecheap, etc.)
   - Point your domain to GitHub's servers:
     ```
     A records:
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - Or use CNAME if pointing to subdomain:
     ```
     CNAME: banjarasudesh33-web.github.io
     ```

3. **SSL Certificate:**
   - GitHub Pages automatically provides free SSL
   - Check "Enforce HTTPS" in Settings → Pages
   - Wait 24 hours for DNS propagation

### Deployment Workflow

```
Local Changes
    ↓
git add .
git commit -m "feat: your changes"
git push origin main
    ↓
GitHub detects push
    ↓
Builds website
    ↓
Deploys to GitHub Pages
    ↓
Live at https://banjarasudesh33-web.github.io/Company-website/
```

---

## 🔄 Workflow: Staging → Production

### Using Branches for Staging

1. **Main Branch (Production)**
   ```bash
   # Always production-ready code
   # Direct automatic deployment
   ```

2. **Develop Branch (Staging)**
   ```bash
   # Create a develop branch for testing
   git checkout -b develop
   ```

3. **Feature Branches**
   ```bash
   # For each feature
   git checkout -b feature/your-feature
   ```

4. **PR Workflow:**
   ```
   feature/your-feature → develop (PR) → main (PR)
   ```

### Setting Up Branch Protection

1. Go to Settings → Branches
2. Click "Add rule"
3. Branch name pattern: `main`
4. Enable:
   - Require a pull request before merging
   - Require status checks to pass
   - Require branches to be up to date

---

## 📦 Alternative Hosting Options

### Netlify

1. **Connect Repository:**
   - Go to [netlify.com](https://netlify.com)
   - Click "New site from Git"
   - Authorize GitHub
   - Select your repository

2. **Configure Build:**
   - Build command: Leave empty (static site)
   - Publish directory: `/` (root)
   - Click "Deploy site"

3. **Custom Domain:**
   - Go to Site Settings → Domain management
   - Add your custom domain
   - Configure DNS records

### Vercel

1. **Connect Repository:**
   - Go to [vercel.com](https://vercel.com)
   - Click "Import Project"
   - Select GitHub repository
   - Click "Import"

2. **Deploy:**
   - Vercel auto-detects static site
   - Click "Deploy"
   - Get your live URL

3. **Custom Domain:**
   - Go to Project Settings → Domains
   - Add custom domain
   - Update DNS records

### Traditional Hosting (cPanel, etc.)

1. **Build Process:**
   ```bash
   # No build needed - static files only
   # Just upload index.html and assets
   ```

2. **FTP Upload:**
   - Connect via FTP client
   - Upload `index.html` to public_html/
   - Upload `assets/` folder
   - Update `.htaccess` for routing

3. **Domain Configuration:**
   - Point domain to hosting IP
   - Update nameservers if needed

---

## 🧪 Pre-Deployment Checklist

### Code Quality
- [ ] All links are functional
- [ ] Forms are working (or have fallback)
- [ ] No console errors
- [ ] Images load correctly
- [ ] CSS renders properly

### Performance
- [ ] Page loads in under 2 seconds
- [ ] Mobile responsive works
- [ ] Touch targets are at least 44x44px
- [ ] No unused CSS or JavaScript

### Accessibility
- [ ] Keyboard navigation works
- [ ] Alt text on all images
- [ ] Color contrast meets WCAG standards
- [ ] Form labels are associated

### SEO
- [ ] Meta description added
- [ ] Meta viewport tag present
- [ ] Headings are semantic
- [ ] Open Graph tags added (optional)

### Security
- [ ] No hardcoded credentials
- [ ] HTTPS enabled
- [ ] No mixed content warnings
- [ ] Form submissions validated

---

## 🔍 Post-Deployment Verification

### Test Live Website

1. **Functionality:**
   ```bash
   # Test in multiple browsers
   # Check all links
   # Submit test form
   # Test responsive design
   ```

2. **Performance:**
   - Use Google PageSpeed Insights
   - Check mobile performance
   - Monitor Core Web Vitals

3. **Analytics Setup (Optional):**
   ```html
   <!-- Add Google Analytics -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=GA_ID"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'GA_ID');
   </script>
   ```

4. **Monitoring:**
   - Set up uptime monitoring
   - Configure error notifications
   - Monitor performance metrics

---

## 🐛 Troubleshooting

### Website Not Appearing

**Issue:** GitHub Pages not showing your site
```bash
# Check branch settings
# Verify Settings → Pages is configured
# Check CNAME file exists (if custom domain)
# Wait up to 10 minutes for deployment
```

### Custom Domain Not Working

**Issue:** Custom domain shows GitHub Pages error
```bash
# DNS propagation takes 24-48 hours
# Verify DNS records in domain provider
# Check GitHub Settings → Pages shows custom domain
# Clear browser cache and try incognito mode
```

### Assets Not Loading

**Issue:** Images or CSS not loading on live site
```bash
# Check file paths are relative (not absolute)
# Verify all assets are committed and pushed
# Check case sensitivity in file names
# Ensure paths don't have spaces or special characters
```

### Form Not Working

**Issue:** Contact form not submitting
```javascript
// If using GitHub Pages (static):
// You need an external service:

// Option 1: Formspree
<form action="https://formspree.io/f/YOUR_ID" method="POST">

// Option 2: Basin
<form method="POST" action="https://usebasin.com/api/v1/455a675c31da">

// Option 3: Google Forms (embedded)
// Configure form to submit to Google Forms endpoint
```

---

## 📊 Deployment Monitoring

### GitHub Actions (Optional)

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Check HTML
        run: |
          # Validate HTML structure
          echo "Checking HTML syntax..."
```

### Uptime Monitoring

Use free services like:
- [UptimeRobot](https://uptimerobot.com) - Free tier
- [StatusCake](https://www.statuscake.com)
- [Pingdom](https://www.pingdom.com)

---

## 🔐 Security Best Practices

### HTTPS
- ✅ Always enabled on GitHub Pages
- ✅ Auto-renewed SSL certificates
- ✅ Redirect HTTP to HTTPS

### Headers
- ✅ CSP (Content Security Policy)
- ✅ X-Frame-Options: DENY
- ✅ X-Content-Type-Options: nosniff

### Form Submissions
- ⚠️ Never process forms server-side (static site)
- ✅ Use external services (Formspree, Basin)
- ✅ Validate on client-side
- ✅ No sensitive data in forms

---

## 📋 Rollback Procedures

### Revert to Previous Deployment

```bash
# Find previous commit
git log --oneline

# Revert to specific commit
git revert abc1234
git push origin main

# Or reset (only for unpublished commits)
git reset --hard abc1234
git push origin main --force
```

### Using Git Tags

```bash
# Create release tag
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# Rollback to tag
git checkout v1.0.0
git push origin main

# Back to latest
git checkout main
git push origin main
```

---

## 📞 Support

**Having deployment issues?**

1. Check the [GitHub Pages Documentation](https://docs.github.com/en/pages)
2. Review [GitHub Status](https://www.githubstatus.com)
3. Check community forums and Stack Overflow
4. Open an issue in the repository

---

**Last Updated:** May 14, 2026
**Version:** 1.0.0
