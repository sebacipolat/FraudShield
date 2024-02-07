<p align="center">
<img src="/banner.png"/>
</p>
Design Example of a Fictional Library for Fraud Prevention.
</br>


## Features
* Device Prevention
* User events
* Transactions record
* Onboarding Protection

> [!NOTE]  
> This is not a real SDK just a Documentation to demostration purpose

## Requirements
* Minimun Android Version API 21
  
  
## Architecture
<img src="/FraudShield.drawio.png"/>

The SDK has a singleton as an entrypoint.

We use multiple ThirdParty Librarys mixed with our own logic usecases.

The users events is stored locally into a Room Database.

# Getting started

* Add Dependency

First ensure that you have defined `mavenCentral` in your Gradle configuration.

```groovy
repositories {
    mavenCentral()
}
```

Next, add wolfguard as a dependency to your project.

Groovy
```groovy
dependencies {
    implementation 'io.github.sebacipolat:fraud-shield-sdk:{version}'
}
```

# Initialize
  
```kotlin
FraudShield.getInstance().init("COMPANY_ID", "API_KEY",
    onStarted = {
        // Callback para cuando FraudShield se ha iniciado con éxito
    },
    onFailure = { error ->
        // Callback para manejar fallos durante la inicialización de FraudShield
    }
)
```
# Identify User

Set User ID.

ie: email, userid

```kotlin
FraudShield.getInstance().setUserID("USER_id")
```

# Events

Set custom events

```kotlin
FraudShield.getInstance().setUserID("USER_id")
```

```kotlin
FraudShield.getInstance().sendEvent("event_name", mapOf("key1" to "value1", "key2" to 123, "key3" to true))
```

# Device Protecion 

Based on WolfGuard SDK

Check the documentation https://github.com/sebacipolat/WolfGuard

```kotlin
FraudShield.getInstance().device()
```
retrieve WolfGuard device class

ie: check root

```kotlin
FraudShield.getInstance().getDevice().root.isRooted(context)
```

# Transaction
Record a transaction 

```kotlin
FraudShield.getInstance().getDevice().recordTransaction("TRANSACTION_ID","body")
```

#  Risk Operation Score Calculation 

FraudShield let check if a operation will be riskly based on data captured and device checks

Return INT value (0-10)

| Score | RISK | 
|-----------|------|
| 0-4  | SAFE | 
| 5-7  | MEDIUM| 
| 8-10 |  RISK    | 


```kotlin
FraudShield.getInstance().checkScore()
```

You should handle the score value and adapt your flow UX to handle the diferent risk values.

# Sync Data

Force send data to FraudShield backend

```kotlin
FraudShield.getInstance().flush()
```

# End Session

Finish Session, clean user id and make a flush.

```kotlin
FraudShield.getInstance().endSession()
```



# License
```xml
Designed and developed by 2024 Sebastian Cipolat

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
