# UniHUB 🎓

UniHUB is a comprehensive university learning management system (LMS) designed to facilitate communication and collaboration between students and instructors. The platform provides a centralized hub for course management, materials sharing, task tracking, and academic discussions.

## 📋 Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Database Setup](#database-setup)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [Contributing](#contributing)

## ✨ Features

### For Students
- **Course Management**: Browse, search, and register for courses
- **Materials Access**: Download and view course materials (PDFs, documents, etc.)
- **Task Management**: Create, track, and complete academic tasks with deadlines
- **Discussion Forums**: Participate in course discussions with posts and comments
- **Rating System**: Rate courses and provide feedback
- **AI Chatbot**: Get assistance with academic queries using OpenAI integration
- **Question Bank**: Access and practice with course-related questions
- **User Profile**: Manage personal information and settings

### For Instructors
- **Course Creation & Management**: Create and manage multiple courses
- **Material Upload**: Share learning materials with students
- **Announcements**: Post announcements and updates for enrolled students
- **Student Analytics**: View course statistics and student engagement metrics
- **Task Assignment**: Create and manage tasks for students
- **Content Moderation**: Edit and delete posts and comments
- **Course Archiving**: Archive old or completed courses

### For Administrators
- **User Management**: View, edit, and manage all user accounts
- **Course Administration**: Create, edit, and delete courses
- **System Overview**: Monitor platform usage and statistics

### General Features
- **Authentication & Authorization**: Secure login with JWT tokens
- **Password Recovery**: Email-based OTP system for password reset
- **Voting System**: Upvote/downvote posts for content quality
- **Dark Mode Support**: Toggle between light and dark themes
- **Responsive Design**: Mobile-friendly interface using Tailwind CSS
- **File Storage**: Cloud storage using Firebase for photos and materials
- **Real-time Updates**: Dynamic content updates without page refresh

## 🛠 Technology Stack

### Frontend
- **Framework**: React 18.3.1
- **Routing**: React Router DOM v6
- **UI Components**: 
  - Tailwind CSS for styling
  - Bootstrap 5.3.3
  - Font Awesome icons
  - React Icons
- **Forms**: Formik with Yup validation
- **HTTP Client**: Axios
- **Charts**: Chart.js with react-chartjs-2
- **Chatbot**: @chatscope/chat-ui-kit-react
- **Authentication**: JWT Decode
- **Notifications**: React Toastify

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MySQL 8.x
- **Authentication**: JWT (jsonwebtoken)
- **Password Hashing**: bcryptjs
- **File Upload**: Multer
- **Email Service**: Nodemailer
- **Cloud Storage**: Firebase Admin SDK
- **AI Integration**: OpenAI API
- **Image Processing**: Sharp
- **CORS**: Enabled for cross-origin requests

### Database
- **Type**: MySQL
- **Tables**: 
  - Users, Courses, Posts, Comments
  - Materials, Tasks, Ratings
  - Registrations, Votes, Tags
  - Books, Question Banks

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js** (v14.x or higher)
- **npm** (v6.x or higher)
- **MySQL** (v8.x or higher)
- **Git**

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/7amota2001/UniHUB.git
cd UniHUB
```

### 2. Install Backend Dependencies
```bash
cd Back-end
npm install
```

### 3. Install Frontend Dependencies
```bash
cd ../Front-End
npm install
```

## ⚙️ Configuration

### Backend Configuration

1. **Database Configuration**: Edit `Back-end/database.js`
```javascript
const pool = mysql.createPool({
    host: 'localhost',
    database: 'uniHub',
    port: '3306',
    user: 'root',
    password: 'your_password',  // Add your MySQL password
    waitForConnections: true,
    connectionLimit: 10,
    queueLimit: 0
});
```
> **Security Note**: For production environments, avoid using the root user. Create a dedicated database user with appropriate permissions and use strong passwords.

2. **Environment Variables**: Edit `Back-end/environment.env`
```env
OPENAI_API_KEY=your_openai_api_key_here
```
> **Security Warning**: Never commit API keys or sensitive credentials to version control. Keep your `.env` files private and add them to `.gitignore`.

3. **Firebase Configuration**: 
   - Obtain your Firebase Admin SDK service account JSON file
   - Place it in the `Back-end` directory
   - Update the path in `Back-end/Utils/firebaseConfig.js` or `admin.js`

### Frontend Configuration

The frontend connects to the backend API. Ensure the API base URL is correctly configured in your axios instances within the React components.

## 💾 Database Setup

1. **Create the Database**:
```bash
mysql -u root -p
CREATE DATABASE uniHub;
EXIT;
```

2. **Import Database Schema**:
Navigate to the `GP-DataBase` directory and import all SQL files:
```bash
cd GP-DataBase
mysql -u root -p uniHub < unihub_user.sql
mysql -u root -p uniHub < unihub_course.sql
mysql -u root -p uniHub < unihub_posts.sql
mysql -u root -p uniHub < unihub_comment.sql
mysql -u root -p uniHub < unihub_material.sql
mysql -u root -p uniHub < unihub_tasks.sql
mysql -u root -p uniHub < unihub_registeredcourses.sql
mysql -u root -p uniHub < unihub_course_rating.sql
mysql -u root -p uniHub < unihub_vote.sql
mysql -u root -p uniHub < unihub_tag.sql
mysql -u root -p uniHub < unihub_post_tag.sql
mysql -u root -p uniHub < unihub_books.sql
mysql -u root -p uniHub < unihub_user_book.sql
mysql -u root -p uniHub < unihub_usermaterials.sql
mysql -u root -p uniHub < unihub_users.sql
mysql -u root -p uniHub < unihub_dehk.sql
```

## 🏃 Running the Application

### Start the Backend Server
```bash
cd Back-end
node app.js
```
The backend server will start on `http://localhost:4000`

### Start the Frontend Development Server
```bash
cd Front-End
npm start
```
The frontend will start on `http://localhost:3000` and automatically open in your browser.

## 📁 Project Structure

```
UniHUB/
├── Back-end/
│   ├── Controllers/           # Business logic controllers
│   │   ├── userController.js
│   │   ├── courseController.js
│   │   ├── postController.js
│   │   ├── commentController.js
│   │   ├── materialController.js
│   │   ├── taskController.js
│   │   ├── voteController.js
│   │   ├── adminController.js
│   │   └── chatGptController.js
│   ├── Services/              # Business services
│   ├── Utils/                 # Utility functions
│   │   ├── db.js             # Database connection
│   │   ├── firebaseConfig.js # Firebase setup
│   │   └── upload.js         # File upload middleware
│   ├── app.js                # Express application entry point
│   ├── routes.js             # API routes definition
│   ├── database.js           # Database configuration
│   ├── package.json          # Backend dependencies
│   └── environment.env       # Environment variables
│
├── Front-End/
│   ├── public/               # Public assets
│   ├── src/
│   │   ├── Components/       # React components
│   │   │   ├── Student/     # Student-specific components
│   │   │   ├── Instructor/  # Instructor-specific components
│   │   │   ├── Admin/       # Admin-specific components
│   │   │   ├── Login/       # Authentication components
│   │   │   ├── Register/
│   │   │   └── Layout/
│   │   ├── Contexts/        # React context providers
│   │   ├── Assets/          # Images and static files
│   │   ├── App.js           # Main application component
│   │   └── index.js         # Application entry point
│   ├── tailwind.config.js   # Tailwind CSS configuration
│   ├── package.json         # Frontend dependencies
│   └── README.md            # Create React App documentation
│
├── GP-DataBase/              # Database schema files
│   ├── unihub_user.sql
│   ├── unihub_course.sql
│   ├── unihub_posts.sql
│   └── ...
│
├── UniHub-GP.pdf             # Project documentation
└── README.md                 # This file
```

## 🔌 API Endpoints

### User Routes
- `POST /signUp` - Register a new user
- `POST /signIn` - User login
- `DELETE /deleteUser` - Delete user account
- `PUT /editUser` - Update user information
- `GET /getUserData` - Get user profile
- `POST /forgetPassword` - Request password reset
- `POST /checkOTP` - Verify OTP code
- `PUT /changePassword` - Change password
- `POST /upload-photo` - Upload profile photo
- `GET /get-photo` - Retrieve profile photo
- `GET /user/:userId` - Get user details

### Course Routes
- `GET /courses` - List all courses
- `POST /courses/register` - Register in a course
- `GET /courses/registered` - Get registered courses
- `GET /courses/search` - Search for courses
- `GET /courses/:courseID` - Get course details
- `GET /courses/:courseId/status` - Get course status
- `POST /course/:courseId/rate` - Rate a course
- `GET /course/:courseId/viewrate` - View course rating
- `PUT /courses/:courseId/archive` - Archive a course
- `POST /upload-course-photo` - Upload course photo
- `GET /course-photo/:courseId` - Get course photo

### Task Routes
- `POST /createTasks` - Create a new task
- `DELETE /deleteTasks` - Delete a task
- `GET /listTasks` - List all tasks
- `PUT /markTaskAsCompleted` - Mark task as completed

### Material Routes
- `POST /material/upload` - Upload course material
- `GET /material/course/:courseId` - Get materials for a course
- `PUT /material/edit` - Edit material
- `PUT /material/:materialId/editDescription` - Update material description
- `DELETE /material/delete/:materialId` - Delete material

### Post Routes
- `POST /post/create/:courseId` - Create a post
- `PUT /post/edit/:postId` - Edit a post
- `DELETE /post/delete/:postId` - Delete a post
- `GET /post/course/:courseId` - Get posts by course
- `GET /posts` - List all posts
- `GET /announcements/recent` - Get recent announcements
- `GET /posts/:courseId/tag/:tag` - Filter posts by tag

### Comment Routes
- `POST /post/:postId/addcomment` - Add a comment
- `PUT /comment/:commentId` - Edit a comment
- `DELETE /comment/:commentId` - Delete a comment
- `GET /post/:postId/comments` - Get comments for a post
- `POST /posts/:postId/comment` - Add AI-generated comment

### Vote Routes
- `POST /upvote/:postId` - Upvote a post
- `POST /downvote/:postId` - Downvote a post
- `GET /votes/:postId` - Get vote counts
- `DELETE /votes/remove/:postId` - Remove vote

### Admin Routes
- `POST /admin/create` - Create a course (admin)
- `DELETE /admin/delete` - Delete a course (admin)
- `PUT /admin/edit/:courseId` - Edit a course (admin)
- `GET /users` - List all users (admin)
- `DELETE /deleteUser/:userId` - Delete user (admin)

### AI Chatbot Route
- `POST /chatGpt` - Chat with OpenAI assistant

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/YourFeature`)
3. Make your changes
4. Commit your changes (`git commit -m 'Add some feature'`)
5. Push to the branch (`git push origin feature/YourFeature`)
6. Open a Pull Request

## 📝 License

This project is part of a graduation project (GP). Please refer to the `UniHub-GP.pdf` document for more information about the project scope and objectives.

## 👥 Authors

- 7amota2001 (GitHub: [@7amota2001](https://github.com/7amota2001))

## 📧 Contact

For any questions or support, please open an issue in the GitHub repository.

---

**Note**: This is an educational project developed as part of a graduation project. Make sure to properly configure all API keys and credentials before running the application in a production environment.
