# Mongoose Schema Example

This example demonstrates how to use Mongoose to create a schema for a `User` model in a Node.js application.

## Importing Mongoose

First, you need to import Mongoose into your project:

```javascript
import mongoose from "mongoose";

const userSchema = new mongoose.Schema({
  username: {
    type: String, // The data type for this field is String.
    required: [true, 'Username is required'], // This field is mandatory. If not provided, the specified error message is displayed.
    unique: true, // Ensures that each value in this field is unique across the collection.
    lowercase: true, // Converts the value to lowercase before storing.
    minlength: [3, 'Username must be at least 3 characters long'], // The minimum length of the string.
    maxlength: [50, 'Username cannot exceed 50 characters'] // The maximum length of the string.
  },
  email: {
    type: String, // The data type for this field is String.
    required: [true, 'Email is required'], // This field is mandatory. If not provided, the specified error message is displayed.
    unique: true, // Ensures that each value in this field is unique across the collection.
    lowercase: true, // Converts the value to lowercase before storing.
    match: [/.+@.+\..+/, 'Please enter a valid email address'] // A regular expression to validate the email format.
  },
  password: {
    type: String, // The data type for this field is String.
    required: [true, 'Password is required'], // This field is mandatory. If not provided, the specified error message is displayed.
    minlength: [8, 'Password must be at least 8 characters long'] // The minimum length of the string.
  },
  age: {
    type: Number, // The data type for this field is Number.
    min: [18, 'Must be at least 18'], // The minimum value for this field.
    max: [65, 'Must be less than 66'] // The maximum value for this field.
  },
  role: {
    type: String, // The data type for this field is String.
    enum: {
      values: ['user', 'admin'], // Allowed values for this field.
      message: '{VALUE} is not supported' // Error message if the value is not in the allowed values.
    },
    default: 'user' // Default value for this field if none is provided.
  },
  createdAt: {
    type: Date, // The data type for this field is Date.
    default: Date.now // Default value is the current date and time.
  },
  todos: [{
    type: mongoose.Schema.Types.ObjectId, // The data type for each item in the array is ObjectId.
    ref: 'Todo' // References the 'Todo' model.
  }],
  profile: {
    firstName: {
      type: String, // The data type for this field is String.
      required: true // This field is mandatory.
    },
    lastName: {
      type: String, // The data type for this field is String.
      required: true // This field is mandatory.
    },
    bio: {
      type: String, // The data type for this field is String.
      default: '' // Default value is an empty string.
    }
  }
}, { timestamps: true }); // Adds `createdAt` and `updatedAt` fields to the schema automatically.

const User = mongoose.model("User", userSchema);

export default User;

```
## Explanation of Terms

type: Defines the data type for the field (e.g., String, Number, Date).
required: Makes the field mandatory. If the condition is not met, the specified error message is shown.
unique: Ensures the field's value is unique across the collection.
lowercase: Converts the string to lowercase before saving it to the database.
minlength: Sets the minimum length of the string.
maxlength: Sets the maximum length of the string.
match: Uses a regular expression to validate the field's value.
min: Sets the minimum value for a numeric field.
max: Sets the maximum value for a numeric field.
enum: Restricts the value of a string to a specified set of values.
default: Sets a default value for the field.
Date.now: A function that returns the current date and time.
mongoose.Schema.Types.ObjectId: Specifies that the field contains an ObjectId, which is typically used for referencing other documents.
ref: Specifies the model that the ObjectId refers to.
timestamps: Adds createdAt and updatedAt fields to the schema automatically.

# Node.js Backend Project Folder Structure

This guide provides an optimal folder structure for a Node.js backend project to ensure maintainability, scalability, and organization.

## Recommended Folder Structure

project-root/
│
├── src/
│ ├── config/
│ │ └── db.js
│ │ └── appConfig.js
│ │ └── ...
│ ├── controllers/
│ │ └── userController.js
│ │ └── authController.js
│ │ └── ...
│ ├── models/
│ │ └── userModel.js
│ │ └── todoModel.js
│ │ └── ...
│ ├── routes/
│ │ └── userRoutes.js
│ │ └── authRoutes.js
│ │ └── ...
│ ├── middlewares/
│ │ └── authMiddleware.js
│ │ └── errorMiddleware.js
│ │ └── ...
│ ├── utils/
│ │ └── emailUtil.js
│ │ └── hashUtil.js
│ │ └── ...
│ ├── services/
│ │ └── userService.js
│ │ └── authService.js
│ │ └── ...
│ ├── app.js
│ └── server.js
│
├── tests/
│ └── controllers/
│ └── models/
│ └── routes/
│ └── ...
│
├── node_modules/
│
├── .env
├── .gitignore
├── package.json
├── package-lock.json
└── README.md


## Explanation of Folders and Files

### src/

Contains all the source code for the application.

#### config/

- **db.js**: Database configuration and connection setup.
- **appConfig.js**: General application configuration settings.
- **...**: Other configuration files.

#### controllers/

- **userController.js**: Handles user-related requests and responses.
- **authController.js**: Manages authentication-related operations.
- **...**: Other controllers for different resources.

#### models/

- **userModel.js**: Mongoose schema and model for users.
- **todoModel.js**: Schema and model for to-dos.
- **...**: Other models representing different data entities.

#### routes/

- **userRoutes.js**: User-related routes.
- **authRoutes.js**: Authentication routes.
- **...**: Other route files for different resources.

#### middlewares/

- **authMiddleware.js**: Middleware for authentication.
- **errorMiddleware.js**: Middleware for error handling.
- **...**: Other middleware functions.

#### utils/

- **emailUtil.js**: Utility functions for sending emails.
- **hashUtil.js**: Utility functions for hashing passwords.
- **...**: Other utility functions.

#### services/

- **userService.js**: Business logic related to users.
- **authService.js**: Business logic related to authentication.
- **...**: Other service files for different business logic.

#### app.js

Sets up the Express app, middleware, and routes.

#### server.js

Starts the server and listens on a specified port.

### tests/

Contains test files for various parts of the application.

### node_modules/

Contains installed Node.js modules. Automatically generated by `npm install`.

### .env

Environment variables configuration file.

### .gitignore

Specifies files and directories to be ignored by Git.

### package.json

Lists project dependencies and scripts.

### package-lock.json

Locks the dependency versions.

### README.md

Provides an overview of the project.

## Additional Tips

- **Consistency**: Maintain consistent naming conventions.
- **Modularity**: Keep code modular to ease testing and maintenance.
- **Documentation**: Document code and folder structure for clarity.
- **Separation of Concerns**: Ensure that each module handles a specific aspect of the application.

By adhering to this structure, you can create a scalable and maintainable Node.js backend application.

# Configuring Prettier in a Node.js Project

This guide explains how to configure Prettier in your Node.js project, including creating the `.prettierrc` and `.prettierignore` files and specifying their locations.

## Step-by-Step Guide

### Step 1: Install Prettier

First, install Prettier as a development dependency:

```bash
npm install --save-dev prettier
```
In the root of your project, create .prettierrc and .prettierignore files.

in .prettierrc file add this:

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80
}
```
now search for .prettierignore on googe and copy paste

## Connect Database

Create a file named db.js inside the src/config folder. Add the following code to db.js:

```javascript
import mongoose from 'mongoose';

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGO_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
      useCreateIndex: true,
      useFindAndModify: false,
    });
    console.log('Database connected successfully');
  } catch (error) {
    console.error('Database connection failed:', error.message);
    process.exit(1); // Exit process with failure
  }
};

export default connectDB;
```
## configure dotenv

npm i dotenv
add the following code in the earliest in your project

```javascript
require('dotenv').config({path: './env'})
```