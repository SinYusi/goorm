## 요구사항

- 그림자는 요소 바깥쪽에 위치
- 그림자는 텍스트의 오른쪽으로 10px, 아래로 10px에 위치
- 그림자의 흐림 정도는 10px
- 그림자의 색상은 rgba(0, 0, 0, 0.5)
- 실습 코드
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <style>
        .button-box {
          width: 100%;
          height: 100vh;
          display: flex;
          justify-content: center;
          align-items: center;
        }

        .btn {
          width: 100px;
          height: 50px;
          background-color: #3498db;
          color: white;
          font-size: 20px;
          border: none;
          border-radius: 5px;
          cursor: pointer;
	        /* 이 부분에 요구사항에 맞는 그림자를 만들어 주세요 */
        }
      </style>
    </head>
    <body>
      <div class="button-box">
        <button class="btn">HELLO</button>
      </div>
    </body>
  </html>
  ```