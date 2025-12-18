# LK1 Longer Alfawise U20 Marlin Firmware

Welcome to the firmware repository for the **Alfawise U20** 3D printer, customized with **Marlin 2.1.x** to support advanced features like **BLTouch**. This project is tailored for users who want to enhance their 3D printing experience with improved hardware compatibility and firmware flexibility.

---

## Project Organization

The repository is structured as follows:

- **`guide.md`**: A detailed guide for installing and configuring the firmware, including hardware modifications and BLTouch setup.
- **`builds/`**: Contains precompiled firmware binaries for different configurations as well as Longer3D.UI files.
  - `base_working_canada_print/`
  - `bltouch_marlin_2.1.2.5/`
- **`sources/`**: The source code for Marlin firmware.
  - `Marlin-2.1.2.5/`: Main firmware source directory.
    - `Marlin/`: Core Marlin configuration files.
    - `config/`: Example configurations and defaults.
    - `docs/`: Documentation for developers and advanced users.
    - `ini/`: PlatformIO configuration files for various boards.

---

## Hardware Guide

To get started with the hardware installation,  please refer to the [hardware_guide.md](hardware_guide.md)

## Compilation Guide

To see how to configure a new Marlin installation, please refer to the [software_guide.md](software_guide.md) file. It details what change to made to Marlin files to make

## Actual flashing

To flash your Alfawise U20/Longer LK1 printer, either compile a new `project.bin` or use an existing one from the "builds" directory.

Copy both project.bin file and the "Longer3D.UI" file from "builds", and put them onto the printer SD card root directory.

Insert the card in your printer, turn it on, you should see a progress bar, wait for it to complete, once complete the printer should automatically start. 

Check that you can deploy/retract the BLTouch probe from the configuration > BLTouch menu, configure your z-offset to match the real world, store/reload the parameters and your done !

---

## License

This project is distributed under the terms of the **GPL v3 License**. See the `LICENSE` file in the `sources/Marlin-2.1.2.5/` directory for more details.

---

## Contributions

Contributions are welcome! Feel free to submit issues, feature requests, or pull requests to improve the firmware and documentation.

---

## Acknowledgements

- **Marlin Firmware**: The base firmware that has been customized for the Alfawise U20.
- **BLTouch**: For their auto bed leveling sensor, which inspired the enhanced features in this firmware.

