## 요구사항

이미지 URL은 아래를 사용해주세요.

- 위 이미지 : http://poiemaweb.com/img/bg/stock-photo-125979219.jpg
- 아래 이미지 : http://poiemaweb.com/img/bg/stock-photo-155153867.jpg

font 는 이걸 활용해주세요 : `font: 15px/2 Georgia, Serif;`

이미지 `최소 높이`는 `600px` 입니다.

- 실습 코드
  ```html
  <!DOCTYPE html>
  <html>
  <head>
    <style>
      *, *:after, *:before {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }

      html, body {
        width:100%;
        height:100%;
      }

      /* 여기에 실습 코드를 작성해주세요 */
    </style>
  </head>
  <body>
    <div class="bg-wrap parallax">
      <div id="page-wrap">
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid ipsum maxime libero, impedit necessitatibus quas blanditiis tenetur vero aut esse unde ab similique, delectus placeat enim quae expedita excepturi laboriosam.</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid ipsum maxime libero, impedit necessitatibus quas blanditiis tenetur vero aut esse unde ab similique, delectus placeat enim quae expedita excepturi laboriosam.</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid ipsum maxime libero, impedit necessitatibus quas blanditiis tenetur vero aut esse unde ab similique, delectus placeat enim quae expedita excepturi laboriosam.</p>
      </div>
    </div>
    <div class="bg-wrap normal"></div>
  </body>
  </html>
  ```