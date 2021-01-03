---
title: "Reading NFC tags in SwiftUI"
date: 2020-11-02T18:58:42+01:00
slug: ""
description: ""
keywords: []
draft: true
tags: [technical]
math: false
toc: true
---

I couldn't find a short tutorial on CoreNFC's `NFCTagReader`, so here goes nothing.


## Prerequisites

* You will need an Apple developer account
* Add the NFC capability to your project (in Signing & Capabilites, click the plus sign in the corner)
* Add a NFC Scan Usage Description to your `Info.plist`


## NFC overview

Generally speaking there are two types of NFC devices: *active* (e.g. your smartphone) and *passive* (e.g. a simple NFC tag). For communication to happen there has to be at least one active device, but it's also possible for two active devices to communicate. Passive devices are generally called **tags**.

At the time of writing, there are five types of tags (see [here](https://archive.is/NzaWH)). Mostly, they differ in storage and transfer speed, but some tags can also have additional capabilities such as "self-modification of NDEF content", that is, the tag can modify its contents. It's important to know what type of tag you have because that dictates the software interface exposed to you by Apple's CoreNFC.

The tag types are specified by the **NFC Forum**. There are corresponding ISO standards such as ISO 14443 or ISO 15693 which are implemented by NFC tag types (see table). Access to those specifications isn't exactly cheap at $100+, but as a hobbyist they're probably a bit too much to digest anyway. To get details such as specific command codes or flags, you can instead look at manuals for devboards which implement the standard ([example](https://archive.is/9x02H)).


| Tag type    | ISO   |
|-------------|-------|
| 1 (NFC-A)   | 14443 |
| 2 (NFC-A)   | 14443 |
| 3 (NFC-F)   | -     |
| 4 (NFC-A+B) | 14443 |
| 5 (NFC-V)   | 15693 |


### ISO 7816

This spec is particularly notable because to scan these tags, you will need to provide **application identifiers** (AIDs) to CoreNFC. Only tags with a matching AID will be scanned. For a list of AIDs, see [here](https://www.eftlab.com/knowledge-base/211-emv-aid-rid-pix/). A common AID might be the generic D2760000850101. To set your supported AIDs, add "ISO7816 application identifiers for NFC Tag Reader Session" to your `Info.plist`, and enter the AIDs.


## CoreNFC

The abstract base NFC reader class is `NFCReaderSession`, though you can only instantiate its two subclasses `NFCNDEFReaderSession` and `NFCTagReaderSession`. The former is basically a higher level abstraction of the latter which exposes a simpler API to read data tags. The latter allows you to send a custom sequence of commands, and more importantly you can also select the polling type which determines the tag types to communicate with.

Structurally, both options are similar. They take a delegate object which is called back to handle errors and/or communication, and you start the process by creatin a **session**. So generally, a common way to structure your code (independent of what reader you use) might look something like this:

```swift
import Foundation
import CoreNFC

class NFCReader: NSObject, NFCNDEFReaderSessionDelegate {

    func scan() {
        // Create a reader session and pass self as delegate
        session = NFCNDEFReaderSession(delegate: self, queue: DispatchQueue.main, invalidateAfterFirstRead: false)
        session?.begin()
    }
    
    // MARK: delegate methods
    // Implement the NDEF reader delegate protocol.
    
    func readerSession(_ session: NFCNDEFReaderSession, didInvalidateWithError error: Error) {
        // Error handling
    } 
    
    func readerSession(_ session: NFCNDEFReaderSession, didDetectNDEFs messages: [NFCNDEFMessage]) {
        // Handle received messages
    }
}
```

(Example adapted from [Hacking With Swift](https://www.hackingwithswift.com/example-code/libraries/how-to-scan-nfc-tags-using-core-nfc))


### `NFCNDEFReaderSession`

For this higher level option to work, you need to have the right tag type. Unless there's fancy microcontrollers attached to your tag, or you need to send fancy commands, you likely do. Refer to Apple's tutorial [here](https://developer.apple.com/documentation/corenfc/building_an_nfc_tag-reader_app), and/or adapt the code from above to your needs.


### `NFCTagReaderSession`

This class gives you a lot more control. For one, you can set the tag types to look for:

```swift
func scan() {
    // Look for ISO 14443 and ISO 15693 tags
    let session = NFCTagReaderSession(pollingOption: [.iso14443, .iso15693], delegate: self)
    session?.begin()
}
```

Note that this is the **polling type**, not the tag type, so choose the ISO norm corresponding to your tag type (see [#NFC overview]({{< ref "ios-nfc#nfc-overview" >}})).

Your `NFCReader` class must also adopt the `NFCTagReaderSessionDelegate` protocol instead of the `NDEF` version:

```swift
class NFCReader: NSObject, NFCTagReaderSessionDelegate {
    
    // Error handling again
    func tagReaderSession(_ session: NFCTagReaderSession, didInvalidateWithError error: Error) { }

    // Note that you additionally get a function that's called when the session begins
    func tagReaderSessionDidBecomeActive(_ session: NFCTagReaderSession) { }
    
    // Note that an NFCTag array is passed into this function, not a [NFCNDEFMessage]
    func tagReaderSession(_ session: NFCTagReaderSession, didDetect tags: [NFCTag]) { }
}
```

The main difference is that you're passed a `[NFCTag]`. `NFCTag` is an enum of tag types which you can call `session.connect` on, and each tag type has its own separate class and functions which you can access through `NFCTag`'s associated value:

```swift
func tagReaderSession(_ session: NFCTagReaderSession, didDetect tags: [NFCTag]) { 
    session.connect(to: tags.first) { (error: Error?) in
        if error != nil {
            session.invalidate(errorMessage: "Connection error. Please try again.")
            return
        }

        print("Connected to tag!")

        var importPromise: Promise<TransitTag>?

        switch nfcTag {
        case .miFare(let discoveredTag):
            print("Got a MiFare tag!", discoveredTag.identifier, discoveredTag.mifareFamily)
        case .feliCa(let discoveredTag):
            print("Got a FeliCa tag!", discoveredTag.currentSystemCode, discoveredTag.currentIDm)
        case .iso15693(let discoveredTag):
            print("Got a ISO 15693 tag!", discoveredTag.icManufacturerCode, discoveredTag.icSerialNumber, discoveredTag.identifier)
        case .iso7816(let discoveredTag):
            print("Got a ISO 7816 tag!", discoveredTag.initialSelectedAID, discoveredTag.identifier)
        @unknown default:
            session.invalidate(errorMessage: "Unsupported tag!")
        }
}
```

Once you get your tag's class, you can start transferring data. For example, if you're looking for `NFCISO15893Tag`s your switch might look like so:

```swift
switch firstTag {
case .iso15693(let tag):
    tag.readSingleBlock(requestFlags: .highDataRate, blockNumber: 1, resultHandler: { result in
        print(result)
    })
default:
    session.invalidate(errorMessage: "Unsupported NFC tag.")
}
```

Available methods are listed in the docs. You can cross reference the method parameters with the spec or manuals mentioned in [#NFC overview]({{< ref "ios-nfc#nfc-overview" >}}).


## SwiftUI integration

I think the simplest way is making `NFCReader` an `ObservableObject` and adding it as `@ObservedObject` in your view:

```swift
class NFCReader: ObservableObject, NSObject, NFCTagReaderSessionDelegate {
    @Published var scannedData: Data?
    
    func tagReaderSession(_ session: NFCTagReaderSession, didDetect tags: [NFCTag]) { 
        // set scannedData
    }
    
    // ...
}

struct MyView: View {
    @ObservedObject reader = NFCReader()
    
    var body: some View {
        VStack {
            Text(String(data: scannedData, encoding: utf8))
            Button("Scan") {
                reader.scan()
            }
        }
    }
}
```

(Code adapted from [robbiet480's TransitPal](https://github.com/robbiet480/TransitPal))


