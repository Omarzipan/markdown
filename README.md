Hi user,

It looks like there are two things going on here:

1. You're sending requests to the production server at [api.plaid.com](https://api.plaid.com) - test credentials won't work here. The development server where test credentials can be used is [tartan.plaid.com](https://tartan.plaid.com) .
2. You're issuing a GET request rather than a POST request with your curl.
```
curl -G
```
should be
```
curl -X POST
```

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

Hi user,

It looks like you're trying to use an unsupported product for an institution. Not all all institutions support all products. In this case, American Express is not supported by Auth. To see a list of institutions and the products that they support, you can issue the following request:

```
curl https://tartan.plaid.com/institutions
```

Additionally, in the future it would be helpful if you could supply the Plaid error code (it should be alongside the HTTP status code returned) alongside any support request. It usually gives more context to what went wrong.

Best,
Omar
