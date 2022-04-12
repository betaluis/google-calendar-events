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
            <p class="text-slate-400 text-sm">Feb 3</p>
            <h2 class="font-bold text-2xl">
                <a href="#">Really Cool Event</a>
            </h2>
        </div>
    </div>