# LCLS Maintenance Dashboard

A standalone single-file web application for the LCLS (Linac Coherent Light Source) Maintenance Dashboard.

## 🌐 Live Demo

Once GitHub Pages is configured, the site will be available at:
**https://planetoftheweb.github.io/maint-test/**

## 🚀 GitHub Pages Setup

This repository is now configured to deploy automatically to GitHub Pages using GitHub Actions.

### Required Configuration Steps

To complete the GitHub Pages setup:

1. Go to **Settings** → **Pages** in your GitHub repository
2. Under **"Build and deployment"**, set:
   - **Source**: `GitHub Actions` (not "Deploy from a branch")
3. Save the changes

The deployment workflow will run automatically when you push to the `copilot/fix-github-pages-issues` branch.

### Manual Deployment

You can also trigger a deployment manually:
1. Go to **Actions** tab in GitHub
2. Select **"Deploy to GitHub Pages"** workflow
3. Click **"Run workflow"**

## 📁 Project Structure

```
maint-test/
├── index.html                    # Complete standalone application
├── maintenance-dashboard.jsx     # Legacy React component (not used)
├── .nojekyll                     # Disables Jekyll processing
├── .github/
│   └── workflows/
│       └── deploy.yml           # GitHub Pages deployment workflow
├── CLAUDE.md                     # Development guide for AI assistants
└── README.md                     # This file
```

## 🛠️ Technology Stack

All dependencies are loaded via CDN (no build process required):

- **React 18** - UI framework
- **Chart.js 4.4.0** - Data visualizations
- **Tailwind CSS** - Styling
- **Babel Standalone** - In-browser JSX transformation

## 🔧 Local Development

Simply open `index.html` in any modern web browser:

```bash
# Using Python's built-in HTTP server
python3 -m http.server 8080

# Then visit http://localhost:8080
```

No build, compilation, or installation required!

## 📊 Features

The dashboard includes 6 main views:

1. **Overview** - Key metrics and summary statistics
2. **Equipment** - Maintenance frequency, on-time performance, and downtime by equipment
3. **Technicians** - Workload distribution and performance analysis
4. **Tasks** - Task type frequency and downtime patterns
5. **Trends** - Monthly trends over Q1 2024
6. **AI** - Interface for AI-powered analysis (demo mode)

## 🐛 Troubleshooting

### GitHub Pages not working?

**Issue**: Site not deploying or showing 404

**Solutions**:
1. ✅ Ensure GitHub Pages source is set to "GitHub Actions" (not "Deploy from a branch")
2. ✅ Check that the `.nojekyll` file exists in the repository root
3. ✅ Verify the workflow ran successfully in the Actions tab
4. ✅ Check that GitHub Pages is enabled for your repository

### Console warnings in browser?

The following warnings are expected in development and can be ignored:
- Tailwind CSS CDN usage warning
- Babel in-browser transformer warning

These are suggestions for production builds but don't affect functionality.

## 📝 Data

All maintenance data is embedded as a CSV string within the application (no external API calls).

## 🤝 Contributing

This is a demonstration project. To modify:

1. Edit `index.html` directly - all code is in one file
2. Test locally by opening in a browser
3. Push changes to trigger automatic deployment

## 📄 License

This project is for demonstration purposes.
