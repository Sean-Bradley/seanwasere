# Consuming and Displaying a RSS feed with Flash AS3

In this video, I demonstrate using the native AS3 ‘URLLoader’ class to load externally hosted xml data into a native dynamic text field object placed on the flash canvas.

[![Consuming and Displaying a RSS feed with Flash AS3](https://img.youtube.com/vi/H1k954EHc88/0.jpg)](https://www.youtube.com/watch?v=H1k954EHc88)

[Consuming and Displaying a RSS feed with Flash AS3](https://www.youtube.com/watch?v=H1k954EHc88)

This is the code used from the video, and you can copy and paste it.

```
var xmlLoader:URLLoader = new URLLoader();
var xmlData:XML = new XML();
xmlLoader.addEventListener(Event.COMPLETE, LoadXML);
xmlLoader.load(new URLRequest("http://feeds.bbci.co.uk/news/rss.xml"));
function LoadXML(e:Event):void {
	xmlData = new XML(e.target.data);
 	parseData(xmlData);
}
function parseData(xmlData:XML):void {
	//txtRSSFeed.appendText(xmlData);
	for (var i:int = 0; i<xmlData.channel.item.length(); i++){
		txtRSSFeed.appendText(xmlData.channel.item[i].title + "n");
	};
}
stop();
```

If you want to know more about AS3 ‘XML’ Class

[http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/XML.html](http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/XML.html)

If you want to know more about AS3 ‘UrlLoader’ Class

[http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/URLLoader.html](http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/URLLoader.html)

If you want to know more about AS3 ‘TextField’ class

[http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/text/TextField.html](http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/text/TextField.html)

