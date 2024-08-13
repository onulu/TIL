# 터미널에서 webp로 이미지 변환하기

webP는 최신 압축 기술을 사용해 jpeg나 png에 비해 더 작은 파일 크기에 비슷한 퀄리티의 이미지를 사용할 수 있다. `cwebp`는 JPEG, PNG 또는 TIFF 형식의 이미지를 WebP로 인코딩하고, `dwebp`는 다시 PNG로 디코딩한다.

1. 설치하기

```bash
brew install webp
```

1. 기본 사용법

```bash
cwebp -q 80 img.png -o img.webp
```

2. 품질 조절 (0-100, 기본값 75)

```bash
cwebp -q 80 input.jpg -o output.webp
```

3. webp를 png로 변환하기

```bash
dwebp image.webp -o image.png
```