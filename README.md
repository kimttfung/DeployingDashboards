# Deploying a Dashboards.jl project on Heroku

Before we get started, you will need the following: your Dashboard files, a Heroku account, an installation of Julia, as well as the [Heroku Command Line Interface](https://devcenter.heroku.com/articles/heroku-cli#download-and-install) (CLI) installed. Click on the link for more instructions.

Now, you can create a new folder to store all of the files required to deploy your application. Here, I will be using the folder `juliadash` as an example directory. After that, type `julia` to enter Julia.

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
Once you are done, you may close your cmd/terminal window.

Next, we will be creating a `Procfile`, which is a blank file that Heroku uses to instruct the deployment of your files.
You will need to create the file called Procfile and cooy and paste the following line of code into the file.
```
web: julia --project app.jl $PORT
```
You will need to replace `app.jl` with the filename of the starting file of your application.
Then, you may save the file into your directory where your app will be.

Now, your directory should have your Dashboard files, `Project.toml`, `Manifest.toml`, as well as `Procfile`.

As you normally host your Dashboards app on a port on localhost, you will need to replace your host method and number because Heroku deploys the application on a random port. If you are using HTTP.jl, you will need to replace your port with the following:

Host Method: Replace `HTTP.Sockets.localhost` with `"0.0.0.0"`

Host Port: Replace `8080` with `parse(Int,ARGS[1])`

(If you are wondering, the `parse(Int,ARGS[1])` corresponds to the `$PORT` in the `Procfile`.)

This is what my HTTP serve function looks like: (For more details, look at my code in this repository.)
```
HTTP.serve(handler, "0.0.0.0", parse(Int,ARGS[1]))
```

After that is done, you can open up a new window on your cmd or Terminal and log into your Heroku CLI account by typing:
```
heroku login
```
It should open up a browser window for you to enter your credentials. You will find yourself logged in after you are done logging in and closing the browser window. Now, you can enter your directory once again and deploy your app.

Please replace `my-app-name` with the name you would like to call your app in the following code!

```
cd juliadash
git init
HEROKU_APP_NAME=my-app-name
heroku create $HEROKU_APP_NAME --buildpack https://github.com/Optomatica/heroku-buildpack-julia.git
git heroku git:remote -a $HEROKU_APP_NAME
git add .
git commit -am "make it better"
git push heroku master
```
Once the process is completed, the application will be deployed and live!

It should take a while, but once you are finished, you can run the following to open your deployed app on a browser!

```
heroku open -a $HEROKU_APP_NAME
```
Hope this helped you in learning more about using Heroku to deploy apps. This method isn't just limited to Dashboard apps.

If you would like to have a look at the final product of what I did, click on [https://juliadash.herokuapp.com/](https://juliadash.herokuapp.com/) to find out!

**Reference**: the `dashex.jl` file in this repository comes from [here](https://github.com/waralex/DashboardsExamples/blob/master/dash_tutorial/5_interactive_graphing_2.jl)!
