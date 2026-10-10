# hand-frame-effect
# Hand Frame Video Effect

Make a rectangle with your fingers (thumb and index finger of both hands like a camera frame gesture). Only the area inside the frame gets a look, such as a thermal color map, a slight time delay and scanlines while everything outside stays normal.

Works on video files and on a webcam preview.

## Features

- Hand tracking with MediaPipe using both the mp.solutions) and new (mp.tasks) APIs

- Four effects: thermal, invert, glitch, bw

- Optional frame delay inside the frame so it feels like another moment in time

- Optional scanline overlay

- Smoothed frame corners with a short hold when the hands are briefly lost

- Feathered edges for a clean composite

- Original audio is copied to the output if ffmpeg is installed

## Installation

```bash

git clone https://github.com/morning-coffee-code/hand-frame-effect.git

cd hand-frame-effect

pip install -r requirements.txt

```

With newer MediaPipe versions, a small hand model (~8 MB) is downloaded automatically on first run and saved next to the script as hand_landmarker.task.

ffmpeg is optional. If it is on your PATH the original audio is kept in the output video.

## Usage

```bash

# Process a video file

python hand_frame_effect.py input.mp4 output.mp4

# Choose an effect. Delay

python hand_frame_effect.py input.mp4 output.mp4 --effect invert --delay 6

# Live webcam preview (press q to quit)

python hand_frame_effect.py 0

```

### Options

| Option Description | Default |

|---|---|---|

| input | Video file or a webcam index such as 0 | 0 |

output | Output.mp4 (not needed for webcam) | none |

| thermal, invert, glitch or bw | thermal |

| --delay | Frames of delay inside the frame (0 = off) 4 |

| --no-scanlines | Disable the scanline overlay | off |

## How it works

1. MediaPipe detects the thumb tip and index fingertip of up to two hands.

2. The four points are ordered into a convex quadrilateral.

3. The quad is smoothed over time to reduce jitter.

4. The chosen effect is applied to the content ( from an older frame) scanlines are added and the result is blended into the original frame through a feathered mask.

## Tips

- Keep both hands clearly visible with lighting.

- Form the frame with the thumb of one hand and the index finger of the other (or both pairs) so the four fingertips make a rectangle.

- Increase --delay, for a stronger "different moment" look.

## Requirements

- Python 3.8+

- mediapipe opencv-python, numpy

## License

Released under the MIT License.
