### Настройка файла config.plist

Здесь описано то, как я изменил чистый конфиг, который идет вместе с Clover ревизии 5033.

Вы можете скачать образ диска с данным конфигом с официальной страницы загрузчика Clover: https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/ Для распаковки .lzma и .tar файлов в Windows лучше используйте [7zip](https://www.7-zip.org/) или [Bandizip]([https://bandisoft.com/bandizip](https://www.bandisoft.com/bandizip))

Вот, что я изменил в своем файле [config.plist](/EFI/CLOVER/config.plist):

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

Это не рабочий config.plist. Выше я привел только те пункты, которые были изменены по сравнению с родным конфигом из ISO образа Clover ревизии 5033.

Такой SMBIOS подойдет для загрузки, но потом лучше сгенерировать его пункты полностью, например с помощью Clover Configurator.

Так же вам не помешает прочитать книгу "[Clover цвета хаки](https://sourceforge.net/projects/cloverefiboot/files/Documents/)", чтобы понимать какие пункты в config.plist за что отвечают.
