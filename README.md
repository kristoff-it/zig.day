# zig.day
https://zig.day

## Organizer Docs
This section explains how to make changes to the website as an organizer.

### Overview
Zig.day is a static website that builds with [Zine](https://zine-ssg.io).

Announcing an event consists in publishing a new content page that, on top of updating
the website itself, will also:

1. Add an entry to the RSS feed of your Zig Day location.
2. Add an event to the iCalendar of your Zig Day Location.
3. Send out emails to people subscribed to your Zig Day.

Since this repository is shared by all organizers and making changes to the website can
send out emails, there are some restrictions in place to protect each other from accidents.

More specifically organizers cannot push directly to the main branch and instead have to
create a branch and then PR any change. The PR will be processed by a bot that will
compare the list of changed files with the patterns in `.github/CODEOWNERS` and will merge
automatically any PR that only changes files owned by the submitter.

This way event organizers are protected from mistakes while still being able to announce
events in full authonomy.


### Initial setup
The initial setup for your Zig Day should be done by Loris, after which you should have
a call where he shows you how everything works.

The setup consists in adding you as a collaborator to this repository, creating a
directory in `/content` that corresponds to your city and adding your GitHub handle to
`.github/CODEOWNERS`, plus some more backend work to setup automated emails.

### Making changes

Clone the repository (don't fork it, just clone directly).
The files that correspond to your event will be located under `/content/<country>/<city>/`.

At the beginning your Zig Day should have the following files:
  
- `banner.png`: the banner image with aspect ratio 3:1 you were asked to provide initially
- `index.smd`: the content page that describes your Zig Day location as a whole
- `0.smd`: (initially disabled because of `.draft` set to `true` in the frontmatter) the page that describes the first event

`.smd` files are basically markdown files with a slightly different frontmatter language (Ziggy instead of YAML). If you are using VSCode to edit those files you can install the `Ziggy` and `SuperMD` extensions from the marketplace to get syntax highlighting (and in the future also LSP features), both extensions are from Loris Cro.

If you're using a different editor, see `https://zine-ssg.io` for more information about tooling support.

On the Zine website you will also find instructions on how to setup Zine locally, which is **highly** recommended in order to preview changes locally before committing.

The official website is the authoritative source on how to setup Zine but, long story short, you can just download a release from GitHub and place it in your `PATH` on any of the main OSs.

To run the local web server just run `zine` without any subcommand.
Open `https://localhost:1990` and any change you make to your content files will immediately be reflected
in the open web page.

### Content file semantics

#### `/content/<country>/<city>/banner.png`

Your banner image with an aspect ratio 3:1. You can change it whenever you want, just try to compress the
file size a little in order to not burn your user's data unnecessarily.

#### `/content/<country>/<city>/index.smd`
This file represents your Zig Day location as a whole (i.e. it's not about any specific scheduled event, for that we have numbered smd files).

You are not expected to need to change anything in the frontmatter of this file, only the markdown content below it.



#### `/content/<country>/<city>/0.smd`

This file represents the first event announcement and by default it's disabled by setting `.draft` to `true`.

When you edit this file for the first time remember to set `.draft` to false (or delete the line entirely).

The frontmatter contains the following important fields (everything else can be ignored):

- `.date`: The date when your announcement goes live and must be updated to the present day.
- `.custom`: This section contains the fields used to specify all metadata that pertains your event
  - `"version"`: Instructs calendar client applications that they need to update the event information. Must be increased whenever a change to any of the contents of `.custom` is made **after the event has been first published** (e.g. when you need to change the date of the event *after* publication). The `version` counter is independent across different events and can be reset when publishing a new event (i.e. when creating a new numbered smd file).
  - `"start"`: The start time and date of your event, your local time.
  - `"duration"`: Duration of your event in hours, currently only supports integers. This value changes the ending time displayed on the event page.
  - `"address"`: Phisical address of your event.
  - `"longitude" and "latitude"`: Coordinates of your event that will be shown in a map on the page specific to this event (i.e. this is unrelated to the pin shown on the homepage of zig.day). One way of getting this information is to go on google maps, right click on the location and then select the first entry from the contextual menu, which will copy in your clip board the coordinates.

It's highly recommended to double check any change you make by having `zine` run a local copy of the site and seeing with your own eyes that everything checks out.

Once the metadata is all entered correctly, you can work on changing the event descrition by modifying the markdown contents below the frontmatter.

The event description should explain to people how to get to the location as appropriate (which metro/train stop to take if applicable, how to find the right door, etc) and what the schedule will roughly look like (e.g. is there nearby food places or do people need to bring food from home?).

Other than that you can put whatever you want in your event description but here are two important suggestions:

1. Do repeat some of the information in `index.smd` also in each numbered event page. People will receive a link to the specific event and most of them will not navigate upwards to the event as a whole, meaning that they will only learn the information you put in this page. Some redundancy will help you make sure that people have all the key information.
2. Setup RSVPs. RSVP is a French achronym used to indicate a "ticketing system" where people can actively confirm or cancel their participation to an event. In the future zig.day will offer this feature natively but for now you can use third party systems such as https://lu.ma (but asking people to send you an email is fine too!). There are two big reasons why you will want to have a system like that in place:
   - A new Zig Day will most likely need to build up its audience and the first event you will want to know if anybody will even show up. An RSVP system will help you get some piece of mind (although be aware that sometimes people sign up for an event and still don't show up, especially if it's a free event).
   - After you start getting traction you might end up in a situation where you don't have enough capacity for everybody who wants to come and an RSVP system will allow you to have a queue of people who will be let in when an accepted participant cancels their participation.


### Pushing your changes

As mentioned earlier, you cannot push commits directly to the main branch. Instead you will have to create a new branch, push your commit to it, and then create a pull request (you can go on the GitHub website after pushing, it will ask you if you want to make a PR from your newly pushed branch).

If you want to collaborate with others on your branch, avoid creating a PR after pushing it.

Once you do create a PR, a bot will immediately attempt to merge it.

As soon as the PR is merged, a main branch CI job will publish the website (takes a minute or two) and your event will be live. Emails will be sent out a few minutes after that.
  
  





