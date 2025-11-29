# Web Print Portal

A modern, user-friendly web application designed to streamline document printing. Users can upload files, specify the number of copies, and send print jobs directly to a configured printer via a webhook endpoint.

Built with React and TypeScript, this portal provides a clean interface with dark mode support and real-time feedback for a seamless printing experience.

---

## Features

### Core Functionality
- **📄 Document Upload** - Drag-and-drop or click to upload files for printing
- **🔢 Copy Control** - Specify number of copies with manual input or increment/decrement buttons
- **❌ File Management** - Remove uploaded files before submission to select different documents
- **✅ Real-time Feedback** - Status messages keep users informed throughout the print process

### User Experience
- **🌓 Dark Mode** - Automatic theme detection based on system preferences with manual toggle
- **📱 Responsive Design** - Works seamlessly on desktop, tablet, and mobile devices
- **♿ Accessible** - ARIA labels and semantic HTML for screen reader compatibility
- **⚡ Fast & Lightweight** - Minimal dependencies with optimized performance

### Technical
- **🔒 Secure Configuration** - Environment variables for API keys and webhook URLs
- **🔄 Auto-dismiss Notifications** - Success and error messages automatically clear after 5 seconds
- **🎨 Modern UI** - Tailwind CSS styling with smooth transitions and hover effects

---

## Prerequisites

- **Node.js** (v14 or higher recommended)
- **npm** or **yarn** package manager
- A webhook endpoint configured to receive print jobs (e.g., n8n, Zapier, custom API)

---

## Installation & Setup

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd Web-Print-Portal
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Environment Variables

Copy the example environment file:
```bash
cp .env.example .env.local
```

Edit `.env.local` and configure the following variables:

| Variable | Description | Required |
|----------|-------------|----------|
| `VITE_APP_TITLE` | Custom application title displayed in the UI | ❌ No (default: "Web Print Portal") |
| `VITE_PRINT_API_KEY` | API key for authenticating with your print webhook | ✅ Yes |
| `VITE_PRINT_WEBHOOK_URL` | Full URL of your print webhook endpoint | ✅ Yes |

**Example `.env.local`:**
```env
VITE_APP_TITLE=My Custom Print Portal
VITE_PRINT_API_KEY=your-api-key-here
VITE_PRINT_WEBHOOK_URL=https://your-webhook.com/endpoint
```

### 4. Run the Development Server
```bash
npm run dev
```

The application will be available at `http://localhost:3000`

---

## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server on port 3000 |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build locally |

---

## Building for Production

### 1. Create a Production Build

To build the application for production deployment:

```bash
npm run build
```

This command:
- Compiles TypeScript to JavaScript
- Bundles all assets using Vite
- Minifies code for optimal performance
- Outputs static files to the `dist/` directory

### 2. Preview the Production Build (Optional)

Before deploying, you can test the production build locally:

```bash
npm run preview
```

This starts a local server serving the production build from the `dist/` directory, allowing you to verify everything works as expected.

### 3. Deploy the Build

The `dist/` folder contains all the static files needed for deployment. You can deploy these files to any static hosting service:

**Popular Hosting Options:**
- **Netlify** - Drag and drop the `dist/` folder or connect your Git repository
- **Vercel** - Import your repository or use the Vercel CLI
- **GitHub Pages** - Host directly from your repository
- **AWS S3** - Upload to an S3 bucket with static website hosting
- **Traditional Web Server** - Copy `dist/` contents to your web server's public directory (e.g., `/var/www/html`)

**Example: Deploy to a Web Server**
```bash
# After building, copy dist contents to your web server
scp -r dist/* user@yourserver.com:/var/www/html/
```

**Important Notes:**
- Ensure your `.env.local` variables are properly configured before building
- The production build includes your environment variables in the JavaScript bundle
- Configure your web server to serve `index.html` for all routes (SPA fallback)

---

## How It Works

1. **User uploads a file** through the drag-and-drop interface
2. **User specifies number of copies** (default: 1)
3. **Form submits** the file and copy count to the configured webhook
4. **Webhook processes** the print job (requires external configuration)
5. **User receives feedback** via success or error messages

### API Request Format

The application sends a `POST` request with:
- **Method:** `POST`
- **Headers:** `X-API-KEY` with your configured API key
- **Body:** `multipart/form-data` containing:
  - `file` - The uploaded document
  - `copies` - Number of copies to print

---

## Technology Stack

- **React 19.2.0** - UI framework
- **TypeScript** - Type-safe development
- **Vite 6.2.0** - Build tool and dev server
- **Tailwind CSS** - Utility-first styling (via CDN)
- **ES Modules** - Modern JavaScript modules

---

## Configuration

### Customization

**Application Title**

You can customize the application title by setting the `VITE_APP_TITLE` environment variable in your `.env.local` file:

```env
VITE_APP_TITLE=Acme Corp Print Portal
```

If not set, the default title "Web Print Portal" will be displayed. This allows you to brand the portal for your organization or specific use case.

### Webhook Requirements

Your webhook endpoint should:
- Accept `POST` requests with `multipart/form-data`
- Validate the `X-API-KEY` header
- Process the `file` and `copies` fields
- Return appropriate HTTP status codes (200 for success)

### Example Webhook Integration

This portal works well with:
- **n8n** - Workflow automation platform
- **Zapier** - No-code automation
- **Custom APIs** - Any endpoint accepting multipart form data

---

## Security Notes

⚠️ **Important:** API keys and webhook URLs are exposed in the frontend JavaScript bundle. While environment variables protect them from Git, they remain visible in the browser.

**Recommendations:**
- Use API keys with limited permissions
- Implement rate limiting on your webhook
- Consider adding a backend proxy for production deployments
- Restrict webhook access by IP or domain when possible

---

## License

MIT License - see [LICENSE](LICENSE) file for details.

---

## Support

For issues, questions, or contributions, please open an issue in the repository.
