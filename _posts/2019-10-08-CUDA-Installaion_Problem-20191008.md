---
layout: post
title:  "노트북 CUDA 설치시 문제 발생 (미해결)"
date:   2019-10-08 23:30:00
---



# 노트북 CUDA 설치시 문제설명할

노트북으로 Keras 하나를 돌렸는데, 너무 느리다. 시간을 측정하지는 않았는데, 한 6시간 정도 걸린 것 같다.

GPU를 사용하면 빠르다고 해서, GPU를 사용하기 위해서 CUDA를 설치하는데, 삽질을 너무 했다.

윈도우 10에 설치했다.


설치하고 사용하는 것이 너무 힘들다.

노트북에 설치되어 있는 그래픽 카드가 GTX1060Ti Q-Max인데, GPU 사용하는 것이 효과적일지 모르겠다.


설치시 문제점들 중에서

1. "ImportError: Could not find 'cudart64_100.dll'"는 에러가 발생했는데, 이는 Ndivia Forum에 같은 문제를 언급한 내용이 있는데, 해결책을 따라했더니 해결되었다.
   (https://devtalk.nvidia.com/default/topic/1060937/importerror-could-not-find-cudart64_100-dll-/)

2. 설치후에는 "Warning! HDF5 library version mismatched error"가 발생했다.
  이거는 h5py를 다시 설치하니 해결되었다.

3. 설치시에는 conda 가상환경을 활용했다. 근데, keras 설치하고 나서 실행을 해 보니, tensorflow-gpu는 사용을 하지 않고, cpu를 사용한다.
   속도가 느려서 cpu와 gpu 점유율 확인하는 방법을 사용해서 gpu를 사용하지 않고, cpu를 사용한다는 것을 알았다. (https://rfriend.tistory.com/425)
   검색을 하니 conda 가상환경의 문제라고 하면서, conda install이 아닌 pip install을 사용하라고 한다.
   그리고 tensorflow-gpu 설치시의 명령어도 알려주었다. (http://blog.naver.com/PostView.nhn?blogId=sw4r&logNo=221261544830&parentCategoryNo=&categoryNo=117&viewDate=&isShowPopularPosts=true&from=search)
   (pip install --ingnore-installed 에 대해서는 https://stackoverflow.com/questions/51913361/difference-between-pip-install-options-ignore-installed-and-force-reinstall 참조)


이렇게 어렵게 설치해서 케라스를 통한 인공지능 주식투자에 대한 코드를 돌렸다.

가장 큰 문제가 발생했다.

설치는 끝났는데, 지속적으로 에러가 발생해서 진행이 안 된다.
처음에는 cublas64_100.dll이 없다는 내용인데, CUDA 10.1 버전에서는 파일 이름이 cublas64_10.dll로 되어 있다.
검색해 보니 중국쪽에서 파일 이름을 바꿔 놓으면 된다는 내용(https://zhuanlan.zhihu.com/p/84619067)이 있어서 따라했다.

위의 내용은 사라졌는데, ".\tensorflow/core/kernels/random_op_gpu.h:227] Non-OK-status:"라는 내용으로 F가 앞에 뜨면서 파이썬 인터프리터에서 나와버리는 현상이 발생한다.

깃허브에는 CUDA10.0과 TF1.14를 사용 추천으로 내용이 나와 있다.(https://github.com/tensorflow/tensorflow/issues/30665)
관련 문제에 대해 이슈가 지속적으로 발생하고 있는 것 같으며, 아직 해결된 것 같지는 않다.
당분간 GPU 사용하는 건 참아야겠다.
