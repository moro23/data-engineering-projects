FROM python:3.12-alpine 

RUN pip install pandas 

WORKDIR /code 

COPY pipeline.py pipeline.py 

ENTRYPOINT [ "python", "pipeline.py"]