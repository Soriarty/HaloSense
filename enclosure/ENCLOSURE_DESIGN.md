# HaloSense Enclosure

3D-printable housing design for the HaloSense presence sensor.

## 🚧 Work in Progress

Enclosure design is currently under development. Check back for updates!

## Overview

The HaloSense enclosure is designed to be:
- **3D printable** on common FDM printers
- **Professional looking** for home installations
- **Functional** with proper ventilation and sensor windows
- **Modular** with multiple mounting options

## Directory Structure

```
enclosure/
├── stl/            # STL files for 3D printing
├── step/           # STEP files for editing in CAD software
└── README.md       # This file
```

## Design Goals

### Aesthetics
- Clean, modern design suitable for visible installation
- Minimal visible mounting hardware
- Professional appearance

### Functionality
- Adequate ventilation for ESP32 heat dissipation
- Clear sensor windows for mmWave, PIR, and light sensors
- LED indicator visible but not distracting
- Easy access to USB-C and Ethernet ports

### Printability
- Printable without supports (where possible)
- Compatible with common FDM printers (220x220x250mm build volume)
- Reasonable print time (target <8 hours for main body)
- Standard layer heights (0.2mm works well)

### Assembly
- Minimal hardware required
- Snap-fit or screw assembly
- Easy PCB installation and removal
- Cable management built-in

## Planned Components

### Main Housing
- **Top Cover** - Sensor windows, LED diffuser
- **Bottom Base** - PCB mounting, port access
- **Middle Ring** (optional) - Cable management, additional features

### Mounting Options
- **Wall Mount** - Low-profile bracket for vertical surfaces
- **Ceiling Mount** - Flush or pendant style
- **Desk Stand** - Weighted base for desk placement

### Accessories
- **Cable Clips** - Route and secure cables
- **Lens Covers** - Protect sensors during installation
- **Mounting Template** - Paper template for marking holes

## Design Specifications

### Dimensions
- **Diameter:** TBD (based on PCB size)
- **Height:** TBD (accommodate PCB + clearance)
- **Wall Thickness:** 2-3mm (balance strength vs print time)

### Materials
- **Recommended:** PETG (temperature resistant, durable)
- **Alternative:** PLA (easier to print, less temperature resistant)
- **Advanced:** ABS (strongest, requires heated chamber)

### Clearances
- **PCB to walls:** Minimum 2mm
- **Component clearance:** Minimum 3mm from enclosure
- **Ventilation slots:** Strategic placement for airflow

### Sensor Windows
- **mmWave radar:** Unobstructed or thin plastic (plastic-transparent to radar)
- **PIR sensor:** Clear line of sight
- **Light sensor:** Translucent or clear window

## Print Settings

### Recommended Settings (FDM)

```
Material: PETG
Layer Height: 0.2mm
Infill: 20%
Wall Thickness: 3 perimeters (1.2mm)
Top/Bottom Layers: 4-5 layers
Print Speed: 50mm/s
Support: None (design to avoid)
Bed Temperature: 70-80°C
Nozzle Temperature: 230-250°C
```

### Post-Processing
- Remove support material (if any)
- Light sanding of contact surfaces
- Optional: Paint or finish for aesthetics

## Assembly Instructions

*Coming soon after design is finalized*

General steps:
1. Print all components
2. Clean up prints (remove brim, supports)
3. Test fit before assembly
4. Install PCB with spacers
5. Route cables through guides
6. Secure top cover
7. Attach mounting bracket

## CAD Software

### Recommended Tools
- **FreeCAD** (free, open-source)
- **Fusion 360** (free for personal use)
- **Blender** (free, powerful for organic shapes)
- **OpenSCAD** (free, parametric design)

### File Formats
- **STEP (.step)** - Universal CAD format for editing
- **STL (.stl)** - 3D printing standard format
- **3MF (.3mf)** - Modern 3D printing format (optional)

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines on contributing to enclosure design.

**Key points:**
- Include both STL and STEP files
- Document print settings
- Provide assembly instructions
- Test print before submitting

### Design Considerations
- Must provide adequate ventilation for ESP32
- Must accommodate sensor beam angles
- Must be mechanically robust
- Should be printable without supports (preferred)
- Should work on common FDM printers

## Testing Checklist

Before finalizing design:
- [ ] Print prototype
- [ ] Verify PCB fits properly
- [ ] Check sensor window alignment
- [ ] Confirm port accessibility
- [ ] Test ventilation (temperature monitoring)
- [ ] Verify mounting bracket strength
- [ ] Check assembly/disassembly ease
- [ ] Evaluate aesthetics

## Known Design Challenges

### Challenge: Heat Dissipation
- **Issue:** ESP32 + PoE can generate significant heat
- **Solutions:** Ventilation slots, heat sinks, material choice

### Challenge: Sensor Window Material
- **Issue:** mmWave needs radio-transparent material
- **Solutions:** Thin plastic (<2mm), strategic openings, testing

### Challenge: Circular PCB Mounting
- **Issue:** Non-standard form factor
- **Solutions:** Custom mounting posts, flexible design

## Resources

### 3D Printing Guides
- [All3DP Beginner's Guide](https://all3dp.com/2/3d-printing-beginner-guide/)
- [Prusa Knowledge Base](https://help.prusa3d.com/en/)

### CAD Tutorials
- [FreeCAD Tutorials](https://wiki.freecadweb.org/Tutorials)
- [Fusion 360 Learning](https://help.autodesk.com/view/fusion360/ENU/courses/)

### Design Inspiration
- Thingiverse
- Printables
- MyMiniFactory

## License

Enclosure design files are licensed under CC BY-NC-SA 4.0. See [LICENSE.md](../LICENSE.md) for details.

---

**Project:** HaloSense
**Maintainer:** [@Soriarty](https://github.com/Soriarty)
**Repository:** https://github.com/Soriarty/HaloSense
