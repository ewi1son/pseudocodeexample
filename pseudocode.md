<code>
Functionality (use case)- operator wants to pull correct medication for patient or location.

Order is pushed from SCM
Is stock sufficient? (>= request)
Print label
Spin to corresponding row
Operator scans barcode of medication
Does barcode match barcode on file?
Update inventory count

/*
Objects/Data Structures

    * Talyst
        - Computer
            - SCM (Clinical Manager)
                -updates inventory at pyxis locations (critical low)
                -pushes patient specific medication orders
            - Autopharm
                -which medication is needed
                    -ID 01-01-01
                    -barcodeCorrect (bool)
                        -true/false
                -isSpinning (bool)
                    -true/false
                -amount of medication requested
                    -check against local inventory
                        -inventorySufficient function
                -is the correct barcode scanned
                    -check against barcode database
            - Display
                -alerts
                    -"incorrect barcode scanned"
                    -"approved - updated inventory"
        - Carousel
            -spin to correct location
                -spinTo function
            -rows
                -sections
                    -medications

        - Printer
            -prints labels
                -onPrintLabel function
        - Scanner
            -inputs barcodes
                -onRequestScan function
*/

Pseudo Code

Start

//Begin

INIT()

SCM.requestMed(01-01-01)
AutoPharm.requestReceived(01-01-01)



if(AutoPharm.inventorySufficient = true)
    Carousel.spinTo(01-01-01)
    Printer.dispenseInfo

if(barcodeCorrect)
    AutoPharm.sendMessage("Accepted. Inventory updated")
    display.showMessage
    AutoPharm.updateInventory

//End



// Define Objects, Functions

    INIT
        CREATE SCM
        CREATE AutoPharm
        CREATE Computer
        CREATE Carousel
        CREATE Printer
        CREATE Scanner
        CREATE Operator

    SCM
        Set variables
            patientInfo
            hospitalLocation
        requestMed(type)

    AutoPharm
        INIT    
            Set variables
                medLocation
                medBarcode
                medInventory
                localInventory
            requestReceived
            inventorySufficient(localInventory > SCM.requestMed) true/false
            denyRequest
            barcodeCorrect() true/false
                sendMessage("Incorrect Barcode")
                sendMessage("Accepted. Inventory updated.")
            updateInventory(localInventory - SCM.requestMed)

    Display
        showMessage
    Carousel
        spinTo()
    Printer
        dispenseInfo(SCM.patientInfo + SCM.hospitalLocation)
    Scanner

    Operator
        scansMed
        removesMed

</code>
