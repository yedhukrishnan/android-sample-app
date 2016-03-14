android-sample-app
==================

[![Circle CI](https://circleci.com/gh/hasgeek/kulfi.svg?style=svg)](https://circleci.com/gh/hasgeek/kulfi)

This sample android app demonstrates how to setup [Robolectric](http://robolectric.org/) to write/run tests and how to create a continuous integration/deployment setup either in Wercker/CircleCI

1. [x] Creating an Android Project in Android Studio
2. [x] Integrating Robolectric
3. [x] Writing Your First Test
4. [x] Running Robolectric Tests
5. [x] Continuous Delivery using CircleCI
6. [x] Setting Environment-dependent Configurations
7. [ ] Generating Signed APK in CircleCI

#### Creating an Android Project in Android Studio

Create a blank activity project in Android Studio with MainActivity. Android Studio uses a gradle-based build setup which also makes it easy to run Robolectric tests .

#### Integrating Robolectric

Add `junit` and `robolectric` as dependencies in [app/build.gradle](https://github.com/multunus/android-sample-app/blob/master/app/build.gradle)

``` gradle
dependencies {
    ...
    compile 'junit:junit:4.12'
    compile "org.robolectric:robolectric:3.0"
}
```

See the wiki page for a detailed version: [Integrating Robolectric to Android App](https://github.com/multunus/android-sample-app/wiki/Integrating-Robolectric-to-Android-App)

#### Writing Your First Test

Test files reside in `app/src/test/` directory. For now, create a test file for MainActivity, [MainActivityTest](https://github.com/multunus/android-sample-app/blob/master/app/src/test/java/com/multunus/cdapp/MainActivityTest.java).

The file contains a sample test. To learn more about writing Robolectric tests, see: [Robolectric Samples](https://github.com/robolectric/robolectric-samples)

#### Running Robolectric Tests

You can run the tests via the terminal. Go to the root directory of the project and run:

``` bash
./gradlew clean test
```

To build APK locally, run:

``` bash
./gradlew clean build
```


#### Continuous Delivery using CircleCI

The [circle.yml](https://github.com/multunus/android-sample-app/blob/master/circle.yml) configuration takes care of running the tests and building the app once it it pushed to remote using CircleCI. If you are using a different version of SDK tools, you'll have to update it in dependencies section.

#### Setting Environment-dependent Configurations

You might want to use different variables or configurations based on the environment. The easiest way to achieve this is to create a [Configuration.java.example](https://github.com/multunus/android-sample-app/blob/master/app/src/main/java/com/multunus/cdapp/Configuration.java.example) file containing default configuration for release environment. While developing locally, copy this file:

``` bash
cp Configuration.java.example Configuration.java
```

and change it to configuration required for local development. `Configuration.java` should be added to `.gitignore` to avoid accidentally committing the file. `circle.yml` file contains the command to copy the example file and generate `Configuration.java` before creating the release APK.

Check out our [OneMDM Client](https://github.com/multunus/onemdm-client) for a configuration file ([Config.java.example](https://github.com/multunus/onemdm-client/blob/master/app/src/main/java/com/multunus/onemdm/config/Config.java.example)) with more examples.
