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