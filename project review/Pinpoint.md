- Pinpoint is an AI powered Hyperlocal marketing platform powered by Nokia's NAC and IBM wastonx Orchestrator.
- Problem statement /usecase of pinpoint:
	- Imagine that you walk pass a bakery shop down the street, they are giving an offer of 20% today, but you are not aware of it. The visibility of the shop goes invisible just as you walk past it.
	- The local business cant spend a lot of money in digital marketing via google ads etc. So it is a problem for both the consumer and tthe business owners.

- Solution:
	- Shop owner registers their shop in our application , once they register they can add their products and create offer campaigns to attract footfall customers.
	- So when the Consumer who has onboarded into our application will get notification of the offer, when the shop comes inside the Geofence of the customer.
	- HE IS THE BEST PART: Geofence when created, when user comes in or goes out triggers notification. but we used it otherway, instead of creating geofence around the shops we did around the user. since notification is only sent to the users who have subscribed to that fence, which would be impossible for a consumer who hasnt visited shop before.
	  
	  
	  THE NAC Used are:
	  - Location Retrieval API
	  - Geofence
	  - Device status -> If device is online could send push notification, if network connected send SMS
	  
	 Features :
	 - Our custom built campaign poster creates poster via HTML.
	 - Push Notification
	 
	 Usage of IBM WastonX orchestrator:
	 *  So when the shop owner creates Campaign here is what is done:
		 * Master agent: Orchestrates Agents like Poster agent A,B , Push Notification Text Generator , Review Agent, Personalization agent.
		 * Poster Agent A & B: 
			 * Gets the Campaign title, offer, shop details with its products
			 * Creates HTML code, which is later snapshot into Image and saved in backend
		- Push Notification:
			- To attract users with catchy phrases just like swiggy and zomato, created an agent, that takes the campaign details and the products details of the shop to created push notification text and send it along with image url to push it as push notification with firebase 
	     - 