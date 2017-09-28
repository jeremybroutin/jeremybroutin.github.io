---
layout: post
title: "Bittrex API - HMAC-SHA512 Signing"
date: 2017-09-28
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

Lately I have been busy a new app in the context of my [professional certificate][3] with the University of Washington, which is the finale project to validate this certificate.
As my interest grew for cryptocurrencies, I was a bit frustrated with the mobile web experience provided by one of my favorite exchange: Bittrex, so I decided to build an app to access and manage my Bittrex account.

One of the recent challenge I encountered was **encryption**, to securely access my accounts.
The Bittrex API documentation provides the following example on how to leverage HMAC-SHA512 signing to access your accounts:
```php
$apikey='xxx';
$apisecret='xxx';
$nonce=time();
$uri='https://bittrex.com/api/v1.1/market/getopenorders?apikey='.$apikey.'&nonce='.$nonce;
$sign=hash_hmac('sha512',$uri,$apisecret);
$ch = curl_init($uri);
curl_setopt($ch, CURLOPT_HTTPHEADER, array('apisign:'.$sign));
$execResult = curl_exec($ch);
$obj = json_decode($execResult);
```

The way to apply this encoding in Swift is to leverage two "well known" frameworks:
- [CryptoSwift][1], for the encryption part
- [Alamofire][2], for the HTTP request part

Here is a sample function that can be used to retrieve the JSON data out the Bittrex API /getbalances endpoint:
```swift
import Alamofire
import CryptoSwift
...

func getBittrexAccountBalances() {
    // Necessary parameters for HTTP request and headers
    let apiKey = "your_api_key"
    let apiSecret = "your_api_secret"
    let nonce = String(Int(NSDate().timeIntervalSince1970))

    // HTTP url to be requested
    let urlString: String = "https://bittrex.com/api/v1.1/account/getbalances" + "?apikey=\(apiKey)&nonce=\(nonce)"
    
    // Hash-based message authentication code (HMAC)
    let urlData = Array(urlString.utf8)
    let hmac: Array<UInt8> = try! HMAC(key: apiSecret.utf8.map({$0}), variant: .sha512).authenticate(urlData)
    let hmacData = Data(bytes:hmac)
    let hmacString = hmacData.hex

    // Pass HMAC within HTTP Headers
    let authHeaders = [
      	"apisign": hmacString
    ] as HTTPHeaders

    // Execute HTTP request with headers to get JSON data
    Alamofire.request(urlString, headers: authHeaders).responseJSON { (response) in
    	if let result = response.result.value {
        	let balances = result as! NSDictionary
        	print("Balances: \(balances)")
      	} else {
        	print("response.result.value is nil")
      	}
    }
}
```

Last but not least, you will also have to add an extension to the Data type in order to convert your HMAC data to an **hex string** (see `hmacData.hex` in the above code).
There are multilple ways to achieve this conversion, as highlighted in this [StackOverflow thread][4] and here is the one I chose:

```swift
extension Data {
  	var hex: String {
    	return self.map { b in String(format: "%02X", b) }.joined()
  	}
}
```

[1]: https://cocoapods.org/pods/CryptoSwift
[2]: https://cocoapods.org/pods/Alamofire
[3]: https://www.pce.uw.edu/certificates/ios-application-development
[4]: https://stackoverflow.com/questions/7520615/how-to-convert-an-nsdata-into-an-nsstring-hex-string/38131414#38131414
