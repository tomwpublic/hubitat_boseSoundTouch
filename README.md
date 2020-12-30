# hubitat_boseSoundTouch

This provides AudioNotification, AudioVolume, MusicPlayer, and SpeechSynthesis driver capabilities as well as various functionality using PushableButton.

Most operations are local only, especially playback controls like play/pause/stop and volume controls.  However, most of the functions that initiate or change playback (including TTS) do have a cloud interaction.

# Installation instructions:

* In the *Drivers Code* section of Hubitat, add the boseSoundTouchDevice driver.
* In the *Apps Code* section of Hubitat, add the boseSoundTouchDiscovery app.
* For automated discovery, go to the *Apps* section of Hubitat and use *Add User App* to install and configure the Bose SoundTouch Discovery app.  This will create *Device* entries for each speaker.  Note that this discovery method has been unreliable on some systems, so reboot your Bose speakers if they are not discovered.  If it fails completely, use the manual configuration option.
* For manual configuration, visit the *Devices* section of Hubitat and *Add Virtual Device(s)* of type Bose SoundTouch Device.  Enter your speaker's IP address and click *Save Preferences.*
* For TTS operations, acquire a Consumer Key by registering an app on this site:  https://developer.bose.com/user/me/apps
    * Note that Bose currently only supports notifications (used for TTS) on these models:  SoundTouch 10, SoundTouch 20 Series III, and SoundTouch 30 Series III

# Usage instructions:

* **Background information**

The *Device* entry for a speaker allows it to be controlled independently and also allows it to act as a master for its zone.  The Bose SoundTouch Device driver caches information about known slaves.

In order for the user-friendly features described below to work, a given slave has to be added at least once after the *Device* creation in Hubitat.  You can accomplish this by creating a group in the SoundTouch app or by using the *addZoneSlave* or *createZone* (either is fine) commands in the driver.
<br><br>


* ***Push* operations**

The Push command is versatile:
* Pushing button numbers 1 through 6 will perform the same function as pushing the physical buttons on the SoundTouch device, for example restoring saved presets.
* Pushing button numbers 10 through 20 will restore zones captured using the driver (note: range of zone numbers is configurable in the configure() function within the driver code)
* Pushing button numbers 30 through 40 will restore content items captured using the driver (note: range of item numbers is configurable in the configure() function within the driver code).
* Pushing a button with a string 'number' (e.g. Kitchen) will attempt to add or remove from the zone a slave of that name.
<br><br>

* **captureZone command**

Use this command to capture the current zone configuration and store it into a numbered zone in the range of 10 to 20.  Use *Push* with the number to restore the zone configuration at any time.

You can read the *zoneMap* entry in *State Variables* on the Device page to read the saved zone information.  You can replace an existing saved zone by executing captureZone again with the same number.
<br><br>

* **captureContentItem command**

Use this command to capture the current content item and store it into a numbered zone in the range of 30 to 40.  Check for *isPresetable* flag to be *true* in *trackData* to determine whether this will work for a given content item.  Use *Push* with the number to restore the content item at any time.

You can read the *itemMap* entry in *State Variables* on the Device page to read the saved content item information.  You can replace an existing saved item by executing captureContentItem again with the same number.
<br><br>

* **trackArt attribute**

This attribute contains an HTML-formatted image display of the album art for the track or playlist, if available.  You can use an Attribute tile on your Dashboard to display the image. 


# Disclaimer

I have no affiliation with any of the companies mentioned in this readme or in the code.


