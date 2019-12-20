# Deploying a Dashboards.jl project on Heroku (kfung)

Before we get started, you will need the following: your Dashboard files, a Heroku account, an installation of Julia, as well as the [Heroku Command Line Interface](https://devcenter.heroku.com/articles/heroku-cli#download-and-install) (CLI) installed. Click on the link for more instructions.

Now, you can create a new folder to store all of the files required to deploy your application. Here, I will be using the folder "juliadash" as an example directory.

```
mkdir juliadash
cd juliadash
```

Once everything is sorted, you can open up your cmd or Terminal and log into your Heroku CLI account by typing
```
heroku login
```
It should open up a browser window for you to enter your credentials. You will find yourself logged in after you are done logging in and closing the browser window.




A sample project to deploy julia on heroku using [julia-buildpack](https://github.com/Optomatica/heroku-buildpack-julia)

#### Build and Deploy steps
```
git clone https://github.com/Optomatica/heroku-julia-sample.git
cd heroku-julia-sample
HEROKU_APP_NAME=my-app-name
heroku create $HEROKU_APP_NAME --buildpack https://github.com/Optomatica/heroku-buildpack-julia.git
git push heroku master
heroku open -a $HEROKU_APP_NAME
```

#### Server launch must block

If the julia script exits, then the app will shutdown.

This app accomplishes a synchronous (blocking) call to Mux.jl's `serve` with `fetch(serve(test,parse(Int,ARGS[1])))`. This ensures `julia app.jl $port` does not quit just after starting about the web server.

If you use another web framework, make sure their `serve` call also works synchronously.
