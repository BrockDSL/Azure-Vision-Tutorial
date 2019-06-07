<img src="azure-logo.png" alt="Logo" width="150px" hight="150px">

# Azure-Vision-Tutorial
An introduction to using a Microsoft Azure API for image analysis



The Microsoft Computer Vision API is a state-of-the-art service provided by Microsoft through Azure that enables developers to analyze and retrieve information from images in a very simple way and with little code. This tutorial will walk you through the basics of using the API in python to produce a list of descriptive words that relate to the image you provide.


## Step 1 - Getting your API Key

The first thing that you will need to do is to go to your Microsoft Azure Portal and get an API Key for the Computer Vision API.  If you have not logged in to Azure before but you are a student or staff at an institution that has an Office 365 membership you can click on the free trial option and log in with your institution log in to access the portal.  Otherwise you can start the free trial by following the steps on the Azure website.
  
Once you have logged into the Microsoft Azure Portal, search for "Computer Vision" in the menu at the top and select it from the "Marketplace" section of results.  Fill in the form that appears by naming your key, leaving subscription as "Azure for Students" (unless you are not using a student subscription in which case you should choose what is appropriate), set location to "(US) West Central US", set pricing to "S1", and either select an existing resource group for your key or make a new one.  Once you have done this click the "Create" button.
  
![Screenshot 1][scrn1]

Navigate to your new key selecting "All Resources" from the left menu and clicking on the name of the key that you created.  Under the "Resource Management" section select "Keys" and you should see your two new keys with a "Copy to Clipboard" button beside each one that you can use to quickly copy your keys.
















[scrn1]: azure-vision-scrn1.png