# RemindMe - Email Reminder System

A full-stack web application that allows users to schedule email reminders for important tasks, deadlines, and communications. Built with Node.js, Express, MongoDB, and Nodemailer.

**Developer:** Froz Naasim N  
**Project:** IBM Naan Mudhalvan College Project

---

## Features

- User-friendly interface to schedule email reminders
- Automatic email delivery at scheduled times
- View and manage all your scheduled reminders
- Persistent data storage with MongoDB
- Beautiful responsive design with light theme
- Real-time reminder tracking

---

## Tech Stack

- **Backend:** Node.js, Express.js
- **Database:** MongoDB
- **Email Service:** Nodemailer
- **Scheduling:** Node-Cron
- **Frontend:** EJS, Bootstrap 5, HTML, CSS, JavaScript
- **Authentication:** EJS Layouts

---

## Prerequisites

Before you begin, ensure you have the following installed:

- Node.js (v14 or higher)
- npm (Node Package Manager)
- MongoDB (local or MongoDB Atlas cloud account)
- Git

---

## Installation

### Step 1: Clone or Download the Project

```bash
git clone <your-repository-url>
cd email-reminder-system
```

### Step 2: Install Dependencies

```bash
npm install
```

This will install all required packages from the `package.json` file.

### Step 3: Create Environment File

Create a `.env` file in the root directory of your project:

```bash
cp .env.example .env
```

Or manually create a `.env` file with the following variables.

### Step 4: Configure .env File

Open the `.env` file and add your configuration:

```env
# Server Configuration
PORT=3000
NODE_ENV=development

# MongoDB Configuration
MONGODB_URI=mongodb://localhost:27017/email-reminder

# For MongoDB Atlas (Cloud):
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/email-reminder?retryWrites=true&w=majority

# Email Configuration
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-specific-password
```

### Step 5: Set Up Database

If using local MongoDB:
```bash
# Make sure MongoDB service is running
mongod
```

If using MongoDB Atlas (Cloud):
- Create an account at https://www.mongodb.com/cloud/atlas
- Create a cluster
- Get your connection string
- Add it to MONGODB_URI in .env

### Step 6: Set Up Email Service

**For Gmail:**

1. Go to https://myaccount.google.com/security
2. Enable "2-Step Verification"
3. Go to https://myaccount.google.com/apppasswords
4. Select "Mail" and "Windows Computer"
5. Copy the generated 16-character password
6. Add to EMAIL_PASS in .env file

**For Other Email Services:**

Replace EMAIL_USER and EMAIL_PASS with your email credentials from:
- Outlook
- Yahoo
- Gmail
- Any SMTP-compatible email service

### Step 7: Run the Application

```bash
npm start
```

Or for development with auto-reload:

```bash
npm run dev
```

The application will run on `http://localhost:3000`

---

## Environment Variables (.env) Explained

| Variable | Description | Example |
|----------|-------------|---------|
| `PORT` | Server port number | 3000 |
| `NODE_ENV` | Environment mode | development or production |
| `MONGODB_URI` | MongoDB connection string | mongodb://localhost:27017/email-reminder |
| `EMAIL_USER` | Your email address | your-email@gmail.com |
| `EMAIL_PASS` | Email app-specific password | xxxx xxxx xxxx xxxx |

---

## How to Use

### 1. Access the Application

Open your browser and go to:
```
http://localhost:3000
```

### 2. Schedule a Reminder

1. Click on the **"Schedule"** button in the navigation bar
2. Fill in the following details:
   - **Email Address:** Where you want to receive the reminder
   - **Reminder Message:** What you want to be reminded about
   - **Date & Time:** When you want to be reminded
3. Click **"Schedule Reminder"**
4. You'll see a success message confirming the reminder is scheduled

### 3. View Your Reminders

1. Click on **"My Reminders"** in the navigation bar
2. You'll see a table with all your scheduled reminders
3. Each reminder shows:
   - Email address
   - Reminder message
   - Scheduled date and time
   - Status (Pending or Sent)

### 4. How Reminders Work

- The system checks for due reminders every minute
- When the scheduled time arrives, an email is automatically sent
- The reminder status changes from "Pending" to "Sent"
- You receive the email in your inbox

---

## Important Notes

### Email Delivery

- Reminders are processed every 60 seconds
- Make sure your MongoDB connection is active
- The application must be running for reminders to be sent
- Check your spam/junk folder if you don't receive emails

### MongoDB Connection Issues

If you get a MongoDB connection error:

1. Check if MongoDB service is running (local)
2. Verify MONGODB_URI is correct in .env
3. For MongoDB Atlas, ensure IP is whitelisted (allow 0.0.0.0/0 for development)

### Email Issues

If emails are not being sent:

1. Verify EMAIL_USER and EMAIL_PASS are correct
2. For Gmail, ensure you used an App Password (not your regular password)
3. Check that 2-Step Verification is enabled on Gmail
4. Allow less secure app access if needed

---

## Project Structure

```
email-reminder-system/
├── app.js                 # Main Express app
├── models/
│   └── reminder.js        # Reminder database model
├── views/
│   ├── layout.ejs        # Base layout template
│   ├── index.ejs         # Home page
│   ├── schedule.ejs      # Schedule reminder page
│   ├── reminders.ejs     # View reminders page
│   └── about.ejs         # About page
├── public/               # Static files (CSS, JS)
├── .env.example          # Environment variables example
├── package.json          # Project dependencies
└── README.md            # This file
```

---

## Troubleshooting

### Problem: Port Already in Use

**Solution:** 
Change PORT in .env file to a different number (e.g., 3001, 3002) or kill the process using port 3000:

```bash
# On Windows
netstat -ano | findstr :3000

# On Mac/Linux
lsof -ti:3000 | xargs kill -9
```

### Problem: MongoDB Connection Error

**Solution:**
- Ensure MongoDB is running
- Check MONGODB_URI in .env
- Test connection string in MongoDB Compass

### Problem: Emails Not Sending

**Solution:**
- Verify EMAIL_USER and EMAIL_PASS are correct
- Check email service SMTP settings
- Review application logs for errors

### Problem: Reminders Not Processing

**Solution:**
- Ensure application is running
- Check MongoDB connection
- Verify Node-Cron is properly configured
- Check scheduled time is in future

---

## Development

### Available Scripts

```bash
# Start production server
npm start

# Start development server with auto-reload
npm run dev
```

### Making Changes

The application will work as follows:

1. User submits reminder form → Saved to MongoDB
2. Cron job checks for due reminders every minute
3. When due, email is sent via Nodemailer
4. Reminder status updated to "Sent"

If you want to modify the check frequency:
- Edit `app.js` 
- Change `cron.schedule('* * * * *')` to your desired frequency

---

## Contact

**Developer:** Froz Naasim N

For any questions or issues with this project, please review the troubleshooting section above or contact the developer.

---

## License

MIT License - Feel free to use this project for educational purposes.

---

**Last Updated:** 2025  
**Version:** 1.0.0