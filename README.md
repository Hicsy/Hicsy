🚧 ETA: 14-SEP-2020 🚧  
# About
Hi there 👋

My public repos are mostly tutorials, the occasional hobby, and experiments for work tomorrow.  
Below are examples of my coding-style in a couple languages.  
They are usually just a relevant snippet that has been stripped from my bitbucket and anonymised.

🚧 ETA: 14-SEP-2020 🚧  
>Please bear with me while I put together some chosen examples from my bitbucket... My goal is to have this all done on Monday.


## Terms used

- **Tool**/**toolscript**: Generally a module or "black-box" function which probably has some common parameters and will push one output. eg `get-smsReport`
- **Controller**/**controlscript**: A separate function often used with pre-defined variables to operate one or more tools such as a batch-file or a GUI. eg `SendWeeklySmsEmail.bat managers.csv`

## Preferred Styleguides / Conventions:
I will try to stick to these styleguides where I can:

- PowerShell: https://poshcode.gitbooks.io/powershell-practice-and-style/content/Style-Guide/Function-Structure.html
- JavaScript: https://google.github.io/styleguide/jsguide.html
- Python: https://google.github.io/styleguide/pyguide.html
- C#/CSharp: https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions
- If a sentence ends with code: I put a space before the full-stop for clarity `/example` .

---

# Examples

## PowerShell tool/controller example
<details>
<summary>
[show details]

- Language: PowerShell
- Description: Uses the old Azure module to scrape from the Office 365 Graph.
</summary>

### Link
https://github.com/Hicsy/AzureV1Report

### About
<details>
<summary>overview
</summary>

The function was written as a work-around for a client with O365 which we didnt have administrator access to. Before this little tool: it was considered normal to bounce a ticket to vendor (3-day turnaround) just to get a login-name, or to diagnose why a caller's Skype was no longer connecting. I (ab)used the old V1 Microsoft Graph API module to scrape the client's full graph for login names, SIP, aliases, staff id, and licenses... then cobble in some less ambiguous product names, and spit out a tab-delimited .csv file.

This is a stripped out example of toolcode that was actually used in production quite frequently. It was hacky and quick, and only a [POC](https://en.wikipedia.org/wiki/Proof_of_concept) which unfortunately never got approved for development... so instead, I slapped some controlcode within; at-least my colleagues could also use what we had on-the-fly.
Time savings from this script alone gained me about 5-10 hours per week, with ~5 other techs using it daily, we'd consistently save 20+ hours weekly using this simple script.

With more time I would have liked to:

- Add some nice dedicated controller scripts and keep the module pure.
- Create module manifests and tests.
- Update to support PowerShell core / v7.
- Code in a fallback to the real productnames (for any license names I hadn't overridden).
- Break those advanced-properties into a second step so the lookups (licences, aliases etc) don't holdup the core loop. *3x lookups on 200k users not using parralel pipelines becomes slooow...*

</details>


### Goals

- Build user-reports on an O365 tenant without using an administrator account.
- Support single-user lookups and wildcards on various fields.
- ~~Output can be sent to my other tools later~~; Converted to a single-use mode controlscript instead.


### Outcomes
- ➖ Concept **not** approved by management for further development.  
- ➖ Use-case changed from a pure "tool" to a *controller* for junior staff.  
- ➕ Widely adopted by my coworkers.  Saves 10-20hrs labor per week.
- ➖ Single-Use was scrapped as out-of-scope. Techs just manually lookup users in the CSV instead to save MFA+2FA hoop-jumping time.
</details>

---

## Python REST server (bottle) example
<details>
<summary>🚧[show details]

- Language: Python / BottlePy
- Description: A quick REST listener I used for testing my APIs
</summary>

### About
<details>
<summary>overview
</summary>

This Python 3 RESTful* server is what I used as a simple queue service while I was testing my game server mod. The videogame only supported HTTP GET and POST (rather than PUT/PATCH) so it would respond appropriately to those requests.  

I programmed some buttons on my StreamDeck device to send requests to this API and tested it live with about 8 friends. Later I added some "quick command" endpoints which my friends could trigger (while I was away) by simply refreshing pre-defined webpages.  
This is why the app went from being a pure REST server, to just RESTful functions.

The front-end was beyond the scope of this example hence choosing Bottle as the lightest, fastest option for prototype testing. I would consider Django (with authentication, templates, and a persistent database) to support a production front-end.
</details>

### Link
🚧 ETA: 12-SEP-2020
### Goals
### Outcomes
</details>

---

## NodeJS Screeps bot
<details>
<summary>🚧[show details]

- Language: Javascript (functional Node.js)
- Description: My bot I use in online Screeps battles
</summary>

### About
<details>
<summary>overview
</summary>

Screeps is an online game where you battle your army of bots on (what they call) a real-time strategy battlefield. It's really turn-based gameplay: Every second-or-so it will run all your javascripts top-to-bottom, serialise it, execute on the C++ game server, and then deserialise the whole game-state as a json string to run from scratch again next tick.  
As such, I don't think callbacks etc would have any real use to a simple bot.
I fluffed-out the screeps tutorial by breaking it out into more modular functions... functional is definitely the key-word here.

Once I get my head around game ai stategraphs I am interested to rebuild this as an object-based bot and then compare performance.
</details>

### Link
🚧 ETA: 11-SEP-2020
### Goals

- Learn google's .js formatting styleguide.
- Practice basics like arrow functions and lodash filters.
- Start using GitHub for more than just an "origin backup".
### Outcomes
</details>

---

## LUA game mod example
<details>
<summary>🚧[show details]

- Language: LUA
- Description: A remote-control mod I wrote for Don't Starve Together.
</summary>

### About
🚧 ETA: 11-SEP-2020
### Link
### Goals

- Practice my LUA.
- Learn the Don't Starve Together environment.
- Mod my gameservers to accept external command inputs.
### Outcomes
</details>

---
<!--
## Example Project
<details open>
<summary>👈 Click for details

- Language: 
- Description: 
</summary>

### About
### Link
### Goals
### Outcomes
</details>

-->
🚧 ETA: 14-SEP-2020 🚧  

<!--
**Hicsy/Hicsy** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
