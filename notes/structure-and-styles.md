 # The body


    <body class="bg-slate-50 dark:bg-slate-700 p-4 md:p-6 lg:p-8 min-h-screen gird gap-4 md:gap-6 lg:gap-8 text-slate-600 dark:text-slate-100">
        
        <script type="module" src="/main.js"></script>
    </body>



# Header

    <header class="text-center grid p-4 place-items-center content-center"></header> 

## Heading
Add the page title inside the heading.

    <h1 class="text-3xl sm:text-5xl font-bold bg-clip-text text-transparent bg-gradient-to-br pb-4 md:pb-6 from-blue-500 to-violet-700">My Calendar Events</h1>

## Label
The label goes below the title.

    <label for="eventAmt">Events to Show</label>

## Input
This will control the amount of events that will be shown.

    <input type="range" name="eventAmt" value="9" id="eventAmt" min="1" max="20" class="accent-blue-600 cursor-grab">

# Main tag

    <main class="max-w-6xl w-full mx-auto"></main>

---
## Section

    <section class="grid gap-4 md:gap-6 lg:gap-8 items-start" id="events-container"></section>

---
## Articles
Flesh out the structure and styles of the event card.

    <article class="bg-white dark:bg-slate-800 shadow-xl shadow-slate-200 dark:shadow-slate-800 rounded-lg"> </article>

Top section of the card (date section)

    <div class="p-3 shadow bg-indigo-500 text-indigo-50 uppercase grid place-items-center rounded-t-lg">
        <p class="text-sm">Feb</p>
        <p class="text-3xl font-bold">3</p>
    </div>

Middle section of the card (date and event title)
            
    <div class="p-4 md:p-6 lg:p-8 grid gap-4 md:gap-6">
        <div class="grid gap-1">
            <p class="text-slate-400 text-sm">Thursday, 11:00AM - 3:00PM</p>
            <h2 class="font-bold text-2xl">
                <a href="#">Really Cool Event</a>
            </h2>
        </div>
    </div>

### Button that controls the details section. 
*This button is located right after the `h2`.*

Create its container:

    <div class="grid gap-1"></div>

Create button:

    <button class="text-slate-400 flex gap-1 items-center cursor-pointer"></button>

You will need to add a couple of things to the button because it will be interacting with the page.

>aria-expanded="false"

>aria-controls="details-1"

>id="btn-1"

Flesh out the content within the button:

    <p class="pointer-events-none">See deatils</p>

    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 pointer-evetns-none transition-transform" fill="none" viewbox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2" d="M19 9l-7 7-7-7" />
    </svg>

### The section that expands when button is "see details" is clicked.
*Placed right below the `<button>`.*

Create container:

    <div class="grid gap-1" id="details-1" aria-labeledby="btn-1"></div>


Content within:

    <p class="text-slate-400>lorem 50</p>

### Create button for the event card (not the details button)
*Location will be outside of the details section but within the article and container.*

    <a href="#" class="
    bg-indigo-500
    rounded-md
    px-4
    py-2 
    text-indigo-50
    shadow-2xl
    shadow-indigo-200
    dark:shadow-none
    text-center
    font-bold
    hover:shadow-none
    right-offset-0
    ring-indigo-400
    focus:outline-none
    focus:ring-offset-2
    transition-all">
    View Event</a>

### Repeat each card several times to be able to work on the layout of the events.

First, we're going to have to extend the grid options in tailwind and customize them the way we want them.

* Go to tailwind.config.js
* Add the following:

        extend: {
            gridTemplateColumns: {
                'cards': 'repeat(auto-fit, minmax-(250px, 1fr))'
            }
        }

* Add grid-cols-cards as a class to the `<section>`.

* Now we need the top title section to holds its place at the top and not try to share the space with the cards. We're going to do something similar as the previous step and create our own auto-row class within tailwind. 

        extend: {
            gridTemplateRows: {
                'auto-row': 'auto 1fr'
            },
            gridTemplateColumns: {
                'cards': 'repeat(auto-fit, minmax-(250px, 1fr))'
            }
        }
* Add the class grid-rows-auto-row as a class to the `<body>`. Now, the title section will only take up as much space as it needs and the cards will automatically fit into their place.
        
<br>
<br>
That's the end of the structure and styles.