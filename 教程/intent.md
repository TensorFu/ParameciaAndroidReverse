# Intent 以及 PendingIntent

- [Intent 以及 PendingIntent](#intent-以及-pendingintent)
  - [Intent](#intent)
    - [什么是 intent ？](#什么是-intent-)
    - [intent 的种类](#intent-的种类)
      - [Explicit Intents（显式Intent）](#explicit-intents显式intent)
      - [Implicit Intents（隐式Intent）](#implicit-intents隐式intent)
    - [Intent 主要组件](#intent-主要组件)
    - [通过显式的方式设置Intent（意图）并且打开一个组件](#通过显式的方式设置intent意图并且打开一个组件)
      - [setClass](#setclass)
      - [setClassName](#setclassname)
      - [setClassName](#setclassname-1)
      - [setComponent](#setcomponent)
      - [注意](#注意)
    - [通过 Intent 启动其他的组件](#通过-intent-启动其他的组件)
  - [PendingIntent](#pendingintent)


## Intent

### 什么是 intent ？

你在家里，突然想要一杯咖啡。这个“想要一杯咖啡”的意图，可以看作是你心中的一个 "Intent"。

比方说，你想要打开一个 activity 但是，你不能和电脑直接沟通，你需要一个中间件，你把你要做的事情，包装在 intent 当中，然后发送出去，就可以实现你的目的了	

Intent Extras（额外信息）:

- 假设你想要一杯加糖、加牛奶的咖啡。这时，“加糖”和“加牛奶”是你的额外需求或信息。
- 在 Android 的 Intent 中，你可以通过 "Extras" 传递额外的信息或数据。

Intent Filter（）:

- 假设家里的每个人都有特定的能力或喜好。例如，爸爸可能擅长做浓缩咖啡，妈妈可能擅长做拿铁，而你的兄弟姐妹可能只会泡速溶咖啡。每个人的这种“特长”或“喜好”就像是他们的“Intent Filter”，指明了他们能够做什么。
- 在 Android 中，组件（如 Activity）使用 Intent Filter 来说明它们可以处理哪些 Intent。

​			

​				

### intent 的种类

#### Explicit Intents（显式Intent）

指定了要启动的组件的名称（例如特定的 Activity 或 Service）。它们通常用于应用内部组件之间的通信。

【就像你直接打电话给一个特定的朋友。你知道你要打给谁。】			

​			

#### Implicit Intents（隐式Intent）

没有指定特定组件，但指定了一种行为。Android 系统会找到能执行该行为的应用并启动它。例如，你可以使用隐式 Intent 请求显示一个网页，系统会打开用户的默认浏览器。考虑是否真的需要设置你的 Intent 为隐式，因为其他的应用可能会接收并处理这些 Intent。可以使用权限来限制哪些应用可以响应你的 Intent							

【就像你发出一个广播说：“谁能帮我订外卖？”然后等着看谁会回应】

​				

### Intent 主要组件

- **Action**：表示要执行的动作，如 `ACTION_VIEW`、`ACTION_EDIT` 等。
- **Data**：与 action 相关的数据 URI。例如，要查看某个联系人，你的 data 可能是该联系人的 URI。
- **Category**：为 Intent 提供额外的信息，使其能够执行特定的操作。例如，`CATEGORY_HOME` 表示应用的主屏幕。
- **Extras**：键值对，用于传递额外的数据。例如，通过 `putExtra()` 传递一些参数给新的 Activity。
- **Component Name**：明确指定应被启动的组件的名称。

​				

### 通过显式的方式设置Intent（意图）并且打开一个activity（startActivity）

#### setClass

```java
Intent intent = new Intent();
intent.setClass(context, TargetActivity.class);
context.startActivity(intent);
```

​			

#### setClassName

```java
Intent intent = new Intent();
intent.setClassName(context, "com.example.app.TargetActivity");
context.startActivity(intent);
```

​				

#### setClassName

```java
Intent intent = new Intent();
intent.setClassName("com.example.app", "com.example.app.TargetActivity");
context.startActivity(intent);
```

​			

#### setComponent

【component : 组件】

```java
ComponentName componentName = new ComponentName("com.example.app", "com.example.app.TargetActivity");
Intent intent = new Intent();
intent.setComponent(componentName);
context.startActivity(intent);
```

​				

#### 注意

最后的两种都会指定包名，这是因为，他可以用来打开其他应用的 activity 	

​				

### 通过 Intent 启动其他的组件（服务，广播）

#### 打开一个服务 startService 

```java
Intent serviceIntent = new Intent(context, MyService.class);
context.startService(serviceIntent);
```



#### 打开一个广播[其实应该叫做发送一个广播]

```java
Intent broadcastIntent = new Intent("MY_CUSTOM_ACTION");
// 可选：添加额外的数据
broadcastIntent.putExtra("key", "value");
context.sendBroadcast(broadcastIntent);
```

​			



----

## PendingIntent

