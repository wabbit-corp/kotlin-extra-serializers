# Kotlin Extra Serializers

Kotlin Extra Serializers is a Kotlin-based project designed to extend the Kotlin serialization capabilities by providing custom serializers for various data types that are commonly used but not natively supported by the standard Kotlin serialization library.

## Overview

"Kotlin Extra Serializers" enhances the Kotlin serialization library by introducing additional serializers that simplify working with complex data types. By integrating these serializers into your Kotlin project, you can handle data structures involving `BigInteger`, `LocalDateTime`, and `UUID` seamlessly during serialization processes.

## Installation

Add the following dependency to your project:

```kotlin
repositories {
    maven("https://jitpack.io")
}

dependencies {
    implementation("com.github.wabbit-corp:kotlin-extra-serializers:1.0.0")
}
```

## Usage

The repository contains three custom serializers for `BigInteger`, `LocalDateTime`, and `UUID`. Here's a detailed explanation of each, including usage examples derived from the serializer files:

### BigIntegerSerializer

**Description**: 
The `BigIntegerSerializer` converts `BigInteger` objects to and from their string representations using the `kotlinx.serialization` library.

**Example Usage**:
```kotlin
import kotlinx.serialization.Serializable
import kotlinx.serialization.json.Json
import one.wabbit.serializers.BigIntegerSerializer
import java.math.BigInteger

@Serializable
data class ExampleData(
    @Serializable(with = BigIntegerSerializer::class) val bigNumber: BigInteger
)

fun main() {
    val data = ExampleData(BigInteger("12345678901234567890"))
    
    // Serializing
    val jsonString = Json.encodeToString(ExampleData.serializer(), data)
    println("Serialized JSON: $jsonString")
    
    // Deserializing
    val deserializedData = Json.decodeFromString(ExampleData.serializer(), jsonString)
    println("Deserialized Data: ${deserializedData.bigNumber}")
}
```

### LocalDateTimeSerializer

**Description**:
The `LocalDateTimeSerializer` handles `LocalDateTime` objects, converting them to and from strings.

**Example Usage**:
```kotlin
import kotlinx.serialization.Serializable
import java.time.LocalDateTime
import kotlinx.serialization.json.Json
import one.wabbit.serializers.LocalDateTimeSerializer

@Serializable
data class Event(
    val name: String,
    @Serializable(with = LocalDateTimeSerializer::class)
    val dateTime: LocalDateTime
)

fun main() {
    val event = Event("Meeting", LocalDateTime.of(2023, 10, 1, 12, 30))
    val json = Json.encodeToString(Event.serializer(), event)
    println("Serialized JSON: $json")
    val deserializedEvent = Json.decodeFromString(Event.serializer(), json)
    println("Deserialized Data: ${deserializedEvent.dateTime}")
}
```

### UUIDSerializer

**Description**:
The `UUIDSerializer` converts `UUID` objects to and from their string representations.

**Example Usage**:
```kotlin
import kotlinx.serialization.Serializable
import kotlinx.serialization.json.Json
import one.wabbit.serializers.UUIDSerializer
import java.util.UUID

@Serializable
data class MyDataClass(
    @Serializable(with = UUIDSerializer::class) val id: UUID
)

fun main() {
    val myData = MyDataClass(UUID.randomUUID())
    
    // Serialize
    val jsonString = Json.encodeToString(MyDataClass.serializer(), myData)
    println("Serialized: $jsonString")
    
    // Deserialize
    val deserializedData = Json.decodeFromString(MyDataClass.serializer(), jsonString)
    println("Deserialized: ${deserializedData.id}")
}
```

## Licensing

This project is licensed under the GNU Affero General Public License v3.0 (AGPL-3.0) for open source use.

For commercial use, please contact Wabbit Consulting Corporation (at wabbit@wabbit.one) for licensing terms.

## Contributing

Before we can accept your contributions, we kindly ask you to agree to our Contributor License Agreement (CLA).
