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
准备文件：sh download_model.sh
Full pipeline,按照顺序把三个都跑一遍，sync指标的值会在run_syncnet.py运行完成后在控制台输出，AV offset没啥用，比较有用的是Min dist，应该就是指的是最小延迟之类的，confidence是置信度，是根据所有延迟计算出来的这个最小延迟的可信程度，run_syncnet代码的思路就是先提取每一帧，例如这里有6002帧，然后会给每一帧生成一些数据，得到5007（代码里设置了总帧数-5）个包含31个值的tensor，然后在axis为1上stack一下，就变成了31*5007，然后求个平均，就得到了31个平均值，min dist就是这31个平均值中最小的，而AV offset就是这个最小的位置与第15个位置的差，例如如果在16，则AV offset为-1:
```
python run_pipeline.py --videofile data/$id.mp4 --reference $id
python run_syncnet.py --videofile data/$id.mp4 --reference $id
python run_visualise.py --videofile data/$id.mp4 --reference $id
```

Outputs:
```
data/work/pycrop/$id/*.avi - cropped face tracks
$id_offsets.txt - audio-video offset values
data/work/pyavi/$id/video_out.avi - output video (as shown below)
```
<p align="center">
  <img src="img/ex1.jpg" width="45%"/>
  <img src="img/ex2.jpg" width="45%"/>
</p>

