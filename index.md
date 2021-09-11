# 保存图片到相册

```
$(".share .save-gallery").click(function(){

		var imgsrc = $(".poster_box").find('img').attr('src');
		if(imgsrc==''||imgsrc==undefined){
			alert(langData['siteConfig'][44][94]);//下载失败，请重试
			return 0
		}
		var b=new plus.nativeObj.Bitmap();

		b.loadBase64Data(imgsrc,function(){
			console.log("创建成功");
		},function(){
			console.log("创建失败");
		});
		b.save('_www/img1.jpg',{overwrite:true},function(){
			console.log("保存成功");
		},function(){
			console.log("保存失败");
		});

		plus.gallery.save( '_www/img1.jpg', function () {
			alert( "保存图片到相册成功" );
		},function(){
			alert( "保存图片到相册失败" )});


	});
```

# 微信分享

```
// 缩略图形式

$(".share .weixin-share").click(function(){
		// 获取分享服务
		plus.share.getServices(function(s){
			var sweixin = s[0];
			sweixin.send( {
				type: 'web',
				title: wxconfig.title,
				content:wxconfig.description,
				href: wxconfig.link,
				thumbs: [wxconfig.imgUrl],
				pictures:[wxconfig.imgUrl],

				extra:{scene:"WXSceneSession"}}, function(){
				alert("分享成功！");
			}, function(e){
				alert("分享失败："+e.message);
			});

		}, function(e){
			alert("获取分享服务列表失败： "+JSON.stringify(e));
		});
	});
	
// 分享图片

    $(".share .weixin-share").click(function () {

        var imgsrc = $(".swiper-slide-active .drawImg").find('img').attr('src');
        var b = new plus.nativeObj.Bitmap('poster');
        b.loadBase64Data(imgsrc,function(){
            console.log("创建成功");
        },function(){
            console.log("创建失败");
        });

        b.save('_www/poster.png',{overwrite:true},function(){
            // 获取分享服务
            plus.share.getServices(function(s){
                var sweixin = s[0];
                sweixin.send( {
                    type: 'image',
                    pictures:["_www/poster.png"],
                    extra:{scene:"WXSceneSession"}}, function(){
                    alert("分享成功！");
                }, function(e){
                    alert("分享失败："+e.message);
                });

            }, function(e){
                alert("获取分享服务列表失败： "+JSON.stringify(e));
            });
        },function(){
            console.log("保存失败");
        });


    });

```
