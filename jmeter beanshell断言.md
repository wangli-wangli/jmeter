从csv文件中获得请求参数，将获得响应的请求参数存储到output文件中
```
import org.json.*;
import org.apache.jmeter.samplers.SampleResult;

//获取上一个请求的返回值
String response = prev.getResponseDataAsString();
//将返回值转换为json
JSONObject responseJson = new JSONObject(response);
//获取responseMessage
JSONObject result = responseJson.getJSONObject("result");
JSONObject data = result.getJSONObject("data");
int total = (int)data.get("total");
if(total!=0){
	//获取请求参数中的关键词
	String samplerData= prev.getSamplerData(); 
	samplerData=samplerData.substring(samplerData.indexOf("{"));
	int index1=samplerData.indexOf(":");
	int index2=samplerData.indexOf(",");
	String keyword=samplerData.substring(index1+2,index2-1);
	Failure = true; 
    FailureMessage = "关键词:"+keyword;

//写进csv文件
    FileWriter fstream = new FileWriter("C:/Users/lenovo/Desktop/新建文件夹/output.csv",true); //写入数据到文件
BufferedWriter out = new BufferedWriter(fstream);
//","体现在csv文档中就是向右移一个单元格
out.write(keyword); 
//换行
out.write(System.getProperty("line.separator"));
out.close();
fstream.close();
}
```
