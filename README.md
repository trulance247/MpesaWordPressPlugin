#TruExpress MPESA Payment Gateway

The Lipa na MPesa (LNM) API is an API designed to utilize the new feature introduced by Safaricom known as STK Push. This feature allows the transaction initiation to be moved from the paying customer's side to the payee Organization's side. This eliminates the challenge of having to remember business paybill numbers and account numbers and allows customers to simply confirm the transaction by entering their MPesa PIN on their mobile phone. This is done via the STK push/Pop-up which appears on a customer's phone that prompts them to enter their PIN. For the business, this API enables them to preset all the correct info in the payment request and reduce chances of wrong payments being performed to their systems. It is a C2B transaction, but with the initiator being the organization instead of the customer. Since the organization has the option of presetting all required variables in the request before sending the request, this API has no Validation-Confirmation process like the previous C2B API.

The B2B process is as explained below:

    The Business sets the data in the request and sends it
    The API receives the request and validates it internally first, then sends you an acknowledgement response.
    The API then sends an STK Push request to the target customer's mobile phone. The customer's phone has to be online and unlocked to receive the request.
    The customer confirms the payment amount via the message displayed on-screen, then either enters the PIN or cancels the request accordingly.
    The API receives the customer's response. If the response is a negative, it cancels the transaction and sends a corresponding callback to the initiating 3rd party via the predefined callback URL in the initial request, with the info on why the transaction was cancelled. The possible negative responses could be due to the following scenarios:
        An invalid PIN entered by the customer
        Timeout due to customer not entering the PIN within a given time period (usually 1 min 30 secs)
        The customer's SIM card not having the STK applet on it
        A literal request cancellation by the user on their phone
        Another STK transaction is already underway on the customer's phone (no more than one request can be processed at the same time on the same phone)
    If the PIN is correct, it means the customer accepted the request. The API forwards the transaction to MPesa.
    MPesa automatically processes the request, then sends the response back to the API system which then forwards it to you via the callback URL specified in your initial request. Here, the callback can also either be a success or failure, just like a normal C2B transaction.
    There are no repeat calls for failed callbacks, thus if the API is unable to send the callback to you, you have the Transaction Status Query API to confirm the status of the request, or also confirm via the MPesa Org. portal.

For this API, you will need your actual production line to test the API. Your line must have the STK applet installed (you can update by dialing *234*1*6# on your handset (as of the day of writing of this tutorial). If the update does not work and your physical SIM card is more than 3 years old, consider replacing it), and you must be registered on MPesa. The funds utilized are automatically refunded at midnight. I suggest using values as low as 1 - 10 shillings to perform your transactions to lengthen the number of tries you make. Also beware, the API does not allow one to perform more than 5 consecutive STK requests without completing them. This is marked as phishing, and will cause your line to be blocked from making any more STK requests over 24 hours.
