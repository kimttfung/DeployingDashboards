# Deploying a Dashboards.jl project on Heroku

Before we get started, you will need the following: your Dashboard files, a Heroku account, an installation of Julia, as well as the [Heroku Command Line Interface](https://devcenter.heroku.com/articles/heroku-cli#download-and-install) (CLI) installed. Click on the link for more instructions.

Now, you can create a new folder to store all of the files required to deploy your application. Here, I will be using the folder "juliadash" as an example directory. After that, type `julia` to enter Julia.

```
mkdir juliadash
cd juliadash
julia
```
Once you are in Julia, you will need to create a new project with `Project.toml` and `Manifest.toml` files containing the information of the versions of packages and registries you will need to use. The following code activates your new environment with the 2 files and adds the packages you will need for your app, which then stores all the information in the 2 files.

```
using Pkg; Pkg.activate(".")
]add <replace with package name>       #Do this as many times as you need to, eg.  ]add Dashboards
```
Once you are done, you may close your cmd/terminal window and open a new one.
Now, you can open up a new window on your cmd or Terminal and log into your Heroku CLI account by typing
```
heroku login
```
It should open up a browser window for you to enter your credentials. You will find yourself logged in after you are done logging in and closing the browser window. Once again, enter your app directory, in this case

```
cd juliadash
HEROKU_APP_NAME=my-app-name
heroku create $HEROKU_APP_NAME --buildpack https://github.com/Optomatica/heroku-buildpack-julia.git
git push heroku master
heroku open -a $HEROKU_APP_NAME
```





A sample project to deploy julia on heroku using [julia-buildpack](https://github.com/Optomatica/heroku-buildpack-julia)
