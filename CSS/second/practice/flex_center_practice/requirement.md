- 요구 사항
    - 각각 수평정렬 / 수직정렬 및 중앙정렬을 만들어주자
        
- 실습 코드
    
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <title>Flexbox</title>
        <meta charset="UTF-8" />
        <style>
          .container-1 {
            margin: 20px;
            padding: 20px;
            background-color: lightcyan;
          }
    
          .container-2 {
            margin: 20px;
            padding: 20px;
            background-color: lightblue;
          }
        </style>
      </head>
      <body>
        <div class="container-1">
          <h1>수평 정렬</h1>
          <div class="main-axis-container">
            <button>flex button 1</button>
            <button>flex button 2</button>
            <button>flex button 3</button>
          </div>
        </div>
    
        <div class="container-2">
          <h1>수직 정렬</h1>
          <div class="cross-axis-container">
            <button>flex button 1</button>
            <button>flex button 2</button>
            <button>flex button 3</button>
          </div>
        </div>
      </body>
    </html>
    
    ```