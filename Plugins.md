# Plugins #

## New Plugins to access the Residence File ##

#### Filesystem ####
  * URL
> > ` http://host:8080/ami.lab@aminet.org/Filesystem/xml/file.xml `
  * Description
> > This function can be used to access the residence xml file.
  * Returns
> > file.xml in plaintext.
  * Error messages
> > None

#### getState() ####
  * URL
> > ` http://host:8080/ami.lab@aminet.org/get/state?string=request `
  * Description
> > This function returns all the currentValues in the requested room.
  * Request example:
> > {„l“:“1“,“r“:“0“}
  * Returns
> > This link returns a JSON string containing device- and state-arrays and the currentValue.
    * For example it could look like:
> > > {d:[{id:0,s:[{id:0,cv:1}]},{id:1,s:[{id:0,cv:1}]},{id:2,s:[{id:0,cv:1}]},{id:3,s:[{id:0,cv:19}]}]}
  * Error messages
    * „ERROR: OUT OF RANGE” (id does not exist)
    * „ERROR: FILE NOT FOUND“
    * „ERROR: JSON SYNTAX“
    * „ERROR: VALUE IS NOT DIGIT“


#### getEnergy() ####
  * URL

> > ` http://host:8080/ami.lab@aminet.org/get/energy?string=request `
  * Description
> > This function can be used to calculate the consumptions at the moment for defined levels, rooms or devices.
  * Request example:
    * get the consumption of the whole residence for the current month
> > > {}
    * get the consumption of a room for the current month
> > > {„l“:“1“,“r“:“0“}
    * get the consumption of the whole residence for last month without current month
> > > {„m”:”1”}
    * get the consumption of a room for last 6 months without current month
> > > {„l”:”1”,”r”:”0”,”m”:”6”}
  * Returns

> > If the request worked a JSON string will be returned:
    * for whole residence:
> > > {l:[{id:0,r:[{id:0,watt:0.0,kwh:0.0,eur:0.0}]},{id:1,r:[{id:0,watt:0.0,kwh:0.0,eur:0.0},{id:1,watt:0.0,kwh:0.0,eur:0.0}]}]}
    * for a single room:
> > > {d:[{id:0,watt:0.0,kwh:0.0,eur:0.0}]}
  * Error messages
    * “ERROR: FILE NOT FOUND”
    * “ERROR: JSON SYNTAX”
    * “ERROR: TOO MANY MONTHS” (if m > 12)
    * “ERROR: TOO FEW MONTHS” (if m < 1)
    * „ERROR: OUT OF RANGE“ (id does not exist)

#### setState() ####
  * URL

> > ` http://host:8080/ami.lab@aminet.org/set/state?string=request `
  * Description
> > This function parses the request and writes the new currentValue in the xml file.
  * Request example:
> > {„l“:“0“,“r“:“0“,“d“:“0“,“s“:“0“,“cv“:“0“}
  * Returns
> > If the request worked, „SUCCESSFUL“ will be returned.
  * Error messages
    * „ERROR: FILE NOT FOUND“
    * „ERROR: JSON SYNTAX“
    * „ERROR: NOTHING WRITTEN“ (request was ok, but change could not be written to file)
    * „ERROR: OUT OF RANGE“ (id does not exist)
    * „ERROR: VALUE IS NOT DIGIT“
    * „ERROR: VALUE IS OUT OF MIN/MAX“
    * „ERROR: VALUE IS ALREADY SET”
    * „ERROR: NOT CONTROLLABLE“ (e.g. a weather station)
    * „ERROR: WRONG DIMENSION“

#### setMultiState() ####
  * URL
> > ` http://host:8080/ami.lab@aminet.org/set/multiState?string=request `
  * Description
> > This function parses an array of requests and sends the single requests to setState()
  * Request example:
    * level 1 [(room 0 [(dev 0 state 1 to 0), (dev 1 state 0 to 0)]), (room 1 [(dev 0 state 0 to 0)])]
> > > {„l“:[{„id“:“1“,“r“:[{„id“:“0“,“d“:[{„id“:“0“,“s“:[{„id“:“1“,“cv“:“0“}]},{„id“:“1“,“s“:[{„id“:“0“,“cv“:“0“}]}]},{„id“:“1“,“d“:[{„id“:“0“,“s“:[{„id“:“0“,“cv“:“0“}]}]}]}]}
    * level 1 [(room 0 [(dev 0 state 1 to 0)])], level 0 [(room 0 [(dev 0 state 1 to 1)])]
> > > {„l“:[{„id“:“1“,“r“:[{„id“:“0“,“d“:[{„id“:“0“,“s“:[{„id“:“1“,“cv“:“0“}]}]}]},{„id“:“0“,“r“:[{„id“:“0“,“d“:[{„id“:“0“,“s“:[{„id“:“1“,“cv“:“1“}]}]}]}
  * Returns

> > If the request worked, „SUCCESSFUL“ will be returned.
  * Error messages
    * „ERROR: FILE NOT FOUND“
    * „ERROR: JSON SYNTAX“
    * „ERROR: NOTHING WRITTEN“ (request was ok, but change could not be written to file)
    * „ERROR: OUT OF RANGE“ (id does not exist)
    * „(JSON) ERROR: VALUE IS OUT OF MIN/MAX”
    * „(JSON) ERROR: VALUE IS NOT DIGIT „
    * „(JSON) ERROR: NOT CONTROLLABLE” (e.g. a weather station)
    * „(JSON) ERROR: WRONG DIMENSION”


> JSON e.g. „{l:0,r:1,d:0,s:0,cv:0}”
> Errors containing JSON are separated by whitespace

#### changeElement() ####
  * URL
> > ` http://host:8080/ami.lab@aminet.org/change/element?string=request `
  * Description
> > This function can be used to change the value of any element of the xml file.
  * Request example:
    * change the name of the device #0 in room #0 in level #1 to „Toaster”
> > {„l“:“1“,“r“:“0“,“d“:“0“,“e“:“name“,“nv“:“Toaster“}
    * change the name of the room #1 in level #1 to „Office”
> > {„l“:“1“,“r“:“1“,“e“:“name“,“nv“:“Office“}
  * Returns
> > If the request worked, „SUCCESSFUL“ will be returned.
  * Error messages
    * „ERROR: FILE NOT FOUND“
    * „ERROR: JSON SYNTAX“
    * „ERROR: NOTHING WRITTEN“ (request was ok, but change could not be written to file)
    * „ERROR: OUT OF RANGE“ (id does not exist)

