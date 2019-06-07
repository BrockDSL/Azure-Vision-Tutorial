<img src="azure-logo.png" alt="Logo" width="150px" hight="150px">

# Azure-Vision-Tutorial
An introduction to using a Microsoft Azure API for image analysis



The Microsoft Computer Vision API is a state-of-the-art service provided by Microsoft through Azure that enables developers to analyze and retrieve information from images in a very simple way and with little code. This tutorial will walk you through the basics of using the API in python to produce a list of descriptive words that relate to the image you provide.


## Step 1 - Getting your API Key

The first thing that you will need to do is to go to your Microsoft Azure Portal and get an API Key for the Computer Vision API.  If you have not logged in to Azure before but you are a student or staff at an institution that has an Office 365 membership you can click on the free trial option and log in with your institution log in to access the portal.  Otherwise you can start the free trial by following the steps on the Azure website.
  
Once you have logged into the Microsoft Azure Portal, search for "Computer Vision" in the menu at the top and select it from the "Marketplace" section of results.  Fill in the form that appears by naming your key, leaving subscription as "Azure for Students" (unless you are not using a student subscription in which case you should choose what is appropriate), set location to "(US) West Central US", set pricing to "S1", and either select an existing resource group for your key or make a new one.  Once you have done this click the "Create" button.
  
![Screenshot 1][scrn1]

Navigate to your new key selecting "All Resources" from the left menu and clicking on the name of the key that you created.  Under the "Resource Management" section select "Keys" and you should see your two new keys with a "Copy to Clipboard" button beside each one that you can use to quickly copy your keys.
  
  
  
## Step 2 - The Code

The Python code below takes the URL of an image and processes it using the Computer Vision API. The results are returned in a JSON format which is then cleaned up a bit and printed out. Try it out by replacing the text "IMAGE-URL-GOES-HERE" with a URL of an image from somewhere on the internet (make sure that it is the images URL, not a webpage). The function will ask for your API key each time you run it so have it handy to copy and paste into the input field that appears.

```

def img_analysis(image_url):
    import requests
    import json
    from PIL import Image
    from io import BytesIO
    
    subscription_key = input("Enter your API key here: ")
    assert subscription_key
    vision_base_url = "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/"
    # You have use the same region from your subscription key in the above address
    
    analyze_url = vision_base_url + "analyze"
    
    headers = {'Ocp-Apim-Subscription-Key': subscription_key }
    params = {'visualFeatures': 'Description'}
    data = {'url': image_url}
    response = requests.post(analyze_url, headers=headers, params=params, json=data)
    response.raise_for_status()
    
    #The code below cleans up and prints out the JSON
    analysis = response.json()
    print(json.dumps(response.json()).replace('"',''))

img_analysis("IMAGE-URL-GOES-HERE")

```

Another way to use this code is to provide an image locally for analysis. In the code below, replace "IMAGE-PATH-GOES-HERE" with the path to the image that you want to analyze.


```
def image_analysis_local(image_path, subscription_key):
    import requests
    import matplotlib.pyplot as plt
    from PIL import Image
    from io import BytesIO
    
    assert subscription_key
    
    # You have to use the same region from your subscription key in the above address
    vision_base_url = "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/"
    analyze_url = vision_base_url + "analyze"
    
    image_data = open(image_path, "rb").read()
    headers = {'Ocp-Apim-Subscription-Key': subscription_key, 'Content-Type': 'application/octet-stream'}
    params = {'visualFeatures': 'Description'}
    response = requests.post(analyze_url, headers=headers, params=params, data=image_data)
    response.raise_for_status()
    
    #The code below prints out the JSON stuff so you can see what gets returned 
    #and makes up a caption based on the keywords that the tool finds
    analysis = response.json()
    print(analysis)
    image_caption = analysis["description"]["captions"][0]["text"].capitalize().replace('"','')
    
image_analysis_local("IMAGE-PATH-GOES-HERE", input("Enter your API key here: "))

```





<br/>
<br/>
<br/>
<br/>

![DSL Logo][imglogo]  
  
**This tutorial is brought to you by the Brock University Digital Scholarship Lab.  For more information on the DSL check out our website at [www.brocku.ca/library/dsl/](https://brocku.ca/library/dsl/) or you can e-mail us at dsl@brocku.ca.**  
  
You can also find us on:  
[Facebook](https://www.facebook.com/Brock-University-Digital-Scholarship-Lab-349407235866792/)  
[Twitter](https://twitter.com/brock_dsl)  
[Instagram](https://www.instagram.com/brock_dsl/?hl=en)  



[imglogo]: dsl-logo.jpg
[scrn1]: azure-vision-scrn1.png