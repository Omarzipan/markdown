Hi user,

It looks like there are 2 things going on here:

You're sending requests to the production server at (api.plaid.com) - test credentials won't work here. The development server where test credentials can be used is (tartan.plaid.com) .
You're issuing a GET request (with the -G) rather than a POST request with your curl.
Try this snippet instead:
```
curl -X POST https://tartan.plaid.com/auth \
  -d client_id=test_id \
  -d secret=test_secret \
  -d username=plaid_test \
  -d password=plaid_good \
  -d type=chase
```
Also note that because you're using Chase instead of Well Fargo, you'll receive a different response from the documentation's example. This is because Chase uses MFA whereas Wells Fargo does not.

Feel free to ask if you have any further questions.

Best, 
Omar
