# Response structure

## Response codes

A valid response (status code 200) returns information about a single consignment. Other responses do not return any data:

Status | Meaning | Comment
:----: | ------- | -------
200 | **OK** | Response includes information for references provided
400 | **Bad Request** | Request could not be completed
401 | **Unauthorized** | Request didn’t include correct or sufficient credentials
403 | **Forbidden** | Request cannot be completed at this time or the provided credentials don’t allow for the request to be executed
404 | **Not Found** | No information was found that matches the request
500 | **Internal Server Error** | An error occured while executing the request
409 | **Conflict** | Request parameters do not unambiguously identify a single consignment. Please use alternative request formats.

The response will be available in XML (default) or JSON, depending on the Accept header used.

## Structure details

Two examples have been provided:
* [sample XML response](../data/exampleResponse.xml)
* [sample JSON response](../data/exampleResponse.json)


### Overall structure

```
<ImportConsignmentData xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <Disclaimer>Response format subject to change</Disclaimer>
    <References> ... </References>
    <Measurements> ... </Measurements>
    <Parties> ... </Parties>
    <Locations> ... </Locations>
    <EquipmentInformation> ... </EquipmentInformation>
    <Goods> ... </Goods>
    <Status> ... </Status>
</ImportConsignmentData>
```

### References

```
<References>
    <StayNumber>112233</StayNumber>
    <BillOfLadingId>BMSINGLE001</BillOfLadingId>
    <ImoNumber>L1234567</ImoNumber>
    <FilingAgentCode>CCCFC</FilingAgentCode>
    <SequenceNumber>1</SequenceNumber>
    <ParentDocument>
        <Id>112233L1234567100</Id>
        <SenderId>CCCFC</SenderId>
    </ParentDocument>
</References>
```
    
#### StayNumber
Either corresponds to the stay number provided in the request or to the actual stay number for the consignment.

#### ImoNumber
Ship's IMO reference.

#### BillOfLadingId
Corresponds with the bill of lading reference provided in the request.

#### FilingAgentCode
The agent sending the summary declaration to customs.

##### SequenceNumber
Sequence of this consignment in the original CUSCAR document (article number).

#### ParentDocument
##### Id
Provides a reference to a document which provided this information. 

##### SenderId
Sender of the parent document.

### Totals

Total pieces and weight information for the consignment.

```
<Measurements>
    <TotalQuantity>80</TotalQuantity>
    <TotalWeight>32000</TotalWeight>
</Measurements>
```

### Parties

Relevant parties available in the consignment. 

```
<Parties>
    <Party>
        <PartyTypeCode>CONSIGNEE</PartyTypeCode>
        <UnstructuredAddress>CONSIGNEE ADDRESS</UnstructuredAddress>
    </Party>
    <Party>
        <PartyTypeCode>CONSIGNOR</PartyTypeCode>
        <UnstructuredAddress>CONSIGNOR ADDRESS</UnstructuredAddress>
    </Party>
    <Party>
        <PartyTypeCode>CONSIGNEESAGENT</PartyTypeCode>
        <UnstructuredAddress>ADDRESS</UnstructuredAddress>
    </Party>
</Parties>
```

Possible values for party type code:

| Name
| --- 
|    CONSIGNEE
|    CONSIGNOR
|    CONSIGNEESAGENT
|    CUSTOMSBROKER
|    IMPORTER
|    APPROVEDCONSIGNOR
|    ULTIMATECONSIGNEE
|    TERMINALOPERATOR
|    ACCEPTINGPARTY
    
### Locations

Consignment ports and warehouse information

```
<Locations>
    <PlaceOfDestination>BEANR</PlaceOfDestination>
    <PlaceOfLoading>USBAL</PlaceOfLoading>
    <PlaceOfDischarge>S123</PlaceOfDischarge>
</Locations>
```

* Place of origin: UnLocode
* Place of destination: UnLocode
* Place of loading: UnLocode
* Place of discharge: BE Customs location code
* Warehouse: BE Customs location code 


### Equipment

Related equipment information.


```
<EquipmentInformation>
    <Equipment>
        <EquipmentType>CN</EquipmentType>
        <ContainerNumber>CNPPI111001</ContainerNumber>
        <SizeAndType>45G0</SizeAndType>
        <EmptyFull>FULL</EmptyFull>
        <ServiceCode1>FULLLOADS</ServiceCode1>
        <ServiceCode2>FULLLOADS</ServiceCode2>
        <GrossWeight>24000</GrossWeight>
        <GrossWeightUom>KGM</GrossWeightUom>
        <Seals>
            <Seal>
                <SealPartyTypeCode>UNKNOWN</SealPartyTypeCode>
                <Number>12341234</Number>
            </Seal>
        </Seals>
    </Equipment>
    <Equipment>
        <EquipmentType>CN</EquipmentType>
        <ContainerNumber>CNPPI111002</ContainerNumber>
        <SizeAndType>45G0</SizeAndType>
        <EmptyFull>FULL</EmptyFull>
        <ServiceCode1>FULLLOADS</ServiceCode1>
        <ServiceCode2>FULLLOADS</ServiceCode2>
        <GrossWeight>8000</GrossWeight>
        <GrossWeightUom>KGM</GrossWeightUom>
        <Seals>
            <Seal>
                <SealPartyTypeCode>UNKNOWN</SealPartyTypeCode>
                <Number>12341234</Number>
            </Seal>
        </Seals>
    </Equipment>
</EquipmentInformation>
```

During CUSCAR processing, a few conversions from the original EDIFACT CUSCAR documents are performed to facilitate the reading of the response:

Possible values for *EmptyFull*:

| EDIFACT value | Code | Meaning
| :---: | --- | ---
|    4 | EMPTY |
|    5 | FULL |
|    7 | FULLMIXEDCONSIGNMENT  | FCL with LCL
|    8 | FULLSINGLECONSIGNMENT | FCL with FCL

Possible values for ServiceRequirement (1 and 2):

| EDIFACT value | Code 
| :---: | --- 
|    2 | FULLLOADS
|    3 | LESSTHANFULLLOADS
    
Possible values for SealPartyTypeCode:

| SealPartyTypeCode
| ---
|    CARRIER
|    CUSTOMS
|    SHIPPER
|    UNKNOWN
|    QUARANTAINE AGENT
|    TERMINAL OPERATOR
|    CONSOLIDATOR
    
    
### Goods

Related goods information

```
<Goods>
    <Good>
        <SequenceNumber>1</SequenceNumber>
        <OuterPackageType>PK</OuterPackageType>
        <NumberOfPackages>80</NumberOfPackages>
        <Description>Coffee</Description>
        <GoodsGrossWeight>32000</GoodsGrossWeight>
        <GoodsGrossWeightUom>KGM</GoodsGrossWeightUom>
        <CustomsStatus>T1</CustomsStatus>
        <RelatedEquipmentInfo>
            <RelatedEquipment>
                <ContainerNumber>CNPPI111001</ContainerNumber>
                <EquipmentQuantity>60</EquipmentQuantity>
            </RelatedEquipment>
            <RelatedEquipment>
                <ContainerNumber>CNPPI111002</ContainerNumber>
                <EquipmentQuantity>20</EquipmentQuantity>
            </RelatedEquipment>
        </RelatedEquipmentInfo>
    </Good>
</Goods>
```

A link to the related equipment information is provided when available.

### StatusInfo

This status is the result of the pairing of the CUSCAR (submitted to customs) with the CUSRES response. 

**In this release of the API, the status is always  CUSCARCREATEDACCEPTED.**

```
<Status>
    <Value>CUSCARCREATEDACCEPTED</Value>
    <Description>The CUSCAR for this consignment was accepted by BE Customs.</Description>
</Status>
```
 
 
Read next: [Sample data](../data/samples.md)