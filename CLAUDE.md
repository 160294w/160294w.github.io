## Repository Structure and Jekyll Multi-Theme Deployment

### Repository Layout
- Contains multiple Jekyll themes deployed as static sites
- Organized with separate theme directories (theme1/, theme2/)
  - obsidian, mypage, everyday
- Optional GitHub Actions for automated deployment
- Uses GitHub Pages for hosting multiple static sites

### Theme Building Process
- Themes are pre-built using Jekyll
- Source directories are kept separate from output directories
- Build command pattern: `jekyll build --source ./sourceX --destination ./themeX`

### Deployment Strategy
- Hosts multiple themes under same repository
- Access themes via GitHub Pages URLs
- Optional index.html as portal linking to different themes

### Key Considerations
- Use GitHub Pages "Deploy from main branch / root folder" mode
- Themes are static HTML, CSS, JS outputs
- Source Jekyll projects can be in separate repositories or branches