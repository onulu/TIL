# Anaconda(miniconda) CLI

아나콘다와 미니콘다는 python과 R 사용을 편리하게 해주는 오픈소스 툴이고 주고 환경관리, 패키지관리 그리고 배포를 위해 사용된다.
데이터 사이언스와 머신러닝을 위한 즉시 사용 가능한 환경을 제공해준다.
아나콘다는 풀버전?인 distribution과 최소 설치 버전인 Miniconda 둘 중에 용도에 맞게 설치해서 사용할 수 있다.

- 가상환경 목록 확인하기

```bash
conda env list
```

- 가상환경 생성하기

```bash
conda create -n myenv python=3.8
```

- 가상환경 진입

```bash
conda activate myenv
```

- 가상환경 빠져나오기

```bash
conda deactivate
```

- 가상환경 삭제

```bash
conda env remove --name myenv
```

- 패키지 설치

```bash
conda install numpy
# conda install numpy
# conda install numpy==1.26.0 (== 두개 주의)
```
