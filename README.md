svgRelation图表
===

使用svg建立关系图表。可以拖拽节点，使用上(up)、下(down)、左(left)、右(right)键可以改变视口。

##参数

+ `wrap`：css选择符或者jquery对象；svg对象包装元素，默认是`body`

+ `width`：svg画布的宽度

+ `height`：svg画布的高度

+ `circleStyle`：图表中节点的属性配置
	+ `fill`：填充颜色
	+ `stroke`：线条颜色
	+ `stroke-width`：线条的宽度，默认为 1
		
			circleStyle: {
				fill: '#94CFF6',
                stroke: '#82BDF5',
                'stroke-width': 1	
			}

+ `textStyle`：文字属性配置
	+ font-size：字体大小，默认14px
	+ font-family：字体
	+ fill：字体颜色
		
			textStyle: {
			    'font-size': '14px',
			    'font-family': 'Arial',
			    fill: '#fff'
			}

##数据格式

    var data = {
        'id': '0', 'title': 'A', 'childNodes': [
            { 'id': '1', 'title': 'B', 'parent': '0', 'childNodes': [
                    { 'id': '7', 'title': 'C', 'parent': '1', 'childNodes': [] },
                    { 'id': '8', 'title': 'D', 'parent': '1', 'childNodes': [] }
                ]
            },
            { 'id': '2', 'title': 'E', 'parent': '0', 'childNodes': [] },
            { 'id': '3', 'title': 'F', 'parent': '0', 'childNodes': [] },
            { 'id': '4', 'title': 'G', 'parent': '0', 'childNodes': [] },
            { 'id': '6', 'title': 'H', 'parent': '0', 'childNodes': [
                    { 'id': '9', 'title': 'I', 'parent': '6', 'childNodes': [] },
                    { 'id': '10', 'title': 'K', 'parent': '6', 'childNodes': [] }
                ]
            }
        ]
    };

    var rel = {
        '0-1':  ['hello', 'world'],
        '0-3':  'AAA'
    };

+ data对象存储着关系节点的信息，每一个节点都有唯一的`id`，节点的名称`title`，以及子节点信息`childNodes`，父节点信息`parent`；

+ rel对象存储这两个节点的关系，key是两个关系节点的id，以`-`连接起来，即`id-id`；value可以是数组或者单个字符串，是数组的话，每一个元素为一条关系，最多显示3条关系；单个字符串表示只有一条关系。

##Demo
这里要引入三个库：`jquery.js`，`raphael.js`，`underscore.js`。此外，还有一个`relation.js`和`relation.css`

###HTML

	<!doctype html>
	<html lang='en'>
	<head>
	    <meta charset='UTF-8'>
	    <title>Relations</title>
	    <link rel='stylesheet' href='relation.css'>
	    <script src='raphael.js'></script>
	    <script src='underscore.js'></script>
	    <script src='jquery-1.9.1.min.js'></script>
	    <script src='relation.js'></script>
	</head>
	
	<body>
		// wrap
		<div id='svg-view'></div>
	<script>
    $(function () {
        var json = {
            'id': '0', 'title': 'A', 'childNodes': [
                { 'id': '1', 'title': 'B', 'parent': '0', 'childNodes': [
                        { 'id': '7', 'title': 'C', 'parent': '1', 'childNodes': [] },
                        { 'id': '8', 'title': 'D', 'parent': '1', 'childNodes': [] }
                    ]
                },
                { 'id': '2', 'title': 'E', 'parent': '0', 'childNodes': [] },
                { 'id': '3', 'title': 'F', 'parent': '0', 'childNodes': [] },
                { 'id': '4', 'title': 'G', 'parent': '0', 'childNodes': [] },
                { 'id': '6', 'title': 'H', 'parent': '0', 'childNodes': [
                        { 'id': '9', 'title': 'I', 'parent': '6', 'childNodes': [] },
                        { 'id': '10', 'title': 'K', 'parent': '6', 'childNodes': [] }
                    ]
                }
            ]
        };
  
        var info = {
            '0-1':  ['hello', 'world'],
            '0-3':  'AAA'
        };

		// 实例化relation
        var relation = new Relation(json, info, { wrap:  '#svg-view' });
    })
	  </script>
	</body>
	</html>