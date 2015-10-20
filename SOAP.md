Money20/20
=========
# SOAP API

## Endpoints

https://w1.mercurycert.net/ws/ws.asmx

## Merchant Info Clear Text

MID: 003503902913105

PWD: xyz

## Merchant Info E2E/MTOKEN

MID: 019588466313922

PWD: xyz

## Using Mercury’s Web Services Libraries

Web Services are Web APIs that can be accessed over a network and/or the internet, and are executed on a remote system hosting the requested services. Mercury’s Web Service development URL is https://w1.mercurycert.net/ws/ws.asmx with the full WSDL accessed at: https://w1.mercurycert.net/ws/ws.asmx?WSDL

Any development environment supporting Web Services can add a reference to that URL and have access to the methods and classes it provides.

## CreditTransaction

Send Credit, U.S. PIN Debit, EBT, Check Authorization, CardLookup, BatchSummary and BatchClose.

Two arguments:  CreditTransaction(trans as string, password as string)

1. trans is an XML string
2. password is the string provided in the merchant information above.

## GiftTransaction

Send a gift card transactions

Two arguments:  GiftTransaction(trans as string, password as string)

1. trans is an XML string
2. password is the string provided in the merchant information above.

## Credit Sale Example

### Copy the following into a text file named:  soap.txt

```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:mer="http://www.mercurypay.com">
   <soapenv:Header/>
   <soapenv:Body>
      <mer:CreditTransaction>
         <mer:tran><![CDATA[<?xml version="1.0"?>
	<TStream>
          <Transaction>
          <MerchantID>003503902913105</MerchantID>
          <OperatorID>dano</OperatorID>
          <TranType>Credit</TranType>
          <TranCode>Sale</TranCode>
          <Memo>Team1 money2020</Memo>
          <InvoiceNo>123456</InvoiceNo>
          <RefNo>123456</RefNo>
          <Amount>
              <Purchase>2.26</Purchase>
          </Amount>
          <Account>
		<AcctNo>5499990123456781</AcctNo>
		<ExpDate>0816</ExpDate>
		<AccountSource>Keyed</AccountSource>
          </Account>
          </Transaction>
        </TStream>]]></mer:tran>
         <mer:pw>xYz</mer:pw>
      </mer:CreditTransaction>
   </soapenv:Body>
</soapenv:Envelope>
```

### execute this command:

```
curl -k -v -X POST -H "Content-Type:text/xml;" -H "SOAPAction:""http://www.mercurypay.com/CreditTransaction""" -d "@soap.txt" -o output.txt https://w1.mercurycert.net/ws/ws.asmx
```

### Expected result:

```
<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"><soap:Body><CreditTransactionResponse xmlns="http://www.mercurypay.com"><CreditTransactionResult>&lt;?xml version="1.0"?&gt;
&lt;RStream&gt;
	&lt;CmdResponse&gt;
		&lt;ResponseOrigin&gt;Processor&lt;/ResponseOrigin&gt;
		&lt;DSIXReturnCode&gt;000000&lt;/DSIXReturnCode&gt;
		&lt;CmdStatus&gt;Approved&lt;/CmdStatus&gt;
		&lt;TextResponse&gt;AP&lt;/TextResponse&gt;
		&lt;UserTraceData&gt;&lt;/UserTraceData&gt;
	&lt;/CmdResponse&gt;
	&lt;TranResponse&gt;
		&lt;MerchantID&gt;003503902913105&lt;/MerchantID&gt;
		&lt;AcctNo&gt;5499990123456781&lt;/AcctNo&gt;
		&lt;ExpDate&gt;0816&lt;/ExpDate&gt;
		&lt;CardType&gt;M/C&lt;/CardType&gt;
		&lt;TranCode&gt;Sale&lt;/TranCode&gt;
		&lt;AuthCode&gt;008746&lt;/AuthCode&gt;
		&lt;CaptureStatus&gt;Captured&lt;/CaptureStatus&gt;
		&lt;RefNo&gt;0007&lt;/RefNo&gt;
		&lt;InvoiceNo&gt;123456&lt;/InvoiceNo&gt;
		&lt;OperatorID&gt;dano&lt;/OperatorID&gt;
		&lt;Memo&gt;Team1 money2020&lt;/Memo&gt;
		&lt;Amount&gt;
			&lt;Purchase&gt;2.26&lt;/Purchase&gt;
			&lt;Authorize&gt;2.26&lt;/Authorize&gt;
		&lt;/Amount&gt;
		&lt;AcqRefData&gt;KbMCC0148601024  lMCC&lt;/AcqRefData&gt;
		&lt;ProcessData&gt;|00|410100700000&lt;/ProcessData&gt;
	&lt;/TranResponse&gt;
&lt;/RStream&gt;
</CreditTransactionResult></CreditTransactionResponse></soap:Body></soap:Envelope>
```

## PrePaid Balance Example

### Copy the following into a text file named:  soap.txt

```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:mer="http://www.mercurypay.com">
   <soapenv:Header/>
   <soapenv:Body>
      <mer:GiftTransaction>
         <mer:tran><![CDATA[<?xml version="1.0"?>
	<TStream>
          <Transaction>
          <MerchantID>003503902913105</MerchantID>
          <OperatorID>dano</OperatorID>
          <TranType>PrePaid</TranType>
          <TranCode>Balance</TranCode>
          <Memo>Team1 money2020</Memo>
          <InvoiceNo>123456</InvoiceNo>
          <RefNo>123456</RefNo>
          <Amount>
              <Purchase>2.26</Purchase>
          </Amount>
          <Account>
		<AcctNo>6050110010021825120</AcctNo>
		<ExpDate>0816</ExpDate>
		<AccountSource>Keyed</AccountSource>
          </Account>
          </Transaction>
        </TStream>]]></mer:tran>
         <mer:pw>xYz</mer:pw>
      </mer:GiftTransaction>
   </soapenv:Body>
</soapenv:Envelope>
```

### execute this command:

```
curl -k -v -X POST -H "Content-Type:text/xml;" -H "SOAPAction:""http://www.mercurypay.com/GiftTransaction""" -d "@soap.txt" -o output.txt https://w1.mercurycert.net/ws/ws.asmx
```

### Expected result:

```
<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"><soap:Body><GiftTransactionResponse xmlns="http://www.mercurypay.com"><GiftTransactionResult>&lt;?xml version="1.0"?&gt;
&lt;RStream&gt;
	&lt;CmdResponse&gt;
		&lt;ResponseOrigin&gt;Processor&lt;/ResponseOrigin&gt;
		&lt;DSIXReturnCode&gt;000000&lt;/DSIXReturnCode&gt;
		&lt;CmdStatus&gt;Approved&lt;/CmdStatus&gt;
		&lt;TextResponse&gt;Approved&lt;/TextResponse&gt;
		&lt;UserTraceData&gt;&lt;/UserTraceData&gt;
	&lt;/CmdResponse&gt;
	&lt;TranResponse&gt;
		&lt;MerchantID&gt;003503902913105&lt;/MerchantID&gt;
		&lt;TranType&gt;PrePaid&lt;/TranType&gt;
		&lt;TranCode&gt;Balance&lt;/TranCode&gt;
		&lt;InvoiceNo&gt;123456&lt;/InvoiceNo&gt;
		&lt;OperatorID&gt;dano&lt;/OperatorID&gt;
		&lt;AcctNo&gt;6050110010021825120&lt;/AcctNo&gt;
		&lt;Amount&gt;
			&lt;Balance&gt;28.29&lt;/Balance&gt;
		&lt;/Amount&gt;
	&lt;/TranResponse&gt;
&lt;/RStream&gt;
</GiftTransactionResult></GiftTransactionResponse></soap:Body></soap:Envelope>
```
