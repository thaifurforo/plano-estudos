# GitHub Copilot Instructions

## Context
This document provides comprehensive guidance for leveraging GitHub Copilot to prepare for a Senior Software Engineer position. The focus will include skills, certifications, and resources specific to this role, tailored for Brazilian Portuguese speakers.

## Requirements
### Language
- Proficiency in Brazilian Portuguese is essential for understanding documentation and resources available in this language.

### Skills Development
1. **Programming Languages**
   - Focus on languages relevant to the industry, such as Python, JavaScript, and Go.
2. **System Design**
   - Study principles of scalable architecture, microservices, and cloud-based solutions.
3. **Software Development Practices**
   - Emphasize agile methodologies, DevOps, and continuous integration/continuous deployment (CI/CD).

### Certifications
- Explore certification paths that may enhance your profile, such as:
  - AWS Certified Solutions Architect
  - Google Cloud Professional Developers
  - Full Stack Developer certifications.

## Using MkDocs
MkDocs is a static site generator that's geared towards project documentation, and it's perfect for creating a personalized study guide.

### Installation
1. Ensure you have Python installed on your system.
2. Use pip to install MkDocs:
   ```bash
   pip install mkdocs
   ```
3. Create a new project:
   ```bash
   mkdocs new my-project
   cd my-project
   ```

### Development
- To start a local development server and preview your documentation, run:
  ```bash
  mkdocs serve
  ```

### Structure Your Documentation
- Create structured documents in the `docs` directory. Use Markdown for easy formatting. 
- Example:
  - `src/` folder for source code.
  - `docs/` folder for your documentation content.

## Deployment to GitHub Pages
### Step-by-step Guide
1. Make sure your `mkdocs.yml` is properly configured. 
2. Build your documentation:
   ```bash
   mkdocs build
   ```
3. Deploy to GitHub Pages:
   ```bash
   mkdocs gh-deploy
   ```

4. Configuring your GitHub repository for Pages:
   - Go to your repository settings and configure GitHub Pages to serve from the `gh-pages` branch.

By following these instructions, you will be well-prepared in using GitHub Copilot for advancing your career as a Senior Software Engineer in Brazil.