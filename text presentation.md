Electron is an open source library developed by GitHub for building cross-platform desktop applications with HTML, CSS, 
and JavaScript. Electron accomplishes this by combining Chromium and Node.js into a single runtime and apps can be packaged for Mac,
Windows, and Linux.
Electron began in 2013 as the framework on which Atom, GitHub's hackable text editor, would be built.
The two were open sourced in the Spring of 2014.
It has since become a popular tool used by open source developers, startups, and established companies. 
Electron is maintained by a team at GitHub as well as a group of active contributors from the community. Some of the contributors
are individuals and some work at larger companies who are developing on Electron. We're happy to add frequent contributors to the
project as maintainers.
#Updating Dependencies
Electron's version of Chromium is usually updated within one or two weeks after a new stable Chromium version is released, 
depending on the effort involved in the upgrade.

When a new version of Node.js is released, Electron usually waits about a month before upgrading in order to bring in a more 
stable version.

In Electron, Node.js and Chromium share a single V8 instance—usually the version that Chromium is using. Most of the time this 
just works but sometimes it means patching Node.js.
Long term support of older versions of Electron does not currently exist. If your current version of Electron works for you, you 
can stay on it for as long as you'd like. If you want to make use of new features as they come in you should upgrade to a newer version.
#Core Philosophy
In order to keep Electron small (file size) and sustainable (the spread of dependencies and APIs) the project limits the scope of
the core project.

For instance, Electron uses Chromium's rendering library rather than all of Chromium. This makes it easier to upgrade Chromium but
also means some browser features found in Google Chrome do not exist in Electron.

New features added to Electron should primarily be native APIs. If a feature can be its own Node.js module, it probably should be. 
History
Below are milestones in Electron's history.


April 2013	Atom Shell is started .
May 2014	Atom Shell is open sourced .
April 2015	Atom Shell is re-named Electron .
May 2016	Electron releases v1.0.0 .
May 2016	Electron apps compatible with Mac App Store .
August 2016	Windows Store support for Electron apps .

#Electron Application Architecture
Before we can dive into Electron's APIs, we need to discuss the two process types available in Electron. They are fundamentally
different and important to understand.

#Main and Renderer Processes
In Electron, the process that runs package.json's main script is called the main process. The script that runs in the main process 
can display a GUI by creating web pages. An Electron app always has one main process, but never more.

Since Electron uses Chromium for displaying web pages, Chromium's multi-process architecture is also used. Each web page in 
Electron runs in its own process, which is called the renderer process.

In normal browsers, web pages usually run in a sandboxed environment and are not allowed access to native resources.
Electron users, however, have the power to use Node.js APIs in web pages allowing lower level operating system interactions.

#Differences Between Main Process and Renderer Process
The main process creates web pages by creating BrowserWindow instances. Each BrowserWindow instance runs the web page in its own
renderer process. When a BrowserWindow instance is destroyed, the corresponding renderer process is also terminated.

The main process manages all web pages and their corresponding renderer processes. Each renderer process is isolated and only cares 
about the web page running in it.

In web pages, calling native GUI related APIs is not allowed because managing native GUI resources in web pages is very dangerous and
it is easy to leak resources. If you want to perform GUI operations in a web page, the renderer process of the web page must communicate
with the main process to request that the main process perform those operations.

#Developer Environment
Electron development is essentially Node.js development. To turn your operating system into an environment capable of building
desktop apps with Electron, you will merely need Node.js, npm, a code editor of your choice, and a rudimentary understanding of
your operating system's command line client.
#Security, Native Capabilities, and Your Responsibility
When working with Electron, it is important to understand that Electron is not a web browser. It allows you to build feature-rich
desktop applications with familiar web technologies, but your code wields much greater power. JavaScript can access the filesystem,
user shell, and more. This allows you to build high quality native applications, but the inherent security risks scale with the 
additional powers granted to your code.

With that in mind, be aware that displaying arbitrary content from untrusted sources poses a severe security risk that Electron 
is not intended to handle. In fact, the most popular Electron apps (Atom, Slack, Visual Studio Code, etc) display primarily local
content (or trusted, secure remote content without Node integration) – if your application executes code from an online source,
it is your responsibility to ensure that the code is not malicious.

It can be concluded that the electron has a number of advantages and disadvantages: the main advantage is the use of well-known web 
technologies. the main disadvantage is the excessive consumption of memory by electronically built applications



