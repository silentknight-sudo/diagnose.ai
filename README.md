# diagnose.ai

An AI-powered medical imaging analysis platform built with Node.js and modern web technologies. Leverages cutting-edge machine learning to provide instant insights, detailed analysis, and risk assessments for medical professionals.

## Features

- **AI-Powered Analysis**: Advanced machine learning algorithms analyze medical images with high accuracy using the Groq API
- **3D Visualization**: Convert 2D medical images into detailed 3D models for better surgical planning
- **Quantitative Analysis**: Get precise measurements including size, density, and volume with risk scores
- **Instant Results**: Receive comprehensive analysis within seconds
- **Secure & Compliant**: Enterprise-grade security with HIPAA compliance ready
- **Dark & Light Theme**: Professional dark healthcare theme with light mode toggle
- **Responsive Design**: Works seamlessly across desktop, tablet, and mobile devices
- **Demo Mode**: Full demo functionality without API key for testing and development

## Tech Stack

### Backend
- **Node.js & Express**: RESTful API server
- **Multer**: Image upload handling (in-memory storage, 10MB limit)
- **Axios**: HTTP client for Groq API integration
- **dotenv**: Environment variable management
- **CORS**: Cross-origin resource sharing support

### Frontend
- **HTML5**: Semantic markup
- **Tailwind CSS**: Utility-first CSS framework via CDN
- **Vanilla JavaScript**: No external dependencies for interactivity
- **Font Awesome**: Icon library for UI elements
- **Google Fonts (Inter)**: Professional typography

## Project Structure

```
diagnose.ai/
├── server.js                 # Express server entry point
├── package.json              # Dependencies and scripts
├── .env                       # Environment variables (not in repo)
├── README.md                 # This file
├── public/                    # Static assets
│   ├── index.html            # Landing/home page
│   ├── login.html            # Login page
│   ├── dashboard.html        # Main application dashboard
│   └── assets/
│       ├── css/
│       │   └── styles.css    # Custom styling (dark/light theme)
│       └── js/
│           └── main.js       # Frontend logic (auth, analysis, theme)
└── services/
    └── genai.js              # Groq API integration & demo generator
```

## Getting Started

### Prerequisites
- Node.js 14+ and npm/yarn
- Groq API key (optional - demo mode works without it)
- A modern web browser (Chrome, Firefox, Safari, Edge)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/silentknight-sudo/diagnose.ai.git
   cd diagnose.ai
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables** (create `.env` file in project root)
   ```env
   PORT=8000
   NODE_ENV=development
   GROQ_API_KEY=your_groq_api_key_here
   DEMO_MODE=true
   ```

   **Environment Variables:**
   - `PORT`: Server port (default: 8000)
   - `NODE_ENV`: Environment (development/production)
   - `GROQ_API_KEY`: Your Groq API key for medical image analysis
   - `DEMO_MODE`: Set to `true` to use demo data instead of API calls

### Running the Server

**Development mode with auto-reload:**
```bash
npm run dev
```

**Production mode:**
```bash
npm start
```

The server will start on `http://localhost:8000`

## Usage

### 1. Access the Application
- **Landing Page**: http://localhost:8000
- **Login**: http://localhost:8000/login
- **Dashboard**: http://localhost:8000/dashboard

### 2. Demo Credentials
For testing with demo mode enabled:
- **Email**: demo@diagnose.ai
- **Password**: demo123

### 3. Upload and Analyze
1. Log in to the dashboard
2. Upload a medical image (JPEG, PNG, or DICOM format)
3. View detailed analysis results including:
   - Risk scores (abnormality %, urgency level, confidence)
   - Quantitative measurements (size, density, volume)
   - Qualitative findings
   - Clinical recommendations

## API Endpoints

### Authentication
- `POST /api/login` - User login
  - Request body: `{ email: string, password: string }`
  - Response: `{ success: boolean, token?: string, message: string }`

### Analysis
- `POST /api/analyze` - Upload and analyze medical image
  - Multipart form with `image` file
  - Returns: Structured analysis with risk scores, measurements, and recommendations

### Health
- `GET /api/health` - Server health check
  - Response: `{ status: string, timestamp: string, version: string }`

## Theme Customization

### Dark Theme (Default)
Professional dark healthcare theme with:
- Dark background (#051421)
- Cyan accents (#06b6d4)
- Light text for readability

### Light Theme
Toggle between themes using the sun/moon button in the top-right corner. Theme preference is saved to localStorage.

### Customizing Colors
Edit `/public/assets/css/styles.css`:
```css
:root {
    --primary-color: #06b6d4;      /* Cyan accent */
    --primary-dark: #0891b2;
    --text-primary: #e6f0f6;       /* Light text */
    --text-secondary: #9fb3c8;     /* Muted light */
    --bg-light: #051421;           /* Dark background */
    /* ... more variables ... */
}
```

## Demo Mode

When `DEMO_MODE=true`, the application generates realistic demo medical analysis without requiring a Groq API key:
- Random risk scores and measurements
- Sample clinical findings
- Mock recommendations

Perfect for:
- Testing the UI/UX
- Development and debugging
- Demos to stakeholders
- Understanding the data flow

## Security Considerations

- **CORS**: Configured to handle cross-origin requests
- **File Upload**: Limited to 10MB, memory storage only
- **MIME Types**: Restricted to medical image formats (JPEG, PNG, DICOM)
- **Demo User**: For development only, should be removed in production
- **Environment Variables**: Keep `.env` and API keys private

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Development

### Project Scripts

```bash
npm start       # Run production server
npm run dev     # Run with nodemon (auto-reload)
npm install     # Install dependencies
```

### Code Organization

- `server.js` - Express routes and middleware
- `services/genai.js` - AI integration and analysis logic
- `public/assets/js/main.js` - Frontend state management and UI interactions
- `public/assets/css/styles.css` - Styling and theme variables

### Key Features Implementation

**Authentication** (`main.js`):
```javascript
diagnoseAI.auth.login(email, password)  // User login
diagnoseAI.auth.logout()                // Clear session
```

**Image Analysis** (`main.js`):
```javascript
diagnoseAI.analysis.uploadImage(file)   // Process medical image
diagnoseAI.analysis.displayResults()    // Show analysis
```

**Theme Toggle** (`main.js`):
```javascript
diagnoseAI.theme.init()                 // Initialize theme
diagnoseAI.theme.toggle()               // Switch dark/light
```

## Performance Optimization

- Lightweight dependencies (no heavy frameworks)
- In-memory image processing
- Efficient CSS with semantic classes
- Font smoothing and optimized rendering
- Responsive image handling

## Future Enhancements

- [ ] User registration and authentication system
- [ ] Patient record management
- [ ] Multi-image batch analysis
- [ ] Report generation (PDF export)
- [ ] Integration with PACS systems
- [ ] Real-time collaboration features
- [ ] Advanced 3D visualization engine
- [ ] Machine learning model fine-tuning
- [ ] Mobile native app (React Native)

## Troubleshooting

### Server won't start
- Check if port 8000 is already in use: `lsof -i :8000`
- Try a different port: `PORT=3000 npm start`

### Images not uploading
- Ensure file size is under 10MB
- Check if MIME type is supported (JPEG, PNG, DICOM)
- Verify server is running (`curl http://localhost:8000/api/health`)

### Demo data not showing
- Confirm `DEMO_MODE=true` in `.env`
- Clear browser cache and localStorage
- Refresh the page

### Theme not persisting
- Check browser localStorage is enabled
- Verify localStorage permissions in browser settings

## License

Proprietary - All rights reserved

## Support

For issues, questions, or contributions:
- GitHub Issues: [project-issues]
- Email: contact@diagnose.ai
- Documentation: http://localhost:8000#features

## Authors

- **silentknight-sudo** - Creator & Maintainer

---

**Last Updated**: December 2025 | **Version**: 1.0.0
