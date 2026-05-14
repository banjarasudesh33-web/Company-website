# Development Setup Guide

This guide will help you set up your local development environment for contributing to the Lalasa Private Ltd website.

## 📋 Prerequisites

- **Git** - Version control system
- **Code Editor** - VS Code (recommended), Sublime Text, or similar
- **Web Browser** - Chrome, Firefox, Safari, or Edge
- **Terminal/Command Line** - Familiarity with basic commands

### Installation

#### Git
- **macOS:** `brew install git`
- **Windows:** Download from [git-scm.com](https://git-scm.com)
- **Linux:** `sudo apt-get install git`

#### Code Editor (VS Code)
- Download from [code.visualstudio.com](https://code.visualstudio.com)
- Recommended extensions:
  - Live Server
  - Prettier
  - HTML Validator
  - CSS Peek

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
# SSH (if SSH key is configured)
git clone git@github.com:banjarasudesh33-web/Company-website.git

# HTTPS (alternative)
git clone https://github.com/banjarasudesh33-web/Company-website.git

# Navigate to project
cd Company-website
```

### 2. Open in Code Editor

```bash
# Using VS Code
code .
```

### 3. Start Local Server

**Option A: VS Code Live Server**
- Right-click `index.html`
- Select "Open with Live Server"
- Browser opens at `http://127.0.0.1:5500`

**Option B: Python (Built-in)**
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Visit: http://localhost:8000
```

**Option C: Node.js HTTP Server**
```bash
# Install globally (if not installed)
npm install -g http-server

# Start server
http-server

# Visit: http://localhost:8080
```

---

## 📁 Project Structure

```
Company-website/
├── index.html              # Main website (HTML/CSS/JS combined)
├── README.md               # Project documentation
├── CONTRIBUTING.md         # Contribution guidelines
├── LICENSE                 # MIT License
├── .gitignore              # Files to ignore in Git
├── docs/
│   ├── DEVELOPMENT.md      # This file
│   ├── DEPLOYMENT.md       # Deployment guide
│   └── GIT-WORKFLOW.md     # Git workflow guide
└── assets/                 # (Future) Images, fonts, icons
    ├── images/
    ├── fonts/
    └── icons/
```

### Recommended Structure After Refactoring

```
Company-website/
├── index.html              # HTML only
├── src/
│   ├── css/
│   │   └── styles.css      # Separated CSS
│   ├── js/
│   │   ├── main.js         # Main JavaScript
│   │   ├── form.js         # Form handling
│   │   └── utils.js        # Utility functions
│   └── images/
│       ├── logo.png
│       └── bg.jpg
└── docs/
    └── ...
```

---

## 🛠️ Development Workflow

### Creating a Feature

1. **Create a new branch:**
```bash
git checkout -b feature/amazing-feature
```

2. **Make your changes:**
   - Edit `index.html`, CSS, or JavaScript as needed
   - Save files (auto-refresh with Live Server)
   - Test in browser

3. **Commit your changes:**
```bash
git add .
git commit -m "feat: add amazing feature"
```

4. **Push to GitHub:**
```bash
git push origin feature/amazing-feature
```

5. **Create a Pull Request:**
   - Go to GitHub repository
   - Click "Compare & pull request"
   - Add description and submit

---

## 🧪 Testing Locally

### Browser Testing

```bash
# Test Responsiveness
# Press F12 or right-click → Inspect
# Device toolbar: Ctrl+Shift+M (or Cmd+Shift+M on Mac)

# Test Devices:
- Desktop (1920x1080)
- Tablet (768x1024)
- Mobile (375x667)
```

### Cross-Browser Testing

Test on multiple browsers:
```
✓ Chrome/Edge
✓ Firefox
✓ Safari
✓ Mobile Safari (iPhone)
✓ Chrome Mobile (Android)
```

Use BrowserStack or free browser testing:
- Edge on Windows
- Safari on macOS
- Firefox Developer Edition

### Console Validation

```javascript
// Check browser console (F12 → Console tab)
// Should have no errors or warnings

// Test form validation
console.log(document.getElementById('form'));

// Check styles applied
console.log(getComputedStyle(document.getElementById('element')));
```

---

## 🐛 Debugging

### Using Browser DevTools

```javascript
// 1. Open Developer Tools (F12)
// 2. Console tab - check for errors
// 3. Elements tab - inspect HTML structure
// 4. Styles tab - debug CSS
// 5. Network tab - check loading times
```

### Common Issues & Solutions

**Issue: Styles not applying**
```css
/* Check:
1. CSS is linked correctly
2. Selectors are correct
3. Specificity isn't being overridden
4. No typos in class names
5. Browser cache cleared (Ctrl+Shift+Del)
*/
```

**Issue: JavaScript not running**
```javascript
// Check:
// 1. Script is included in HTML
// 2. No syntax errors in console
// 3. Elements exist before script runs
// 4. Event listeners are attached correctly
// 5. Use console.log() to debug
```

**Issue: Form not submitting**
```javascript
// Check form in console:
document.getElementById('hrContactForm').addEventListener('submit', (e) => {
  console.log('Form submitted!', e);
  // Check event handling
});
```

---

## 📝 Editing Files

### HTML Changes

```html
<!-- Keep semantic structure -->
<!-- Use descriptive IDs and classes -->
<!-- Comment complex sections -->

<!-- Bad -->
<div id="x" class="y">Content</div>

<!-- Good -->
<section id="services" class="services-section">
  <!-- Service listings -->
</section>
```

### CSS Changes

```css
/* Keep organized structure */
/* Use CSS variables */
/* Document non-obvious styles */

/* Good structure */
/* 1. Variables */
:root {
  --color-primary: #580000;
}

/* 2. Base styles */
body {
  background-color: var(--color-primary);
}

/* 3. Component styles */
.service-card {
  padding: 20px;
}

/* 4. Responsive */
@media (max-width: 768px) {
  .service-card {
    padding: 10px;
  }
}
```

### JavaScript Changes

```javascript
// Use meaningful names
// Add comments for complex logic
// Keep functions focused

// Bad
function x(a) {
  var b = a.value;
  alert(b);
}

// Good
function handleFormSubmit(formElement) {
  const userInput = formElement.value;
  // Validate and process input
  validateAndProcess(userInput);
}
```

---

## 🎨 Code Formatting

### Using Prettier (Optional)

```bash
# Install Prettier
npm install -g prettier

# Format file
prettier --write index.html

# Format all HTML
prettier --write "*.html"
```

### Manual Formatting Checklist

- ✓ Consistent indentation (2 spaces)
- ✓ Proper line breaks
- ✓ Organized CSS properties
- ✓ Meaningful variable/function names
- ✓ Comments for complex code

---

## 📚 Learning Resources

### HTML
- [MDN HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [HTML Best Practices](https://www.w3schools.com/html/default.asp)

### CSS
- [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS Tricks](https://css-tricks.com)
- [CSS Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

### JavaScript
- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [JavaScript.info](https://javascript.info)
- [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS)

### Git
- [Git Documentation](https://git-scm.com/doc)
- [Git Workflow Guide](./GIT-WORKFLOW.md)
- [Oh Shit, Git!?!](https://ohshitgit.com)

---

## 🚀 Performance Tips

### Optimize CSS
```css
/* Good: Use classes instead of IDs for styling */
.button { padding: 10px; }

/* Avoid: Overly specific selectors */
body > div > section > .service-card { padding: 10px; }

/* Good: Use CSS variables for maintainability */
:root { --spacing: 20px; }

/* Combine related properties */
.card {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
```

### Optimize JavaScript
```javascript
/* Cache DOM queries */
const form = document.getElementById('form');
form.addEventListener('submit', handleSubmit);

/* Use event delegation */
document.addEventListener('click', (e) => {
  if (e.target.matches('.btn')) {
    handleButtonClick(e);
  }
});

/* Avoid expensive operations in loops */
// Bad
for (let i = 0; i < arr.length; i++) {
  element.innerHTML += arr[i];
}

// Good
const html = arr.join('');
element.innerHTML = html;
```

---

## 🔍 Accessibility Checklist

- [ ] Semantic HTML used
- [ ] Alt text on images
- [ ] Keyboard navigation works
- [ ] Color contrast sufficient
- [ ] Form labels present
- [ ] Focus states visible
- [ ] ARIA labels where needed

---

## 📞 Getting Help

### Local Issues
1. Check browser console for errors (F12)
2. Clear browser cache (Ctrl+Shift+Delete)
3. Close and reopen Live Server
4. Check file paths and spelling

### Contributing Questions
1. Read CONTRIBUTING.md
2. Check existing issues/PRs
3. Review documentation
4. Ask in GitHub issues

### Technical Questions
1. Check relevant MDN documentation
2. Search Stack Overflow
3. Review code comments
4. Create an issue with detailed question

---

## ✅ Development Checklist

Before committing changes:

- [ ] Code formatted consistently
- [ ] No console errors
- [ ] Tested in multiple browsers
- [ ] Mobile responsive working
- [ ] Meaningful commit message
- [ ] Related files updated
- [ ] Documentation updated if needed

---

**Happy Developing!** 🚀

For more info, see [Git Workflow Guide](./GIT-WORKFLOW.md)
