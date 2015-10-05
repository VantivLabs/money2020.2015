Money20/20
=========

# REST API

## Endpoint

https://w1.mercurycert.net/PaymentsAPI

## Merchant Info Clear Text

MID: 003503902913105

PWD: xyz

## Merchant Info E2E/MTOKEN

MID: 019588466313922

PWD: xyz

Authentication occurs via HTTP Basic Auth using an HTTP authorization header.

Username: existing MerchantID Password: created and stored by Mercury

1. Create string of [username]:[password]
2. BASE64 encoded string
3. Set Authorization header value to: "Basic [encoded string]"

## Content-Type

Set Content-Type header value to: “application/json”

## POSTS

All transactions are posted to https://w1.mercurycert.net/PaymentsAPI (for development and testing) followed by the transaction type at the end of the URL (referred to in this document as the Resource URL). For example, a credit sale would be: https://w1.mercurycert.net/PaymentsAPI/Credit/Sale

## Example E2E/Token

### Copy the following into a text file named:  json.txt

```
{
"InvoiceNo":"1",
"RefNo":"1",
"Memo":"Team2 Money2020",
"Purchase":"1.00",
"Frequency":"OneTime",
"RecordNo":"RecordNumberRequested",
"EncryptedFormat":"MagneSafe",
"AccountSource":"Swiped",
"EncryptedBlock":"2F8248964608156B2B1745287B44CA90A349905F905514ABE3979D7957F13804705684B1C9D5641C",
"EncryptedKey":"9500030000040C200026",
"OperatorID":"money2020",
}

```

### execute this command:

```
curl -k -v -X POST -H "Content-Type:application/json" -H "Authorization: Basic MDE5NTg4NDY2MzEzOTIyOnh5eg==" -d "@json.txt" -o output.txt https://w1.mercurycert.net/PaymentsAPI/Credit/Sale
```

### Expected result:

```
{
  "ResponseOrigin": "Processor",
  "DSIXReturnCode": "000000",
  "CmdStatus": "Approved",
  "TextResponse": "AP",
  "UserTraceData": "",
  "MerchantID": "019588466313922",
  "AcctNo": "400555XXXXXX0480",
  "ExpDate": "XXXX",
  "CardType": "VISA",
  "TranCode": "Sale",
  "AuthCode": "VI0100",
  "CaptureStatus": "Captured",
  "RefNo": "0004",
  "InvoiceNo": "1",
  "OperatorID": "money2020",
  "Memo": "Team2 Money2020",
  "Purchase": "1.00",
  "Authorize": "1.00",
  "AcqRefData": "aEb014297077004614cRBCAd5e00fJlA  m000005",
  "RecordNo": "RFMWwCKXRt5USrQy0906aaiRuI7MkXBz4gUTEYZ61M0iEgUQCSIQB5FL",
  "ProcessData": "|00|210100200000"
}
```

## Example ClearText

### Copy the following into a text file named:  json.txt

```
{
"InvoiceNo":"1",
"RefNo":"1",
"Memo":"Team2 Money2020",
"Purchase":"1.00",
"AccountSource":"Swiped",
"AcctNo":"5499990123456781",
"ExpDate":"0816",
"OperatorID":"money2020",
}
```

### execute this command:

```
curl -k -v -X POST -H "Content-Type:application/json" -H "Authorization: Basic MDAzNTAzOTAyOTEzMTA1Onh5eg==" -d "@json.txt" -o output.txt https://w1.mercurycert.net/PaymentsAPI/Credit/Sale
```

### Expected result:

```
{
  "ResponseOrigin": "Processor",
  "DSIXReturnCode": "000000",
  "CmdStatus": "Approved",
  "TextResponse": "APROVED TEST CARD",
  "UserTraceData": "",
  "MerchantID": "003503902913105",
  "AcctNo": "549999XXXXXX6781",
  "ExpDate": "XXXX",
  "CardType": "M/C",
  "TranCode": "Sale",
  "AuthCode": "999999",
  "CaptureStatus": "Captured",
  "RefNo": "1",
  "InvoiceNo": "1",
  "OperatorID": "money2020",
  "Memo": "Team2 Money2020",
  "Purchase": "1.00",
  "Authorize": "1.00",
  "AcqRefData": "K",
  "ProcessData": "|00|210100700000"
}
```