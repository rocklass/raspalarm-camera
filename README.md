raspalarm-camera
================
Raspberry Pi as IP camera

Build
-----
```gradle
./gradlew dockerBuildImage -Penv=dev
```

Run
---
```shell
docker run -it -p 8081:8081 --device=/dev/video0 rocklass/raspalarm-camera
```