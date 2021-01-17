# Assignment 2 - Web API.

Name: Yonghui Zhang

## Features.

...... A bullet-point list of the ADDITIONAL features you have implemented in the API **THAT WERE NOT IN THE LABS** ......,
 
 + Feature 1 - add  moviesReviews 
 + Feature 2 - add popular movies 
 + Feature 3 - add search movies
 + Feature 4 - add upcoming movies

## Installation Requirements

Describe what needs to be on the machine to run the API (Node v?, NPM, MongoDB instance, any other 3rd party software not in the package.json). 
npm install 
Describe getting/installing the software, perhaps:

```bat
git clone https://github.com/YonghuiZhangWIT/movies-api-assignment2-
```

followed by installation

```bat
git install
```

## API Configuration
Describe any configuration that needs to take place before running the API. For example, creating an ``.env`` and what variables to put in it. Give an example of how this might be structured/done.
REMEMBER: DON'T PUT YOUR OWN USERNAMES/PASSWORDS/AUTH KEYS IN THE README OR ON GITHUB, just placeholders as indicated below:

NODE_ENV=production
PORT=8080
HOST=localhost
REACT_APP_TMDB_KEY=********
mongoDB=mongodb+srv://admin:************@cluster0.okmz3.mongodb.net/<dbname>?retryWrites=true&w=majority
MONGO_DB=mongodb+srv://admin:******@cluster0.okmz3.mongodb.net/test?retryWrites=true&w=majority
SEED_DB=true
SECRET=ilikecake


## API Design
Give an overview of your web API design, perhaps similar to the following: 

|  |  GET | POST | PUT | DELETE
| -- | -- | -- | -- | -- 
| /api/getmovies |Gets a list of movies |  
| /api/getmovie/{movieid} | Get a Movie | 
| /api/MovieReviews/{movieid}/reviews | Get all reviews for movie | Create a new review for Movie |  
| /api/genres| GET movie genres | 
| /api/popular|GET popular movies|
| /api/Search| GET searched movies|
| /api/upcoming|GET upcoming movies|


If you have your API design on an online platform or graphic, please link to it (e.g. [Swaggerhub](https://app.swaggerhub.com/)).


## Security and Authentication
Give details of authentication/ security implemented on the API(e.g. passport/sessions). Indicate which routes are protected.

## Integrating with React App

Describe how you integrated your React app with the API. Perhaps link to the React App repo and give an example of an API call from React App. For example: 

~~~Javascript
export const getMovies = () => {
  return fetch(
    `/api/getMovies?api_key=${process.env.REACT_APP_TMDB_KEY}&language=en-US&include_adult=false&page=1`
  )
    .then(res => res.json())
    .then(json => json);
};

export const getMovie = id => {
  return fetch(
    `/api/getMovie/movie/${id}?api_key=${process.env.REACT_APP_TMDB_KEY}`
  ).then(res => res.json());
};

export const getGenres = () => {
  return fetch(
    "/movies/api/genres?api_key=" +process.env.REACT_APP_TMDB_KEY + "&language=en-US")
    .then(res => res.json())
    .then(json => json.genres);
};
export const getMovieReviews = id => {
  return fetch(
    `/api/MovieReviews/${id}?api_key=${process.env.REACT_APP_TMDB_KEY}`
  )
    .then(res => res.json())
    .then(json => json);
  }

export const getUpcomingMovies = () => {
  return fetch(
    `/api/upcoming?api_key=${process.env.REACT_APP_TMDB_KEY}&language=en-US&page=1`
  )
    .then(res => res.json())
    .then(json => json.results);
};
export const getPopularMovies = () => {
  return fetch(
    `api/popular?api_key=${process.env.REACT_APP_TMDB_KEY}&language=en-US&page=1`
  )
    .then(res => res.json())
    .then(json => json);
};


export const newToken = () => {
  return fetch(
    `https://api.themoviedb.org/3/authentication/token/new?api_key=${process.env.REACT_APP_TMDB_KEY}`
  )
    .then(res => res.json())
    .then(json => json.request_token)
};
export const newSession = (token) => {
  return fetch(
    `https://api.themoviedb.org/3/authentication/session/new?api_key=${process.env.REACT_APP_TMDB_KEY}`
    , {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        request_token: token
      })
    })
    .then(res => res.json())
    .then(json => json.session_id)
};
export const getAccountDetails = (sessionId) => {
  return fetch(
    `https://api.themoviedb.org/3/account?api_key=${process.env.REACT_APP_TMDB_KEY}&session_id=${sessionId}`
  )
    .then(res => res.json())
};
export const login = (username, password) => {
  return newToken().then(token => {
    return fetch(
      `https://api.themoviedb.org/3/authentication/token/validate_with_login?api_key=${process.env.REACT_APP_TMDB_KEY}`,
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          username, password, request_token: token
        })
      })
  }).then(res => res.json())
};

export const searchMovies = (query) => {
  return fetch(
    `api/Search?api_key=${process.env.REACT_APP_TMDB_KEY}&query=${query}`
  )
    .then(res => res.json())
    .then(json => json || []);
}


~~~

## Extra features

. . Briefly explain any non-standard features, functional or non-functional, developed for the app.  

## Independent learning.

. . State the non-standard aspects of React/Express/Node (or other related technologies) that you researched and applied in this assignment . .  
