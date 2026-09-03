# Q-SYS-Williams-Sound-IRT2-IRT3

- Williams Sound IRT2 / IRT3 IR Hearing Assistance Plugin (RS232)
- Serial Connection - Baud: 115200, Data Bits: 8, Parity: None, Stop Bits: 1, Flow Control: None
- Written by Glen Gorton
- Built with Williams Sound IRT2 running firmware v1.2.0
- Developed and tested using Q-SYS Designer v10.4.1

## NOTES:

- Script has been written with a focus on the William Sounds IRT2 / IRT3 running in 'Monitoring Mode'.
- Script is written to Connect() to device, set it to Command Mode, Reboot the device (in order to obtain firmware version and runtimes), then set it to Monitoring Mode.
- When individual commands are triggered, the device is first set to Command Mode so it will accept the command, command send, then device returned to Monitoring Mode (ie. 3x commands are sent)
- As a result, 'Monitoring Mode' and 'Command Mode' controls (booleans) have been commented out and the individual controls deleted -> can be re-added if needed.
- 'Unique ID', 'Audio ChA Data' and 'Audio ChB Data' is also obtained prior to the reboot at script start. Control EventHandlers have been commented out and control deleted -> can be re-added if needed.
- 'Help' control (trigger) also deleted and commented out.

-- Command Mode commands:
- audio_minmax_reset = Reset CHA & CHB audio capture data
- audio_minmax_cha = min and max of CHA audio since reset
- audio_minmax_chb = min and max of CHB audio since reset
- sleep_now = Put the IR T2 to sleep immediately, if there is no audio
- wake_now = Wake up the IR T2 immediately, even without audio
- mute_audio_input=on = Mute the audio (on reboot, the audio will not be muted)
- mute_audio_input=off = Unmute the audio
- ir_low_power_mode=0 = Put the IR T2 in full power mode for stronger infrared coverage
- ir_low_power_mode=1 = Put the IR T2 in 1/2 power mode for less infrared coverage
- rf_band_select=0 = Change the broadcast channel(s) to 2.3/2.8 MHz IR
- rf_band_select=1 = Change the broadcast channel(s) to 3.3/3.8 MHz IR
- restore_defaults = Reset all settings to the default
- reboot_unit = Restart the IR T2
- visible_leds=enable = Turn on the LED status indicator lights on the back of the unit
- visible_leds=disable = Turn off all of the LED status indicator lights on the back of the unit
- visible_leds=blink_5sec = Turn off and on all of the LED lights for 5 seconds
- unique_id = Display the unique identifier for this IR T2 unit

### 5th August 2026 - Glen Gorton
- Timer.CallAfter surrounds the entire script as the intial 'Force Command Mode' command within GetFirmwareAndRuntime() does not work following a design load. Possibly behaviour of the serial port?
- readTimeout Timer used to detect if any SerialPorts.Events has been received, and if not set a Fault Status.
- Device total runtime (deviceTotalRuntime) is appended to the Status.
