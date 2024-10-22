# JnaFileChooser

This is a small API that uses the native file chooser and folder browser 
dialogs on Windows and Mac OS if possible. It falls back to the Swing JFileChooser 
class if necessary.

## Example Usage

```java
public static void main(String[] args) {
    JnaFileChooser fc = new JnaFileChooser();
    fc.addFilter("All Files", "*");
    fc.addFilter("Pictures", "jpg", "jpeg", "png", "gif", "bmp");
    if (fc.showDialog(parent)) {
        File f = fc.getSelectedFile();
        // do something with f
    }
}
```

## Installing as dependency

You can install this library as e.g. Maven, Gradle, etc. dependency using [jitpack.io](https://jitpack.io/).

### Maven

Add the jitpack repository to your pom:

```pom
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```

Then you can add the dependency using any release tag, e.g.:

```pom
 <dependency>
    <groupId>com.github.steos</groupId>
    <artifactId>jnafilechooser</artifactId>
    <version>1.1.2</version>
</dependency>
```
## How does it work?

JnaFileChooser uses the awesome [JNA][1] library which enables access to native
code with plain Java code, no JNI necessary.


## Maven Project Setup

JnaFileChooser consists of three modules: win32, api and demo. 

The win32 module contains the low-level code which maps to the win32 API. You 
could use this code directly if you wish. It is a pretty straight-forward
mapping of the relevant parts of the win32 API.

The api module contains the code you usually want to use. It defines three
classes: JnaFileChooser, WindowsFileChooser and WindowsFolderBrowser.
JnaFileChooser is a facade that uses the other two classes if possible or falls
back to the JFileChooser. WindowsFileChooser and WindowsFolderBrowser are
abstractions on top of the low-level code in the win32 module and represent
the corresponding Windows common dialogs.

The demo module contains sample code.


[1]: https://github.com/twall/jna