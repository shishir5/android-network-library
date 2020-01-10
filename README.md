# android-network-library
This is a network client written on top of retrofit to perform network call just by plug n play this
library.

* This library can perform all the rest api calls (GET, POST, PUT, PATCH, DELETE)
* It provides custom protocols if user needs to perform any analytics event for failure/success
* It provides the option to turn on debug logs

### Getting started

#### Initialization

* Initialize the repository in Application class as follows

```kotlin
ZcNetworkManager.builder(this)
    .setDebugLog(true)
    .setNetworkAnalyticsListener(this)
    .addBaseUrl(ApiConstant.BASE_URL)
    .build()
```

#### Making Rest API Call
```kotlin
val zcNetworkBuilder: ZcNetworkBuilder = ZcNetworkBuilder()
    .setActivity(this)
    .setBodyParams(hashMapOf("title" to "foo", "body" to "bar", "userId" to 1))
    .setRequestType(ZcRequestType.POST)
    .setHeaderParams(hashMapOf("Accept" to "application/json", "key" to "value"))
    .setUrl("<API Url>")
    .setListener(object : ZcNetworkListener {
        override fun onSuccess(
            response: JsonElement?,
            responseCode: Int
        ) {
            val user = LoganSquare.parse(response.toString(), User::class.java)
            Log.d(LibTag.TAG, "onSuccess: ${user.name}")
        }

        override fun onError(error: NetworkError) {
            Log.d(LibTag.TAG, "onError: ${error.httpCode}")
        }
    })
zcNetworkBuilder.request()
```

### Find this project useful ? :heart:

* Support it by clicking the :star: button on the upper right of this page. :v:

## License

```
   Copyright (C) 2020 Zoomcar India Pvt Ltd [Zoomcar](https://www.zoomcar.com)
   Copyright (C) 2011 Android Open Source Project

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```