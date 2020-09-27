# About
Hi there 👋

My public repos are mostly tutorials, the occasional hobby, and experiments for work tomorrow.  
Below are examples of my coding-style in a couple languages.  
They might just be a relevant snippet that has been stripped from my bitbucket and anonymised.
<br>
<br>

## Terms used
<details>
<summary>[Expand Section: Terminology definitions]

</summary>

- **Controller**/**controlscript**: A separate function often used with pre-defined variables to operate one or more tools such as a batch-file or a GUI. eg `SendWeeklySmsEmail.bat managers.csv`
- **PR**: A Pull-Request in Git.
- **Tool**/**toolscript**: Generally a module or "black-box" function which probably has some common parameters and will push one output. eg `get-smsReport`
</details>
<br>

## Preferred Styleguides / Conventions:
<details>
<summary>[Expand Section: Links for StyleGuides used with each language]

</summary>

I will try to stick to these style-guides where I can:

- C++: https://google.github.io/styleguide/cppguide.html
- C#/CSharp: https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions
- JavaScript: https://google.github.io/styleguide/jsguide.html
- PowerShell: https://poshcode.gitbooks.io/powershell-practice-and-style/content/Style-Guide/Function-Structure.html
- Python: https://google.github.io/styleguide/pyguide.html
- If a sentence ends with code: I put a space before the full-stop for clarity `/example` .
</details>
<br>

---

# Examples

## Contribution example: VS-Code Plugin 🧩
<details>
<summary>📜[show details + PR link]

- Language: JSON / Regex
- Description: Add `;region` code-folding support to .ahk files in VS-Code.
</summary>

### Link
https://github.com/cweijan/vscode-autohotkey/pull/43

### About
<details>
<summary>💬[Show/Hide overview]
</summary>

Visual Studio Code is a nifty all-in-one editor/debugger for AutoHotKey, but the language hasn't defined cold-folding regions like other languages such as C# (`#region`/`#endregion`), or JavaScript (`//#region`/`//#endregion`).

I found a good active plugin with syntax-highlighting for AutoHotKey's `.ahk` files, and got to work with a proposal to implement folding:

1. I double-checked [folding conventions](https://code.visualstudio.com/docs/editor/codebasics#_folding) for other languages.
2. Learned how [VS-Code Language-Extenstension features](https://code.visualstudio.com/api/language-extensions/language-configuration-guide#folding) are defined with [examples](https://github.com/microsoft/vscode-extension-samples/tree/master/language-configuration-sample).
3. Checked my usual [Regex resources](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference) and [examples](https://www.rexegg.com/regex-style.html) for guidance.
3. Tested my concept locally in VS Code.
4. Started [discussions](https://github.com/stef-levesque/vscode-autohotkey/issues/22) for the [Enhancement Request](https://github.com/cweijan/vscode-autohotkey/issues/44) in GitHub.
5. Created a [Pull-Request](https://github.com/cweijan/vscode-autohotkey/pull/43) with my code using GitHub's new propose a change feature.

</details>


### Goals

- Implement Code-Folding regions for .ahk scripts in VS-Code.
- Support various whitespace arrangements.
- Allow for H1/H2 rules on the same comment line for current AHK users.


### Outcomes
- ➕ PR was accepted and implemented.
- ➕ Successfully added `.ahk` code-folding to my VS-Code by myself.
- ➕ Got some great practice with the new way to do quick PR's in GitHub.
- ➕ Learned a lot about .NET's RegEx and then created some awesome new [automated code snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variable-transforms) using my new skills.
</details>

---

## PowerShell tool/controller example 🛠
<details>
<summary>📜[show details + repo link]

- Language: PowerShell
- Description: Uses the old Azure module to scrape from the Office 365 Graph.
</summary>

### Link
https://github.com/Hicsy/AzureV1Report

### About
<details>
<summary>💬[Show/Hide overview]
</summary>

The function was written as a work-around for a client with O365 which we didn't have administrator access to. Before this little tool: it was considered normal to bounce a ticket to vendor (3-day turnaround) just to get a login-name, or to diagnose why a caller's Skype was no longer connecting. I (ab)used the old V1 Microsoft Graph API module to scrape the client's full graph for login names, SIP, aliases, staff id, and licenses... then cobble in some less ambiguous product names, and spit out a tab-delimited .csv file.

This is a stripped out example of tool-code that was actually used in production quite frequently. It was hacky and quick, and only a [POC](https://en.wikipedia.org/wiki/Proof_of_concept) which unfortunately never got approved for development... so instead, I slapped some control-code within; at-least my colleagues could also use what we had on-the-fly.
Time savings from this script alone gained me about 5-10 hours per week, with ~5 other techs using it daily, we'd consistently save 20+ hours weekly using this simple script.

With more time I would have liked to:

- Add some nice dedicated controller scripts and keep the module pure.
- Create module manifests and tests.
- Update to support PowerShell core / v7.
- Code in a fallback to the real productNames (for any license names I hadn't overridden).
- Break those advanced-properties into a second step so the lookups (licences, aliases etc) don't holdup the core loop. *3x lookups on 200k users not using parallel pipelines becomes slooow...*

</details>


### Goals

- Build user-reports on an O365 tenant without using an administrator account.
- Support single-user lookups and wildcards on various fields.
- ~~Output can be sent to my other tools later~~; Converted to a single-use mode control-script instead.


### Outcomes
- ➖ Concept **not** approved by management for further development.  
- ➖ Use-case changed from a pure "tool" to a *controller* for junior staff.  
- ➕ Widely adopted by my coworkers.  Saves 10-20hrs labour per week.
- ➖ Single-Use was scrapped as out-of-scope. Techs just manually lookup users in the CSV instead to save MFA+2FA hoop-jumping time.
</details>

---

## Python REST server (bottle) example 🧪
<details>
<summary>📜[show details + repo link]

- Language: Python / BottlePy
- Description: A quick REST listener I used for testing my APIs
</summary>

### About
<details>
<summary>💬[Show/Hide overview]
</summary>

This Python 3 RESTful* server is what I used as a simple queue service while I was testing my game server mod. The videogame only supported HTTP GET and POST (rather than PUT/PATCH) so it would respond appropriately to those requests.  

I programmed some buttons on my StreamDeck device to send requests to this API and tested it live with about 8 friends. Later I added some "quick command" endpoints which my friends could trigger (while I was away) by simply refreshing pre-defined webpages.  
This is why the app went from being a pure REST server, to just RESTful functions.

The front-end was beyond the scope of this example hence choosing Bottle as the lightest, fastest option for prototype testing. I would consider Django (with authentication, templates, and a persistent database) to support a production front-end.
</details>

### Link
https://github.com/Hicsy/DST-Rest-Prototype

### Goals

- Playing with REST API's in Python.
- Take some 'command' in JSON, queue it at the right REST endpoint, update its status once retrieved.
- Quick testing with POSTMAN + StreamDeck buttons to quickly simulate/test inbound commands.
- Just a prototype, so no Auth/Database/WebPage

### Outcomes

- Practised Google's Python stylesheet, and basic BottlePy (Bottle/Flask templates = beyond scope / not practised).
- Completed testing of my game mods using this tool.
- Added a couple basic HTTP-GET endpoints for friends to test via web (non-RESTful).
</details>

---

## NodeJS Screeps bot 🤖
<details>
<summary>📜[show details + Repo URL]

- Language: Javascript (functional Node.js)
- Description: My bot I use in online Screeps battles
</summary>

### About
<details>
<summary>💬[show/hide overview]
</summary>

Screeps is an online game where you battle your army of bots on (what they call) a real-time strategy battlefield. It's really turn-based gameplay: Every second-or-so it will run all your JavaScripts top-to-bottom, serialise it, execute on the C++ game server, and then deserialise the whole game-state as a JSON string to run from scratch again next tick.  
As such, I don't think callbacks etc would have any real use to a simple bot.
I fluffed-out the Screeps tutorial by breaking it out into more modular functions... functional is definitely the key-word here.

Once I get my head around game ai StateGraphs I am interested to rebuild this as an object-based bot and then compare performance.
</details>

### Link
https://github.com/Hicsy/Screeps

### Goals

- Learn google's .js formatting styleguide.
- Practice basics like arrow functions and Lodash filters.
- Start using GitHub for more than just an "origin backup".
- (stretch) Implement testing and make a deployment workflow.

### Outcomes

- This one is still a work in progress.
- Got to learn Javascript formatting, but not normal nodeJS programming.
- I have started to learn about deployment workflows.
- Started practising GitHub partial sync and additional remotes.

</details>

---

## LUA game mod example 🎮
<details>
<summary>📜[show details + Repo Link]

- Language: LUA
- Description: A remote-control mod I wrote for Don't Starve Together.
</summary>

### About
<details>
<summary>💬[show/hide overview]

The videogame Don't Starve Together is hardly documented but the game itself is just a little binary that runs LUA scripts out of a .zip file... So I had a look through them and thought this would be a chance to refresh my LUA.  
I like the idea of external sites, devices, sensors, and services being able to send commands to the gameserver but I couldn't work out how to open a socket connection so I thought a mod that polls a queue would be a fun addon...
</summary>


</details>

### Link
https://github.com/Hicsy/DST-MOD-REST-API

### Goals

- Practice my LUA.
- Learn the Don't Starve Together environment.
- Mod my gameservers to accept external command inputs.

### Outcomes

- Needs API-key support added, otherwise done.
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
