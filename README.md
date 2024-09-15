# AWS-Serveless-Service

# CloudSnap Service

CloudSnap is a serverless image processing and tagging system using AWS services. It allows users to upload images, detect objects, store and manage image metadata, and perform various operations like adding/removing tags and searching for images based on tags or other images.

## Features

- User authentication (including Google login)
- Image upload and storage in S3
- Object detection using YOLO (You Only Look Once)
- Image metadata storage in DynamoDB
- Add and remove tags for images
- Search images by tags or by uploading a similar image
- Delete images and their metadata

## Architecture

The system uses the following AWS services:

- AWS Lambda for serverless computing
- Amazon S3 for image storage
- Amazon DynamoDB for metadata storage
- Amazon API Gateway for RESTful API endpoints
- AWS Amplify for hosting the frontend application
  
![image](https://github.com/user-attachments/assets/ef29d0b1-17df-4c26-9748-2dceb84c9182)


## Components

1. `object_detection`: Performs object detection on uploaded images using YOLO.
2. `image_store`: Stores image metadata (username, S3 URL, tags) in DynamoDB.
3. `image_delete`: Deletes image metadata from DynamoDB and the image from S3.
4. `image_query_by_tag`: Searches for images based on tags.
5. `image_query_by_image`: Finds similar images by first detecting objects in the uploaded image.
6. `tags_update`: Updates tags for a specific image.

## DynamoDB Schema

- Partition key: `s3_url`
- Sort key: `username`

This schema ensures that users can only access images stored under their username.

## Usage

1. **Authentication**: Users can sign in with their email and password or use Google Login. New users can create an account, which requires email verification.

2. **Upload Image**: On the home page, users can upload a single JPG or PNG image. The system will store it in S3, perform object detection, and display the S3 URL and detected tags.

3. **Search by Tags**: Navigate to Search -> By Tags. Enter tag names and counts, then click "+" to add multiple tags. Click "Search" to find matching images.

4. **Search by Image**: Go to Search -> By Image. Upload a PNG or JPG image to find relevant images.

5. **Update Tags**: In Search -> Update tags, enter the S3 URL of an image. You can then add or remove multiple tags.

6. **Delete Image**: Navigate to Image Processing -> Delete. Enter the S3 URL of the image and click the red trash bin button to delete it.

7. **Logout**: Hover over your email address in the top right corner and click the logout button.

