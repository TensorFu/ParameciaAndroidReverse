# Bundle

### Description

`Bundle` is an important class in Android used for storing and passing key-value pair data, primarily utilized for transferring data between different components (such as `Activity`, `Fragment`, `Service`).

The essence of `Bundle` is a collection of key-value pairs (similar to a `Map`), and it supports serialization. It serves as an efficient tool for inter-process communication within the Android system.

### **Common Uses of Bundle**

1. **Data Transfer Between Components**:
    - Used in `Intent` to carry data for transfer.
2. **Saving State Data**:
    - Used in `onSaveInstanceState` and `onRestoreInstanceState` to save and restore the UI state.

**Features of Bundle**

1. **Supports Multiple Data Types**:
    - `Bundle` supports storing basic data types (e.g., `int`, `String`) and objects that implement the `Parcelable` or `Serializable` interface.
2. **Inter-Process Communication (IPC)**:
    - Can be used in IPC, along with mechanisms such as `Intent` or `Messenger`.

### **Supported Data Types**

`Bundle` supports storing the following types of data:

- **Primitive Types**: `int`, `float`, `double`, `long`, `char`, `short`, `boolean`

```java
bundle.putInt("intKey", 100);
bundle.putBoolean("boolKey", true);
```

- String: `String`, `CharSequence`
    
    ```java
    bundle.putString("stringKey", "Hello");
    ```
    
- Arrays: `int[]`, `String[]`, etc.
    
    ```java
    bundle.putIntArray("intArray", new int[]{1, 2, 3});
    ```
    
- Objects that implement `Parcelable`
    
    ```java
    bundle.putParcelable("parcelableKey", myParcelableObject);
    ```
    
- **Object that implement `Serializable`**
    
    ```java
    bundle.putSerializable("serializableKey", mySerializableObject);
    ```
    
- Binder
    
    ```java
    bundle.putBinder("binderkey", iBinder);
    ```
    

### **Common Methods**

Below are the common methods of the `Bundle` class and their uses:

**1. Data Storage**

- `putString(String key, String value)`: Stores a string.
- `putInt(String key, int value)`: Stores an integer.
- `putParcelable(String key, Parcelable value)`: Stores an object that implements the `Parcelable` interface.
- `putSerializable(String key, Serializable value)`: Stores an object that implements the `Serializable` interface.

**2. Data Retrieval**

- `getString(String key)`: Retrieves a string.
- `getInt(String key)`: Retrieves an integer.
- `getParcelable(String key)`: Retrieves a `Parcelable` object.
- `getSerializable(String key)`: Retrieves a `Serializable` object.

**3. Other Operations**

- `clear()`: Clears all data.
- `containsKey(String key)`: Checks whether a specific key exists.
- `isEmpty()`: Checks whether the bundle is empty.

### Example

```java
// Sending Activity
Intent intent = new Intent(this, SecondActivity.class);
Bundle bundle = new Bundle();
bundle.putString("username", "Tensor");
bundle.putInt("age", 25);
intent.putExtras(bundle);
startActivity(intent);

// Receiving Activity
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_second);

    Bundle bundle = getIntent().getExtras();
    if (bundle != null) {
        String username = bundle.getString("username");
        int age = bundle.getInt("age");
        Log.d("SecondActivity", "Username: " + username + ", Age: " + age);
    }
}
```