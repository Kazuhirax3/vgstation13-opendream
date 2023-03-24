# /vg/station - The OpenDream Port [![Build Status](https://travis-ci.org/vgstation-coders/vgstation13.svg?branch=master)](https://travis-ci.org/vgstation-coders/vgstation13)

[![forinfinityandbyond](https://user-images.githubusercontent.com/5211576/29499758-4efff304-85e6-11e7-8267-62919c3688a9.gif)](https://www.reddit.com/r/SS13/comments/5oplxp/what_is_the_main_problem_with_byond_as_an_engine/dclbu1a)

[/vg/station Official Site](http://ss13.moe) - [Original Source Code](https://github.com/vgstation-coders/vgstation13)

Due to this being a side project, there is no actual facet for communication at this time. Do not go into the /vg/ IRC and Discord and expect any help with this. Clone at your own risk.
**In no way is/are the maintainer(s) of this project affiliated with /vg/station at this time. Do not go bothering the /vg/ coders with any problems/suggestions/reports/whatever meant for this branch (and if you do, don't be surprised if you're told to fuck off).**

---

**>what is this**

Just a fork of the main /vg/ code to try and make it OpenDream compatible. Shit will break. This is an effort to fix it.

**>how get code**

Use your favorite git client and clone the repo:
	git clone https://github.com/Kazuhirax3/vgstation13-opendream <folder-to-clone-to>

**>todo**

Clean up the rest of README.md, werk on code, learn DM, kill suicidal thoughts with caffeine

#### Updating the Code

**THIS SECTION NEEDS REWORKING, DUMB FUCK**
After you have cloned, make sure you have a remote to the main repository and your own forked repository by making a remote using the links above. By right clicking on your remote to this repo you can 'pull' the most recent version of the code from the main repository.

You can then create new branches of code directly from our Bleeding-Edge branch on your computer.

Warning: If you checkout different branches or update the code while Dream Maker is open, this can cause problems when someone adds/removes files or when one of the files changed is currently open.

**>code branches**

We have only one branch (for now), and that is the *Bleeding-Edge-OpenDream* branch.

**>installation**

These directions should work for Linux, Windows, and macOS. All you need to do is tweak it to your OS's needs (e.g. adding .exe to the end of the executable files).
**Note: On Linux and macOS, it is recommended you have a functioning 32-bit WINEPREFIX or a VM prepared for BYOND so that you can still use dreammaker.exe!** For the former choice, the [WineHQ AppDB page for BYOND](https://appdb.winehq.org/objectManager.php?sClass=version&iId=41198) has instructions for running BYOND. Keep in mind that you'll only need to use dreammaker.exe out of the entire BYOND suite, and you shouldn't expect BYOND hub, Dreamseeker, or anything else to work *right*.

First, go clone [OpenDream](https://github.com/OpenDreamProject/OpenDream) and compile it. This requires .NET >=7.0 and its SDK, obtainable from [Microsoft](https://dotnet.microsoft.com/en-us/download/dotnet/7.0).

To build OpenDream, you may need to run:

	dotnet restore

before you can run:

	dotnet build

in the root directory containing OpenDream's source code. At least on my Loonux machine, the executables produced are found in:

	<opendream-source-dir>/bin/Content.Server (OpenDreamServer)
	<opendream-source-dir>/bin/Content.Client (OpenDreamClient)
	<opendream-source-dir>/bin/Content.IntegrationTests (DMCompiler)

For the sake of making it easy, I highly recommend you add the OpenDream executables to your PATH.

Next, build /vg/station with DMCompiler by passing the vgstation13.dme file as an argument:

		DMCompiler <path-to-vg-sauce>/vgstation13.dme

Theoretically, the compilation will complete, and a new file named code.json will be made. Run the following to start up the freshly compiled and ready to go server:

		OpenDreamServer --cvar opendream.json_path=<path-to-vg-sauce>/code.json

But given that this fork is very new, the compilation will fail with many, many errors (as of editing on 23-Mar-2023 at around midnight, 111 errors and 1659 warnings).

**EVERYTHING BELOW THIS LINE MAY BE INACCURATE WITH OPENDREAM! FOLLOW AT YOUR OWN RISK!**

To use the SQLite preferences, rename players2_empty.sqlite to players2.sqlite

Next, copy everything from config-example/ to config/ so you have some default configuration.

Once that's done, open up the config folder.  You'll want to edit config.txt to set the probabilities for different gamemodes in Secret and to set your server location so that all your players don't get disconnected at the end of each round.  It's recommended you don't turn on the gamemodes with probability 0, as they have various issues and aren't currently being tested, so they may have unknown and bizarre bugs.

You'll also want to edit admins.txt to remove the default admins and add your own.  "Host" is the highest level of access, and the other recommended admin levels for now are "Game Master", "Game Admin" and "Moderator".  The format is:

    byondkey - Rank

where the BYOND key must be in lowercase and the admin rank must be properly capitalized.  There are a bunch more admin ranks, but these two should be enough for most servers, assuming you have trustworthy admins.

Finally, to start the server, run Dream Daemon and enter the path to your compiled vgstation13.dmb file.  Make sure to set the port to the one you  specified in the config.txt, and set the Security box to 'Trusted'.  Then press GO and the server should start up and be ready to join.

---

### Configuration

For a basic setup, simply copy every file from config-example/ to config/ and then add yourself as admin via `admins.txt`.

---

### SQL Setup

The SQL backend for the library and stats tracking requires a MySQL server.  (Linux servers will need to put libmysql.so into the same directory as vgstation13.dme.)  Your server details go in /config/dbconfig.txt.

The database is automatically installed during server startup, but you need to ensure the database and user are present and have necessary permissions.

---

### IRC Bot Setup

Included in the repo is an IRC bot capable of relaying adminhelps to a specified IRC channel/server (replaces the older one by Skibiliano).  Instructions for bot setup are included in the /bot/ folder along with the bot/relay script itself.
