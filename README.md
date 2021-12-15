# rootme-api
Two wonderful ressources:
- The official API: https://api.www.root-me.org/
- This Python wrapper: https://github.com/Remigascou/rootmeapi
=> The only "drawback": we must be logged to send thoses requests. In fact, the RootMe API is waiting for a `spip_cookie` which changes at each connection.

Another solution, based on web scraping:
- https://github.com/magnussen7/rootme-api
- May not be the most reliable one in mid-term.

## Prerequisites
```bash
pip3 install json rootmeapi
```

## Examples
### Getting solutions proposed by a RootMe player
```python
import rootmeapi
user_to_check='USER'
api_object=rootmeapi.RootMeAPI()
api_object.login('MY_USER')
result=api_object.search_author_by_name(user_to_check)
json_response=api_object.get_author_by_id(result[0].id) # In case we have multiple users, we take the first result
print(json_response.solutions)
```

### Title and points of the all challenges validated by the user
```python
import rootmeapi
user_to_check='USER'
api_object=rootmeapi.RootMeAPI()
api_object.login('MY_USER')
result=api_object.search_author_by_name(user_to_check)
json_response=api_object.get_author_by_id(result[0].id) # In case we have multiple users, we take the first result
# Get name and points of all validated challenge
for i in range(len(json_response.validations)):
    chall_response=api_object.get_challenge_by_id(int(json_response.validations[i]['id_challenge']))
    print(chall_response['titre']+": "+chall_response['score']+" points")
```
