# pw-utils
Several small bash scripts to aid with pipewire scripting and debugging.

Place them in `/usr/local/bin/` and use from command line or scripts.

## pw-link-ls
Lists all active links in an easy to read format. Links are not duplicated as in the pw-link -l ouput.
Links are listed with source first and destination last. e.g.
```
alsa_input.usb-GeneralPlus_USB_Audio_Device-00.mono-fallback:capture_MONO -> myfilter:playback_FL
alsa_input.usb-GeneralPlus_USB_Audio_Device-00.mono-fallback:capture_MONO -> myfilter:playback_FR
```
## pw-link-del
Deletes all active links. Does what pw-link -d is supposed to do

## pw-link-save [filename]
Saves a list of all active links to a file which defaults to "saved_links.txt" unless a filename is passed to it.
This also copes with node names with spaces (which are a bad idea but do crop up).
Output files are formatted as below:
```
"myfilter:capture_FL" "FDV_Mic_to_FreeDV:playback_FL"
"FDV_Mic_to_FreeDV:monitor_FL" "FreeDV:input_FL"
"alsa_input.usb-GeneralPlus_USB_Audio_Device-00.mono-fallback:capture_MONO" "myfilter:playback_FL"
```
This makes it easy to copy/paste any lines manually if required. Maybe as arguments to pw-link in a script.
Note that the quotes are not mandatory unless there are spaces in a node name, however pw-link-save
always adds them.

## pw-link-restore \<filename\>
Restores links saved by pw-link-save unless nodes are either missing or otherwise in use.
Failure or success messages follow each attempt for debugging.
