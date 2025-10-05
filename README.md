

Running backend-services


1.	``` sudo apt install python3 ```
2.	```python3 -m venv *PATH TO ENV*```
3.  ```pip install fastapi```
4.  ```pip install google-genai```
5.  ```pip install uvicorn```
6.	```git pull https://github.com/hackyeah-2025/backend-services main```
7.	run by doing ```uvicorn main:app --reload --host 0.0.0.0```
IMPORTANT NOTE!!!
YOU NEED YOUR TERMINAL TO BE OPEN FOR IT TO WORK, IF YOU DONT WANT THAT RUN IT USING ```nohup uvicorn main:app --reload &```
