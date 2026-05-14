# Contributing to Lalasa Private Ltd Website

Thank you for your interest in contributing! We welcome all contributions that help improve our website and services.

## 🤝 How to Contribute

### Reporting Issues

Found a bug? Have a suggestion? Please create an issue:

1. Go to the [Issues](https://github.com/banjarasudesh33-web/Company-website/issues) page
2. Click "New Issue"
3. Choose a template (Bug Report or Feature Request)
4. Fill in the details clearly

**Bug Report Template:**
```
**Describe the bug:**
A clear description of what the bug is.

**Steps to reproduce:**
1. Go to '...'
2. Click on '...'
3. See error '...'

**Expected behavior:**
What you expected to happen.

**Actual behavior:**
What actually happened.

**Environment:**
- Browser: [e.g., Chrome 95]
- OS: [e.g., macOS 12]
```

**Feature Request Template:**
```
**Describe the feature:**
Clear description of what you want to add.

**Why is this useful?**
Explain the benefit.

**Suggested implementation:**
How you think it should work.
```

### Development Workflow

1. **Fork the Repository**
   ```bash
   # Click "Fork" button on GitHub
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/Company-website.git
   cd Company-website
   ```

3. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or for bug fixes:
   git checkout -b fix/bug-description
   ```

4. **Make Your Changes**
   - Keep changes focused and related
   - Follow the project's code style
   - Update documentation as needed

5. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "feat: add your feature" 
   # or
   git commit -m "fix: resolve specific bug"
   ```

6. **Push to Your Fork**
   ```bash
   git push origin feature/your-feature-name
   ```

7. **Create a Pull Request**
   - Go to the original repository
   - Click "Compare & pull request"
   - Fill in the PR template
   - Link any related issues

### Commit Message Guidelines

Follow conventional commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat:` - A new feature
- `fix:` - A bug fix
- `docs:` - Documentation only changes
- `style:` - Changes that don't affect code meaning (formatting, CSS)
- `refactor:` - Code change that neither fixes a bug nor adds a feature
- `perf:` - Code change that improves performance
- `test:` - Adding missing tests or correcting existing tests
- `chore:` - Changes to build process, dependencies, etc.

**Examples:**
```bash
git commit -m "feat(contact-form): add email validation"
git commit -m "fix(navigation): resolve mobile menu toggle"
git commit -m "docs(readme): update deployment instructions"
```

## 📋 Pull Request Process

### Before Submitting

- [ ] Fork and clone the repository
- [ ] Create a descriptive branch name
- [ ] Make focused, atomic commits
- [ ] Test your changes locally
- [ ] Update documentation if needed
- [ ] Follow code style guidelines

### PR Description Template

```markdown
## Description
Brief description of what this PR does.

## Related Issues
Closes #123

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement
- [ ] Other (please describe)

## How Has This Been Tested?
Describe how you tested your changes.

## Screenshots (if applicable)
Add screenshots for UI changes.

## Checklist
- [ ] My code follows the style guidelines
- [ ] I have updated the documentation
- [ ] I have tested locally
- [ ] No new warnings generated
- [ ] Commits are meaningful and follow conventions
```

### Review Process

1. **Automated Checks** - GitHub will run basic checks
2. **Code Review** - Maintainers will review your code
3. **Feedback** - Address any comments or suggestions
4. **Approval** - Once approved, your PR will be merged
5. **Deployment** - Changes auto-deploy to GitHub Pages

## 🎨 Code Style Guidelines

### HTML
```html
<!-- Use semantic HTML5 elements -->
<section id="services">
  <h2 class="section-title">Our Services</h2>
  <!-- Content here -->
</section>

<!-- Keep indentation clean (2 spaces) -->
<!-- Use meaningful class names -->
```

### CSS
```css
/* Use CSS variables for colors and sizing */
:root {
  --maroon: #580000;
  --spacing-base: 20px;
}

/* Follow BEM naming convention */
.service-card {
  /* Block styles */
}

.service-card__title {
  /* Element styles */
}

.service-card--highlighted {
  /* Modifier styles */
}

/* Group related properties */
.element {
  /* Display properties */
  display: flex;
  flex-direction: column;
  
  /* Box model */
  padding: 20px;
  margin: 10px;
  
  /* Visual */
  background-color: var(--white);
  color: var(--dark-text);
  
  /* Transitions */
  transition: transform 0.3s ease;
}
```

### JavaScript
```javascript
// Use meaningful function names
function handleFormSubmit(event) {
  event.preventDefault();
  // Implementation
}

// Use const by default, let if needed, avoid var
const formElement = document.getElementById('form');

// Add comments for complex logic
// Validate email format against RFC standards
function isValidEmail(email) {
  // Implementation
}

// Use template literals
const message = `Thank you, ${name}! Your request has been sent.`;
```

## 🧪 Testing

### Manual Testing Checklist

- [ ] Test in Chrome/Edge
- [ ] Test in Firefox
- [ ] Test in Safari
- [ ] Test on mobile devices
- [ ] Test keyboard navigation
- [ ] Test form validation
- [ ] Check responsive breakpoints (768px)

### Browser Compatibility

Ensure your changes work on:
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile Safari (iOS 14+)
- Chrome Mobile (Android)

## 📚 Documentation

When adding features:

1. Update README.md if adding major features
2. Add inline code comments for complex logic
3. Update DEVELOPMENT.md if setup changes
4. Update GIT-WORKFLOW.md if workflow impacts change

## 🚀 Performance Tips

- Minimize CSS and keep it organized
- Avoid inline styles - use classes
- Use CSS variables for theming
- Keep JavaScript functions focused and reusable
- Use semantic HTML for better performance

## 🙏 Code of Conduct

### Be Respectful
- Treat everyone with respect
- Be welcoming to newcomers
- Provide constructive feedback

### Be Professional
- Use clear, professional language
- Focus on the code, not the person
- Help others learn and improve

### Be Collaborative
- Work together to solve problems
- Share knowledge and experience
- Support the community

## 📞 Questions?

- Open an issue with your question
- Check existing documentation
- Review past pull requests
- Reach out to maintainers

## 🎉 Recognition

Contributors will be recognized in:
- CONTRIBUTORS.md file
- GitHub contributors page
- Project announcements

---

**Thank you for making Lalasa Private Ltd website better!** ❤️
