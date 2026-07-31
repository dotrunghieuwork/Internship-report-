---
title : "Frontend Setup"
date : 2026-07-30
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Frontend Setup (React & Vite)

To make it convenient for the workshop practice, the frontend user interface (Customer Dashboard) and mock interface (Mock POS Terminal) have been prepared as a skeleton code. You will proceed to download the source code, configure the environment, and run the application locally.

---

### 1. Directory Structure

The project uses a Monorepo architecture with **React combined with Vite** to optimize build speed. Below is the structure of the important directories you need to know:

```text
naturEra-green-banking-web/
  ├── apps/
  │   └── web/                # Main directory containing the Frontend part
  │       ├── public/         # General static files
  │       ├── src/            # Directory containing all React source code
  │       │   ├── assets/     # Static images (hero.png, react.svg, vite.svg)
  │       │   ├── apiService.js # Handles API calls (fetch/axios) to Backend
  │       │   ├── App.jsx     # Root component containing the main layout
  │       │   ├── config.js   # Project configuration parameters
  │       │   ├── index.css   # Global CSS formatting file
  │       │   └── main.jsx    # Entry point to launch the React application
  │       ├── .env.local      # Local environment variable configuration file
  │       ├── index.html      # Root HTML file of the Vite application
  │       ├── package.json    # List of dependencies for the application
  │       └── vite.config.js  # Vite bundling configuration
  └── package.json            # General dependencies configuration for the whole project
```

---

### 2. Source Code Download and Library Installation

Open your terminal at your working directory and run the following commands to download the source code and install the necessary dependencies for React:

#### Step 1: Clone the project repository
```bash
git clone [https://github.com/Kenjtermine/naturEra-green-banking-web.git](https://github.com/Kenjtermine/naturEra-green-banking-web.git)
cd naturEra-green-banking-web
cd apps/web
```

#### Step 2: Install dependencies
This process takes about 1-2 minutes:
```bash
npm install
```

<img src="/Internship-report-/images/5-Workshop/5.4-FrontEnd/2-npm.png" width="80%" />

---

### 3. Environment Variables Configuration

This is a critical step. The frontend needs to know the API Gateway address and Amazon Cognito information (generated from the Backend deployment part using AWS SAM) to operate.

In the `apps/web/` directory, create a new file named `.env.local` (or copy from a sample file if available).

Open the `.env.local` file and fill in the Outputs values obtained after running the `sam deploy` command in the previous step:

```env
# API Gateway Address (Retrieved from SAM Outputs)
VITE_API_GATEWAY_URL=https://<your-api-id>[.execute-api.ap-southeast-1.amazonaws.com/Stage](https://.execute-api.ap-southeast-1.amazonaws.com/Stage)

# AWS Cognito Configuration for Login (Retrieved from SAM Outputs)
VITE_COGNITO_USER_POOL_ID=ap-southeast-1_<your-pool-id>
VITE_COGNITO_CLIENT_ID=<your-app-client-id>

# API Key used to call the POS card swiping endpoint
VITE_POS_API_KEY=<your-api-key>
```

> ⚠️ **Note:** Do not leave these fields blank, otherwise the interface will return a 404 error or fail to log in.

> <img src="/Internship-report-/images/5-Workshop/5.4-FrontEnd/3-env.png" width="80%" />

---

### 4. Running the Application Locally

Once the environment variables are configured, start the development server:

```bash
npm run dev
```

The terminal will display a local link (usually `http://localhost:5173`). Press `Ctrl + Click` (or `Cmd + Click` on Mac) on that link to open the NaturEra Green Banking interface in your browser and start exploring!

<img src="/Internship-report-/images/5-Workshop/5.4-FrontEnd/4-login.png" width="80%" />
<img src="/Internship-report-/images/5-Workshop/5.4-FrontEnd/5-web.png" width="80%" />