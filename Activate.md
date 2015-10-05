Money20/20
=========

# Activate API

##Overview

MercuryActivate&trade; is a secure enrollment service that enables merchants to apply to Mercury through an online form.  There is a great PHP example at:  https://github.com/MercuryPay/Activate.PHP.  Most of the info below is taken from that repository.

## Step 1: Choose Your Payload Style and Entry Point

You can use either JSON or XML payloads.

There are three entry points each with varying number of data attribute requirements: **Lead**, **Prospect** or **hybrid**.

* A **Lead** submission requires five data attributes.
* A **Prospect** submission requires over 30 data attributes.
* A **hybrid** submission consists of the five required data attributes plus a subset of the data attributes for a Prospect. The developer decides which data attributes to include. 

## Step 2: Get a test API Key and password from Mercury 

An API Key is required to communicate with the MercuryActivate&trade; service. Each API Key is unique for each developer and to the certification environment used for testing. When the certification review is complete, new production credentials will be provided.

Your API Key is sent using Basic Authentication by passing the key in the authorization header as below.

'Authorization: Basic APIKey'

## Step 3: Build your Payload

### Submit A Lead

Here is a JSON example for a Lead submission:

```
{
  "OwnerFirstName":"Jenny",
  "OwnerLastName":"Smith",
  "OwnerEmail":"Jenny@HelpMe.com",
  "DBAName":"What's For Dinner?",
  "DBAPhone":"7192223333"
}
```

### Submit a Prospect

Here is an XML example for a Prospect submission 

```
<Request>
  <OwnerTitle>General Manager Store 5150</OwnerTitle>
  <OwnerFirstName>Gustavo</OwnerFirstName>
  <OwnerMiddleName>Reyna</OwnerMiddleName>
  <OwnerLastName>Argo</OwnerLastName>
  <OwnerSuffix>PHD</OwnerSuffix>
  <OwnerDOBDay>10</OwnerDOBDay>
  <OwnerDOBMonth>6</OwnerDOBMonth>
  <OwnerDOBYear>1985</OwnerDOBYear>
  <OwnerSSN>123456789</OwnerSSN>
  <OwnerEmail>grargo@HelpMe.com</OwnerEmail>
  <OwnerAddress>200 Main St</OwnerAddress>
  <OwnerCity>Denver</OwnerCity>
  <OwnerStateOrProvince>CO</OwnerStateOrProvince>
  <OwnerPostalCode>80229</OwnerPostalCode>
  <OwnerCountry>US</OwnerCountry>
  <DBAName>What&apos;s for Dinner?</DBAName>
  <DBAAddress>100 Main St</DBAAddress>
  <DBACity>Denver</DBACity>
  <DBAStateOrProvince>CO</DBAStateOrProvince>
  <DBAPostalCode>80229</DBAPostalCode>
  <DBACountry>US</DBACountry>
  <DBAPhone>3031112222</DBAPhone>
  <DBAExtension>1234</DBAExtension>
  <LegalName>Zoom Dinner Inc</LegalName>
  <LegalAddress>300 Main St</LegalAddress>
  <LegalCity>Denver</LegalCity>
  <LegalStateOrProvince>CO</LegalStateOrProvince>
  <LegalPostalCode>80229</LegalPostalCode>
  <LegalCountry>US</LegalCountry>
  <LegalPhone>3031113333</LegalPhone>
  <LegalExtension>1122</LegalExtension>
  <ProductServiceSold>Prepared Food</ProductServiceSold>
  <Market>722210</Market>
  <SIC>5812</SIC>
  <TaxId>1231111234</TaxId>
  <AvgTicket>15.50</AvgTicket>
  <DailyVolume>4125.00</DailyVolume>
  <AnnualSalesVisaMc>1240000.00</AnnualSalesVisaMc>
  <CurrencyType>USD</CurrencyType>
  <PercentRetailSwipedTransactions>80</PercentRetailSwipedTransactions>
  <PercentCardKeyedTransactions>10</PercentCardKeyedTransactions>
  <PercentMailOrderTransactions>0</PercentMailOrderTransactions>
  <Dda>123 4567 8900</Dda>
  <Routing>111222333</Routing>
  <FinancialInstitutionName>Wells Fargo</FinancialInstitutionName>
  <IsChecking>true</IsChecking>
  <FinancialInstitutionNumber>111222333</FinancialInstitutionNumber>
  <OwnershipType>LLC</OwnershipType>
  <ReferenceString>Admin@HelpMe.com</ReferenceString>
</Request>
```

## Step 4: Submit Request to Mercury

### Submit A Lead

To submit a Lead or hybrid through an HTTP POST use this endpoint:  https://activatebeta.mps-lab.com:8121/Lead/Submission

### Submit a Prospect

To submit a Prospect through an HTTP POST use this endpoint:  https://activatebeta.mps-lab.com:8121/QualifiedLead/Submission
	
### Status Response

To get the status on the application via an HTTP GET use this endpoint:  https://activatebeta.mps-lab.com:8121/Application/Status/{id}

Where {id} is the integer representing the ApplicationID returned from the submission.

The format of the successful status responses messages for the get lead status or get Prospect status calls is identical. 

Here is the JSON formatted response:

```
{
  "CmdStatus":"Success",
  "TextResponse":"Submitted",
  "ApplicationId": "0D9217A9-1559-437D-A1A6-6283215CAD44"
}
```


