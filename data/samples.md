# Sandbox Examples

We've created sample data for the sandbox edition of this API. The description of the examples is below. Feel free to try the various request formats for these examples. 

## Example 1 (SINGLE)

Basic example with a consignment with one good (Coffee) in 2 containers

    bl = "BMSINGLE001"

    stay = "112233"
    agent = "CCCFC"
    cn ="CNPPI111001" 
    cn ="CNPPI111002"

## Example 2 (DUAL)

Basic example with a consignment with two goods (Coffee and tea) in 2 containers

    bl = "BMDUAL001" (bl)

    stay = "112233" (stay)
    agent = "CCCFC"
    cn ="CNPPI222001" (cn)
    cn ="CNPPI222002" (cn)
    cn ="CNPPI222003" (cn)

## Example 3 (Apples and Oranges)

**Marc's Markets (MM)** has bought apples and oranges from **Plantation Products International (PP)**, with Incoterm CFR. PP is shipping the goods from Cape Town (South Africa) to Antwerp on board of the **Fisk**, a ship from **Southern Ships (SS)** carrier company. **Tardis NV** is the local agency of the carrier who arranges the stay of the ship. **Filips Forwarding Services (FF)** is arranging the import for Marc's Markets. They have arranged for **Tom's Trucking (TT)** to pick up the goods at the **Quality Quay terminal (QQ)** and deliver them to the central warehouse of Marc's markets in Brussels. Filips Forwarding Services relies on **Cathy Customs Services (CC)** to do the import declaration.

    bl = "SSCL123450001"

    stay = "245882" 
    imo number = "L9976297"
    agent = "SOSIAN"
    cn ="SSCZ1111112"
    cn ="SSCZ2222223"

## Example 4 (Coffee and drugs)

**Marc's Markets (MM)** has bought coffee and drugs from **Plantation Products International (PP)**, with Incoterm DDP. PP is shipping the goods from Dakar (Senegal) to Antwerp on board of the **Stovel**, a ship from **Southern Ships (SS)** carrier company. **Order BE** is the local agency of the carrier who arranges the stay of the ship. 
Due to the Incoterm, PP also has to get the goods to MM, and so apart from the ocean transport, they also book the import services at the carrier. This means that Order BE will arrange for **Barry's Barge Company (BB)** to pick up the goods at the **Quality Quay terminal (QQ)** and bring them to the central warehouse of Marc's Markets in Brussels, which happens to have a barge quay. Order BE also relies on the services of on **Cathy Customs Services (CC)** to do the import declaration.


    bl = "SSCL123450001"
    
    stay = "175174"
    agent = "SOSIAN"
    cn ="SSCZ3333334"


