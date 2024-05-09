# Phone Dashboard

Phone Dashboard is a mobile application and suopporting cloud-based data server that allows researchers to track active application usage on Android devices and to implement behavioral interventions to try and change user behavior.

It was originally developed to support the research aims of Hunt Allcott, Matthew Gentzkow, and Lena Song, resulting [the National Bureau of Economic Research working paper on Digital Addiction](https://www.nber.org/papers/w28936). As such, its design and implementation reflects thats study's approach and design.

## Phone Dashboard Mobile App

The source code for the mobile app is located in the [Phone-Dashboard-Android](https://github.com/lenasong/Phone-Dashboard-Android) repository and this consists of the full Android project needed to build the app. Refer to that repository's README for build instructions.

## Phone Dashboard Data Collection Server

The Android mobile app relies on a cloud-based data collection server for retrieving its configuration periodically (such as whether to apply an intevention or not, and where to transmit gathered data). The server code and installation instructions are available in the [Phone-Dashboard-Django](https://github.com/lenasong/Phone-Dashboard-Django) repository.

## Overall Data Flow

Users entering a Phone Dashboard study are typically instructed to install the app from the Google Play app store.

When the app is installed and the user runs it for the first time, they are prompted for their e-mail address, which is transmitted to the cloud server. The cloud server checks that e-mail address against a list of prior enrollments and returns the study identifier if the user had previously enrolled with that address or generates a new unique study identifier if this is the user's first time using the app. On the server, e-mail addresses are not stored in their raw forms, but are instead stored (and compared against) as cryptographic hashes, in order prevent any unnecessary personally-identifiable information from being retained.

When the server responds to the app's enrollemnt request, in addition to returning the study identifier - which is the only identifier used to tag data originating from the device - it also returns a configuration document that the app interprets to set itself up as needed for the study design. When a network is available, the device periodically queries the server typically every five minutes or so for configuration updates, so that the app can change its behavior to accomodate scheduled changes in the study design.
