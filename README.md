# F2B

## Frame Too Big

So we slice and dice, infer, then merge them back.

### Before f2b

If you just stuff a 4K image into a detector:
![noslice](illustrations/seoul-station_4K_det_noslice.jpg)

### After f2b

Just **purely slice, dice and infer**
![f2bed](illustrations/seoul-station_4K_det_maxinfsize1333.jpg)

After **deconflicting union** (at the overlapping regions)
![f2bed_dcu](illustrations/seoul-station_4K_det_DCU80.jpg)

**Final results!**
![f2bed_dcu_nosmol](illustrations/seoul-station_4K_det_DCU80_nosmol.jpg)

Just for comparison, here's the **no**-f2b version again..
![noslice2](illustrations/seoul-station_4K_det_noslice.jpg)

## How to run

See `run.py` for example. Initialise, `register`, `detect`.

## Arguments

- `detect_fn` (`Callable`): object detection inference function
- `max_inference_width` and `max_inference_height` (`int`): usually the size your detector will shrink ur oversized image to, in pixels
- `overlapx_px` and `overlapy_px` (`int`): overlapping regions, in pixels
- `pad` (`bool`): if we add pad to orphan slices, probably don't pad for faster rcnn

## How to use f2b for annotating huge images

If images are too big to be fed into cvat for annotations, `img_cutter.py` comes to the rescue to cut up the images into more reasonable smaller images. Use `img_cutter_batch.sh` to run this on a batch of images in a directory. The cut-up images to be uploaded into cvat will be stored in your specified `out_dir`.

After annotations are done on the cut-up images, use `img_merger.py` to merge back the annotations into specified `biggie_annot_file`. Both coco json and 'cvat for images' xml formats are currently supported.
