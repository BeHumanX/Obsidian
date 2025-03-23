### What is laravel?
Laravel is a php framework. laravel used a MVC architectural pattern to break app into 3 parts: data, views, and operations.
Laravel has built-in routing,[[database]] access,validation, caching, queues and file storage

Laravel project and packed are downloaded and managed through composer. so composer is the prerequisite 
### How to install Laravel Project?
1. There's 2 way to create a new project
   - with `laravel new {your_project}`
   - or with manual composer installation `composer create-project laravel/laravel {your_project_name} {version}`
2. go inside the project directory with `cd {your_project}`
3. you can download specific package with `composer require {package}`(usually comes with **author/package** format)

#### How to upload laravel project to [[github]] remote repository?
1. Change directory to laravel project
2. `git init` to initialize a local project
3. `git add .` to add all file to stage
4. `git commit -m "message"` to commit changes
5. `git branch -M main` to add branch to the remote repositories
6. `git remote add origin {github_repo}` to add remote origin repositories
7. `git push -u origin master` to push git changes into remote repositories
8. next step are just `git add` -> `git commit` -> `git push` after doing changes 