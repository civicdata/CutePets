CutePets
========

Post a random adoptable pet from a shelter to a twitter feed
-------------------------------------------------------------------

Based off of Code for America's [CutePetsDenver](https://github.com/codeforamerica/cutepetsdenver) made by Team Denver.

### Environmental variables
Edit a the local .env file by adding the appropriate config values. How to get Twitter/PetHarbor/Petfinder config variables is stated below.

### Run
`rake tweet_pet`

## Deployment

### Twitter
1. Create a new [twitter app](https://apps.twitter.com/).
2. On the API key tab for the Twitter app, modify permissions so the app can **Read and Write**.
3. Create an access token. On the API Key tab in Twitter for the app, click **Create my access token**
4. Take note of the values for environment set up below.
*Note:* It's important to change permissions to Read/Write before generating the access token. The access token is keyed for the specific access level and will not be updated when changing permissions.

### Heroku 
1. Download and install the [Heroku Toolbelt](from: https://toolbelt.heroku.com).
2. Create heroku project: `heroku create [app name]`
3. Push code: `heroku push heroku master`
4. Add Twitter environment variables
    1. `heroku config:set consumer_key="your_consumer_key_goes_here"`
    2. `heroku config:set consumer_secret="your_consumer_secret_key_goes_here"`
    3. `heroku config:set access_token="your_access_token_goes_here"`
    4. `heroku config:set access_token_secret="your_access_token_secret_goes_here"`
5. Configure pet datasource

**Petfinder**

Register for an account at [petfinder.com](https://www.petfinder.com/) and then get your [API key](https://www.petfinder.com/developers/api-key). To find the shelter id, find a shelter's page on petfinder.com. The id is the last two letters followed by three numbers in the shelter page url. i.e. For this shelter page, [http://www.petfinder.com/shelters/CA154.html](http://www.petfinder.com/shelters/CA154.html), the shelter id is CA154.
Add Petfinder environment variables.
    1. `heroku config:set petfinder_key="your_api_key_goes_here"`
    2. `heroku config:set petfinder_key="your_api_secret_goes_here"`
    3. `heroku config:set petfinder_shelter_id="shelter_id_goes_here"`
    4. `heroku config:set pet_datasource="petfinder"`

**PetHarbor**

Find the petharbor shelter id. The shelter id can be found near the end of the url, before the pet id, when    clicking on the short like for a pet through petharbor.com. i.e. the shelter id in [http://www.petharbor.com/pet.asp?uaid=BRKL.A034281](http://www.petharbor.com/pet.asp?uaid=BRKL.A034281) is BRKL.
Add Petharbor environment variables
    1. `heroku config:set petharbor_shelter_id="shelter_id_goes_here"`
    2. `heroku config:set pet_datasource="petharbor"`
    
6. Schedule Tweets 
    1. Add the **Heroku Scheduler** add on: `heroku addons:add scheduler`
    2. Schedule tweets: `heroku addons:open scheduler`
    3. In the task field: `rake tweet_pet`.

