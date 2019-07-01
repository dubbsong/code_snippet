#### HTML

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no, user-scalable=no">
  <title>BASE</title>

  <!-- Favicon -->
  <link rel="shortcut icon" type="image/x-icon" sizes="16x16 32x32" href="./favicon.ico">
  <link rel="icon" type="image/x-icon" href="./favicon.ico">

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css?family=Ubuntu:300,400,500,700" rel="stylesheet">

  <!-- Stylesheets -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css">
  <link rel="stylesheet" href="./base.css">
</head>

<body>
  <section id="header">
    <h1>BASE CODE</h1>
  </section>

  <!-- Scripts -->
  <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
  <script src="./base.js"></script>
</body>

</html>
```

<br>

#### CSS

```css
html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Ubuntu', sans-serif;
  text-align: center;
}

#header {
  background-color: #9DC8C8;
  height: 100vh;
}

#header h1 {
  color: #519D9E;
  font-weight: 700;
  line-height: 100vh;
  margin: 0;
}
```

<br>

#### JS

```js
// Mobile
let size = {
  width: window.innerWidth || document.body.clientWidth,
  height: window.innerHeight || document.body.clientHeight
};

if (size.width < 768) {
  // Some code
}
```

<br>