To build and host your personal portfolio website on AWS, follow these steps:

### *1. Create the Portfolio Website*

1. *Design Your Website:*
   - Create your portfolio website using HTML, CSS, and JavaScript. You can use frameworks or libraries like Bootstrap or React for a more dynamic site.

  
### *2. Set Up AWS S3 for Hosting*

*Amazon S3* will be used to host your static website.

1. *Open S3 Console:*
   - Go to the [Amazon S3 Console](https://console.aws.amazon.com/s3/).

2. *Create a New S3 Bucket:*
   - Click "Create bucket."
   - *Bucket Name:* Enter a unique name (e.g., my-portfolio-website).
   - *Region:* Choose your preferred AWS region.
   - *Click "Create bucket":*

3. *Configure Bucket for Website Hosting:*
   - Go to the bucket you created.
   - *Click on "Properties"* and scroll to the "Static website hosting" section.
   - *Click "Edit":*
     - *Enable Static Website Hosting:* Select "Enable."
     - *Index Document:* Enter index.html.
     - *Error Document:* Enter error.html (optional).
   - *Click "Save changes":*

4. *Upload Your Website Files:*
   - Go to the "Objects" tab of your bucket.
   - *Click "Upload"* and add your index.html, styles.css, and any other assets.

5. *Set Bucket Policy for Public Access:*
   - Go to the "Permissions" tab of your bucket.
   - *Click on "Bucket Policy":*
     - Add a policy to make the content publicly readable:

       json
       {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Sid": "PublicReadGetObject",
                   "Effect": "Allow",
                   "Principal": "*",
                   "Action": "s3:GetObject",
                   "Resource": "arn:aws:s3:::my-portfolio-website/*"
               }
           ]
       }
       

   - **Replace my-portfolio-website** with your bucket name.
   - *Click "Save":*

### *3. Set Up AWS CloudFront (Optional)*

*Amazon CloudFront* can be used to distribute your content with low latency.

1. *Open CloudFront Console:*
   - Go to the [Amazon CloudFront Console](https://console.aws.amazon.com/cloudfront/).

2. *Create a New Distribution:*
   - *Click "Create Distribution":*
     - *Select "Web" for the distribution type.*
   - *Origin Settings:*
     - *Origin Domain Name:* Select your S3 bucket from the dropdown.
     - *Origin Path:* Leave empty.
   - *Default Cache Behavior Settings:*
     - *Viewer Protocol Policy:* Choose "Redirect HTTP to HTTPS" or "HTTPS Only."
   - *Distribution Settings:*
     - *Price Class:* Choose the appropriate price class based on your needs.
   - *Click "Create Distribution":*

3. *Update DNS (Optional):*
   - *If you have a custom domain:* Update your DNS settings to point to the CloudFront distribution.

### *4. Access Your Website*

- *S3 Website Endpoint:* 
  - Go to the "Properties" tab of your S3 bucket, and find the "Static website hosting" section. Use the endpoint URL provided there.
- *CloudFront Distribution Domain Name (if used):*
  - Use the domain name provided by CloudFront.

By following these steps, you will have created, deployed, and hosted your personal portfolio website on AWS using S3 and optionally CloudFront for content delivery.
