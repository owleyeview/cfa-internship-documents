# WECO app architecture
This document is intended to orient developers to the WECO code base.

### App Architecture Overview
#### Frontend 
A single page application using :
- [React](https://react.dev/)
- [Typescript](https://www.typescriptlang.org/docs/)
- [SCSS](https://sass-lang.com/documentation/)
Code held in the `web-app` repo
port 3000 when run locally
#### Backend
API server using:
- [Node](https://nodejs.org/en/docs)
- [Express](https://expressjs.com/)
- [Sequelize](https://sequelize.org/)
- [Socket.io](https://socket.io/docs/v4)
Code held in the `rest-api` repo
port 5000 for HTTP
port 5001 for sockets
#### MySQL Database
ports 3307/3306 when run locally
### Codebase Details
The client and server code is stored in two separate repos (`web-app` and `rest-api` respectively)
The three main structures of the app are Posts, Spaces(or Groups) and Users.
#### Key Directories & Files
##### rest-api
- `models/`:  Defines database columns in tables using Sequelize
- `routes/`:  These files define the REST endpoints
- `middleware/`:  Auth token checks
- `seeders/`:  Used to populate the database with sample data for dev purposes
- `Server.js`:  Sets up the Express server
- `Helpers.js`:  Helper functions used in multiple endpoints
- `package.json`:  Describes app dependencies

##### web-app
- `src/`
	- `components/`:  Reusable components are defined here
		- `cards/`:  Cards are pop-up UI components that display in front of the existing page
	- `contexts/`:  Data that defines the app context is defined here
		- `ContextProviders.tsx/`:  Holds the contexts
	- `pages/`:  Core pages defined here
	- `styles/`:  CSS styles for components and pages are defined here
	- `svgs/`:  Icons are stored here and can be imported as React components
	- `App.tsx`:  The main entry point for the React application
#### API Endpoints (from /rest-api/routes/)

|Endpoint|HTTP Method|Description|
|---|---|---|
|**Account Routes**|||
|`/account-data`|`GET`|Retrieve account details|
|`/toybar-data`|`GET`|
|`/streams`|`GET`|Retrieve active streams|
|`/stream-sources`|`GET`|Get the sources that populate a particular stream|
|`/muted-users`|`GET`|Lists users muted by the authenticated user
|`/account-notifications`|`POST`|
|`/toggle-emails-disabled`|`POST`|
|`/followed-spaces`|`POST`|List followed spaces
|`/followed-people`|`POST`|List followed people|
|`/stream-posts`|`POST`|
|`/create-stream`, `/edit-stream`, `/delete-stream`|`POST`|Manage streams
|`/liked-posts`|`POST`|
|`/update-account-name`, `/update-account-bio`, `/update-account-email`|`POST`|Updating account info|
|`/toggle-notification-seen`|`POST`|Manage notifications|
|`/save-muted-users`|`POST`|Update the muted users list|
|`/delete-account`|`POST`|Delete a users account and content|
|`/help-message`|`POST`|Sends a help message from the user|
|`/respond-to-mod-invite`|`POST`|Responds to a moderator invitation for a space|
|**Auth Routes**|||
|`/register`|`POST`|Register a new user|
|`/log-in`|`POST`|Login a user|
|`/reset-password-request`|`POST`|Request a password reset. Returns a password reset token.|
|`/reset-password`|`POST`|Reset user password. Requires a password reset token.|
|`/resend-verification-email`|`POST`|Resends a verification email.  Takes a `userID` and generates a new verification token.|
|`verify-email`|`POST`|Verifies a user's email address.  Takes an email token in the request body|
|`/claim-account`|`POST`|Claim an account with an email and password|
|**Post Routes**|||
|`/post-data`|`GET`|
|`/comment-data`|`GET`|
|`/likes`|`GET`|
|`/post-reposts`|`GET`|
|`/ratings`|`GET`|
|`/links`|`GET`|
|`/link-data`|`GET`|
|`/post-comments`|`GET`|
|`/post-indirect-spaces`|`GET`|
|`/poll-data`|`GET`|
|`/create-post`|`POST`|Takes post data and creates a post|
|`/update-post`|`POST`|Update post data|
|`/repost-post`|`POST`|Repost a post|
|`/add-like`|`POST`|Add a 'like' to a post|
|`/remove-like`|`POST`|Remove a 'like' from a post|
|`/add-link`|`POST`|Add a link to a post|
|`/delete-link`|`POST`|Delete a post link|
|`/create-comment`, `/delete-comment`, `/update-comment`|`POST`|Manage comments
|**Space Routes**|||
|`/space-data`|`GET`|Takes a space handle to fetch detailed data about a space|
|`/space-modal-data`|`GET`|Fetch less detailed space data for a modal view|
|`/find-child-spaces`|`GET`|Search for child spaces of a given space based on query parameters|
|`/top-contributors`|`GET`|List top contributors to a space|
|`/space-about`|`GET`|Provides 'about' information for a space|
|`/nav-list-spaces`|`POST`|Lists parent and child spaces for navigation purposes|
|`/space-posts`|`POST`|Fetches posts related to a space|
|`/post-map-data`|`POST`|Provides data for a map view of posts within a space|
|`/space-spaces`|`GET`|Fetch data about child spaces|
|`/space-people`|`GET`|List users associated with a given space|
|`/space-map-data`|`POST`|Generates data for a space hierarchy map|
|`/create-space`|`POST`|Handles the creation of a new space|
|`/find-spaces`|`GET`|Searches for spaces based on a query|
|`/users-with-access`|`GET`|List users who have access to a particular space|
|**Upload Routes**|||
|`/image-upload`|`POST`|Upload an image|
|`/gbg-background`|`POST`|Update a background image for a Glass Bead Game|
|`/gbg-audio-upload`|`POST`|Upload and process GBG audio|
|**User Routes**|||
|`/all-users`|`GET`|Retrieve all users. Supports various query parameters.|
|`/user-data`|`GET`|Fetch detailed user data of a filtered set or individual, depending on parameters and auth token.|
|`/user-modal-data`|`GET`|Fetch user profile data|
|`/user-posts`|`GET`|Fetch a users posts filtered by query parameters. Requires auth token|
|`/find-people`|`POST`|Find users based on a search query|
|`/toggle-follow-user`|`POST`|Follow or unfollow a user. Requires auth token.|

*This list of routes is not exhaustive*

### How to Contribute
Check out the 'Issues' tab in the WECO repositories.  See if there are any issues you'd like to contribute to resolving.  Feel free to ask for clarification by leaving a comment on the page of the issue you're curious about.

Additionally, all WECO issues can be explored in the [Main Task Board](https://github.com/orgs/wecollective/projects/1) project.

Code formatting for this project is defined in the `.prettierrc.js` and `.eslintrc.js` files in the root directories.  Before committing code, run Prettier and ESLint to check formatting.

For further questions contact [admin@weco.io](mailto:admin@weco.io)