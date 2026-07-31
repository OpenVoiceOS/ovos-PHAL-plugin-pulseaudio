# ovos-PHAL-plugin-pulseaudio

This is a PHAL (Platform/Hardware Abstraction Layer) plugin for [OpenVoiceOS](https://github.com/OpenVoiceOS). It controls system volume through PulseAudio. The plugin loads only when it finds `pulseaudio` on the system, so it does not interfere with devices that use a different audio server.

## Install

```bash
pip install ovos-PHAL-plugin-pulseaudio
```

## Usage

The plugin registers as a PHAL entry point (`opm.phal`) and starts automatically when OVOS PHAL loads it. It listens for these bus messages:

```python
self.bus.on("mycroft.volume.get", self.handle_volume_request)
self.bus.on("mycroft.volume.set", self.handle_volume_change)
self.bus.on("mycroft.volume.increase", self.handle_volume_increase)
self.bus.on("mycroft.volume.decrease", self.handle_volume_decrease)
self.bus.on("mycroft.volume.set.gui", self.handle_volume_change_gui)
self.bus.on("mycroft.volume.mute", self.handle_mute_request)
self.bus.on("mycroft.volume.unmute", self.handle_unmute_request)
self.bus.on("mycroft.volume.mute.toggle", self.handle_mute_toggle_request)
self.bus.on("mycroft.volume.get.sliding.panel", self.handle_volume_request)
```

On first boot, the plugin sets the volume to 50%. Volume changes play a sound unless the caller sets `play_sound` to `False` in the message data.

## Related projects

- [OpenVoiceOS/ovos-PHAL-plugin-alsa](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-alsa): the same volume control, for systems that use ALSA instead of PulseAudio.
- [OpenVoiceOS/ovos-plugin-manager](https://github.com/OpenVoiceOS/ovos-plugin-manager): loads and manages PHAL plugins.

## License

Apache-2.0
