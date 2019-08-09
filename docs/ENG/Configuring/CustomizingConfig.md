### Setup the config.plist file

Here is described how I have changed net config that goes along with Clover revision 5033.

You can download the disk image with this config from the official page of the loader Clover: https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/ For unpacking .lzma and .tar files in Windows use [7zip](https://www.7-zip.org/) or [Bandizip]([https://bandisoft.com/bandizip](https://www.bandisoft.com/bandizip))

Here's what I changed in my [config.plist](/EFI/CLOVER/config.plist):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>ACPI</key>
	<dict>
		<key>DSDT</key>
		<dict>
			<key>Fixes</key>
			<dict>
				<key>#AddHDMI</key>
				<true/>
				<key>#AddIMEI</key>
				<false/>
				<key>#FixDisplay</key>
				<true/>
				<key>#FixIntelGfx</key>
				<false/>
			</dict>
		</dict>
		<key>SSDT</key>
		<dict>
			<key>Generate</key>
			<dict>
				<key>CStates</key>
				<true/>
				<key>PStates</key>
				<true/>
			</dict>
		</dict>
	</dict>
	<key>Devices</key>
	<dict>
		<key>Audio</key>
		<dict>
			<key>Inject</key>
			<integer>13</integer>
		</dict>
		<key>Properties</key>
		<dict>
			<key>PciRoot(0x0)/Pci(0x2,0x0)</key>
			<dict>
				<key>AAPL,ig-platform-id</key>
				<data>
				BwCbPg==
				</data>
				<key>enable-hdmi20</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con0-busid</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con0-enable</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con0-type</key>
				<data>
				AAgAAA==
				</data>
				<key>framebuffer-con2-enable</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con2-index</key>
				<data>
				/////w==
				</data>
				<key>framebuffer-fbmem</key>
				<data>
				AACQAA==
				</data>
				<key>framebuffer-patch-enable</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-stolenmem</key>
				<data>
				AAAwAQ==
				</data>
				<key>framebuffer-unifiedmem</key>
				<data>
				AAAAgA==
				</data>
			</dict>
		</dict>
	</dict>
	<key>Graphics</key>
	<dict>
		<key>Inject</key>
		<dict>
			<key>ATI</key>
			<false/>
			<key>Intel</key>
			<false/>
			<key>NVidia</key>
			<false/>
		</dict>
		<key>ig-platform-id</key>
		<string></string>
	</dict>
	<key>RtVariables</key>
	<dict>
		<key>MLB</key>
		<string>C07WM5ZSJYVX94ADA</string>
		<key>ROM</key>
		<data>
		jOxLlUG7
		</data>
	</dict>
	<key>SMBIOS</key>
	<dict>
		<key>BiosReleaseDate</key>
		<string>09/17/2018</string>
		<key>BiosVendor</key>
		<string>Apple Inc.</string>
		<key>BiosVersion</key>
		<string>MM81.88Z.F000.B00.1809171422</string>
		<key>Board-ID</key>
		<string>Mac-7BA5B2DFE22DDD8C</string>
		<key>BoardManufacturer</key>
		<string>Apple Inc.</string>
		<key>BoardSerialNumber</key>
		<string>C07WM5ZSJYVX94ADA</string>
		<key>BoardType</key>
		<integer>10</integer>
		<key>BoardVersion</key>
		<string>1.0</string>
		<key>ChassisAssetTag</key>
		<string>Mini-Aluminum</string>
		<key>ChassisManufacturer</key>
		<string>Apple Inc.</string>
		<key>ChassisType</key>
		<string>0x09</string>
		<key>EfiVersion</key>
		<string>220.207.27.0.0</string>
		<key>Family</key>
		<string>Mac mini</string>
		<key>FirmwareFeatures</key>
		<string>0xFC0FE137</string>
		<key>FirmwareFeaturesMask</key>
		<string>0xFF1FFF3F</string>
		<key>LocationInChassis</key>
		<string>Part Component</string>
		<key>Manufacturer</key>
		<string>Apple Inc.</string>
		<key>Mobile</key>
		<false/>
		<key>PlatformFeature</key>
		<string>0x02</string>
		<key>ProductName</key>
		<string>Macmini8,1</string>
		<key>SerialNumber</key>
		<string>C07WM5ZSJYVX</string>
		<key>SmUUID</key>
		<string>35E5C172-AE15-400F-B3DD-6432BBD44366</string>
		<key>Version</key>
		<string>1.0</string>
	</dict>
</dict>
</plist>

```

This is not a working config.plist. I brought only those items that have been modified compared to the native configuration file of the ISO image Clover revision 5033.

Such SMBIOS will be suitable for loading, but then it is better to generate its points completely, for example with the help of Clover Configurator.

Also, you should read the book "[Clover Hacky](https://sourceforge.net/projects/cloverefiboot/files/Documents/)" to understand which items in config.plist responsible for what.