# ZkSpy
ZkSpy is an application for Windows or Linux which allows spying on the communication between a client application and a timeclock with ZKTeco firmware. At present it only supports communication over TCP. If your client application uses UDP it is still useful as an investigative tool because the TCP datagrams differ from their UDP counterparts by a leading 4 byte marker (0x50, 0x50, 0x82, 0x7D) and a 4 byte little endian field which contains the length of the message to follow (that is to say not including the marker or length field itself).

Note that as best as I can tell, the datagrams used to communicate with a clock over a serial interface (RS-232/485) are different from the datagrams used in both the TCP and UDP cases. If anyone knows what purpose is served by the "extra" bytes in the serial case then I'd sincerely appeciate the information.

It spys on the communication between the clock and the application by inserting itself as a "man in the middle". In other words, ZkSpy is configured with the IP address and port of the clock on which to spy and the application is configured to direct its traffic to ZkSpy. ZkSpy logs the bytes received from either application or clock and forwards them to the counterparty. This is more intrusive than using a tool like Wireshark, say, but much less painful to pull off. :-)

ZkSpy can also be used to spy on the communication with hand punch clocks made by Schlage.

ZkSpy is distributed as a single file executable with no dependencies. It was tested on a 64 bit version of Windows 7 and on Linux Mint 19.3 Tricia. 

ZkSpy is run at the command line using the following switches:

  **-a, --address**    Clock IP address; default is 192.168.1.201

  **-t, --type**       Clock type; (Z[KTeco] or S[chlage]); default is ZKTeco

  **-p, --port**       Clock port; usually 4370 for ZKTeco, always 3001 for Schlage

  **-n, --name**       Clock name; default is 'clock'

  **-i, --ip**         Host IP address; default is '127.0.0.1'

  **-l, --log**        Log file for hard copy; default is a console log

  **-@, --config**     Settings file; default is 'ZkSpy.config' with NO command line

  **--help**           Display help

  **--version**        Display version information.
   
  A configuration file may be used to decrease the amount of typing required to launch the application repeatedly. 
  
  This is a sample configuration for a ZkTeco clock:
  
  ```xml
  <?xml version="1.0" encoding="utf-8" ?>
  <configuration>

    <appSettings>

        <add key="Clock.IPAddress" value="192.168.1.202" />
        <add key="Clock.Port" value="4370" />
        <add key="Clock.Name" value="TFT-900" />

        <add key="Host.IPAddress" value="127.0.0.1" />

        <add key="LogFile" value="" />

    </appSettings>
 </configuration>
 ```
 This is a sample configuration for a Schlage clock
 ```xml

 <?xml version="1.0" encoding="utf-8" ?>
 <configuration>

    <appSettings>

        <add key="Clock.IPAddress" value="192.168.1.205" />
        <add key="Clock.Port" value="3001" />

        <add key="Host.IPAddress" value="127.0.0.1" /> 

        <add key="LogFile" value="" />

    </appSettings>
 </configuration>

 ZkSpy by William DePalo is licensed under CC BY-NC-ND 4.0. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-nd/4.0/
  The legal text is at the link. See the LICENSE file for comments.
 ```
  
  

