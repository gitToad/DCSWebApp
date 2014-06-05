DCSWebApp
=========

Try it on your desktop or phone/tablet browser at:
http://snacknack.com/1

Idea is to provide a reference app for DCS World pilots that is also easily extensible by anyone.

There are a few iOS and Android native app implementations out there. 
And they are nice, but they are

- not open source
- and even if they were, they require serious coding skills (java, Xcode etc.)

Instead, this is a HTML/Javascript only single web page implementation that should work on iPhones, 
Android phones, tablets and desktop browsers alike. It uses jquery and jquery mobile to reduce the amount
of markup and coding. And although I am personally not a fan of copy/pasting this makes it easy for
non-programmers to extend the "app" (web page really) with new planes, checklists, reference pages etc.

So far, the intended functionality is:

- Airfield reference
  - overall theater map with clickable airports
  and per airfield:
  - Tower, ILS, TACAN frequencies, airport IDs (for autopilots)
  - runways
  - callsigns
  - airport charts with parking positions
  - approach charts with entry/exits and patterns
  - google earth map for reference
  
DCS Modules
  - SU-25T Frogfoot (only one I have worked on so far)
  - TF51D Mustang trainer (TBD)
  - A-10C Warthog (TBD)
  - ... all the other modules: FC3, CA, BS, UH, Mi8, ...(TBD)
  
per module:
  - checklists
  - emergency procedures
  - cockpit information (instruments etc.) (TBD)
  - loadouts (TBD)
  
Checklists
  - allow "click to check off"
  - can issue spoken per step instructions
  - also show keyboard shortcuts
  
Command Map
  - View commands (TBD)
  - Command map (TBD)
  perhaps this needs to be per module rather than global reference
  as some keys will obviously vary per plane (and more so with CA)
  
Weapons and Threats
  - weapons reference
  - threat indicators on RWRs for various planes (again, should this be per plane perhaps?)

Reference 
  - links to other helpful DCS apps, forums, tools, users, youtube channels etc.
  - configuration tricks/tips culled from forums (PeterPs monitor config etc.)
  (perhaps this is a bit too much for this app, since it should not be required
  during flight which is what this app is for: quick reference) TBD
  
Glossary
  - did you forget what CICU or LASTE means ?
  
Calculators
  - easy unit conversion calculators 
  - might add other specialized calcs too (bombing with wind ? etc.)
  
Settings
  - so far just a preference whether you want checklists spoken or not


Tools available on every page (with a button in the bottom toolbar):

Search field
  - you can type any string into the search bar to filter long lists
    
Notes
  - for your personal notes (help, questions, bugs etc.)
  - on the home screen there is a notes section where all your notes
    are available from across the app 

Favorites
  - any page can be bookmarked as a favorite (your home airfield, 
    landing checklist for the SU25T etc.)
  - again the home screen has a Favorites section which lists them
    all just like a browser would.
    
  
Home and Back buttons
  - on every screen's top toolbar (except the home screen)


Some notes:

- I have tried to keep everything in one file - most of it is just text that compresses pretty easily
  this is (for now) easier to maintain, play with, keep in browser cache etc.
  At some point - with multiple DCS modules - this will no longer be practical and be split into
  multiple pages (easy to do)
  
- no server side code (PHP etc.) or configuration is needed. In fact you can just download the
  html and images and run it from your file system as you debug or add information.
  
- I purposely kept the amount of graphics, icons etc minimal to reduce load and browser
  memory requirements. Currently most airfield charts link out to the hoggit server
  (which reminds me I need to add third party credits)
  
- again, I'd like to make this available for non coders/CS engineers to extend. There are plenty
  of very knowledgable and helpful DCS users and I would like to make and keep it possible for 
  anyone to contribute checklists, reference information etc.
  Remains to be seen whether github forking and pull requests are too geeky for that purpose,
  otherwise perhaps I will enable "by email" additions to the app...
  
- I will work on actual code extension tutorials, but for now simply ignore the javascript
  code sections and find an existing page that looks similar to what you want to add and 
  get ready to copy & paste !
  You can see every page's name in the browser URL bar, for example
  http://snacknack.com/1/index.html#SU25T-refuel-rearm
  Here the page name for the Repair/rearm/refuel checklist would be "SU25T-refuel-rearm". 
  Just find that in the page HTML source code, and you will see:
  
```html
    <div data-role="page" id="SU25T-refuel-rearm">
        <div data-role="header" data-theme="a">
            <a data-rel="back">Back</a>
            <h1>SU25T Refuel/Rearm</h1>
            <a href="index.html">Home</a>
        </div>
        <div data-role="content">
            <ul data-role="listview" class="checklist" data-filter="true">
                <li>
                    <h1>Engines off, cockpit open</h1>
                    <p>on ground, stopped</p>
                    <p><i class="key">rs End</i> engines off (not just idle)</p>
                    <p><i class="key">lc C</i> cockpit open</p>
                </li>
                <li>
                    <h1>Request repair</h1>
                     <p><i class="key">\</i> Radio</p>
                     <p><i class="key">F8</i> Ground crew</p>
                     <p><i class="key">F3</i> Request repair</p>
                     <p>Ground crew: "copy"</p>
                     <p>Countdown timer starts</p>
                     <p>repair takes about 3 mins</p>
                </li>
                <li>
                    <h1>Request rearm/refuel</h1>
                    <p><i class="key">la '</i> rearm/refuel</p>
                    <p>select stores/fuel</p>
                </li>
                <li>
                    <h1>Tip: if fuel pump is too LOUD</h1>
                    <p><i class="key">F2</i> external view & zoom out</p>
                    <p>to reduce annoying sound</p>
                </li>
                <li>
                    <h1>Wait for "rearming complete"</h1>
                    <p>rearm also provides new drag chute</p>
                </li>
           </ul>
        </div>
        <div data-role="footer" data-theme="a" data-position="fixed" data-disable-page-zoom="false" data-tap-toggle="false">
            <a href="#edit-note" data-role="button" data-transition="slideup" data-icon="edit" class="footer-button">Notes</a>
            <a href="#favs" data-role="button" data-icon="star" class="footer-button">Favs</a>
            <a href="#" data-role="button" data-icon="back" class="checklist-reset footer-button">Reset</a>
        </div>
    </div>
```

    Copy and paste that whole thing into the page.
    Leaving the header and footer unchanged, it should be fairly obvious how to edit
    content for your own new checklist. Make sure you also change the page name
    in the outermost DIV: <div data-role="page" id="SU25T-refuel-rearm">
    to whatever your page is called (stay consistent with naming schemes and make sure
    your chosen name does not already exist as a page)
    
    Now you only need to hook your new page into an appropriate menu page
    elsewhere, for this checklist, you would look in the SU25T checklists main page:
    http://snacknack.com/1/index.html#SU25T-checklists
    
    Find "SU25T-checklists" and you will see 

```html
        <div data-role="page" id="SU25T-checklists">
        <div data-role="header" data-theme="a">
            <a data-rel="back">Back</a>
            <h1>SU25T Checklists</h1>
            <a href="index.html">Home</a>
        </div>
        <div data-role="content">
            <ul data-role="listview" data-filter="true">
                <li><a href="#SU25T-coldstart">Cold Start & Taxi</a></li>
                <li><a href="#SU25T-takeoff">Takeoff</a></li>
                <li><a href="#SU25T-rtb">Return to Base</a></li>
               ....more checklist items here...
```

    Just find a spot to insert your checklist and copy paste a line from
    above and change the href to your checklist name and the displayed
    text to something descriptive and you are done:
    Save, reload the page in the browser and test your page !
    
    The search field, notes, favorites, home, back etc. functionality will 
    appear in your page automatically.
    
    
  
Future ideas

Sync Favorites, Notes, Settings across your devices

At the moment, Favorites and Notes are stored locally in the browser (although persistently
so you will not lose them if you close and reopen the page) It might be nice to synchronize
these across your devices (phone, tablet, laptop etc) 
so you could for example collect notes while you fly on your phone
and later on file a bug reoprt / make a forum post using those notes on a desktop browser
This will require some form of user account and login mechanism with server support though.

Graphics annotations

It might be nice to annotate (with your finger or a stylus) any graphic in the app and use
it much like a real kneeboard. This could be an extension of the "Notes" feature on
graphics pages.
But it could be even better: how about allowing shared scribbling across multiple users
in a team or flight ? (perhaps even a JTAC or AWACS to complement the 9-lines ?)
Imagine being able to mark out enemies, approach tactics, friendlies etc.
Shared SPI on steroids !
Not that hard to do, but again would require per user accounts, logins, and server support










  
  
