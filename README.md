#EazyPay Version One

# MpesaWordPressPlugin
The new 2018 mpesa REST API implementation in form of a wordpress plugin.

#FirstTest&Implementation will be done on the eazypro.net ecosystem

How it works

1. Onclick radio button, open a div payment instructions with complete payament button

2. On clicking the button:
  i.  Connect to MPESA server
  ii. Send request with parameters
  iii.Process the request and time it(TODO: make sure the time is as short as possible)
  iv. Get the response and display to the user the appropriate response
  v.  On successful payment, redirect to the business set up account.
  vi. Else display the error page with custom message

3. Continue browsing, ;-)
