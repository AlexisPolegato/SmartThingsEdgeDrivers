# NodOn SIN-4-FP-21 Fil Pilote Controller - SmartThings Edge Driver

This Edge driver provides SmartThings integration for the NodOn SIN-4-FP-21 Zigbee fil pilote controller, which is used to control French electric heating systems.

## Features

- Full support for manufacturer cluster 0xFC00
- Control all 6 fil pilote heating modes:
  - OFF (0x00) - Heater off
  - Comfort (0x01) - Full heating
  - Eco (0x02) - Reduced heating
  - Anti-Freeze (0x03) - Frost protection
  - Comfort-1 (0x04) - Comfort variant 1
  - Comfort-2 (0x05) - Comfort variant 2

## SmartThings Mode Mapping

The driver maps fil pilote modes to standard SmartThings thermostat modes:

| Fil Pilote Mode | SmartThings Mode |
|----------------|------------------|
| OFF | off |
| Comfort | heat |
| Comfort-1 | heat |
| Comfort-2 | heat |
| Eco | eco |
| Anti-Freeze | emergency heat |

## Installation

### Option 1: Using SmartThings CLI

1. Install the SmartThings CLI if you haven't already:
   ```bash
   npm install -g @smartthings/cli
   ```

2. Login to your SmartThings account:
   ```bash
   smartthings login
   ```

3. Package and upload the driver:
   ```bash
   smartthings edge:drivers:package .
   smartthings edge:drivers:install
   ```

4. Enroll your hub in the driver channel and install the driver to your hub

### Option 2: Manual Installation via Developer Workspace

1. Go to [SmartThings Developer Workspace](https://smartthings.developer.samsung.com/workspace)
2. Create a new Edge driver project
3. Upload the driver files (config.yml, profiles/, src/)
4. Deploy to your hub

## Pairing the Device

1. Put your SmartThings hub in Zigbee pairing mode:
   - Open SmartThings app
   - Go to Devices > Add Device > Scan for nearby devices

2. Put the NodOn SIN-4-FP-21 in pairing mode according to the manufacturer's instructions

3. The device should be discovered and added automatically with the correct driver

## Usage

Once paired, you can control the heating mode through:

- SmartThings mobile app (Thermostat control)
- SmartThings automations and scenes
- Voice assistants (Alexa, Google Home)

### Available Commands

- **Set Thermostat Mode**: Change between off, heat, eco, and emergency heat
- **Refresh**: Read the current mode from the device

## Technical Details

### Manufacturer Cluster (0xFC00)

- **Manufacturer Code**: 0x128B (NodOn)
- **Attribute 0x0000**: Current mode (read/report)
- **Command 0x00**: Set mode (write)

### Driver Files

- `config.yml`: Driver configuration and metadata
- `profiles/nodon-fil-pilote.yml`: Device capability profile
- `src/init.lua`: Main driver logic with manufacturer cluster handling

## Troubleshooting

### Device not pairing
- Ensure the device is in pairing mode
- Reset the device according to manufacturer instructions
- Check that your hub supports Zigbee 3.0

### Mode changes not working
- Use the Refresh command to read current state
- Check SmartThings CLI logs: `smartthings edge:drivers:logcat`
- Verify the manufacturer cluster is responding

### Viewing Driver Logs

```bash
smartthings edge:drivers:logcat
```

This will show real-time logs including mode changes and Zigbee communication.

## Extending the Driver

If you need to add more functionality:

1. **Custom Capabilities**: Create custom capabilities for Comfort-1/Comfort-2 modes
2. **Preferences**: Add user preferences in config.yml for default modes
3. **Additional Clusters**: Add support for other Zigbee clusters if needed

## Support

For issues or questions:
- Check SmartThings Community forums
- Review SmartThings Edge driver documentation
- Check device logs for detailed debugging information

## License

This driver is provided as-is for use with NodOn SIN-4-FP-21 devices.
