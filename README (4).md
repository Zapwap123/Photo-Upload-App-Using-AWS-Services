# 📸 Photo Sharing App with AWS S3, Lambda, and API Gateway

This project is a simple photo sharing web application using the following AWS services:

- **Amazon S3**: To store uploaded images and resized thumbnails.
- **AWS Lambda**: To resize images using PIL when they are uploaded.
- **Amazon API Gateway**: To expose an endpoint for listing thumbnail URLs.
- **Static HTML frontend**: To upload and display images.

---

## 🚀 Features

- Upload an image via web browser
- Automatically generates a thumbnail using a Lambda function
- Displays thumbnails in a gallery view
- API Gateway endpoint to list all thumbnails from another Lambda function
- Upload card with responsive layout
- Loading spinner for better UX

---

## 🛠️ Requirements

- AWS CLI configured
- S3 buckets (e.g., `zeth1-photo-sharing-app-bucket`, `zeth1-photo-sharing-thumbnails`)
- Lambda function with PIL for image processing
- API Gateway setup to expose `/images` GET method
- CORS enabled on S3 and API Gateway

---

## 📁 Project Structure

```
📁 photo-sharing-frontend/
├── index.html              # Frontend HTML file
├── lambda_function.py      # Lambda function for resizing images
└── README.md               # Project documentation (this file)
```

---

## 📷 Sample Frontend Usage

Upload an image and see the gallery update with thumbnails.

Frontend URL example (S3 Static Site Hosting):

```
http://zeth1-photo-sharing-app-bucket.s3-website-eu-west-1.amazonaws.com
```

API Gateway example (for fetching all thumbnails):

```
https://1954a7bbn0.execute-api.eu-west-1.amazonaws.com/prod/images
```

API Gateway example (for fetching a single thumbnail):

```
https://1954a7bbn0.execute-api.eu-west-1.amazonaws.com/prod/images/thumb-bird.jfif
```

---

## 🧠 Lambda Function Behavior

- Triggered by `ObjectCreated` event on the **main upload bucket** called `zeth1-photo-sharing-app-bucket`.
- Uses PIL to resize the image to 150x150.
- Saves the resized image as `thumb-{originalName}` in the **thumbnails bucket**.

---

## ✅ API Gateway

- REST API
- Route: `/images`
- Method: `GET`
- Integration: Lambda
- CORS: Enabled with `Access-Control-Allow-Origin: *`

---

## 📜 Example CORS Configuration for S3

```xml
<CORSConfiguration>
  <CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedHeader>*</AllowedHeader>
  </CORSRule>
</CORSConfiguration>
```

---

## 👨‍💻 Author

Seth Anmawen
