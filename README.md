# Project Title: Workshop2

## Project Description: a practice on how to use git

## Installation Instructions

1. Create a new repository, and name it “myFirstGit”

2. Clone the new repository on to your local machine

## Run instructions

1. Make your myFirstGit as a node project (in directory myFirstGit: npm init)

2. Create a new file index.js that prints out "hello world" using the console.log() function.

3. Add a README.md file (it can be empty for now)

4. Check your node project into repository myFirstGit (git add and git commit)

5. Update your git repository at github with your local myFirstGit (git push origin master)

## Weeks and course content

Week | Content
--------------- | --------------- 
Week1 | Introduction to JavaScript and Nodejs
Week2 | Code Version Control with Git and GitHub
Week3| NodeJS as a Server

## Data Structure

### Server Side:

#### 1. Users (`user.json`)

- **id**: User ID
- **username**
- **password**
- **email**
- **roles**: Roles the user has (super admin, group admin, chat user)

#### 2. Group (`group.json`)

- **id**: Group ID
- **name**: Group name
- **admins**: Group admins
- **users**: Group chat users
- **createUser**: The user who created the group

#### 3. Channels (`channel.json`)

- **id**: Channel ID
- **name**: Channel name
- **groupId**: Corresponding group ID
- **banUsers**: List of users banned from the channel

#### 4. Ban User Logs (`log.json`)

- **id**: Log ID
- **content**: Description of which user has been banned for which channel

### Client Side:

#### 1. Group Component:

- **userInfo**: User roles
- **groupId**: Currently displayed group id
- **groupData**: Information about the currently displayed group
- **joinedList**: List of people in the group
- **waitList**: List of applicants waiting for approval
- **channelList**: List of channels
- **newChannelRowVisible**: Boolean indicating whether to display new channels
- **newChannelName**: Name of the new channel
- **currentBanUserChannelId**: ID of the channel where the user is currently banned
- **banUsername**: Username to be banned
- **currentSelectChannel**: Information about the currently selected channel

#### 2. Home Component:

- **userInfo**: User roles
- **groupList**: List of group names

#### 3. Login Component:

- **username**
- **password**
- **email**
- **isReg**: Boolean check for registration status

#### 4. Manage User Component:

- **userList**: List of users containing [id, username, email, role]
- **logList**: List of logs containing [id, content]

#### 5. Profile Component:

- **userInfo**: User details [id, username, password, email, roles]

<br>

## Angular Architecture

### 1. Components

- **Group Component**: `group component`
- **Home Component**: `home component`
- **Login Component**: `login component`
- **Manage-User Component**: `manage-user component`
- **Profile Component**: `profile component`

### 2. Routes

- **Root Path**: Empty path that redirects to the `/home` route.
- **Home Route**: 
  - Path: `home`
  - Module: `HomeModule`
- **Login Route**: 
  - Path: `login`
  - Module: `LoginModule`
- **Manage User Route**: 
  - Path: `manage-user`
  - Module: `ManageUserModule`
- **Profile Route**: 
  - Path: `profile`
  - Module: `ProfileModule`
- **Group Route**: 
  - Path: `group`
  - Module: `GroupModule`

### 3. Services

Services have not been utilized in this project. Instead, Angular components directly employ the `HttpClient` from `@angular/common/http` to execute HTTP requests. This choice is due to the logic being uncomplicated and the project having a relatively small scope.

### 4. Models

Models have not been incorporated in this project. Given the limited data structure, the components in the application directly process the data as retrieved from the API. This approach was taken to expedite the delivery of functional features.

<br>

## REST API Documentation

### 1. Node server architecture

#### Modules
- **fs**: Handle the file system.
- **path**: Manage file paths.
- **express**: Web application framework.
- **createError**: Simplifies the creation of HTTP errors for Express applications.
- **cookieParser**: Parses Cookie header and populates `req.cookies`.
- **logger (morgan)**: Log HTTP requests to the console.
- **cors**: Enable CORS in Express applications.

#### Functions and files

##### `query` folder
- **query/index.js**: Manage local storage for JSON data.
  - Functions: `select`, `insert`, `update`, `del`

##### `routes` folder
- **routes/channel.js**: Channel related routes.
  - Functions: Post methods for `/add`, `/list`, `/delete`, `/ban-user`
- **routes/group.js**: Group related routes.
  - Functions: Post and Get methods for `/add`, `/list`, `/join`, `/info`, `/approve`, `/remove-user`, `/delete`
- **routes/log.js**: Log related routes.
  - Functions: Get method for `/list`
- **routes/user.js**: User related routes.
  - Functions: Get method for `/`, Post methods for `/login`, `/register`, `/delete/account`, `/add-role`

##### `service` folder
- **service/channel.js**: Business logic for channels.
  - Functions: `insert`, `selectByGroupId`, `deleteById`, `banUser`
- **service/group.js**: Business logic for groups.
  - Functions: `selectAll`, `insert`, `selectOneByName`, `joinGroup`, `selectOneById`, `update`, `deleteById`
- **service/log.js**: Business logic for logs.
  - Functions: `insert`, `selectAll`
- **service/user.js**: Business logic for users.
  - Functions: `selectAll`, `selectOneByName`, `selectOneById`, `insert`, `deleteByid`, `changeRole`

##### `utils` folder
- **utils/index.js**: Utility function to generate random strings.
  - Functions: `randomStrWithLength`
- **utlis/response.js**: Response utilities.
  - Functions: `success`, `error`, `auth`

##### `data` folder
- **data/channel.json**: Store channel information.
- **data/group.json**: Contains group details.
- **data/log.json**: Maintains logs.
- **data/user.json**: Stores user information.

##### `app.js` file
- Express application main entry point.
  - Functions: `select`, `insert`, `update`, `del`


###	2. A list of server side routes, parameters, return values, and there purpose

#### 1. Channel Routes

- **Add Channel**  
  - **Route:** `/add`
  - **Method:** POST
  - **Parameters:** `channelName`, `groupId`
  - **Return Value:** Success with the created channel
  - **Purpose:** To add a new channel.

- **List Channels**  
  - **Route:** `/list`
  - **Method:** POST
  - **Parameters:** `userId`, `groupId`
  - **Return Value:** Success with a list of channels.
  - **Purpose:** List channels based on the user and group id.

- **Delete Channel**  
  - **Route:** `/delete`
  - **Method:** POST
  - **Parameters:** `channelId`
  - **Return Value:** Success message.
  - **Purpose:** To delete a channel.

- **Ban User**  
  - **Route:** `/ban-user`
  - **Method:** POST
  - **Parameters:** `username`, `channelId`
  - **Return Value:** Success message or error.
  - **Purpose:** To ban a user from a channel and log the action.

#### 2. Group Routes

- **Add Group**  
  - **Route:** `/add`
  - **Method:** POST
  - **Parameters:** `groupName`, `userId`
  - **Return Value:** Success with the created group.
  - **Purpose:** To add a new group.

- **List Groups**  
  - **Route:** `/list`
  - **Method:** GET
  - **Parameters:** `userId`
  - **Return Value:** Success with a list of groups.
  - **Purpose:** List groups based on the user id.

- **Join Group**  
  - **Route:** `/join`
  - **Method:** POST
  - **Parameters:** `groupName`, `userId`
  - **Return Value:** Success message.
  - **Purpose:** Join a user to a group.

- **Group Info**  
  - **Route:** `/info`
  - **Method:** GET
  - **Parameters:** `id` (group id)
  - **Return Value:** Success with group details.
  - **Purpose:** Get details about a specific group.

- **Approve User**  
  - **Route:** `/approve`
  - **Method:** POST
  - **Parameters:** `groupId`, `userId`
  - **Return Value:** Success message or error.
  - **Purpose:** Approve a user in a group.

- **Remove User**  
  - **Route:** `/remove-user`
  - **Method:** POST
  - **Parameters:** `groupId`, `userId`
  - **Return Value:** Success message or error.
  - **Purpose:** Remove a user from a group.

- **Delete Group**  
  - **Route:** `/delete`
  - **Method:** POST
  - **Parameters:** `groupId`
  - **Return Value:** Success message.
  - **Purpose:** Delete a group and its associated channels.

#### 3. Log Routes

- **List Logs**  
  - **Route:** `/list`
  - **Method:** GET
  - **Return Value:** Success with a list of logs.
  - **Purpose:** List all logs.

#### 4. User Routes

- **List All Users**  
  - **Route:** `/`
  - **Method:** GET
  - **Return Value:** Success with a list of users.
  - **Purpose:** List all users.

- **User Login**  
  - **Route:** `/login`
  - **Method:** POST
  - **Parameters:** `username`, `password`
  - **Return Value:** Success with user details or error message.
  - **Purpose:** User login.

- **User Registration**  
  - **Route:** `/register`
  - **Method:** POST
  - **Parameters:** `username`, `password`, `email`
  - **Return Value:** Success with user details or error message.
  - **Purpose:** User registration.

- **Delete Account**  
  - **Route:** `/delete/account`
  - **Method:** POST
  - **Parameters:** `userId`
  - **Return Value:** Success message.
  - **Purpose:** Delete a user account.

- **Add Role**  
  - **Route:** `/add-role`
  - **Method:** POST
  - **Parameters:** `userId`, `roleName`
  - **Return Value:** Success message or error.
  - **Purpose:** Add a role to a user.

### Interaction between client and server

#### 1. Channel Routes:

##### a. Add Channel:

- **Client**: 
    - The Angular component might have a form where users input the channelName and select the associated groupId.
- **Server**: 
    - Upon POSTing the form data to /add, the server creates a new channel associated with the given group.
- **Update**: 
    - After a successful channel creation, the component might display a success message and perhaps update a displayed list of channels.

##### b. List Channels:

- **Client**: 
    - On loading the component page, it might send a POST request with the user's ID and group ID to retrieve channels.
- **Server**: 
    - The server checks the user's roles and responds with a list of channels.
- **Update**: 
    - The Angular component displays the list of channels based on the server's response.

##### c. Delete Channel:

- **Client**: 
    - Users might select a channel and click on a delete option.
- **Server**: 
    - Upon receiving the POST request with channelId, the server deletes the channel.
- **Update**: 
    - The component can immediately remove the channel from the displayed list and show a success message.

##### d. Ban User:

- **Client**: 
    - Admins or moderators can select a user within a channel and choose the ban option.
- **Server**: 
    - After receiving the POST request, it bans the user and logs the action.
- **Update**: 
    - The user might be removed from the list of active users in the channel, and a ban notification could be displayed.

#### 2. Group Routes:

##### a. Add Group:

- **Client**: 
    - Users fill out a form with the groupName.
- **Server**: 
    - On POSTing to /add, it creates a new group and associates it with the user.
- **Update**: 
    - Refresh the list of groups or navigate the user to the newly created group page.

#####  b. List Groups:

- **Client**: 
    - On accessing a dashboard or groups page, it sends a GET request with the user's ID.
- **Server**: 
    - Responds with a list of groups based on the user's roles.
- **Update**: 
    - The component displays the groups.

#####  c. Join Group:

- **Client**: 
    - Users can select a group and choose to join.
- **Server**: 
    - Adds the user to the group's waiting list until approved.
- **Update**: 
    - Display a message that the user's join request is pending approval.

#####  d. Group Info:

- **Client**: 
    - On selecting a specific group, the client sends a GET request with the group's ID.
- **Server**: 
    - Returns group details, including users.
- **Update**: 
    - The component displays group information.

####  3. Log Routes:

#####  a. List Logs:

- **Client**: 
    - Admin or moderator accesses the logs page.
- **Server**: 
    - Sends back a list of logs on the GET request.
- **Update**: 
    - The component displays the logs in a readable format.

####  4. User Routes:

#####  a. User Login:

- **Client**: 
    - Users enter their username and password.
- **Server**: 
    - Validates the credentials and returns user details or an error.
- **Update**: 
    - On success, navigate the user to their dashboard. On error, display an error message.

#####  b. User Registration:

- **Client**: 
    - New users fill out a registration form.
- **Server**: 
    - Creates a new user and returns user details.
- **Update**: 
    - Navigate the user to their dashboard or display any errors.

#####  c. Delete Account:

- **Client**: 
    - Users might access their profile settings and opt to delete their account.
- **Server**: 
    - Deletes the user account and all associated data.
- **Update**: 
    - Log out the user and navigate them to the homepage.

#####  d. Add Role:

- **Client**: 
    - Admins can select a user and assign roles.
- **Server**: 
    - Updates the user's roles based on the POST request.
- **Update**: 
    - Reflect the changed roles in the user's details on the admin panel.