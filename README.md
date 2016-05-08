# VerisAPI

## Flask Web Service API For Veris Community Database
- Requires MongoDB
- MongoDB Requires Authentication
- MongoDB Needs Database 'veris'

#### Description:
The verisAPI Python(2.7) flask web application is a web service API interface to the Veris Community Database.  MongoDB is currently the only supported database for this web application.  MongoDB also must have user authentication enabled.  

Anyone can register a user on the /veris/register URL.
###### Example:
$curl -d "username=alice&password=pwd" "http://127.0.0.1:8000/veris/register"

{ "Response" : "User Successfully Created." }


##### Installation:
1. Update veris.app.conf with MongoDB connection details.
2. Update veris.app.conf with JSON_PATH variable (VCDB JSON Files)
 - Files Located @: https://github.com/vz-risk/VCDB/tree/master/data/json
3. sudo pip install -r requirements.txt
4. python run.py
5. Create user via /veris/register
6. Load Veris JSON via /veris/load

###### Example API Call:

curl -u "username:password" "http://127.0.0.1:8000/veris/victims"

#### 1. Web Root Returns 403 Forbidden.
http://127.0.0.1:8000/
- methods = GET
- Returns 403 Forbidden

#### 2. Registers A User For Basic Authentication.
http://127.0.0.1:8000/register
- methods = POST
- POST parameters = 'username','password'

$curl -d "username=alice&password=pwd" "http://127.0.0.1:8000/veris/register"

### -- Veris JSON MongoDB Data Ingest --
#### 3. Loads MongoDB with JSON VCDB files.
http://127.0.0.1:8000/veris/load
- methods = GET

$curl -u "username:password" "http://127.0.0.1:8000/veris/load"


### -- Incidents --
#### 4. Returns JSON object of all Veris Incident IDs.
http://127.0.0.1:8000/veris/incidents
- methods = GET

$curl -u "username:password" "http://127.0.0.1:8000/veris/incidents"

#### 5. Return JSON object of Veris Incident by ID.
http://127.0.0.1:8000/veris/incident
- methods = POST
- POST parameters = 'incident'

$curl -u "username:password" -d "incident:XXXX-XXXX-XXXX-XXXX" "http://127.0.0.1:8000/veris/incident"


### -- Victims & Industry --

#### 6. Returns JSON object of Veris Victim Titles.
http://127.0.0.1:8000/veris/victims
- methods = GET

$curl -u "username:password" "http://127.0.0.1:8000/veris/victims"

#### 7. Returns JSON object of Veris Victim Incidents By Search.
http://127.0.0.1:8000/veris/victim
- methods = POST
- POST parameters = 'victim'

$curl -u "username:password" -d "victim:ACME Inc" "http://127.0.0.1:8000/veris/victim"

#### 8. Return All Victims by industry ID.
###### E-Commerce is industy ID: 454111
http://127.0.0.1:8000/veris/industry
- methods = POST
- POST parameters = 'industry'

$curl -u "username:password" -d "industry:454111" "http://127.0.0.1:8000/veris/industry"


### -- Trends --

#### 9. Returns Top Ten Recent Veris Record Create Dates.
http://127.0.0.1:8000/veris/newest
- methods = GET

$curl -u "username:password" "http://127.0.0.1:8000/veris/newest"

#### 10. Returns Distinct Threat Actions & count.
http://127.0.0.1:8000/veris/actions/count
- methods = GET

$curl -u "username:password" "http://127.0.0.1:8000/action/count"

#### 11. Returns Distinct Victims & Geo Location.
http://127.0.0.1:8000/veris/victims/geo
- methods = GET

$curl -u "username:password" "http://127.0.0.1:8000/veris/victims/geo"
