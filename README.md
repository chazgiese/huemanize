# 🎨 Huemanize - Perceptual Color Interpolation Plugin

A Figma plugin that creates beautiful color scales using perceptual color interpolation. Generate harmonious color palettes from a single base color with various interpolation methods, including support for both light and dark mode scales.

## Features

- **Perceptual Color Interpolation**: Uses OKLCH color space for perceptually uniform color transitions
- **Multiple Interpolation Methods**: Choose from Linear, Bezier, Catmull-Rom, and easing functions
- **Customizable Scales**: Control the number of steps, lightness range, and chroma range
- **Light & Dark Mode Support**: Generate separate color scales for light and dark themes
- **Real-time Preview**: See your color scales with tabbed interface for light and dark modes
- **Figma Variables Integration**: Automatically creates color variables with Light and Dark modes in a "Colors" collection

## How to Use

### 1. Input Base Color
Enter a hex color code (e.g., `#FF6B6B`) in the input field. The plugin will validate the format and show a preview.

### 2. Choose Interpolation Method
Select from different interpolation methods:
- **Linear**: Straight-line interpolation
- **Bezier**: Smooth cubic bezier curve
- **Catmull-Rom**: Smooth spline interpolation
- **Ease In**: Gradual start, fast finish
- **Ease Out**: Fast start, gradual finish
- **Ease In-Out**: Smooth acceleration and deceleration

### 3. Adjust Scale Settings
- **Steps**: Number of colors in the scale (3-20)
- **Lightness**: Range of lightness variation (0-100%)
- **Chroma**: Range of chroma/saturation variation (0-100%)

### 4. Preview Your Scales
- **Light Mode Tab**: View the light mode color scale (light to dark progression)
- **Dark Mode Tab**: View the dark mode color scale (dark to light progression) - always available for preview
- **Export Mode**: Choose how to export your scales to Figma variables using the radio buttons:
  - **Light Mode Only**: Export only light mode variables
  - **Dark Mode Only**: Export only dark mode variables  
  - **Both Light & Dark**: Export variables with both light and dark mode values

### 5. Add to Figma
Click "Add to Figma Variables" to create color variables in your current file. The plugin will:
- Create a "Colors" collection if it doesn't exist
- Create "Light" and/or "Dark" modes based on your export mode selection
- Add color variables named like "primary/100", "primary/200", etc.
- Set appropriate color values for the selected mode(s):
  - **Light Mode Only**: Variables with light mode values only
  - **Dark Mode Only**: Variables with dark mode values only
  - **Both Light & Dark**: Variables with both light and dark mode values

## Dark Mode Support

### How It Works
The plugin generates two separate color scales:

1. **Light Mode Scale**: Traditional light-to-dark progression suitable for light backgrounds
2. **Dark Mode Scale**: Inverted dark-to-light progression suitable for dark backgrounds

### Export Options
Choose from three export modes to control what gets added to Figma:

- **Light Mode Only**: Perfect for projects that only need light theme support
- **Dark Mode Only**: Ideal for dark-themed applications or when you want to start with dark mode
- **Both Light & Dark**: Complete solution for applications that support both themes

### Figma Variable Modes
The plugin automatically handles Figma variable modes:
- **Light Mode**: Contains colors optimized for light UI backgrounds
- **Dark Mode**: Contains colors optimized for dark UI backgrounds
- **Mode Creation**: Only creates the modes you need based on your export selection
- **Mode Order**: Works correctly regardless of whether Light or Dark mode comes first in your collection

### Best Practices
- Use the light mode scale for text, borders, and UI elements on light backgrounds
- Use the dark mode scale for text, borders, and UI elements on dark backgrounds
- The same variable name (e.g., "primary/500") will have different color values for each mode

## Technical Details

### Color Space
The plugin uses the OKLCH color space for interpolation, which provides:
- **Perceptually uniform lightness**: Changes in lightness appear consistent to the human eye
- **Better color transitions**: More natural-looking color scales
- **Accurate color representation**: Maintains color relationships across different displays

### Interpolation Methods
- **Linear**: `f(t) = t`
- **Bezier**: `f(t) = t²(3 - 2t)` (smoothstep function)
- **Catmull-Rom**: Cubic spline interpolation for smooth curves
- **Easing Functions**: Standard CSS-like easing curves

### Dark Mode Algorithm
When generating dark mode scales, the plugin:
1. Inverts the lightness interpolation direction (dark to light instead of light to dark)
2. Maintains the same chroma and hue values for color consistency
3. Creates a separate scale optimized for dark backgrounds

### Building the Plugin

1. Install dependencies:
   ```bash
   npm install
   ```

2. Build the plugin:
   ```bash
   npm run build
   ```

3. Load in Figma:
   - Open Figma
   - Go to Plugins > Development > Import plugin from manifest
   - Select the `manifest.json` file

## Development

### Project Structure
```
huemanize/
├── code.ts          # Main plugin logic
├── ui.html          # Plugin UI
├── manifest.json    # Plugin manifest
├── package.json     # Dependencies
├── tsconfig.json    # TypeScript configuration
└── types.d.ts       # Type declarations
```

### Key Dependencies
- **culori**: Color manipulation and interpolation library
- **@figma/plugin-typings**: TypeScript definitions for Figma API

### Color Interpolation Algorithm
1. Convert input hex to OKLCH color space
2. Generate lightness interpolation from 0.1 to 0.9 (or inverted for dark mode)
3. Generate chroma interpolation from 0 to base color chroma
4. Combine both interpolations using the selected easing function
5. Convert back to hex format

## Contributing

Feel free to submit issues and enhancement requests!

## License

MIT License - see LICENSE file for details. 