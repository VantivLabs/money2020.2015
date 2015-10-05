Money20/20
=========

# HostedCheckout API

## Endpoints

https://hc.mercurydev.net/hcws/hcservice.asmx -- initialize payment, cardinfo, verify payment

https://hc.mercurydev.net/tws/transactionservicegift.asmx -- gift

https://hc.mercurydev.net/CheckoutPOS.aspx -- redirect for POS

https://hc.mercurydev.net/Checkout.aspx -- redirect ecomm

https://hc.mercurydev.net/tws/TransactionService.asmx -- token
	
## Merchant Ids

### Merchant Info Hosted Checkout POS
MID: 018847445761734

PWD: Y6@Mepyn!r0LsMNq

### Merchant Info Hosted Checkout Ecomm
MID: 013163015566916

PWD: ypBj@f@zt3fJRX,k

## Integration

Three easy steps to a hosted checkout integration:

1. Initiate the Payment Process
2. Display the Mercury HostedCheckout Page
3. Verify the Payment

### Initiate the Payment Process

#### Add this to hc.txt

````
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <InitializePayment xmlns="http://www.mercurypay.com/">
      <request>
        <MerchantID>013163015566916</MerchantID>
        <Password>ypBj@f@zt3fJRX,k</Password>
        <Invoice>1234</Invoice>
        <TotalAmount>2.22</TotalAmount>
        <TaxAmount>0</TaxAmount>
        <TranType>Sale</TranType>
        <Frequency>OneTime</Frequency>
        <Memo>Team1 money2020</Memo>
        <ProcessCompleteUrl>http://localhost/test.html</ProcessCompleteUrl>
        <ReturnUrl>http://localhost/test.html</ReturnUrl>
        <OperatorID>dano</OperatorID>
      </request>
    </InitializePayment>
  </soap:Body>
</soap:Envelope>
````

#### Execute this command

````
curl -k -v -X POST -H "Content-Type:text/xml;" -H 'SOAPAction:"http://www.mercurypay.com/InitializePayment"' -d "@hc.txt" -o output.txt https://hc.mercurydev.net/hcws/hcservice.asmx
````

#### Expected Result

````
<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"><soap:Body><InitializePaymentResponse xmlns="http://www.mercurypay.com/"><InitializePaymentResult><ResponseCode>0</ResponseCode><PaymentID>d20eb481-d7be-4d91-b1ff-c47c3dfbd150</PaymentID><Message>Initialize Successful</Message></InitializePaymentResult></InitializePaymentResponse></soap:Body></soap:Envelope>
````

### Display Mercury CheckoutPage

POST the PaymentID returned from the above request to the following URL and the Mercury hosted payments page will be displayed in the browser:  https://hc.mercurydev.net/Checkout.aspx

The customer will then enter their credit card information and press the submit button

HostedCheckout will then POST the results to the url sent in ProcessCompleteUrl of InitializePayment

### Finally Call Verify Payment

#### Add this to hc.txt

Use the PaymentID returned from the InitializePayment response.

````
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <VerifyPayment xmlns="http://www.mercurypay.com/">
      <request>
        <MerchantID>013163015566916</MerchantID>
        <Password>ypBj@f@zt3fJRX,k</Password>
        <PaymentID>d20eb481-d7be-4d91-b1ff-c47c3dfbd150</PaymentID>
      </request>
    </VerifyPayment>
  </soap:Body>
</soap:Envelope>
````

#### Execute this command

````
curl -k -v -X POST -H "Content-Type:text/xml;" -H 'SOAPAction:"http://www.mercurypay.com/VerifyPayment"' -d "@hc.txt" -o output.txt https://hc.mercurydev.net/hcws/hcservice.asmx
````

#### Expected Result

````
<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"><soap:Body><VerifyPaymentResponse xmlns="http://www.mercurypay.com/"><VerifyPaymentResult><ResponseCode>0</ResponseCode><Status>Error</Status><StatusMessage>Payment ID Expired.</StatusMessage><DisplayMessage>We are unable to process the payment because this payment session has expired.</DisplayMessage><AvsResult /><CvvResult /><AuthCode /><Token /><RefNo /><Invoice>1234</Invoice><AcqRefData /><CardType /><MaskedAccount /><Amount>2.22</Amount><TaxAmount>0</TaxAmount><TransPostTime>0001-01-01T00:00:00</TransPostTime><CardholderName /><AVSAddress /><AVSZip /><TranType>Sale</TranType><PaymentIDExpired>true</PaymentIDExpired><CustomerCode /><Memo>Team1 money2020</Memo><AuthAmount>0</AuthAmount><VoiceAuthCode /><ProcessData /><OperatorID>dano</OperatorID><TerminalName /><ExpDate /></VerifyPaymentResult></VerifyPaymentResponse></soap:Body></soap:Envelope>
````


