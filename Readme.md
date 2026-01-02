# Tibber x Cheap Yellow Display 
Displays todays & tomorrows tibber prices in a Cheap Yellow Display (CYD) that can be mounted anywhere at home.

# Prerequesites

* Get the CYD [ CYD ESP32 Bruce 2432S028 ] from https://de.aliexpress.com/

* Get a Tibber Account: https://tibber.com and note down your personal tibber token 
   
* Set up esphome https://esphome.io/ 

* Checkout any free licenced font, e.g. ]https://github.com/googlefonts/RobotoMono into a directory witin this project, called `fonts`. It will require only on font file called `Roboto-Regular.ttf`

* Now, power on the CYD, check the IP address on your wifi router. Note this IP.

# Build & Deploy 

* (*optional*) Within this cloned github repository, you can do a `esphome compile tibberdisplay.yaml` to just compile the application. If this works, do the next step to verify all is set up.

* Within this cloned github repository, do a `esphome run tibberdisplay.yaml --device=<<IP of you device>>` to build & deploy the tibber application onto your device.


## Configuration 

* Edit `secrets.yaml` with your wifi credentials. It should look like this: 

    ```
    wifi_ssid: "ReplacemeWifi"
    wifi_password: "SecretPassword123"
    ```

* Edit `tibberdisplay.yaml` search for for `strings` and switch to german if you like to change the language and currency. 

* This project needs your *tibber token* to run. Please fetch it from your tibber account via developer tools.

* Browse to `<IP of you device>>:80` enter your *tibber token* in the form field at the left bottom, press enter or leave the field to save it in your CYD.

* after a 5 minutes, the displa should display the tibber graph 

# Testing & Debugging 

## Testing your Tibber Token:
The token is a Header Parameter that is used in the Authorization HTTP Header.
To test your Tibber Auth token, please check it on the console :

```
curl \
 -H "Authorization: Bearer <YOUR_TIBBER_TOKEN>" \
 -H "Content-Type: application/json" \
 -X POST \
 -d  ' {"query":"{ viewer { homes { currentSubscription { priceInfo { today { startsAt total }  } } } } }"}' https://api.tibber.com/v1-beta/gql 
```

This should return HTTP 200 valid json.

## Showin the JSON Response in the Web UI

The web ui also displays the Json Response in the field Tibber Json Response to watch what the CYD got responded. There should be a valid json in it.


## Refresh time


The refresh time is set to 5 minutes and can be configured in the project. 