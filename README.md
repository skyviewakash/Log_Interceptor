# Log_Interceptor
--------



<p align="center">
    <img height="500px" src="https://github.com/skyviewakash/Log_Interceptor/blob/main/Screenshot%202023-04-07%20164437.png"/>
</p>

Usage
--------

```kotlin
val client = OkHttpClient.Builder()
    client.addInterceptor(LoggingInterceptor.Builder()
             .setLevel(Level.BASIC)
             .log(VERBOSE)
             .addHeader("Authorization", "Bearer ${prefrenceHelper.getToken()}")
             .addHeader("Content-Type", "application/json")
             .addHeader("Accept", "application/json")
             .build())
```




Logger & Mock Support
---------------------
```kotlin
LoggingInterceptor.Builder()
    //Add logger to print log as plain text
    .logger(object : Logger {
          override fun log(level: Int, tag: String?, msg: String?) {
              Log.e("$tag - $level", "$msg")
          }
      })
      //Enable mock for develop app with mock data
      .enableMock(BuildConfig.MOCK, 1000L, object : BufferListener {
          override fun getJsonResponse(request: Request?): String? {
              val segment = request?.url?.pathSegments?.getOrNull(0)
              return mAssetManager.open(String.format("mock/%s.json", segment)).source().buffer().readUtf8()
          }
      })
```	

Level
--------

```kotlin
setLevel(Level.BASIC)
	      .NONE // No logs
	      .BASIC // Logging url,method,headers and body.
	      .HEADERS // Logging headers
	      .BODY // Logging body
```	

Platform
--------

```kotlin
log(Platform.WARN) // setting log type
```



