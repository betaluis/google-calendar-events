
# Creating serverless functions

## Create repository and connect to netlify

* Import from existing project on netlify.

* Deploy the site.

* Change the domain settings to change the name of the project.

* Log in to your google calendar and make sure you have actual events in it.

## Get the API key from google

* Go to [this link.](https://console.developers.google.com)

* Create a new project. Make sure you select project.

* Click sidebar > API services > Enable API services

* Click at the top and search for calendar api > Enable

* Create credentials > generate the key and copy

* Restrict key > Goggle Calendar API

* HTTP (only your site)

* Go back to Netlify > Build & Deploy > Key: CAL_API + Paste the key. 

* In the google calendar go to sharing > find google id > go back to Netlify and add CAl_ID + paste google id under value.

## Connect Netlify to machine and local project

> $ npm install netlify-cli -g

> $ npm install netlify-cli --save-dev

Link the local project to the netlify site:  

> $ netlify link

Install node fetch:

> $ npm install node-fetch

Create local server:

> $ netlify dev


## Building out the function

* Create folder at the root of the project called functions.

* Create a file inside this folder called "calFetch.js" and add the following:

        exports.handler = async function(event, context) {
            return {
                statusCode: 200,
                body: JSON.stringify({
                    message: "Hello World"
                }),
            };
        }

* Create another file at the root level called "netlify.tom." This file will tell netlify where to look for the functions. Add the following to the file.

        [build]
            functions = 'functions'

* Run the netlify server. You should see your message "hello world" at this point.

> $ netlify dev

* Time to write the function.

        import fetch from 'node-fetch';

        const { CAL_API, CAL_ID } = process.env;

* Grap the fetch url from Calendar dev docs. Go to the "list" on the side menu and you should see the url under "HTTP request."

        import fetch from 'node-fetch';

        const { CAL_API, CAL_ID } = process.env;

        const BASEPARAMS = `orderBy=startTime&singleEvents=true&timeMin=${new Date().toISOString()}`
        const BASEURL = `URL?${BASEPARAMS}` // Remember to pass in the calendar id.

        exports.handler = async function(event, context) {
            const finalURL = `${BASEURL}&key=${CAL_API}`

            try {
                if ( event.httpMethod === 'GET' ) {
                    return fetch(finalURL)
                        .then((response) => response.json())
                        .then((data) => ({
                            statusCode: 200,
                            body: JSON.stringify(data.items)
                        }))
                }
                return {
                    statusCode: 401
                }
            } catch (e) {
                console.error(e)
                return {
                    statusCode: 500,
                    body: e.toString()
                }
            }
        }

* Add HEADERS below the BASEURL constant.

        const HEADERS = {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Methods': 'GET',
        }

* Pass in the HEADERS.

        .then((data) => ({
            statusCode: 200,
            body: JSON.stringify(data.items),
            HEADERS
        }))
    
* Organize the data a little better with some tabs.

        body: JSON.stringify(data.items, null, 2),

* Pass in the event parameters. This will let the user decide how many events they want to be fetched.

        const finalURL = `${BASEURL}${event.queryStringParameters.maxResults ? `& maxResults=${event.queryStringParameters.maxResults}` : ''}&key=${CAL_API}`


## End of building out the serverless functions.