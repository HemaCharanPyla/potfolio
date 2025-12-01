# Database Setup Guide for Contact Form

## Overview
This guide explains how to set up the MongoDB database for your contact form.

## Prerequisites
- **Node.js** (v14 or higher) - Download from https://nodejs.org/
- **MongoDB** (Community Edition) - Download from https://www.mongodb.com/try/download/community

## Installation Steps

### 1. Install Node.js
- Download and install from https://nodejs.org/
- Verify installation: `node --version` and `npm --version`

### 2. Install MongoDB
- Download MongoDB Community Edition from https://www.mongodb.com/try/download/community
- Follow the installation guide for your OS
- Start MongoDB service

**For Windows:**
- MongoDB is installed as a Windows Service by default
- Run Services (services.msc) and ensure "MongoDB Server" is running
- Or manually start: `mongod` from MongoDB bin folder

**For Mac:**
- If using Homebrew: `brew services start mongodb-community`

**For Linux:**
- Use your package manager or follow MongoDB installation guide

### 3. Install Project Dependencies
Navigate to your project folder and run:
```bash
npm install
```

This will install:
- **express**: Web framework for Node.js
- **mongoose**: MongoDB object modeling
- **cors**: Enable cross-origin requests
- **dotenv**: Environment variables management

### 4. Configure Environment Variables
The `.env` file is already created. You can modify it if needed:
```
MONGODB_URI=mongodb://localhost:27017/vcard_portfolio
PORT=3000
NODE_ENV=development
```

### 5. Start the Server
Run one of these commands:

**Development (with auto-reload):**
```bash
npm run dev
```

**Production:**
```bash
npm start
```

You should see:
```
MongoDB connected successfully
Server running on http://localhost:3000
```

## API Endpoints

### POST /api/contact
Send a new contact message
```
Method: POST
URL: http://localhost:3000/api/contact
Body: {
  "fullname": "John Doe",
  "email": "john@example.com",
  "message": "Your message here"
}
```

### GET /api/messages
Retrieve all contact messages
```
Method: GET
URL: http://localhost:3000/api/messages
```

### GET /api/messages/:id
Get a specific message by ID
```
Method: GET
URL: http://localhost:3000/api/messages/[message_id]
```

### DELETE /api/messages/:id
Delete a message
```
Method: DELETE
URL: http://localhost:3000/api/messages/[message_id]
```

## Database Structure

### Contact Collection
Each message stored in MongoDB has this structure:
```json
{
  "_id": ObjectId,
  "fullname": "String",
  "email": "String",
  "message": "String",
  "createdAt": "Date"
}
```

## Testing the Form

1. Start MongoDB service
2. Run `npm install` (if not already done)
3. Run `npm run dev` to start the server
4. Open your portfolio in a browser (http://localhost:3000)
5. Go to the Contact section
6. Fill in and submit the contact form
7. Check the browser console (F12) for success/error messages
8. Messages are automatically saved to MongoDB

## Verify Messages in Database

### Using MongoDB Compass (GUI)
1. Download MongoDB Compass from https://www.mongodb.com/products/tools/compass
2. Connect to `mongodb://localhost:27017`
3. Navigate to `vcard_portfolio` database
4. View the `contacts` collection

### Using MongoDB Shell
```bash
# Start MongoDB shell
mongosh

# Or for older versions
mongo

# Switch to database
use vcard_portfolio

# View all messages
db.contacts.find()

# View formatted
db.contacts.find().pretty()
```

## Troubleshooting

**Issue: "Cannot GET /"**
- Make sure static files are being served from the correct directory
- Check that the server is running on http://localhost:3000

**Issue: "MongoDB connection error"**
- Ensure MongoDB service is running
- Check that `MONGODB_URI` in `.env` is correct
- Verify MongoDB is listening on port 27017

**Issue: "CORS error" when submitting form**
- CORS is already enabled in the server
- Make sure the API endpoint URL is correct

**Issue: Form not submitting**
- Open browser console (F12) and check for errors
- Ensure server is running
- Check that fetch URL matches: `http://localhost:3000/api/contact`

## Production Deployment

For production, use a MongoDB service:
- **MongoDB Atlas**: https://www.mongodb.com/cloud/atlas (cloud-hosted)
- Update `MONGODB_URI` in `.env` to your production database URL

Example MongoDB Atlas URI:
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/vcard_portfolio
```

## Next Steps

1. Install dependencies: `npm install`
2. Ensure MongoDB is running
3. Start the server: `npm run dev`
4. Test the contact form in your browser
5. Verify messages are saved in MongoDB

