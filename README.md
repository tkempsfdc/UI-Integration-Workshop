### UI Workshop Instructions

## Setup

1. Open VS Code and open the terminal. In your projects folder, create SFDX project with` sfdx force:project:create —n SalesforceWorkshop`
2. Change directory into the folder you just created
3. Open project folder in VS Code `code .`
4. In VS Code, bring up terminal. Confirm you are in the same directory where you created your sfdx project.
5. Initialize the local directory as a git repository `git init`
6. Add files (what was created in step 1) to staging for commit `git add .`
7. Commit the staged files from step 6 `git commit -m "[comment]"`
8. Create a scratch org: `sfdx force:org:create -s -f config/project-scratch-def.json -a [alias of scratch org]`
9. Open your scratch org: `sfdx force:org:open` . Click the Astro (racoon kid) image, then settings. Note the username for your user.
10. Set a password for your scratch org: `sfdx force:user:password:generate --targetusername <username>`
11. Log out of the scratch org, then log back in with your username and password.


sfdx force:user:display -u [test-l3rsumcrrmvb@example.com](mailto:test-l3rsumcrrmvb@example.com)

## Canvas

### Set up App

Do this in a **new** **browser tab**

1. Go to: https://github.com/davescruggs/sample-canvas-app
2. If you’d like to inspect code locally, git clone the repo
3. Scroll to bottom of repo and click “Deploy to Heroku”
4. If you do not have a Heroku account, sign up for one
5. Name your app
6. After all checkmarks complete, click “Manage App”
7. Leave this tab open in your browser

### Configurations

Do this in your **browser tab with scratch org**

1. In setup, search for App Manager
2. Click New Connected App
3. Fill out the form (leave fields not referenced blank):
    1. Basic Information
        1. Connected App Name: Canvas Sample
        2. API Name (will autofill)
        3. Contact email: [your email address]
    2. API (Enable OAuth Settings)
        1. Enable OAuth Settings - Check the box
        2. Callback URL: `https://[yourapp].herokuapp.com/canvas-demo/` (Replace [yourapp] with whatever you named your app. If you don’t remember, go to the Heroku tab. It will be in the upper left next to where it says “Personal”)
        3. OAuth Scopes - Select and Add all Oauth scopes
    3. Canvas
        1. Canvas - Check the box
        2. Canvas App URL - `https://[yourapp].herokuapp.com/canvas-demo/` (Same URL as used in OAuth settings)
        3. Locations - Select and add all options
        4. Enable as a Canvas Personal app - Check the box
4. Save the connected app
5. Pull your change down to your local repo :  `sfdx force:source:pull`

### Configure Heroku App

Do this in your **browser tab with Heroku**

1. Go back to the browser tab with Heroku open and click the Settings subtab
2. Under Config Vars, click Reveal Config Vars
3. For Key enter CANVAS_CONSUMER_SECRET and for Value, copy the Consumer Key from the Connected App you created above, then click add
4. In the second row, for Key enter IMAGE_URL and enter the URL for an image
5. Test your Heroku app by clicking Open App and appending `canvas-demo/` to the end of the URL

### Create the Aura component

Do this in **VS Code**

1. In VS Code, type Command+Shift+P and then type aura. Choose SFDX: Create Aura Component
2. Enter a name and select the default directory
3. Copy and paste the following code:
4. `<aura:component implements="force:appHostable,forceCommunity:availableForAllPageTypes,flexipage:availableForAllPageTypes" access="global">  
        <force:canvasApp width="100%" maxWidth="infinite" height="700px" maxHeight="infinite"
                            developerName="your-api-name-for-connected-app-here"/>
    </aura:component>`

1. Replace `your-api-name-for-connected-app-here` with the name of the Connected App you created
2. Save the file, then push to your scratch org `sfdx force:source:push`

### Create the Lightning App

Do this in your **browser tab with scratch org**

1. In Setup, search for Lightning App Builder
2. Click the “New” button
3. Select App Page and click the “Next” button
4. Give your page a name and click “Next”
5. Select whichever layout you like and click Finish
6. On the left side panel, in the section called “Custom” you should see the Aura Component. Look for the name you set above. Click and drag this component somewhere onto the design canvas.
7. Click the blue Save button. In the modal, click “Activate”
8. Select the Lighting Experience tab, select Sales under Add to Lightning Apps, then click the blue “Add page to app” button,
9. Click the blue Save button.
10. Click ← Back to return to setup
11. From the terminal in VS Code, pull your changes `sfdx force:source:pull`
12. If you are using git, you may want to stage and commit your changes at this point.

### Seeing the Result

Do this in your **browser tab with scratch org**

1. Under the Salesforce cloud on the left, click the waffle menu and select the Sales app
2. Click the tab with the name you defined above for your app tab
3. You should see your canvas app with the image you chose displayed

## Lightning Out

### Set Up Your Repo & Scratch Org

Do this in **terminal and VS Code**

1. In terminal, navigate to the desired directory and clone the github repo `git clone https://github.com/trailheadapps/lwc-recipes`
2. Navigate to the lwc-recipes directory that was just created and open vs code `code .`
3. Command+Shift+P and select Focus Terminal
4. Create a scratch org: `sfdx force:org:create -s -f config/project-scratch-def.json -a [alias of scratch org]`
5. Open your scratch org: `sfdx force:org:open` . Click the Astro (racoon kid) image, then settings. Note the username for your user.
6. Set a password for your scratch org: `sfdx force:user:password:generate --targetusername <username>`
7. Log out of the scratch org, then log back in with your username and password.

### Create the Integration Aura App

Do this in ** VS Code**

1. Command+Shift+P, search for Aura and select Create Aura App. Call the app “integration” and select default location
2. Open the file integration.app and copy the following code:

```
<aura:application access="GLOBAL" extends="ltng:outApp"> 
    <aura:dependency resource="c:wirelistview"/>
    <aura:dependency resource="c:miscrestapicall"/>
    <aura:dependency resource="c:createUIRecord"/>
</aura:application>
```

1. Push all files to your scratch org: `sfdx force:source:push`

### Deploy the Lightning Out App to Heroku

Do this in a **new browser tab**

1. Navigate to https://github.com/tkempsfdc/ui-integration then scroll down and click the Deploy to Heroku button.

### Create a Connected App

Do this in your **browser tab with scratch org**

1. In setup, search for App Manager
2. Click New Connected App
3. Fill out the form (leave fields not referenced blank):
    1. Basic Information
        1. Connected App Name: lwc out
        2. API Name (will autofill)
        3. Contact email: [your email address]
    2. API (Enable OAuth Settings)
        1. Enable OAuth Settings - Check the box
        2. Callback URL: `https://[yourapp].herokuapp.com/oauth/_callback `(Replace [yourapp] with whatever you named your app. If you don’t remember, go to the Heroku tab. It will be in the upper left next to where it says “Personal”)
        3. OAuth Scopes - Select and Add all Oauth scopes
4. Save the connected app
5. Back in VS Code, pull your change down to your local repo :  `sfdx force:source:pull`

### Configure Heroku App

Do this in your **browser tab with Heroku**

1. Go back to the browser tab with Heroku open and click the Settings subtab
2. Under Config Vars, click Reveal Config Vars
3. For Key enter CONSUMER_KEY and for Value, copy the Consumer Key from the Connected App you created above, then click add
4. In the second row, for Key enter CONSUMER_SECRET. In your scratch org on the Connected App screen, click “Click to Reveal” then copy the consumer secret. Paste this as the Value and click add
5. In the third row, for Key enter CALLBACK_URL. Copy the callback url from your Connected app and paste it as the Value, then click add
6. In the fourth row, for Key enter LIGHTNING_URL and for Value, copy the first part of the URL of your scratch org. Make sure there is no / at the end of the url.

### Add domain to CORS allow list

Do this in your **browser tab with scratch org**

1. In Setup, search for CORS
2. Click New
3. Add `https://[yourapp].herokuapp.com` (make sure to remove the / if you copy/paste) and save

### Check out your Lightning Out app

Do this in your **browser tab with Heroku**

1. Test your Heroku app by clicking Open App. At this point, you will see the Lightning Out header but no components.


