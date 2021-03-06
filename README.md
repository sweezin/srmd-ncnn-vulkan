# SRMD ncnn Vulkan

ncnn implementation of SRMD super resolution.

srmd-ncnn-vulkan uses [ncnn project](https://github.com/Tencent/ncnn) as the universal neural network inference framework.

## Usages

### Example Command

```shell
srmd-ncnn-vulkan.exe -i input.jpg -o output.png -n 3 -s 2
```

### Full Usages

```console
Usage: srmd-ncnn-vulkan -i infile -o outfile [options]...

  -h                   show this help
  -v                   verbose output
  -i input-path        input image path (jpg/png) or directory
  -o output-path       output image path (png) or directory
  -n noise-level       denoise level (-1/0/1/2/3/4/5/6/7/8/9/10, default=3)
  -s scale             upscale ratio (2/3/4, default=2)
  -t tile-size         tile size (>=32, default=400)
  -m model-path        srmd model path (default=models-srmd)
  -g gpu-id            gpu device to use (default=0)
  -j load:proc:save    thread count for load/proc/save (default=1:2:2)
```

- `input-path` and `output-path` accept either file path or directory path
- `noise-level` = noise level, large value means strong denoise effect, -1=no effect
- `scale` = scale level, 2=upscale 2x
- `tile-size` = tile size, use smaller value to reduce GPU memory usage, default is 400
- `load:proc:save` = thread count for the three stages (image decoding + srmd upscaling + image encoding), use larger value may increase GPU utility and consume more GPU memory. You can tune this configuration as "4:4:4" for many small-size images, and "2:2:2" for large-size images. The default setting usually works fine for most situations. If you find that your GPU is hungry, do increase thread count to achieve faster processing.

If you encounter crash or error, try to upgrade your GPU driver

- Intel: https://downloadcenter.intel.com/product/80939/Graphics-Drivers
- AMD: https://www.amd.com/en/support
- NVIDIA: https://www.nvidia.com/Download/index.aspx

## Original SRMD Project

- https://github.com/cszn/SRMD
- https://github.com/cszn/KAIR

## ncnn Project (>=20200219)

- https://github.com/Tencent/ncnn/tree/f4b1760a381514b78d526b39472de57af4d2da5b

## Other Open-Source Code Used

- https://github.com/nothings/stb for decoding and encoding image on Linux / MacOS
- https://github.com/tronkko/dirent for listing files in directory on Windows
