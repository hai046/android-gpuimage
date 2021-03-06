###个人参照修改使用GUP直接转换 YUV 到 RGB   [Android OpenGL es GPUImage  by GPU convert YUV to RGB](https://www.zybuluo.com/hai046/note/150753)

根据原来修改后的fragment shader 脚本在  haizhu_fs目录下


另外 对应demo 暂时没有上传  后期补上

----

# GPUImage for Android
[![Build Status](https://api.travis-ci.org/CyberAgent/android-gpuimage.png?branch=master,develop)](https://travis-ci.org/CyberAgent/android-gpuimage)

Idea from: [iOS GPUImage framework](https://github.com/BradLarson/GPUImage)


Goal is to have something as similar to GPUImage as possible. Vertex and fragment shaders are exactly the same. That way it makes it easier to port filters from GPUImage iOS to Android.

## Requirements
* Android 2.2 or higher (OpenGL ES 2.0)

## Usage

### Gradle dependency

```groovy
repositories {
    mavenCentral()
}

dependencies {
    compile 'jp.co.cyberagent.android.gpuimage:gpuimage-library:1.2.3'
}
```

### Sample Code
With preview:

```java
@Override
public void onCreate(final Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity);

    Uri imageUri = ...;
    mGPUImage = new GPUImage(this);
    mGPUImage.setGLSurfaceView((GLSurfaceView) findViewById(R.id.surfaceView));
    mGPUImage.setImage(imageUri); // this loads image on the current thread, should be run in a thread
    mGPUImage.setFilter(new GPUImageSepiaFilter());

    // Later when image should be saved saved:
    mGPUImage.saveToPictures("GPUImage", "ImageWithFilter.jpg", null);
}
```

Without preview:

```java
Uri imageUri = ...;
mGPUImage = new GPUImage(context);
mGPUImage.setFilter(new GPUImageSobelEdgeDetection());
mGPUImage.setImage(imageUri);
mGPUImage.saveToPictures("GPUImage", "ImageWithFilter.jpg", null);
```

### Gradle
Make sure that you run the clean target when using maven.

```groovy
gradle clean assemble
```

## License
    Copyright 2012 CyberAgent, Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
