# se-02-team-32

SE Sprint 03, Team 32, Date: 13.04.2021

# Table of Contents
- [Overview of Changes From Last Sprint](#overview-of-changes-from-last-sprint)
- [Project Overview](#project-overview)
  * [Backend](#backend)
  * [Frontend](#frontend)
    + [Setup](#setup)
    + [Dependencies](#dependencies)
    + [Implementation](#implementation)
    + [File Structure](#file-structure)
    + [Documentation](#documentation)
    + [Tests](#tests)
    + [Future Implementaion](#future-implementaion)
- [Bonus](#bonus)

# Overview of Changes From Last Sprint
* Complete change of backend framework - from Node.js to Django
* Implementation of Django REST framework
* Significant changes in frontend design and structure (mainly using react-bootstrap components)
* Created backend Django API
    - ...
* Connecting frontend and backend using `axios`
    - User login and registration using axios and JWT token authentication
    - Game instances creation

# Project Overview
* **Backend**: Django
* **Frontend**: React

This project is divided into two main apps: [backend](backend) and [frontend](frontend). They must be run separately at the same time. But first clone the repository using:
```
git clone https://github.com/lorenzorota/se-03-team-32.git
```
## Backend

## Frontend
### Setup
To run the frontend, follow these steps:
1. Change to the frontend directory
```
cd frontend
```
2. Install all dependencies (check [`package.json`](frontend/package.json) for more details)
```
npm install
```
3. Run the app in development mode
```
npm start
```
4. Navigate to [http://localhost:3000](http://localhost:3000). The page will reload automatically if you make any changes.

### Dependencies
Some main packages and libraries used in this project:
* [Material UI](https://material-ui.com) (`@material-ui`) - this is a very useful library for using icons and frontend reusable components. Go to the Components sections to find the full documentation on how to implement them. In this project, this is mostly used for icons.
* [React Bootstrap]() (`react-bootstrap`) - rebuilt Bootstrap library specifically for React without needing to implement jQuery. Go to the Components sections to find the full documentation on how to implement them. In this project, some components used from this library are Button, Form, Table, Modal etc.
* [Axios](https://github.com/axios/axios) (`axios`) - library to make it easier to send asynchronous HTTP requests to REST endpoints and perform CRUD operations. We have used `axios` to connect our React app to the Django backend server and handle API requests. The [`axios.js`](frontend/src/App.js) file sets up the axios connection and the token handling.
* [React Router](https://reactrouter.com/web/guides/quick-start) (`react-router-dom`) - DOM bindings for React Router (`react-router`). Useful for using Link components and setting up Routes in the [`App.js`](frontend/src/App.js) file.
* [CanvasJS](https://canvasjs.com/react-charts/) - We used this library to create the plots inside the game view. It has a very easy and handy way of passing data to it to display a graph.

### Implementation
* We made significant changes in the frontend design and structure (mainly using react-bootstrap components) compared to the last sprint
* Functionalities implemented:
    + User Login, Register, Logout, Change Password
    + Game Create, Update, Delete, Monitor, Activate/Deactivate
    + Game / Role Register
    + Game View - Order Beer and display supply chain data for each player
    + Plots inside the game view 
    + Page permissions:
      - Logged in users can't access the Login or Register page - they get redirected to the Monitor Page
      - If not logged in, users can't access other pages - they get redirected to the Login page
      - Instructors can't access the 'Join Games' tab (they can't register or play in games)
      - Students can't access the 'Setup Games' tab (they can't create games)
      - Students can't access games they haven't registered for
      - Students can't access a game until it is activated by the instructor

### File Structure
```
frontend 
├── public                                   
│   ├── index.html                          # every component of the app is loaded into <div id="root"></div>
│   └── ...
├── docs                               
│   ├── index.html                          # main directory for JSDoc documentation
│   └── ...
├── src
│   ├── __tests__                           # tests directory
|   |   ├── __snapshots__                   # snapshots created by tests are saved here
|   |   |   └── ...                      
|   |   ├── App.test.js                
|   |   ├── Components.test.js                    
|   |   ├── setupTests.js                    
|   |   └── Tests.test.js                
│   ├── css
|   |   ├── App.css                         # css file corresponding to App.js (no need to change)
|   |   ├── index.css                       # css file corresponding to index.js (no need to change)
|   |   └── Main.css                        # css file corresponding to the rest of the project
│   ├── pages
|   |   ├── auth                            # pages handling user data
|   |   |   ├── AccountSettings.js          # designated page to change password or delete account 
|   |   |   ├── LogIn.js                    # user log in page
|   |   |   └── Register.js                 # user registration page
│   |   ├── components                      # reusable components
|   |   |   ├── plots                        
|   |   |   |   ├── canvas.min.js           # CanvasJS library import
|   |   |   |   ├── canvas.react.js         # CanvasJS for React utility
|   |   |   |   └── ...                     # all plots are divided in 'game' and 'insights' plots
|   |   |   ├── forms
|   |   |   |   ├── GameCreationForm.js     # game creation form component (button and modal)
|   |   |   |   ├── GameRegisterForm.js     # game registration form copmonent
|   |   |   |   └── GameUpdateForm.js       # game update form copmonent (icon and modal)
|   |   |   ├── lists
|   |   |   |   ├── GamesList.js            # component that maps games in table
|   |   |   |   ├── MonitorGamesList.js     # container of games to monitor
|   |   |   |   ├── RegisteredGamesList.js  # list of games user is registered for
|   |   |   |   ├── SharedInfo.js           # order status info for each role
|   |   |   |   └── WeeksInfo.js            # week info table
|   |   |   ├── Navbar.js                   # navbar component
|   |   |   └── Option.js                   # component for using icons and tooltips
|   |   └── main                             
|   |       ├── Dashboard.js                # displays all created games by the user
|   |       ├── GameInsights.js             # displays game insights and plots after a game is finished
|   |       ├── GameView.js                 # main game view where the user can submit the order
|   |       ├── JoinGame.js                 # displays registered games
|   |       └── MonitorGame.js              # displays list of games with current cost settings
│   ├── tests
|   |   ├── App.test.js
|   |   └── setupTests.js
│   ├── App.js                              # main app - contains routes to all pages
│   ├── axios.js                            # handles api requests (using axios)
|   ├── index.js                            # renders the app into index.html "root"
│   └── reportWebVitals.js                  # captures useful metrics to improve the user experience
├── jsdoc.json 
├── package-lock.json 
└── package.json                            # list of node dependencies
```

### Documentation
For the documentation of the frontend we have used JSDoc. The configuration file is [`jsdoc.json`](frontend/jsdoc.json) and the output directory is the [`docs`](frontend/docs) folder.
1. Intsall JSDoc (globally) using:
```
npm install -g jsdoc
```
2. To compile all the changes made in the documentation run (inside frontend directory):
```
npm run doc
```
3. Open the [`index.html`](frontend/docs/index.html) file (locally is fine), found in the [`docs`](frontend/docs) directory, to see the generated documentation

For more information check out the [JSDoc repository](https://github.com/jsdoc/jsdoc) or this [Style Guide](https://github.com/shri/JSDoc-Style-Guide#links).

### Tests
Tests are set up using `@testing-library/jest-dom` and `@testing-library/react`. All tests are written in the [`__tests__`](frontend/src/__tests__) directory. All test files contain the `.test.js` extension. To run the tests, run the command 
```
npm test
```
After updating or changing any file press `u` inside the testing environment so the snapshots are updated and won't cause errors.
All the tests that are setup are to make sure that the components render correctly.

# Bonus
