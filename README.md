# rot

Iterative browser-based JPEG recompression tool that accumulates generational codec loss in the pixel buffer.

Each pass calls `canvas.toDataURL('image/jpeg', quality)`, decodes the resulting JPEG back onto the 2D canvas context, and re-encodes for `N` generations (default: 50 iterations at quality `0.30`, configurable up to 200 iterations across quality `0.01–1.00`).

## Optional Inter-Pass Stages

Between JPEG encode cycles, three optional pixel-buffer passes can be enabled in fixed order:
1. **Luminance + Chroma Noise**: Shared luminance perturbation plus independent per-channel RGB offsets.
2. **Chromatic Drift**: Warm-to-cool channel bias (red gain, blue attenuation) with a linear contrast curve.
3. **5-Point Convolution Sharpen**: Amplifies 8x8 DCT block boundaries prior to the next quantizer pass.

## Usage

Single self-contained HTML file (`index.html`) using vanilla JavaScript and the HTML5 Canvas API. Open `index.html` directly in any browser or serve locally:

```bash
python3 -m http.server 8000
```
