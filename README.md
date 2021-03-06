# Blog App Project

## Scenario
You have been hired to complete an API for a blog app. The previous developer hasn't shown up for work for a few days. The talk around this office is that he won the lottery but no one really knows for sure. It's kinda a mystery. Unfortunately Sherlock, that's not the puzzle you were hired to solve. Your challenge is to complete the blog app in time for your manager's demo to the CEO next week.

### Here's what you know:
- The previous developer created a front-end client using jQuery and Fetch. And started a API using Node and Express.
- The API currently uses dummy data which is just an array of objects in Javascript. It is not wired up to a database yet.
- The company uses PostgreSQL as their database. And hosts their applications on Heroku.
- Your manager says the specs for the API were documented using Postman's documenter and can be found here: [Blog App API](https://documenter.getpostman.com/view/1161985/blog-app/7EBeDoD).
- And you found the previous developer's todo list which list the tasks and notes that need to be completed.

### Tasks: 
- Create Skeleton endpoints using dummy data
  - [x] GET list all stories - should return status 200 and an array of objects
  - [x] GET get a story by id - should return status 200 and an object
  - [x] POST (create) a story - should return status 201 with a location header and the new object
  - [x] PUT (update) a story - should return status 200 and the updated object
  - [x] DELETE a story - should return status 204 with no content

- Create database
  - [x] Create local Postgres database named `blog-app`
  - [x] Create a `stories` table with the following 3 columns:
    - `id`: an auto-incrementing integer
    - `title`: regular text. Required.
    - `content`: regular text. Can be blank.

  > Note: save the CREATE TABLE and INSERT INTO queries in a file so they can be easily run again later. Examples:
    - Local DB: `psql -f ./create-stories.sql -U <username> -d blog-app`
    - ElephantSQL: `psql -f ./create-stories.sql postgres://<USERNAME>:<PASSWORD>@<SERVER:PORT>/<DATABASE>`

- Wire-up database to the endpoints. IOW, replace **dummy data** with real database calls.
  - [x] Add `knex` and `pg` to the project
  - [x] Update `config.js` with DB connection info
  - [x] Import `knex` and database config into the router file
  - [x] Update GET `/api/v1/stories` endpoint to use `knex.select()...`
  - [x] Update GET `/api/v1/stories/:id` endpoint to use `knex.select()...`
  - [x] Update POST `/api/v1/stories/` endpoint to use `knex.insert()...`
  - [x] Update PUT `/api/v1/stories/:id` endpoint to use `knex.update()...`
  - [x] Update DELETE `/api/v1/stories/:id` endpoint to use `knex.del()...`

- Deploy to Heroku (see [Deploying to Heroku](https://courses.thinkful.com/node-001v5/project/1.3.5))
  - [x] Install Heroku CLI app, if necessary
  - [x] Create app on Heroku
  - [x] Update git remote to point to Heroku
  - [x] Push app to Heroku. (Note: app won't work yet)
  - [x] Create a production database on Elephant SQL. Use `query.sql` from earlier to easily create the database
  - [x] Configure Heroku config vars to use `DATABASE_URL` and the Elephant SQL connection string  


## Add Authors
Congrats! The boss is very impressed with your work and the quick turn-around. She is so impressed in fact that she is wondering if you could add `authors` to the stories. You think about for a bit and decide it should be relatively easy to just update the api. But there is a wrinkle, that sales team is already using the first version and the changes might break their app. After pondering your options for a bit you remember you are using express router so you decide to create a **/v2** route. 

You create the following high-level tasks:

### Tasks:
- Update the Database: 
  - [ ] Create an `authors` table
    - 3 Columns
      - `id`: an autoincrementing integer
      - `username`: regular text. Required.
      - `email`: regular text. Required.
  - [ ] Add `author_id` foreign key column the stories table that references the authors table.
  > Note, when we delete a story, we **do not** want to delete the associate `author`, so choose the correct `ON DELETE` contraint. 
  - [ ] Add a dummy authors to the db and update stories to have authors.
- Create a **V2** router file
  - [ ] Create a `/router/stories-router-v2.js` router file
  - [ ] Require the router file in `server.js` and "mount" using `app.use()`
- Update the queries in the V2 endpoints to use `author` info.
