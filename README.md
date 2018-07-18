Huawei Mobile WiFi LTE Band Selector

Enable LTE band selection within your browser. 

# Working Environment
## Supported devices
Tested on these Huawei devices.
1. E5778
2. E5885 (Global-one egg in Korea)

##Supported clients
Every JS supported modern browsers.

Tested on these clients.
Mac OS Safari, Chrome
iOS Safari

# How-to
1. First go on to your MobileWifi page. (Ex. 192.168.8.1)
2. Log-in to your device.
3. Run these javascript. 
If you add this script to "Bookmark", you can use this tool in iOS Safari.

## Show current LTE band & signal
```javascript
javascript:currentBand();function currentBand(){$.ajax({type:"GET",async:true,url:"/api/device/signal",error:function(request,status,error){alert("Signal Error:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error)},success:function(data){var report="";report=report+"RSRQ/RSRP/SINR :"+extractXML("rsrq",data)+"/"+extractXML("rsrp",data)+"/"+extractXML("sinr",data);report=report+"\nBand : "+extractXML("band",data)+" - "+extractXML("dlbandwidth",data);report=report+"\nEARFCN : "+extractXML("earfcn",data);alert(report)}})}function extractXML(tag,data){try{return data.split("</"+tag+">")[0].split("<"+tag+">")[1]}catch(err){return err.message}}function ltebandselection(){if(arguments.length==0){var band=prompt("Please input desirable LTE band number. If you want to use multiple LTE bands, write down multiple band number joined with '+'. If you want to use every supported bands, write down 'ALL'. (Ex. SKT 1+3+5+7 / KT 1+3+8 / LG U+ 1+5+7)","ALL");if(band==null||band===""){return}}else var band=arguments[0];if(!window.location.href.includes("/html/home.html")){alert("You can use this function only in main page.");return}else{var bs=band.split("+");var ltesum=0;if(band.toUpperCase()==="ALL"){ltesum="7FFFFFFFFFFFFFFF"}else{for(var i=0;i<bs.length;i++){ltesum=ltesum+Math.pow(2,parseInt(bs[i])-1)}ltesum=ltesum.toString(16);console.log("LTEBand:"+ltesum)}$.ajax({type:"GET",async:true,url:"/html/home.html",error:function(request,status,error){alert("Token Error:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error)},success:function(data){var datas=data.split('name="csrf_token" content="');var token=datas[datas.length-1].split('"')[0];setTimeout(function(){$.ajax({type:"POST",async:true,url:"/api/net/net-mode",headers:{__RequestVerificationToken:token},contentType:"application/xml",data:"<request><NetworkMode>03</NetworkMode><NetworkBand>3FFFFFFF</NetworkBand><LTEBand>"+ltesum+"</LTEBand></request>",success:function(nd){alert(nd)},error:function(request,status,error){alert("Net Mode Error:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error)}})},2e3)}})}}
```

## LTE Band Selection
![Alt text](/img1.png)
```javascript
javascript:ltebandselection();function currentBand(){$.ajax({type:"GET",async:true,url:"/api/device/signal",error:function(request,status,error){alert("Signal Error:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error)},success:function(data){var report="";report=report+"RSRQ/RSRP/SINR :"+extractXML("rsrq",data)+"/"+extractXML("rsrp",data)+"/"+extractXML("sinr",data);report=report+"\nBand : "+extractXML("band",data)+" - "+extractXML("dlbandwidth",data);report=report+"\nEARFCN : "+extractXML("earfcn",data);alert(report)}})}function extractXML(tag,data){try{return data.split("</"+tag+">")[0].split("<"+tag+">")[1]}catch(err){return err.message}}function ltebandselection(){if(arguments.length==0){var band=prompt("Please input desirable LTE band number. If you want to use multiple LTE bands, write down multiple band number joined with '+'. If you want to use every supported bands, write down 'ALL'. (Ex. SKT 1+3+5+7 / KT 1+3+8 / LG U+ 1+5+7)","ALL");if(band==null||band===""){return}}else var band=arguments[0];if(!window.location.href.includes("/html/home.html")){alert("You can use this function only in main page.");return}else{var bs=band.split("+");var ltesum=0;if(band.toUpperCase()==="ALL"){ltesum="7FFFFFFFFFFFFFFF"}else{for(var i=0;i<bs.length;i++){ltesum=ltesum+Math.pow(2,parseInt(bs[i])-1)}ltesum=ltesum.toString(16);console.log("LTEBand:"+ltesum)}$.ajax({type:"GET",async:true,url:"/html/home.html",error:function(request,status,error){alert("Token Error:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error)},success:function(data){var datas=data.split('name="csrf_token" content="');var token=datas[datas.length-1].split('"')[0];setTimeout(function(){$.ajax({type:"POST",async:true,url:"/api/net/net-mode",headers:{__RequestVerificationToken:token},contentType:"application/xml",data:"<request><NetworkMode>03</NetworkMode><NetworkBand>3FFFFFFF</NetworkBand><LTEBand>"+ltesum+"</LTEBand></request>",success:function(nd){alert(nd)},error:function(request,status,error){alert("Net Mode Error:"+request.status+"\n"+"message:"+request.responseText+"\n"+"error:"+error)}})},2e3)}})}}
```

## Thanks to 
https://github.com/0xAA/Huawei_Tool