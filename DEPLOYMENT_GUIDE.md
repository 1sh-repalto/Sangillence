# Backend Deployment Guide

## 🚀 Quick Deploy Options

### Option 1: Railway (Recommended - Easy & Free)

1. **Sign up at [Railway.app](https://railway.app)**
2. **Connect your GitHub repository**
3. **Create new project from GitHub**
4. **Set environment variables:**
   ```
   GOOGLE_SHEETS_PRIVATE_KEY=your-private-key
   GOOGLE_SHEETS_CLIENT_EMAIL=your-service-account@project.iam.gserviceaccount.com
   GOOGLE_SHEETS_STUDENT_SPREADSHEET_ID=your-student-sheet-id
   GOOGLE_SHEETS_SCHOOL_SPREADSHEET_ID=your-school-sheet-id
   NODE_ENV=production
   PORT=5000
   CLOUDINARY_CLOUD_NAME=your-cloud-name
   CLOUDINARY_API_KEY=your-api-key
   CLOUDINARY_API_SECRET=your-api-secret
   ```
5. **Deploy!** Railway will automatically detect the Node.js app and deploy it.

### Option 2: Render (Alternative - Free tier)

1. **Sign up at [Render.com](https://render.com)**
2. **Create new Web Service**
3. **Connect your GitHub repository**
4. **Configure:**
   - **Name:** sangillence-backend
   - **Environment:** Node
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Health Check Path:** `/health`
5. **Add environment variables** (same as above)
6. **Deploy!**

### Option 3: Vercel (Serverless)

1. **Sign up at [Vercel.com](https://vercel.com)**
2. **Import your GitHub repository**
3. **Configure as Node.js project**
4. **Add environment variables** (same as above)
5. **Deploy!**

## 🔧 Environment Variables Setup

### Required Variables:
```bash
# Google Sheets API
GOOGLE_SHEETS_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\nYour Private Key Here\n-----END PRIVATE KEY-----\n"
GOOGLE_SHEETS_CLIENT_EMAIL="your-service-account@your-project.iam.gserviceaccount.com"
GOOGLE_SHEETS_STUDENT_SPREADSHEET_ID="your-student-spreadsheet-id"
GOOGLE_SHEETS_SCHOOL_SPREADSHEET_ID="your-school-spreadsheet-id"

# Server Configuration
PORT=5000
NODE_ENV=production

# Cloudinary (for file uploads)
CLOUDINARY_CLOUD_NAME="your-cloud-name"
CLOUDINARY_API_KEY="your-api-key"
CLOUDINARY_API_SECRET="your-api-secret"
```

## 📋 Pre-deployment Checklist

- [ ] All environment variables are set
- [ ] Google Sheets API credentials are configured
- [ ] Spreadsheet IDs are correct
- [ ] CORS origins are updated for production
- [ ] Frontend API endpoints are updated to use production URL

## 🔄 Update Frontend API URLs

After deployment, update your frontend API calls:

```javascript
// Change from:
const response = await fetch('http://localhost:5001/api/student/submit', {

// To:
const response = await fetch('https://your-backend-url.railway.app/api/student/submit', {
```

## 🧪 Testing Deployment

1. **Health Check:** `GET https://your-backend-url/health`
2. **Student Registration:** `POST https://your-backend-url/api/student/submit`
3. **School Registration:** `POST https://your-backend-url/api/school/submit`

## 🚨 Troubleshooting

### Common Issues:
1. **CORS Errors:** Check CORS configuration in server.js
2. **Environment Variables:** Ensure all required variables are set
3. **Google Sheets Access:** Verify service account has proper permissions
4. **Port Issues:** Some platforms use different default ports

### Debug Commands:
```bash
# Check if server is running
curl https://your-backend-url/health

# Test student registration
curl -X POST https://your-backend-url/api/student/submit \
  -H "Content-Type: application/json" \
  -d '{"fullName":"Test","dob":"2020-01-01","email":"test@test.com","class":"4","mobile":"1234567890","schoolEmail":"school@test.com"}'
```

## 📊 Monitoring

- **Railway:** Built-in monitoring dashboard
- **Render:** Application logs and metrics
- **Vercel:** Function logs and analytics

## 🔒 Security Notes

- Never commit `.env` files to version control
- Use environment variables for all sensitive data
- Enable HTTPS in production
- Regularly rotate API keys 