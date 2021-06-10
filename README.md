# UsbMapGuide
## The USB Mapping guide for Hackintoshes

### Requirements:
-	A working macOS installation
-	UsbInjectAll.kext in the kexts folder
- [USBMap](https://github.com/corpnewt/USBMap) by CorpNewt

### What we are going to do in this guide
 - Discover ports
 - Edit and create USBMap.kext
 - Copy the kext over to your kexts folder

#### Part 1 - Discovering Ports
This image is something like what you would see when you open USBMap for the first time.

![Screenshot 2021-06-10 at 8 57 10 PM](https://user-images.githubusercontent.com/82939599/121552900-737fe500-ca2e-11eb-86f4-a78b911a6984.png)

I know it looks complicated, but trust me, it's not.

Unplug every USB device you do not need first.
Plug in only the very minimal usb devices you need. I’d recommend starting with none if you have a laptop. But if you have a PC, you might need the keyboard.

Type `D` to go to the Discovering Ports section of the script.

This picture is what you would see, except you'll have a different list of ports, and possibly a larger list.

![Screenshot 2021-06-10 at 8 58 11 PM](https://user-images.githubusercontent.com/82939599/121553070-9611fe00-ca2e-11eb-8883-016a3d08f7d7.png)

The devices shown in blue are what are currently connected to my usb ports.
I have a Bluetooth card and a webcam, so I see two devices already.

Wait for 5 seconds, and then plug in one device.
in a few seconds, it should show up in green, and it should ask you to rename the port.

![Screenshot 2021-06-10 at 8 23 25 PM](https://user-images.githubusercontent.com/82939599/121547495-d02cd100-ca29-11eb-85a3-ab5c2247fd24.png)

Name the port with a clear name, as you are going to be assigning port types to them after the script recognizes all your USB ports, and you'll need to know what port it is.

Now, wait for 5 seconds, then plug in another device. (you can unplug the first device if you want). 

Do this process again and again until all your ports have been discovered.

#### Note: You will need to plug in a USB2 device AND a USB3 device for each USB 3 port. This is because USB3 ports have 2 personalities, a USB2 personality, and a USB3 personality.

Now that you have succesfully discovered all your ports, your screen should look something like this

![Screenshot 2021-06-10 at 8 58 02 PM](https://user-images.githubusercontent.com/82939599/121553165-acb85500-ca2e-11eb-8c6a-b47f1669219e.png)

These are all the ports on my laptop, with proper nicknames

Now you can press Q to exit, and you should see the title screen again, but now the option Edit and create USBMap.kext is not in red. Which means that we can get to the fun part.

![Screenshot 2021-06-10 at 8 59 24 PM](https://user-images.githubusercontent.com/82939599/121553331-ceb1d780-ca2e-11eb-8c3a-c675bfcc2460.png)

#### Part 2: Editing and creating USBMap.kext

Let’s take a look at this table before we move on, because this will be useful when assigning port types.

![Screenshot 2021-06-10 at 9 00 28 PM](https://user-images.githubusercontent.com/82939599/121553507-f3a64a80-ca2e-11eb-87f2-43a0e6bce6aa.png)

[Source](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html)

This table is pretty easy to understand, Pay close attention to the value under the “Type”  column.

Now we will be selecting `P. Edit & Create USBMap.kext` inside the USBMap script.

![Screenshot 2021-06-10 at 8 31 04 PM](https://user-images.githubusercontent.com/82939599/121548627-cc4d7e80-ca2a-11eb-9266-c7ed43d05f6a.png)

This might look intimidating, but trust me, it’s not.
All we need to do in this part is assign port types to each of our ports. 

If you look closely at the "Type" part in our ports' list, we can see it has assigned port type 3 to all my ports. This might vary for you.

What we are going to do is:
-	Disable ports we do not need
-	Map the ports to their correct types

##### Disabling ports:
 
Let’s say I want to disable port `1`, ie. My top right port. All I need to enter is `1` in the place where it says “Please make your selection:”

If you want to disable port `N`, you type `N` and then press enter.

##### Mapping to correct type:

The syntax for mapping ports is `T:[port_number]:[port_type]`

`Port_number` is the number assigned to the port. For me, `port 1` is my top right port.

`Port_type` is the “Type” value taken from the table I included in the start of this section.

If I want to map `port 2` ie. My top left port, I would type in `T:2:0`	_(2 is my port number, 0 is the type value for usb2 ports)_

If you want to assign a type to a series of ports, you can separate them with commas.

If I want to map port 2, 3 and 4 as `type 3 `, I can do so with `T:2,3,4:3` 	(`2,3,4` does not have spaces in between the commas)

##### Note: Bluetooth devices need to be mapped as internal, ie. type 255 to work properly. Same goes for all internal devices, like integrated webcams, etc.

Now that your ports are mapped, let’s build USBMap.kext!

As you can see near the bottom of your window, you see two options for building USBMap.kext.

![image](https://user-images.githubusercontent.com/82939599/121549946-e8055480-ca2b-11eb-8704-d7f694d45337.png)

In the same text area you entered the  `T:[port_number]:[port_type]` command, enter `K` or `L` for building the USBMap.kext corresponding to your version of macOS.

For some users, you might get this warning.

![Screenshot 2021-06-10 at 8 40 03 PM](https://user-images.githubusercontent.com/82939599/121550203-2864d280-ca2c-11eb-96c5-6c8f975612b3.png)

I tend to select `i` for ignore, but it doesn't really matter.

After entering your selection, a new finder window opens, which points you to the USBMap.kext. That’s your trophy, copy it over to your desktop or someplace you can access.

#### Part 3: Copying the kext over to your kexts folder

Congratulations! You have completed the not-so-easy sections of this guide! All that remains is copying the kext over to the kexts folder.

If you are using OpenCore, you need to navigate to your EFI folder > OC > Kexts and paste the USBMap.kext there.

Now that you have a proper usb map, you can delete UsbInjectAll.kext.

### And you're basically done! Reboot to see the changes apply, and you're good to go!




