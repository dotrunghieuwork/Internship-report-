---
title : "Deploy Frontend to AWS"
date : 2026-07-30
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Deploy Frontend to AWS

After successfully testing the user interface on your local machine, the next step is to deploy the source code to the cloud environment so real users can access it. We will use a static hosting architecture with Amazon S3 and the Amazon CloudFront content delivery network (CDN).

---

### 1. Create an Amazon S3 Bucket (Static Storage)

Instead of renting an expensive server (EC2) just to host a web interface, we will use S3 combined with CloudFront. This architecture delivers maximum performance at almost zero cost.

**Why choose this architecture?**

| DECISION | REASON |
| :--- | :--- |
| **Amazon S3** | Extremely cost-effective storage for static files (HTML, CSS, JS) after building. |
| **Amazon CloudFront** | Global Content Delivery Network (CDN) for fast loading speeds and automatic HTTPS. |
| **Origin Access Control (OAC)** | Secures S3 by denying direct internet access; all traffic must route through CloudFront. |
| **Custom Error Pages** | Crucial configuration to fix the 404 error when users hit F5 (Refresh) on a React SPA. |

**Steps to create the Bucket:**

1. Log in to the AWS Console, search for the **S3** service, and select the `ap-southeast-2` (Sydney) Region.
2. Click **Create bucket**.
3. **Bucket name**: Enter a globally unique name (e.g., `naturera-green-banking-dev-frontendbucket-...`).
4. **Block Public Access settings for this bucket**: Ensure the *Block all public access* option is **CHECKED** (Turned ON). (We will use CloudFront OAC for access instead of making it public).
5. Scroll down to the bottom and click **Create bucket**.

> > <img src="/Internship-report-/images/5-Workshop/5.5-hosting/s3.png" width="80%" />

---

### 2. Configure Amazon CloudFront (Distribution & Optimization)

Now that we have a storage location, we need a CDN "front door" to distribute the web application globally.

**2.1. Create Distribution & Connect S3 (OAC)**
1. Navigate to the **CloudFront** service → Click **Create Distribution**.
2. **Origin domain**: Select the S3 bucket you just created in step 1.
3. **Origin access**: Select **Origin access control settings (recommended)**.
   * Click *Create control setting* and keep the default values.
4. **Viewer protocol policy**: Select **Redirect HTTP to HTTPS** to enforce a secure connection.
5. **Web Application Firewall (WAF)**: Select *Do not enable security protections* (to save costs for the Dev environment).
6. Click **Create distribution**.

> ⚠️ **IMPORTANT:** After creation, CloudFront will display a yellow warning asking you to update the S3 Bucket Policy. Click **Copy policy**, go back to your S3 Bucket → *Permissions* tab → *Bucket Policy* → Paste the JSON block there and save. If you skip this step, CloudFront will throw a 403 Access Denied error.




**2.2. Configure Custom Error Responses (Fix React SPA F5 Error)**
Since the application uses React Router, if a user navigates directly to a sub-path (e.g., `/dashboard`) or hits F5, S3 won't find the `/dashboard` directory and will return a 403/404 error.

1. In your CloudFront Distribution interface, navigate to the **Error pages** tab.
2. Click **Create custom error response**.
3. Configure it to handle 403 errors:
   * **HTTP error code**: `403: Forbidden`
   * **Customize error response**: Yes
   * **Response page path**: `/index.html`
   * **HTTP Response Code**: `200: OK`
4. Repeat the steps above to create another identical rule for **HTTP error code**: `404: Not Found`.

---

### 3. Build & Deploy the Application

Before pushing the code to S3, ensure your Frontend is properly connected to the Backend API Gateway (from the previous lab) to avoid CORS issues.

**Step 1: Check Environment Variables**
Open your frontend source code in VS Code. Check the `.env.local` file and ensure the environment variables point to the correct API Gateway URL:

```env
VITE_API_GATEWAY_URL=https://<api-id>[.execute-api.ap-southeast-2.amazonaws.com/Prod](https://.execute-api.ap-southeast-2.amazonaws.com/Prod)
VITE_COGNITO_USER_POOL_ID=ap-southeast-2_<pool-id>
```
*(Note: To successfully call APIs, ensure your Backend AWS Lambda functions return the Header: `"Access-Control-Allow-Origin": "*"`).*

**Step 2: Build the React/Vite source code**
Open the Terminal at the root of your frontend directory and run:
```bash
npm run build
```
*(This command compresses the code and generates the `dist/` folder).*

**Step 3: Deploy to S3 using AWS CLI**
Use the `s3 sync` command to automatically compare and upload new files to your Bucket:
```bash
aws s3 sync dist/ s3://<your-bucket-name> --delete
```
*(The `--delete` flag removes obsolete files on S3 that no longer exist in your local `dist` folder, keeping the bucket clean).*

🎉 **Done!** You can now copy the **Distribution domain name** (e.g., `d21mxs1a....cloudfront.net`) from the CloudFront Console, paste it into your browser, and experience your NaturEra Green Banking app running live on AWS!