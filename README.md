# ComfyUI-GGF-VideoHelper

GGF fork of [ComfyUI-VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite) — conflict-free nodes for video workflows.

All node types are prefixed `GGF_` instead of `VHS_`, allowing this to coexist with the original VideoHelperSuite in the same ComfyUI installation without any conflicts.

## Installation

```bash
cd ComfyUI/custom_nodes
git clone https://github.com/GeekyGhost/ComfyUI-GGF-VideoHelper.git
cd ComfyUI-GGF-VideoHelper
pip install -r requirements.txt
```

## Differences from VideoHelperSuite

| | Original VHS | This Fork |
|---|---|---|
| Node prefix | `VHS_` | `GGF_` |
| Category | `Video Helper Suite 🎥🅥🅗🅢` | `GGF Video Helper Suite 🎥🅖🅖🅕` |
| Server routes | `/vhs/*` | `/ggf_vhs/*` |
| Settings IDs | `VHS.*` | `GGF.*` |
| Audio type | `VHS_AUDIO` | `GGF_AUDIO` |
| JS extension | `VideoHelperSuite.Core` | `GGF.VideoHelperSuite.Core` |

Existing VHS workflows are **not** compatible — node types have changed. This fork is intended for new workflows or projects that require both repos installed simultaneously.

---

## I/O Nodes

### GGF_LoadVideo — Load Video (Upload)
Converts a video file into a series of images.
- `force_rate`: Discard or duplicate frames to hit a target frame rate. Set to 0 to disable.
- `force_size`: Quick resize to suggested sizes, or set width/height independently.
- `frame_load_cap`: Maximum frames returned (i.e. max batch size).
- `skip_first_frames`: Skip N frames from the start after applying force_rate.
- `select_every_nth`: Skip frames without affecting base frame rate.

A path variant (`GGF_LoadVideoPath`) loads from external paths.

### GGF_LoadImages — Load Images (Upload)
Loads all image files from a subfolder.
- `image_load_cap`: Maximum images returned.
- `skip_first_images`: Skip N images from the start.
- `select_every_nth`: Skip images between each returned frame.

A path variant (`GGF_LoadImagesPath`) also exists.

### GGF_VideoCombine — Video Combine
Combines a series of images into an output video. Optional audio input is supported.
- `frame_rate`: Input frames displayed per second.
- `loop_count`: Additional times the video repeats.
- `filename_prefix`: Base output filename. Supports subfolders: `subfolder/video`.
- `format`: Output container/codec from `video_formats/`.
- `pingpong`: Append the video in reverse to create a loop.
- `save_image`: Save the first frame as a still image alongside the video.

---

## Batch Utility Nodes

All standard VHS batch utilities are available under the `GGF_` prefix:

`GGF_SplitLatents` · `GGF_SplitImages` · `GGF_SplitMasks`  
`GGF_MergeLatents` · `GGF_MergeImages` · `GGF_MergeMasks`  
`GGF_GetLatentCount` · `GGF_GetImageCount` · `GGF_GetMaskCount`  
`GGF_DuplicateLatents` · `GGF_DuplicateImages` · `GGF_DuplicateMasks`  
`GGF_SelectEveryNthLatent` · `GGF_SelectEveryNthImage` · `GGF_SelectEveryNthMask`  
`GGF_SelectLatents` · `GGF_SelectImages` · `GGF_SelectMasks`  
`GGF_Unbatch` · `GGF_VAEEncodeBatched` · `GGF_VAEDecodeBatched`

---

## Audio Nodes

- `GGF_LoadAudio` — Load audio from path with start time and duration options
- `GGF_LoadAudioUpload` — Upload audio directly
- `GGF_AudioToGGFAudio` — Convert ComfyUI AUDIO to legacy GGF_AUDIO (for external node compatibility)
- `GGF_GGFAudioToAudio` — Convert legacy GGF_AUDIO back to ComfyUI AUDIO

---

## Advanced Previews

When enabled in the ComfyUI settings panel under `🎥🅖🅖🅕 > Previews`, Load Video and Load Images nodes display animated previews reflecting current node settings in real time.

---

## Video Formats

Custom output formats can be added by placing `.json` files in the `video_formats/` folder. See the existing files for examples (h264-mp4, h265-mp4, av1-webm, ProRes, etc).

---

## Credits

All core functionality by [Kosinkadink](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite) and [AustinMroz](https://github.com/AustinMroz).  
This fork adds namespace isolation only — no functional changes.
