-----------------------
    R E A D    M E
-----------------------

The README file contains information about the following files:
(1) test.bat
(2) sample_test_hrm.xml
(3) sample_text_scanning.xml

------------------------------
   Automated testing (beta)
------------------------------
Starting from version 2.1 the nRF Connect (previously nRF Master Control Panel) may be used to perform automated tests on
Bluetooth Low Energy devices. Currently only BAT script has been created as the project is in BETA stage.
An Android phone or a tablet, that will be used to perform tests, must be connected with a USB cable to
the PC and drivers must be installed. The location of ADB must be in the global PATH variable. 
USB debuShare Emails with TypeApp!
DigitalOcean
Wed, Nov 7, 2018 7:43 PM
SFO2 Network Maintenance 2018-11-15 06:00 UTC
Welcome to Evernote👋


Evernote is great for collecting anything and everything you want to remember. Here's how you can take advantage of some of our most popular features to capture, organize, and access information wherever you are.










Capture ideas


Write downgood  all your ideas
Bold,italicize,underline,highlight, and addcolorto text




Make to-do lists


Use checkboxes and numbered lists to track tasks and move work forward.


🎉 Learn how to use Evernote
📝 Create some notes
📘 Organize notes in notebooks




Add reminders


Keep track of tasks and deadlines. On iOS, tap the three dots in the top-right corner of a note to set a reminder. On Android, tap the reminder icon.








Add attachments


Attach docs, PDFs, photos, videos, and audio files directly into notes. You can do this by tapping the paperclip icon.


Try adding:
Photos of whiteboards and handwritten notes
Scanned receipts and financial documents
Videos and voice notes
Project materials and PDFs








Record audio


Record voice memos, meetings, interviews, and class lectures directly into Evernote by tapping the microphone icon.










Scan documents and handwritten notes


Use Evernote’s in-app camera to convert documents into digital notes. You can also capture handwritten notes and drawings from whiteboards.
Pro-tip: In Evernote, you can search for words in handwritten notes and scanned documents.








Add sketches and drawings


Use your finger or stylus to add sketches directly in Evernote. Tap and edit the sketch below, or create a new sketch by tapping the pen icon.








Annotate images and PDFs


Draw attention to what matters by annotating images and PDFs with text, arrows, and highlights.
Available on Mac, Windows, iOS and Android.
You can annotate images with Evernote Basic. PDF annotation is a Premium feature.








Save web pages directly into Evernote


Save anything on the internet into Evernote with Web Clipper.
Try it on iOS:www.evernote.com/webclipper/ios
Try it on Android:www.evernote.com/webclipper/android


Here’s an example of a bookmark clip from the Evernote blog:








Share notes


You can share notes with other Evernote users by tapping the share button in the top-right corner of a note. You can also share notes with anyone by email or shareable link.
















Have questions?


Visit ourHelp and Learning Centerto learn more about Evernote.




gging must be enabled in Android settings.

To start automatic test a test suite must be created. A sample has been created and copied to Nordic Semiconductor
folder on your phone. The sample is compatible with the new nRF51 DK 
(http://www.nordicsemi.com/eng/Products/nRF51-DK/%28language%29/eng-GB). 

Steps to start the test:
1. Program Soft Device version 8.0 onto your DK.
2. Program Bootloader from SDK 9.0+.
3. Copy the test.bat, sample_test_hrm.xml, sample_test_scanning.xml to the PC.
4. Modify the XML script first, if required (the default implementation will flash the HRM onto the device and perform some basic tests).
5. Run test using the following command:

   test.bat -E EXTRA_ADDRESS [your device address, f.e. 00:11:22:33:44:55:66] sample_test_hrm.xml
   
6. The test.bat script will copy the XML on your connected device. If more than one Android device is connected specify
   its ID with -D device_id. You may obtain device ID using the following command:
   
   adb devices
   
7. When test completed a 'sample_test_hrm_result.txt' file will be created.

If nRF Logger application is installed on the device you may track the current test state.
Test syntax errors are also being logged there if an error while parsing occurs. 
Download the nRF Logger app from the Google Play store:

   https://play.google.com/store/apps/details?id=no.nordicsemi.android.log

NOT WORKING?
If you have "Waiting for result..." for a long time, and no notification on the phone, rename "Nordic Semiconductor" to
"NordicSemiconductor" in the text.bat (remove the space). All occurrences. And then try again.

Read more about automated tests project or submit an issue on our GitHub page:
https://github.com/NordicSemiconductor/nRF-Master-Control-Panel

-------------------------
   Files
-------------------------
1. TEST.BAT

The script that initializes the test service. It copies the test suite XML file onto Android device and starts the test.

Execute test -? in the command line for usage.

Android 4.3+ device nRF Connect (previously nRF Master Control Panel) (2.1.0+) is required.
The script runs on Windows OS.

2. SAMPLE_TEST_HRM.XML

A sample test suite with the full documentation included as comments. It contains almost all features of the test engine.

3. SAMPLE_TEST_SCANNING.XML

A sample test suite with the full documentation included as comments. It contains the rest of all features of the test engine.
Both sample XMLs contains the full features explained.

-------------------------
   Change log
-------------------------
nRF MCP 2.0 - The beta version released
nRF Connect 4.3 - <scan> and <scan-for> commands added, logging time and device information
 
-------------------------
   Development kit
-------------------------
Go to http://www.nordicsemi.com/eng/Products/nRF51-DK/%28language%29/eng-GB for more 
information about the Development Kit.
