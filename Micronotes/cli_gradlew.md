---
title: cli_gradlew
permalink: Micronotes/cli_gradlew
category: Micronotes
parent: Micronotes
layout: default
has_children: false
share: true
shortRepo:

- micronotes
- default

---

<br/>

<details markdown="block">    
<summary>    
Table of contents    
</summary>    
{: .text-delta }    
1. TOC    
{:toc}    
</details>

<br/>

---

<br/>

# Debug

```bash
./gradlew runSingle --debug-jvm -PmainClass=Mai
```

## `build.gradle`

```gradle
test {
    debugOptions {
        enabled = true
        port = 4455
        server = true
        suspend = true
    }
}
```

> or

```gradle
run{
debugOptions {
        enabled = true
        port = 4455
        server = true
        suspend = true
    }
 }
```

## Remote Debugging in Gradle

```gradle
tasks.withType(JavaExec) {
    if (System.getProperty('DEBUG', 'false') == 'true') {
        jvmArgs '-Xdebug', '-Xrunjdwp:transport=debug_socket,server=y,suspend=y,address=9099'
    }
}
```

> To know what's happening with the arguments, read this about the arguments that you need to send to jvm to make remote debugging possible:
> [enable-remote-debugging](https://www.eclipse.org/jetty/documentation/9.3.x/enable-remote-debugging.html)

## Running instructions

### Step1:

```bash
gradle -DDEBUG=true run
```

> Now in the console you will see something like this:

```shell
Listening for transport debug_socket at address: 9099
```

### Step2:

> `Configuration` -> `Remote Java Application`

- set these fields:
    1. project
    2. host (here its localhost)
    3. port (in this example it will be 9099)