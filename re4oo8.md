# 复写checkbox和radio


```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style type="text/css">
        .label-style {
            margin: 20px 20px 0 0;
            display: inline-block
        }

        .input-radio-style {
            display: none
        }
        .input-checkbox-style {
            display: none
        }
        .input-radio-span-style {
            background-color: #fff;
            border: 1px solid rgba(0, 0, 0, 0.15);
            border-radius: 100%;
            display: inline-block;
            height: 16px;
            margin-right: 10px;
            margin-top: -1px;
            vertical-align: middle;
            width: 16px;
            line-height: 1
        }


        .input-checkbox-span-style {
            background-color: #fff;
            border: 1px solid rgba(0, 0, 0, 0.15);
            border-radius: 0;
            display: inline-block;
            height: 16px;
            margin-right: 10px;
            margin-top: -1px;
            vertical-align: middle;
            width: 16px;
            line-height: 1
        }

        .input-radio-style:checked+.input-radio-span-style:after {
            background-color: #57ad68;
            border-radius: 100%;
            content: "";
            display: inline-block;
            height: 12px;
            margin: 2px;
            width: 12px
        }
        .input-checkbox-style:checked+.input-checkbox-span-style:after {
            background-color: #57ad68;
            border-radius: 0;
            content: "";
            display: inline-block;
            height: 12px;
            margin: 2px;
            width: 12px
        }
    </style>
</head>

<body>
    <div>
        <label class="label-style">
            <input class="input-radio-style" type="radio" name="app">
            <span class="input-radio-span-style"></span>约
        </label>
        <label class="label-style">
            <input class="input-radio-style" type="radio" name="app">
            <span class="input-radio-span-style"></span>不约，叔叔我们不约
        </label>
    </div>
    <div>
        <label class="label-style">
            <input class="input-checkbox-style" type="checkbox">
            <span class="input-checkbox-span-style"></span>苍井空
        </label>
        <label class="label-style">
            <input class="input-checkbox-style" type="checkbox">
            <span class="input-checkbox-span-style"></span>波多野结衣
        </label>
        <label class="label-style">
            <input class="input-checkbox-style" type="checkbox">
            <span class="input-checkbox-span-style"></span>罗玉凤
        </label>
    </div>
</body>

</html>
```

