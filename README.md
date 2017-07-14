# Ajax
learn Ajax
//原生Ajax(兼容)
function ajaxFunction()
 {
 var xmlHttp;
 try
    {
   // Firefox, Opera 8.0+, Safari
    xmlHttp=new XMLHttpRequest();
    }
 catch (e)
    {
  // Internet Explorer
   try
      {
      xmlHttp=new ActiveXObject("Msxml2.XMLHTTP");
      }
   catch (e)
      {
      try
         {
         xmlHttp=new ActiveXObject("Microsoft.XMLHTTP");
         }
      catch (e)
         {
         alert("您的浏览器不支持AJAX！");
         return false;
         }
      }
    }
 }
 
 //Ajax函数
 function ajax(option){
		option = option || {};
		option.type=option.type.toUpperCase() || 'POST'; // GET POST
		option.url = option.url || ''; // string 
		option.async = option.async || true; // True ,False
		option.data =option.data || null; //data
		option.success = option.success || function(){}; //
		option.error = option.error || function(){};
		var request = null;
		if(XMLHttpRequest){
			request = new XMLHttpRequest();//IE8+ Firefox Chorme Opera
		}
		else {
             xmlHttp = new ActiveXObject('Microsoft.XMLHTTP');//IE8-         
         }
		var params =[];
		for(var key in option.data ){
			params.push(key +"="+option.data[key]) //["key=value","key1=value1"]
		}
		var paramsData = params.join("&");// key=value&key1=value1
		if(option.method.toUpperCase() =="POST"){
			request.open(option.method,option.url,option.async);
			request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded;charset=utf-8')
			request.send(paramsData);
		}else if(option.method.toUpperCase() =="GET"){
			request.open(option.method,option.url+'?'+paramsData,option.async);
			request.send();
		}
		request.onreadystatechange = function(){
			if(request.readyState ===4 && request.status===200){
				option.success(JSON.parse(request.responseText))
			}esle{
				option.error(request.status)
			}
		}
	}
	
	
	//Ajax 解决跨域的解决方案
	1.服务器端使用代理
	2.JSONP (仅支持GET方式)
	3.XHR2(IE10以下不支持) 服务端添加
	  header('Access-Control-Allow-Origin:*'); //* 代表所有域可访问
	  header('Access-Control-Allow-Methods:POST,GET');
	
