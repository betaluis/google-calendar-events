# Displaying Calendar Events

First, delete the static cards that we built earlier from the HTML page.

Next, go to main.js file and create a function that loads the events. The function must have the following:

* Give it a name of loadEvents
* The function must be asynchronous
* Takes in a parameter called "max" which will be set to default 8. 
* Inside the function you're going to write a try catch.
* You're going to "try" and fetch from the netlify function. Remember, netlify will look for ./.netlify/functions/calFetch. To this, you'll want to pass in a query of maxResults. The value of the query is equal to the value of the argument passed in.
* catch and console the error.

At this point, your function should look something like the following:

    const loadEvents = async (max=8) => {
        try {
            const endpoint = await fetch(`./netlify/functions/calFetch?maxResults=${max}`)
        }
        catch (e) {
            console.log(e)
        }
    }

Nothing is going to show up on the site, but if everything is working correctly, that data is available and we can pull it.

* Create a constant called "data"
* Pull the data from the endpoint and parse the data with the json api. Make sure that you're waiting for the results.
* Console log the data that you're getting back to make sure it's working. The number of events that are logged out should be represented by the "max" being passed in, so make sure that the results are reflecting this as well.

Example of the code:

    try {
        const endpoint = await fetch(`./.netlify/functions/calFetch?maxResults=${max}`);
        const data = await endpoint.json();
        console.log(data);
    }

Create an events container at the top of the file. We'll use this container to display either an error or the events that are pulled. As of right now, if there's an error, we're only logging it to the console, but we want the user to know that there's an error as well. So let's work on that.

* Constant should be named eventContainer
* Grab the #events-container
* Go inside the catch state and output a paragraph tag to the inner HTML of the events container. Add the necessary tailwind classes to accomplish the following for the paragraph tag:

    - Align the text to the center.
    - Make the text 3 times bigger.
    - "🙀 Something went wrong!"

Example code:

    catch (error) {
        eventContainer.innerHTML = '
            <p class="text-center text-3xl">
                🙀 Something went wrong!
            </p>'
        console.log(error);
    }

Now we want to work on what happens if there aren't any errors.

- We're going to map through the events, so create a constant called "processedEvents." This code will be placed right after the data constant where we parsed it into json data.
- Map through the data and pass in a function. Name the function something relevant and pass in the event that we're mapping through.
- Create the function at the top that we're calling as we map through the events.
- Console log the events to test if we're receiving the events in the console. 

Testing to see if we're getting back the events in the console.

    const eventMapObject = (event) => {
        console.log(event);
    }

    const processedEvents = data.map(event => eventMapObject(event)); // Remember this is supposed to be in the "try"

If successful, we see all the information that is pulled from the Google Calendar API, but we don't need all of this. We need to cut out what we don't need.

This will be accomplished by returning a new object from the eventMapObject();

Return a new object as follows:

    return {
        name: event.summary,
        description: event.description,
        location: event.location,
        start: startDate,
        end: endDate,
        dateRange,
        link: event.htmlLink
    }

The name, description, location, and link all come by default in the API, but the start, end, and dateRange will have to manipulated in order to make it look how we want it to look. The reason for this is because the Google API sends back "all-day" events in a different format than an event that is just a few hours long. 

Let's work on that now.

* Create a constant named "startDate" within the `eventMapObject()` function and make it equal to `event.start.dateTime`.
* Now we want to check if there's an `event.start.dateTime` so we're going to make a tertinary statement.

    - If it does exist, we want to pass in a function that will create a new date out of `event.start.dateTime`. We do this because the format of the date provided by the API is not the format that we want for the start date.

            const startDate = event.start.dateTime ?
                    processDate(new Date(event.start.dateTime))

    - If it doesn't exist, we want to process the `processDate()` differently. Why? Because the dateTime property doesn't exist for events that are all day long; they only have the date property. So, we will change the way we create a new date just by changing how we extract the date from the API. 

            const startDate = event.start.dateTime ?
                    processDate(new Date(event.start.dateTime)) :
                    processDate(new Date(`${event.start.date}T00:00:00`));
    
- Now we need to write the `processDate()` function.

    - Create the function that accepts a "date" as a parameter. 
    - Console log the results.
    - If it throws an error try deleting the `endDate` and `dateRange` properties from the object that is returned.

            const processDate = (date) => {
                console.log(date)
            }
    
    - We're going to return an object in this function as well. The object should have these properties:
        
        - `month: date.getMonth()`
        - `weekday: date.getDay()`
        - `time`
        - `date: date.getDate()`

        <br />
    
    - We now need need to get `date.getMonth()` to say the "Month." We're going to achieve this by creating a function called `getMonth()` and wrapping `date.getMonth()` with it.

            month: getMonth(date.getMonth())

    - Create this function. The function is an array of months and returns the index (which is determined by the month passed in) of the array.

            const getMonth = (month) => ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'][month];

    - Now do the same for the `date.getDay()`.

            weekday: getDayOfWeek(date.getDay())

    - This function is going to have an array with the days of the week. It will accept a number as a parameter and this number will be used to return the index of the array corresponding to the number passed in. 
    - 0 = sunday, 1 = monday, 2 = tuesday, etc.

            const getDatOfWeek = (day) => ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'][day];

    
    - Now we're going to create a few other helper functions that will format the time a little better.

    - Function `isAM()`
        
        - Takes in a parameter called `hour`
        - Returns true if `hour` is less than `12`

    <br />

    - Function `getHour`

        - Takes in a parameter called `hour`.
        - return `hour` if `hour` is less than `12` otherwise returns `hour - 12`.
    <br />
    <br />
    - Function `getMinute()`

        - Takes in a parameter called `minute`
        - returns `00` if `minute` is equal to `0` otherwise returns `minute`
    <br />
    <br />

    - Inside of our `processDate()` function we can create a few variables that will represent the data that we need to display time.

    - Varaible that represents our hour.

            const hour = getHour(date.getHours()) === 0 ?
                false :
                getHour(date.getHours());
    
    - Variable that represents our minute.

            const minute = getMinute(date.getMinutes());

    - Varaible that represents our time suffix (AM or PM):

            const timeSuffix = `
                <small>
                    ${ isAM(date.getHours()) ? "AM" : "PM" }
                </small>
            `
    
    - Variable for time:

            const time = hour && `${hour}:${minute}${timeSuffix}`;

    - If all the above is done correctly, the time property that is being returned by the `processDate()` function should have the correct formatting. 