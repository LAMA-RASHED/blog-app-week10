# SDA2037-Lama 

# Week 10 - Blog App Deployment

This repo is for deploying the blog app (frontend and backend) using AWS Free Tier services.  
The frontend is hosted on S3, the backend is running on EC2, and another S3 bucket is used for media.

# Requirements

- MongoDB Atlas  
- AWS S3 (2 buckets)  
- AWS EC2  
- IAM user  
- Node.js and npm  
- pnpm

## Backend tasks


# MongoDB
I used a connection string from MongoDB Atlas.

# EC2
- Opened ports: 22, 80, 443, 5000  
- Uploaded the backend files to the EC2 server  
- Installed the packages  
- Used  pm2 to keep the backend running  
- Checked the server using:
curl -I http://lama-blogapp-frontend.s3-website.eu-north-1.amazonaws.com/

# .env file for backend

cat > .env << EOF
PORT=5000
HOST=0.0.0.0
MODE=production                                                                                  
  MONGODB=    mongodb+srv://test:qazqwe123@mongodb.txkjsso.mongodb.net/blog-app
# JWT Authentication
JWT_SECRET=$(openssl rand -hex 32)
JWT_EXPIRE=30min
JWT_REFRESH=$(openssl rand -hex 32)
JWT_REFRESH_EXPIRE=3d
# AWS S3 Configuration
AWS_ACCESS_KEY_ID=xxx
AWS_SECRET_ACCESS_KEY=xx
AWS_REGION=eu-north-1
S3_BUCKET=lama-blogapp-media
MEDIA_BASE_URL=https://lama-blogapp-media.eu-north-1.amazonaws.com
# Misc
DEFAULT_PAGINATION=20
EOF

## Frontend Task

# .env for frontend
cat > .env << EOF
VITE_BASE_URL=http://13.48.204.74:5000/api
VITE_MEDIA_BASE_URL=https://lama-blogapp-media.eu-north-1.amazonaws.comEOF

# Build frontend
pnpm install
pnpm run build


# Upload to S3

aws s3 sync dist/ s3:// lama-blogapp-frontend


# S3 Setup

-  Bucket for frontend: 
- Enabled static website hosting  
- Made it public using a bucket policy

# Bucket for media
- Allowed PUT,  GET, and  DELETE using an IAM user  
- Set CORS so the frontend can upload images directly

# IAM

- Created an IAM user called mern-blog-user
- Gave access only to the media bucket  
- Used the access key and secret in the backend

## Screenshots

- Found in the `screenshots/` folder:
- pm2 running the backend on EC2  
- Blog page from S3  
- curl  -I result showing 200 OK  
- Uploaded image inside the S3 bucket

#Notes
- No secrets or credentials are pushed to GitHub

# Result

- the Blog works 
- Media upload works 
- MongoDB saves blog data 
- All parts are connected correctly 

# Cleanup (Done)

- Stopped EC2 to save credits
- Deleted IAM credentials
- Clean and secure 


