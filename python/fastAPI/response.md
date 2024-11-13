# Response 핸들링하기

FastAPI에는 다양한 response 클래스를 가지고 있다.

## Response

- 단일 응답을 반환하는 일반적인 방식으로 데이터를 한 번에 클라이언트에게 전달한다.
- 이미지, JSON, 텍스트 등 비교적 작은 데이터를 반환할 때 적합하다.
- 응답이 준비되면 전체 데이터를 한꺼번에 전송해 클라이언트가 응답 받을 때까지 기다린다. -> 큰데이터나 장시간 작업에는 메모리 부담

```python
from fastapi import FastAPI, Response

app = FastAPI()

@app.get("/")
async def static_response():
	data = "I am static"
	return Response(content=data, media_type="text/plain")
```

## JSONResponse

- 기본 JSON 응답 클래스로, JSON호환 객체를 자동으로 JSON형식으로 반환한다.
- JSON응답을 직접 커스터마이징할 때 유용

```python
from fastapi import FastAPI
from fastapi.responses import HTMLResponse

app = FastAPI()

@app.get("/")
async def json_response():
	data = {"message" : "This is JSON"}
	return JSONResponse(content=data)
```

## FileResponse

- 파일을 다운로드 할 수 있는 응답으로 pdf, 이미지, 문서등의 파일 다운로드에 적합하다.
- 서버에서 파일을 직접 제공하고 싶을 때 유용

```python
 # ...생략

@app.get("/")
async def file_response():
	file_path = "path/to/file.pdf"
	return FileResponse(file_path, filename="download.pdf")
```

## StreamingResponse

- 데이터를 *스트리밍 방식*으로 전송한다. 응답 데이터를 부분적으로 클라이언트에게 보내면서 처리할 수 있다.
- 큰 파일(비디오, 대용량 이미지등), 실시간 데이터 스트리밍에 적합
- 클라이언트가 데이터를 순차적으로 받아볼 수 있으며, 데이터 양이 크더라도 메모리 소비를 줄일 수 있다.
- 데이터를 chuck단위로 보낸다.
