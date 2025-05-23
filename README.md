# 📊 Easy Agile ROI Calculator

Live Demo: https://easy-agile-roi-calculator.netlify.app/

Welcome! This project is a complete **React + Node.js** web application that allows users to:

- Fill out a form and get ROI calculations
- Automatically generate a beautiful, lightweight PDF report (with charts and personalized name)
- Send the report to their email
- Store the submission securely in a MongoDB database

---

## 🔗 Project Repositories

| Project Part | GitHub Repository                                                                       |
| ------------ | --------------------------------------------------------------------------------------- |
| 💻 Frontend  | [Easy-Agile-ROI-Calculator](https://github.com/Leon380Becker/Easy-Agile-ROI-Calculator) |
| 🔧 Backend   | [Roi-backend](https://github.com/Leon380Becker/roi-backend)                             |

---

## 🗂️ What's in the ZIP Package

You’re receiving the **raw React app source code** zipped, ready for:

- Review
- Rebuilding
- Customizing
- Deploying

🔐 Note: `.env` files have been removed for security. You'll find a `env.txt` placeholder that shows the expected environment variables.

---

## ⚙️ How to Run or Customize Locally

### 💻 1. Frontend Setup (React)

#### ✅ Prerequisites

- Node.js installed: [https://nodejs.org](https://nodejs.org)

#### 📦 Install Dependencies

```bash
cd Easy-Agile-ROI-Calculator
npm install
```

#### ⚙️ Environment Setup

Create a `.env.local` file (at root) and add:

```
REACT_APP_BACKEND_URL=https://your-backend-url.com
```

#### 🚀 Run the App

```bash
npm start
```

#### 🛠 To Customize

- All ROI logic is located in `src/components` and `src/utils`.
- To update styles or layout, modify `src/pages/Home.jsx` and relevant components.

---

### 🛠️ 2. Backend Setup (Node.js + Express)

#### ✅ Prerequisites

- Node.js installed
- MongoDB Atlas account (or local MongoDB)

#### 📦 Install Dependencies

```bash
cd roi-backend
npm install
```

#### ⚙️ Create `.env` File

Use the `env.txt` file as a guide. Create `.env` and add:

```
PORT=5000
MONGO_URI=your_mongodb_connection_string
EMAIL_USER=your_email_address
EMAIL_PASS=your_email_password_or_app_password
```

> 🛑 Never commit this `.env` file to GitHub!

#### 🚀 Run the Server

```bash
npm start
```

Server will start at `http://localhost:5000` and your frontend can talk to it via API.

---

## 🌐 Deployment Instructions

### 💻 Frontend Hosting (e.g. Netlify, Vercel)

1. Push your frontend code to GitHub
2. Connect to Netlify or Vercel
3. Add `REACT_APP_BACKEND_URL` as an environment variable in their dashboard
4. Trigger build (Netlify does it automatically)

### ⚙️ Backend Hosting (Recommended: Render)

1. Go to [https://render.com](https://render.com)
2. Create a **Web Service**
3. Connect to the GitHub repo: [roi-backend](https://github.com/Leon380Becker/roi-backend)
4. Set Build Command: `npm install`
5. Set Start Command: `node server.js`
6. Add your `.env` values under "Environment Variables"
7. Deploy and copy your public backend URL

---

## 🌐 Integration into Webflow

## ⚙️ Option A: Iframe Embed (Quick Start)

Use this method if you want to embed the entire app via an iframe into a Webflow or other CMS site with minimal setup.

### ✅ Steps

1. Deploy your frontend (e.g. to Netlify or Vercel)
2. Copy the live URL
3. In Webflow, use an **Embed Component** and paste the iframe:

```html
<iframe
  src="https://easy-agile-roi-calculator.netlify.app"
  width="100%"
  height="800"
  style="border:none; overflow:hidden;"
  title="ROI Calculator"></iframe>
```

### ⚠️ Notes
- Fastest setup with zero code edits
- No Webflow animations/custom styles inside iframe
- Make sure the app is responsive

---

## ⚙️ Option B: Full Code Embed (Advanced)

Use this option for tighter design control or Webflow-native animations.

### 🛠️ Build the Frontend App

```bash
npm run build
```

1. Copy everything from the `/build` folder
2. In Webflow:
   - Go to Page Settings > Custom Code
   - Paste the HTML and link to the JS/CSS files
   - Upload assets via Webflow's Asset Library
   - Update asset paths as needed

### ⚠️ Important
- You may need Webflow’s Business hosting plan

---

## 📩 HubSpot CMS Integration

You can also store submitted data in HubSpot CRM, in addition to MongoDB.

### 🔧 Requirements
- HubSpot Portal ID
- HubSpot Form GUID
- HubSpot Private App Access Token (recommended)

### 🧩 Backend Integration Example

In your `roi-backend/server.js`:

```js
const axios = require('axios');

const sendToHubSpot = async (name, email) => {
  const HUBSPOT_FORM_URL = 'https://api.hsforms.com/submissions/v3/integration/submit/YOUR_PORTAL_ID/YOUR_FORM_GUID';

  const payload = {
    fields: [
      { name: 'firstname', value: name },
      { name: 'email', value: email }
    ]
  };

  try {
    await axios.post(HUBSPOT_FORM_URL, payload, {
      headers: {
        'Content-Type': 'application/json'
      }
    });
    console.log('✅ HubSpot submission successful.');
  } catch (error) {
    console.error('❌ HubSpot integration failed:', error.message);
  }
};
```

Invoke this function after handling the form submission and PDF dispatch:

```js
await sendToHubSpot(name, email);
```

---

## 📁 Folder Structure Highlights

**Frontend**

```
src/
│
├── components/         # ROI calculator, inputs, and graph
├── assets/             # Images used in app and PDF
├── pdf/                # Custom PDF layout (React-PDF)
└── Helpers/Index.js      # Main app logic
```

**Backend**

```
models/
└── Submission.js       # Mongoose schema for form data

public/
└── assets/             # Banner image for email

server.js               # Express server entry point
```

---

## 📧 PDF + Email Integration

- When users submit the form, a PDF is generated in the frontend and sent to the backend.
- The backend:
  - Stores the submission in MongoDB
  - Sends the PDF to the user via Nodemailer (with header banner)

---

## 💼 Feature Summary

| Feature                   | Supported | Details                                                                 |
|--------------------------|-----------|-------------------------------------------------------------------------|
| Webflow Iframe Embed     | ✅ Yes    | Fastest setup using hosted calculator URL                              |
| Webflow Code Embed       | ✅ Yes    | Full control via build output (HTML, CSS, JS)                          |
| HubSpot CRM Sync         | ✅ Yes    | Send user name + email to HubSpot using Forms API                      |
| MongoDB Storage          | ✅ Yes    | Local database storage for internal reporting                          |
| PDF Generation + Email   | ✅ Yes    | Personalized PDF with branding sent to user email                      |

---

## 🚧 Development Tips

- Use `console.log()` generously to debug form data, PDF generation, and backend errors.
- Check Render logs if anything fails during deployment.
- Keep `.env` safe — do not commit it to GitHub.
- If sending emails via Gmail, use an **App Password** and enable "Less secure app access" if needed.

---

## 🧑‍💻 For Developers

- This project is modular and easy to customize.
- Replace branding and banners by swapping the image in `/public/assets/EA_ROI_EDM_Header.png`
- PDF layout can be adjusted in `src/components/pdf`

---

## 🤝 A Note from the Developer

This project was crafted with care and is fully functional both locally and in production. If you need to:

- Modify logic
- Add custom styles
- Extend functionality (e.g. PDF pages or extra fields)

...it's all clearly organized for you to jump in. Happy building!

