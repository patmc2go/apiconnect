---
copyright:
  years: 2017
lastupdated: "2017-08-24"
---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Import your API spec, and proxy an existing REST service by using the Developer Toolkit
Duration: 5 mins  
Skill level: Beginner  


## Objective
This tutorial illustrates how you can bring your existing API under management control with {{site.data.keyword.apiconnect_short}}. In this tutorial, you will import an OpenAPI spec, and create a passthrough API proxy for an existing REST service.

---

## Explore the sample app and test the target endpoints
A sample _weather provider_ app was created for this tutorial.

1. To explore the app, go to http://gettingstartedweatherapp.mybluemix.net/.  
2. Enter a valid 5-digit U.S. zip code to get the _**current weather**_ and _**today's forecast**_.  
![](images/explore-weatherapp-1.png)

  - The sample weather app was created using APIs that provide the weather data. The endpoint to get the **current** weather data is _**https:// myweatherprovider<span></span>.mybluemix.net/current?zipcode={zipcode}**_.
  - Test it out by going to https://myweatherprovider.mybluemix.net/current?zipcode=90210.  
  ![](images/explore-weatherapp-2.png)

  - Similarly, the endpoint to get the forecast data for **today** is _**https:// myweatherprovider<span></span>.mybluemix.net/today?zipcode={zipcode}**_.
  - Test it out by going to https://myweatherprovider.mybluemix.net/today?zipcode=90210.  
  ![](images/explore-weatherapp-3.png)


---

## Import the sample app's OpenAPI spec to create a REST API proxy
1. Launch the **API Designer**. In your terminal window, enter the following command: `apic edit`.
2. Log in using your IBMid.
    ![](images/screenshot_apic-edit_login.png)
3. In the **API Designer**, ensure that the navigation panel is open. If not, click >> to open it.
4. In the navigation panel, click **Drafts**.
5. Go to the **APIs** tab.
6. In the APIs tab, click **Add**.
7. From the drop-down menu, click **Import API from a file or URL**.
   ![](images/toolkit-import-1.png)
8. There is an OpenAPI 2.0 definition of the weather API that you will use for this tutorial. In the "Import OpenAPI (Swagger)" dialog box, enter this URL:
https://raw.githubusercontent.com/ibm-apiconnect/getting-started/master/toolkit/1a-import/weather-provider-api_1.0.0.yaml.
9. Leave the _Add a product_ option unchecked and click **Import**.  
    ![](images/screenshot_import-url.png)  

After you import the OpenAPI spec, you are taken to the Design view of the API. Here you can view various sections of the OpenAPI definition. Scroll to explore, and especially note the Host value. Also you can view the OpenAPI under the Source tab. 
_You'll see that the Host value is set to _ ```$(catalog.host)``` _. This is the base URL for your API proxy._
 


## Test your API proxy

1. Start the local test server by selecting the **Start servers** icon. When the Gateway is started, you will see the status update automatically to _**Running**_.
    ![](images/screenshot_start-server-1.png)

2. Select the **Assemble** tab.

3. Click the play icon (>) to test your API proxy's target invocation.
   _For this tutorial, we will use the embedded Micro Gateway, so ensure **Micro Gateway Policies** is selected.
    ![](images/screenshot_test-0.png)

4. In the test panel:
  - Select the **get /current** operation.  
  - Zipcode is a required parameter for this operation, so enter a valid U.S. zip code (for example, 90210).  
  - Select **invoke**, and verify the response.

    _If you run into a CORS error, follow the instructions in the error message. Click the link in the error to add the exception to your browser, and then click **invoke** again.
  
  - The expected response is a **200 OK** response and the current weather data for zip code 90210.
    ![](images/screenshot_test-1.png)    


## Conclusion

In this tutorial, you saw how an existing REST service can be invoked through an API passthrough proxy. You started by checking the availability of the sample service through the web browser. Then you created an API proxy in API Connect, and linked the proxy to the sample service to be invoked. Finally, you tested this service with the {{site.data.keyword.apiconnect_short}} internal testing tools.
