# PlanAway Vacation Planning Site
Milestone Project Two: Interactive Frontend Development - Code Insitute

The site allows the users to begin to plan their vacation through the search and map tools embedded in the web page. They can select from one of the top 20 most visited countires in the world, then narrow down their search to a city or town within that country. There are 4 selectors once the search is complete which will bring up related results. For further information on the selected country the country info button will reveal useful information appropriate for planning a trip. 

### Demo 
---
A live demo of the site can be found here <a href="https://brad000.github.io/PlanAway-Project/" Target="_blank">PlanAway.</a>

### UX 
--- 
My goal for the overall design of the site was to implement a soft and warm feel, with clean and clear breaks between content. The set up of the content allows the user to easily flow through and achieve their desiared goals. I kept the structure simple to allow more enphasis on the functionality of the site. 

I decided to create a two page site, with an initial landing page and a main page (planner.html), which contains all the functionality. I felt this made the project feel more like a realistic web site and not just a project. 

The landing page contains the created site heading and logo which runs through the whole site. There is brief information on to the basics of the page, there is then a carousel of images based on the user potential search results. the footer is very simple and points to the API used for the site with a link to that page (Google). I felt this was a very appealing visual for users as they enter the site, it also allows them a brief moment to take in the sites basic functions before heading to the main page, the 'Start Planning' button will take users to the main planning page. 

On the main page there is a 'Site Info' button which when clicked will show a dropdown with brief instructions on the workings of the site. There is a simple form and maps where the users can conduct search's of countries and cities. For added information to the user there are country information cards that show when clicked and show information related to the current search result. 

### Technologies
--- 
1.HTML   
2.CSS   
3.JavaScript   
4.Bootstrap (4.4)   
5.Jquery (3.4.1)   
6.Google maps / places API    

### Features
---
* The header is very simple and offers the site name and logo. On the landing page the header contains a link to planner.html, on planner.html the header has a button 'Site Info' which when clicked shows a dropdown with breif pointers on how the site operates.
* The landing page also containers a carousel of images that are put there to offer a pleasant visual on arrival to the site. they are relevant to the search results the user can achieve on the planning page. 
* On the planning page the header contains a 'Site Info' button which activates a dropdown this gives the user a brief insight to the workings of the site.
* The form on the left hand side of the pages works with the map to show the user their desired results. The user can first select a country from the list in the dropdown, once selected this will prompt the map to center and zoom on that country. The autocomplete input box will then be locked to cities / towns within the selected country, The user can then further their search by inputting a city / town into the input field, this will again center and zoom on the search result. 
* There are 4 radio selection buttons below the input fields to filter the results within the selected city. This will bring up results relevant to the selected filter and show them with markers on the map. The user can click these markers and show information on the selected result. 
* There is a clear results button which will reset the search fields. 
* The 'Country Info' button when clicked will show a dropdown card, it will only show information on the country that has been selected from the above dropdown list. If none are selected it will show "please select a country from the list below".
* The sponser site button will activate a modal which shows links to sites used to obtain the information on the page plus other sites to allow users to further continue their vacation planning. 

### Testing 
--- 
Throught the construction of the site i tested various functionality at each stage. All link have been dested and direct you in the intended direction, all link to external source open in a new tab, this has been achieved with the ```target="blank"``` attribute. 

Firstly the JavaScript links were tested by running a simple ```console.log("hello")``` script this was successful. 

The map was then put on to the page using the initmap function taken from the Google API, it was set to a default lnglat co-ordinates, when the function was run the map was visable and set to these default co-orginates, i tested the maps responsivness by changing these co-ordinate and rerunning the code, each time the map changed to the relevant co-ordinates. I then built the form and linked it to the map using the Google Places API tutorial, which gave a default search via country and city. The functionality of this was tested by running user testing, it worked well. I stripped the default end result search of hotels back and added 4 radio buttons that would call on the API to show specific results when selected (Hotels, Attractions, Restaurants and Nightlift). I initially tested this using a eventlistener to wait for one of the radio buttons to be selected before showing the results the test was done using the hotelSearch only. 

``` document.getElementById('hotelCheck').addEventListener('change', onPlaceChanged);``` 

```function hotelSearch() {
 var search = {
  bounds: map.getBounds(),
  types: ['lodging']
 };

 places.nearbySearch(search, function(results, status) {
  if (status === google.maps.places.PlacesServiceStatus.OK) {
   clearResults();
   clearMarkers();
   for (var i = 0; i < results.length; i++) {
    var markerLetter = String.fromCharCode('A'.charCodeAt(0) + (i % 26));
    var markerIcon = MARKER_PATH + markerLetter + '.png';
    markers[i] = new google.maps.Marker({
     position: results[i].geometry.location,
     animation: google.maps.Animation.DROP,
     icon: markerIcon
    });
    
    // Information card if marker is clicked 
    
    markers[i].placeResult = results[i];
    google.maps.event.addListener(markers[i], 'click', showInfoWindow);
    setTimeout(dropMarker(i), i * 100);
    addResult(results[i], i);
   }
  }
 });
}
```

This was repeated for the other 3 radio buttons all came back functional and responsive. A Jquery event was put in to reset and refresh the page when the 'Clear Results' Button, the Jquery link was tested using and event on the button. 

``` $("#button").click(function(){
        $("#button").hide(1000) 
});
```
When clicked the button was hidden confirming the Jquery link was working, i then changed it to refresh the page when the button was clicked. testing was also run on the country info button as there was 20 cards created with information on each country, i wanted for the button to only show the country info relating to the country that had been selected from the dropdown menu. i wrote in a function that would get the selector value and show that card and hide the rest. initially i had issues with this working and after looking over the code i had not included the 'this' parameter which allowed the function to act on the option selected each time. the end code for this function is below 

```
$("select").change(function() {
  $(this).find("option:selected").each(function() {
   var optionValue = $(this).attr("value");
   if (optionValue) {
    $(".extra").not("." + optionValue).hide();
    $("." + optionValue).show();
   }
   else {
    $(".extra").hide();
   }
  });
 }).change();
 
 ``` 
 
Browser testing:

* Chrome
* Firefox
* Safari
* Internet Explorer 

Device testing:

* Pixel 3, 3XL, 4 
* iPhone 8, 10, X, 11 
* Galaxy 11 
* Ipad
* Ipad Pro
* Android Tablet

On testing the internet explorer brower the site rendered a touch short of full screen, i amended the css to improve this and retested, after all browsers and devices tested well for functionality and responsivness. 


### Deployment 
---
The site is hosted on GitHub pages. It is deployed directly from the master branch and is automatically updated whenever there is a commit to that branch ```index.html``` must be the landing page for it to deploy correctly through GitHub pages.

To enable this project to be deployed i logged into GitHub and accessed the repository for this project, went into the settings and then down to the deployment menu, chose to deploy the respository through the master branch and accepted the request. 

To run this code locally you can clone it into your editor by typing ```git clone https://brad000.github.io/PlanAway-Project/``` you can cut ties with by typing ``` git remote rm origin```. 

### Credits 
---
#### Content 
All the HTML and CSS content excluding the map was written by me. 

#### Media 
All photos were taken from a stock image library called <a href="https://www.pexels.com/" target="_blank">Pexels</a>

#### Acknowledgements 
The API and map was taken from the Google API and the maps basic functionality was based on a google places tutorial, this was altered from a HTML, CSS and JavaScript perspective enough to make this unique to my project. 























