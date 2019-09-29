# Pylon Camera and Structure Camera Wrappers

This is a wrapper around amazing Structure io camera and basler cameras. 
All frame acquisition happen in a new thread spawned so that all frames are acquired real time.
Just after the initialization frame grabbing starts. So to find the working of camera, for any USB or
miscellaneous errors the code would give error at initialization phase itself. The reason to ame this repo is because the 
frame acquisition wasn't happening in a different thread or it wasn't easy to integrate into 
complex C++ codes.  
The API is as follows:

## Includes
```cpp
#include <get_depth_frame_Structure.h>
#include <pylon_camera_utils.h>
```

## Getting depth frame and doing ICP (Structure Camera API)

```cpp
structure_io_depthframe dpt_frame;
depth_frame_latest = dpt_frame.get_depth_frame();
# Save reference Frame
dpt_frame.save_reference_frame()
// Do ICP from the reference frame as reference
dpt_frame.icp_detect_movement()
```

## Basler camera API
```cpp
pylon_camera_utils cmos_camera;
while (true) {
    if (!cmos_camera.nm685_current_frame.empty() && !cmos_camera.nm830_current_frame.empty()) {
        // Do some Image processing stuff with the camera frame
        cmos_camera.get_center_of_blob(cmos_camera.nm830_current_frame);
        break;
    }
}
```