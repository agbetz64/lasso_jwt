# lasso_jwt
JWT for Lasso9


#generate JWT:

// payload is actually whatever you want, these are just some suggestions
// exp is used by most libraries to check expiry date [UNIX datetime as integer]

local(payload = map( 'authLevel' = 10, 
                      'exp' = 1493307118, 
                      'ipAddress' = '111.111.111.111', 
                      'iss' = 'https://[ISSUING_SITE]', 
                      'ist' = 1493307117, 
                      'sub' = '[UNIQUE ID]', 
                      'userName' = '[WHOEVER]') )

jwt_encode(#payload, '//*** TOP SECRET ***//', 'HS256')


#decode JWT:

//the debugger @ https://jwt.io/ is usefull to ensure that everything is working correctly

jwt_decode('//*** JWT ***//', '//*** TOP SECRET ***//')


#use on site:

// this retrieves the JWT from the header and checks it for validity, the checks are note extensive 
// and only an example of what can be done


local(authorization = jwt_authorization())

if( #authorization->auth_level > 5 ) => {^
	
   'authorized stuff here'	
	
^}



