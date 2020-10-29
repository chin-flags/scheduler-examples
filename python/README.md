# Example: Hosted OAuth + Scheduling

This is an example project that implements login via [Nylas Hosted OAuth flow](https://docs.nylas.com/reference#oauth) and demonstrates both instant and smart integration types with the Nylas Scheduler.

Try it out now! Visit [http://nylas-customer-example.herokuapp.com/](http://nylas-customer-example.herokuapp.com/).

This example uses the [Flask](http://flask.pocoo.org/) web framework for Python. In order to successfully run this example and go through the Nylas OAuth flow, you need to follow the steps below.


## Get an Application Client ID & Client Secret from Nylas

To do this, login (or create) your Nylas developer account using the [Nylas Dashboard](https://dashboard.nylas.com/) account. You should see your `client_id` and `client_secret` on the dashboard.

## Update the `config.json` File

Open the `config.json` file in this directory, and replace the example `client_id` and `client_secret` with the real values that you got from the Nylas Developer dashboard. You'll also need to replace the example secret key with any random string of letters and numbers: a keyboard mash will do.

## Set Up HTTPS

The OAuth protocol requires that all communication occur via the secure HTTPS connections, rather than insecure HTTP connections. There are several ways to set up HTTPS on your computer, but perhaps the simplest is to use
[ngrok](https://ngrok.com), a tool that lets you create a secure tunnel from the ngrok website to your computer. Install it from the website, and then run the following command:

```
ngrok http 5000
```

Notice that ngrok will show you two "forwarding" URLs, which may look something like `http://ed90abe7.ngrok.io` and `https://ed90abe7.ngrok.io`. (The hash subdomain will be different for you.) You'll be using the second URL, which starts with `https`.

Alternatively, you can set the `OAUTHLIB_INSECURE_TRANSPORT` environment variable in your shell, to disable the HTTPS check. That way, you'll be able to use `localhost` to refer to your app, instead of an ngrok URL. However, be aware that you won't be able to do this when you deploy your app to production, so it's usually a better idea to set up HTTPS properly.

## Set the Nylas Callback URL

Once you have a HTTPS URL that points to your computer, you'll need to tell Nylas about it. On the [Nylas Dashboard](https://dashboard.nylas.com) click on the Application Dropdown Menu on the left, then "View all Applications". From there, select "Edit" for the app you'd like to use and select the "Application Callbacks" tab. Paste your HTTPS URL into the text field, and add `/login/nylas/authorized` after it. For example, if your HTTPS URL is `https://ad172180.ngrok.io`, then you would put `https://ad172180.ngrok.io/login/nylas/authorized` into the text field in the "Application Callbacks" tab.

Then click the "Add Callback" button to save.

## Install the Dependencies

This project depends on a few third-party Python modules, like Flask. These dependencies are listed in the `requirements.txt` file in this directory. To get started, install [pipenv](https://pypi.org/project/pipenv/) and run the command below to setup your python virtualenv for the example app:

```
pipenv install
```

## Run the Example

Finally, run the example project like this:

```
pipenv run flask run
```

Once the server is running, visit the ngrok URL in your browser to test it out!
