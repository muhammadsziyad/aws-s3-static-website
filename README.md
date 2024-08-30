# AWS S3 Storage for static website

You can use Amazon S3 to host a static website. On a static website, individual webpages include static content. They might also contain client-side scripts.
By contrast, a dynamic website relies on server-side processing, including server-side scripts, such as PHP, JSP, or ASP.NET. Amazon S3 does not support server-side scripting, but AWS has other resources for hosting dynamic websites.

#### 1. Create an S3 Bucket
1. **Sign in to AWS Management Console**:
    
    - Go to the AWS Management Console and log in with your AWS credentials.
2. **Navigate to S3**:
    
    - In the services menu, select "S3" to open the S3 Management Console.
3. **Create a New Bucket**:
    
    - Click on the "Create bucket" button.
    - Enter a unique bucket name (e.g., `my-static-website-bucket`). The bucket name must be globally unique.
    - Choose the AWS Region where you want to create the bucket.
    - Uncheck "Block all public access" since a public website requires public access to the bucket.
    - Acknowledge that you want to grant public access and click "Create bucket".

#### 2. Upload Website Files to the S3 Bucket

1. **Upload Files**:
    - Click on the bucket name you just created to open it.
    - Click the "Upload" button.
    - Drag and drop your website files (e.g., `index.html`, `styles.css`, `script.js`) or click "Add files" to upload the files from your computer.
    - Click "Upload" to add the files to your S3 bucket.

#### 3. Configure the S3 Bucket for Static Website Hosting

1. **Enable Static Website Hosting**:
    - Go to the "Properties" tab of the bucket.
    - Scroll down to the "Static website hosting" section.
    - Click on "Edit" and select "Enable".
    - Choose "Host a static website".
    - Enter the names of your index and error documents (e.g., `index.html` for the index document and `error.html` for the error document).
    - Click "Save changes".

#### 4. Make the Website Files Public

1. **Set Permissions**:
    - Go to the "Permissions" tab of your bucket.
    - Scroll to "Bucket policy" and click "Edit".
    - Add the following bucket policy to make the files publicly accessible:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-static-website-bucket/*"
    }
  ]
}

```

- Make sure to replace `my-static-website-bucket` with your actual bucket name.
- Click "Save changes".

#### 5. Test Your Static Website

1. **Get the Endpoint URL**:
    
    - Go back to the "Properties" tab and look under "Static website hosting" to find the "Endpoint" URL. This is the URL where your website is hosted.
2. **Access the Website**:
    
    - Open a new browser tab and enter the endpoint URL. You should see your static website live!

### Source Code Example

For this example, let's assume you have a simple HTML page with a CSS file:

- **`index.html`**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>My Static Website</title>
</head>
<body>
    <h1>Welcome to My Static Website!</h1>
    <p>This is a static website hosted on AWS S3.</p>
</body>
</html>

```

- **`styles.css`**:

```css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    text-align: center;
    padding: 50px;
}

h1 {
    color: #333;
}

```

### Additional Configuration and Tips

- **Custom Domain**:
    
    - If you want to use your own domain instead of the default S3 endpoint, you can set up an alias using Route 53 or another DNS provider to point your domain to your S3 bucket. Ensure your bucket name matches your domain name (e.g., `example.com` for `example.com`).
- **HTTPS with CloudFront**:
    
    - To enable HTTPS, you can use Amazon CloudFront (AWS's CDN service) to serve your S3 content over HTTPS. Configure CloudFront to point to your S3 bucket as an origin and set up an SSL certificate using AWS Certificate Manager (ACM).
- **Access Logs**:
    
    - You can enable server access logging for your bucket to monitor requests to your S3 bucket. This can be helpful for tracking and analyzing traffic.

By following these steps, you should have your static website hosted on AWS S3 up and running. If you need further assistance or more advanced configurations, feel free to ask!
