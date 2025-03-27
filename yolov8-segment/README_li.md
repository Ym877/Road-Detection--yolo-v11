# **道路识别程序使用与日后迭代说明**

### 1.使用流程（从标注开始）

1.1 在ISAT_witch_segment_any thing-master文件夹中打开main.py（确保环境搭建Python=3.9，库参考目录requirements.txt
1.2标注图片，得到json文件
1.3将图片与json文件分别移入yolov8_project/datasets/segment/的img与json文件夹中
建立新的conda环境便于运行训练文件
1.4在yolov8_segment中打开segment_ json2txt.py运行注意：使用其他程序得到的json文件头名会不同，注意修改py文件中的头名
1.5在conda中激活系统，输入训练指令   (权重文件请依据情况使用)
yolo train task=segment data=datasets/segment/seg/segment.yaml mode=weights /yolo11s.pt epochs=50 imgsz=640 batch=8 workers=0 device=0
1.6训练完成后，输入检验指令或者启动验证文件
yolo prdict task=segment model=runs/segment/train/weights/best.pt source=/path/to/image.jpg conf=0.25 show=True
或者运行文件segment_detect.py
程序为实例分割程序，将不同个体标注不同颜色即为语义分割

### 2.问题与改进方向

2.1目前使用的最小系统训练，结果刚好，日后可以考虑使用大型预权重
2.2图片的标注量和质都不是太高，可以优化数据
2.3使用半自主工具的颜色不能直接使用在yolo v11中，两个工具对颜色的设定编码不一样，需要在标签文件中更改
2.4使用json2txt.py后标签顺序改变，需要手动更改或者优化py文件

### 3.参考网站：

3.1半自主标注工具
https://m.bilibili.com/video/BV1Lk4y1J7uB?buvid=NlVnAmNSNw87XmxdIV0hinfoc&from_spmid=search.search-result.0.0&is_story_h5=false&mid=LZ/UFWAJ2IK9ILMFLCGtoA==&p=1&plat_id=116&share_from=ugc&share_medium=android&share_plat=android&share_session_id=0d682ac0-69ec-457f-bb5c-9cfcfbe8bdb9&share_source=WEIXIN&share_tag=s_i&spmid=united.player-video-detail.0.0&timestamp=1741099479&unique_k=AwaKkwT&up_id=26569087&_unique_id_=c218ce03-ecd8-4ae2-bd6c-bc8106c6f922&code=081vqF000fzSWT1Q3M200qEaLa1vqF0X&state=）
3.2 yolo v11的使用说明
https://blog.csdn.net/Natsuago/article/details/143793404?ops_request_misc=%7B%22request%5Fid%22%3A%22c22627cd778330dceea1311b867dac5f%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=c22627cd778330dceea1311b867dac5f&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-143793404-null-null.142^v101^pc_search_result_base3&utm_term=yolov8语义分割&spm=1018.2226.3001.4187
