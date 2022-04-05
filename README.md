# CS3700 Project 5: Web Crawler
Group Members: Sean Hoerl & Jess Van de Ven

## High-Level Approach
At a high level, our crawler logs in to fakebook, and then begins crawling until we have seen all 5 secret flags. We use HTTP 1.1 for all of the requests. For logging in, we send an initial GET request to the login page of fakebook and obtain all of the relevant info there that we need for logging in. This relevant info includes the csrftoken cookie and the csrfmiddleware token which are both needed in order to successfully login. We then build our POST request for the login page using the cookies and token that we just grabbed in the GET request, and the username and password which were provided in the command arguments. If this login POST request runs successfully and responds with the proper code, we will begin to crawl.

For crawling, we start at the home page of fakebook, and grab all available links there and then add them to our queue. For each link in our queue, we visit the corresponding page, check to see if a secret flag is present, grab all unseen links present on the page and add them to our queue. We do this until we have gathered all 5 secret flags.

## Challenges
There were a few things that came up during development of this project that we had difficulty with. 

The first was in regards to how we dealt with parsing the header of any HTTP response. We initially just parsed it straight into a dictionary, splitting each line and adding the corresponding name/value pair to the dictionary. But this was problematic as when submitting a successful login POST request, we get two lines of Set-Cookie in the header of the HTTP response. In our first attempt of dealing with this, we had the header dictionary have Set-Cookie as a string if there was only one instance of it, and then turn that into an array if we saw a second instance of that, and then adding any more instances of it to that array. We did this using isinstance, so we didn't actually have to hardcode Set-Cookie into the function. While this way of doing it allowed us to abstract out more, we then had to do type checking in our method which built the cookie string for our HTTP requests. We thought that the type checking (isinstance) there was ugly and unintuitive, so we decided to just always have Set-Cookie be an array within our dictionary, which would have 1 or more items. We also check to see if the Set-Cookie string is in the header before initializing said array. For any name, value pair we simply append to the array if the name is Set-Cookie. While this is a little bit less abstract, we figured that since Set-Cookie was the only item we would ever see twice or more times in the header it was fine, and it also was a bit simpler. Since none of the possible solutions were great, we simply opted for the simplest and most understandable one out of them.

The second was figuring out how to properly deal with chunked html messages when they were never actually returned from fakebook. To do accomplish this, we used online examples of chunked responses while developing the function. Then for testing the function, we used hardcoded in one of those examples to ensure the function ran properly.

The third was figuring out where to deal with certain error codes. 

## Properties/Features

## Testing