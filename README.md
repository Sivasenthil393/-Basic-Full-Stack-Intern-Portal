# Intern Portal Dashboard

A full-stack intern portal dashboard built with **React.js** for the frontend and **Firebase Firestore** for a real-time, serverless backend. This application provides interns with a personalized dashboard displaying their name, a unique referral code, and total donations raised. It also features a dynamic leaderboard showcasing top contributors.
This project was developed as part of a full-stack assignment, demonstrating core frontend and backend integration principles.

## ✨ Features
* **Dummy Login/Signup:** A simple, non-authenticated entry point for demonstration purposes.
* **Personalized Dashboard:** Displays the intern's name, a unique dummy referral code, and their total donations raised.
* **Dynamic Donation Tracking:** Includes a button to "Simulate New Donation," which updates the donation amount in real-time in the Firebase Firestore database and reflects instantly on the dashboard.
* **Rewards/Unlockables Section:** A static display of potential achievements and rewards.
* **Leaderboard:** A dedicated page that ranks all interns by their total donations, updated in real-time as donations are simulated.
* **Full-Stack Architecture:** Leverages React for a responsive user interface and Firebase Firestore for robust, scalable data persistence and retrieval.

## 💻 Technologies Used
* **Frontend:**
    * [React.js](https://react.dev/) - A JavaScript library for building user interfaces.
    * [Tailwind CSS](https://tailwindcss.com/) - A utility-first CSS framework for rapid UI development.
* **Backend:**
    * [Firebase Firestore](https://firebase.google.com/docs/firestore) - A flexible, scalable NoSQL cloud database for mobile, web, and server development.

## 🚀 Getting Started
Follow these instructions to get a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites
* Node.js (LTS version recommended)
* npm (comes with Node.js) or Yarn

### Installation
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/intern-portal.git](https://github.com/your-username/intern-portal.git)
    cd intern-portal
    ```
    *(Replace `your-username` with your actual GitHub username and `intern-portal` with your repository name)*
2.  **Install dependencies:**
    ```bash
    npm install
    # or
    yarn install
    ```

### Firebase Project Setup
This application uses Firebase Firestore as its backend. You'll need to set up a Firebase project and configure its security rules.
1.  **Create a Firebase Project:**
    * Go to the [Firebase Console](https://console.firebase.google.com/).
    * Click "Add project" and follow the steps to create a new project.
    * **Important:** When prompted to create a Cloud Firestore database, choose **"Start in production mode"** and select a suitable geographic **location** for your database (e.g., `nam5 (us-central)`, `asia-south1 (Mumbai)`).
2.  **Add a Web App to Your Firebase Project:**
    * In your Firebase project, click the `</>` (web) icon to add a new web app.
    * Register the app (you can give it any nickname).
    * Firebase will provide you with a `firebaseConfig` object. **Copy this entire object.** You'll need it in the next step.
3.  **Configure Firestore Security Rules:**
    * In the Firebase Console, navigate to **"Firestore Database"** (under the "Build" section).
    * Go to the **"Rules"** tab.
    * **Replace the existing rules** with the following to allow authenticated users (including anonymous ones used by the app) to read and write data to the `interns` collection:
    ```firestore
    rules_version = '2';
    service cloud.firestore {
      match /databases/{database}/documents {
        // Allow authenticated users to read and write to public intern data
        match /artifacts/{appId}/public/data/{collection}/{document} {
          allow read, write: if request.auth != null;
        }

        // Deny access to all other paths by default for security
        match /{document=**} {
          allow read, write: if false;
        }
      }
    }
    ```
    * Click **"Publish"** to save the rules.

### Environment Variables (`.env`)
To keep your Firebase credentials secure and out of your public repository, we use environment variables.
1.  **Create a `.env` file:**
    In the **root directory** of your project (where `package.json` is), create a new file named `.env`.
2.  **Add your Firebase config to `.env`:**
    Paste the following content into your `.env` file, **replacing the placeholder values** with the actual `firebaseConfig` object you copied from the Firebase Console in step 2 of "Firebase Project Setup".
    ```dotenv
    # .env file
    # DO NOT COMMIT THIS FILE TO GIT! Add it to your .gitignore.

    # Your Firebase Web App Configuration
    REACT_APP_FIREBASE_CONFIG='{
      "apiKey": "YOUR_ACTUAL_API_KEY_FROM_FIREBASE_CONSOLE",
      "authDomain": "YOUR_ACTUAL_AUTH_DOMAIN_FROM_FIREBASE_CONSOLE",
      "projectId": "YOUR_ACTUAL_PROJECT_ID_FROM_FIREBASE_CONSOLE",
      "storageBucket": "YOUR_ACTUAL_STORAGE_BUCKET_FROM_FIREBASE_CONSOLE",
      "messagingSenderId": "YOUR_ACTUAL_MESSAGING_SENDER_ID_FROM_FIREBASE_CONSOLE",
      "appId": "YOUR_ACTUAL_WEB_APP_ID_FROM_FIREBASE_CONSOLE"
      # "measurementId": "YOUR_ACTUAL_MEASUREMENT_ID_IF_PRESENT"
    }'
    # Your Firebase Project ID (typically the same as projectId above)
    REACT_APP_FIREBASE_PROJECT_ID="YOUR_ACTUAL_PROJECT_ID_FROM_FIREBASE_CONSOLE"
    ```

3.  **Add `.env` to `.gitignore`:**
    Ensure your `.gitignore` file includes `.env` to prevent it from being committed to your Git repository:
    ```
    # .gitignore
    # ... other ignored files/folders ...

    .env
    ```
### Running the Application
1.  **Start the development server:**
    ```bash
    npm start
    # or
    yarn start
    ```
    This will open the application in your browser, usually at `http://localhost:3000/`.

## 📂 Project Structure
The project is organized into modular components for clarity and maintainability:
