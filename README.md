#SDA2037-Lama 
 #Blog App Deployment – Week 10 

 # requirements 

- Frontend: hosting S3 website 
- Backend: Node.js + Express (hosted on EC2)
- Media Uploads: AWS S3 bucket 
- Deployment Tools: PM2, AWS CLI

---

#What I Did 

# 1. S3 – Frontend Hosting
- Created bucket: `lama-blogapp-frontend`
- Enabled static website hosting
- Made it public with a bucket policy

# 2. S3 – Media Uploads
- Created bucket: `lama-blogapp-media`
- Set CORS to allow uploads
- Made it public for media access

# 3.IAM User
- Created IAM user with permissions to access media bucket
- Used its keys in backend `.env` file

#  4. EC2 Instance (Ubuntu)
- Opened required ports: 22, 80, 443, 5000
- Installed Node, PM2, AWS CLI
- Cloned the project repo (https://github.com/cw-barry/blog-app-MERN.git) 
- Created backend and frontend `.env` files
- Installed dependencies and started backend with PM2

#  5.Frontend Build & Deployment
- Built the React app using `pnpm`
- Synced the build folder to the frontend S3 bucket using AWS CLI
# Links

- GitHub Repo: https://github.com/LAMA-RASHED/blog-app-week10
- Frontend S3 Link: http://lama-blogapp-frontend.s3-website.eu-north-1.amazonaws.com
note: I couldn’t sign up in Blog App

---

# Screenshots

All screenshots are in the `screenshots/` folder:

- Website open from S3
- curl -I result with 200 OK
- Uploaded file in media bucket
- PM2 shows backend is running

---

#Result

- the Blog works 
- Media upload works 
- MongoDB saves blog data 
- All parts are connected correctly 

# Cleanup (Done)

- Stopped EC2 to save credits
- Deleted IAM credentials
- Clean and secure 


