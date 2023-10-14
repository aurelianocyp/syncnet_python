## Dependencies
```
environment.yml
```
python 37
In addition, `ffmpeg` is required.

## check environment
run SyncNet demo:
```
python demo_syncnet.py --videofile data/example.avi --tmp_dir /path/to/temp/directory
```
Check that this script returns:
```
AV offset:      3 
Min dist:       5.353
Confidence:     10.021
```

Full pipeline,按照顺序把三个都跑一遍:
```
sh download_model.sh
python run_pipeline.py --videofile data/$id.mp4 --reference $id
python run_syncnet.py --videofile data/$id.mp4 --reference $id
python run_visualise.py --videofile data/$id.mp4 --reference $id
```

Outputs:
```
data/work/pycrop/$REFERENCE/*.avi - cropped face tracks
data/work/pywork/$REFERENCE/offsets.txt - audio-video offset values
data/work/pyavi/$REFERENCE/video_out.avi - output video (as shown below)
```
<p align="center">
  <img src="img/ex1.jpg" width="45%"/>
  <img src="img/ex2.jpg" width="45%"/>
</p>

