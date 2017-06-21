### maven项目test类怎么获取resources中的资源文件？
```java
package com.dimonho.test;

import java.io.IOException;
import java.io.InputStream;
import java.net.URL;

import org.apache.commons.io.IOUtils;
import org.junit.Test;

public class TestPath {
  @Test
  public void getResourcesFile() throws IOException {
    //获取ClassLoader对象，通过this.getClass().getClassLoader(); | TestPath.class.getClassLoader();
    ClassLoader classLoader = ClassLoader.getSystemClassLoader();
    URL url = classLoader.getResource("settings.json");
    String path = url.getPath();
    System.out.println(path);
    InputStream in = classLoader.getResourceAsStream("settings.json");
    String fileStr = IOUtils.toString(in); //or  IOUtils.toString(in,"UTF-8");
    System.out.println(fileStr);
  }
}

```
![java/images/image0001.bmp](https://github.com/DimonHo/DH_Note/blob/master/java/images/image0001.bmp)
