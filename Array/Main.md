
- ### 代码

```java

package interview.array;
	
	import freemarker.cache.ClassTemplateLoader;
	import freemarker.template.Configuration;
	import freemarker.template.Template;
	import freemarker.template.TemplateException;
	import freemarker.template.TemplateExceptionHandler;
	
	import java.io.*;
	import java.nio.charset.Charset;
	import java.util.HashMap;
	import java.util.Map;
	
	public class Main {
	
	    public static void main(String[] args) throws IOException, TemplateException {
	        Configuration cfg = new Configuration(Configuration.VERSION_2_3_22);
	
	        //璇诲彇resources璧勬簮鏂囦欢涓嬬殑妯＄増鏂囦欢
	        cfg.setTemplateLoader(new ClassTemplateLoader(Main.class, "/templates"));
	        cfg.setDefaultEncoding("UTF-8");
	        cfg.setTemplateExceptionHandler(TemplateExceptionHandler.RETHROW_HANDLER);
	        Template template = cfg.getTemplate("template.ftl");
	
	        File file = new File("G:\\workspace\\interview\\src\\main\\java\\interview\\array");
	
	        File[] files = file.listFiles();
	        String rootPath = "F:\\GitHub\\leetcode_node\\Array";
	
	        for(File f : files){
	            String fNAME = rootPath + "\\"+f.getName().substring(0,f.getName().lastIndexOf(".java"))+".md";
	            FileWriter fileWriter = new FileWriter(fNAME);
	            Map<String,String> map = new HashMap<>();
	            map.put("code",readFile(f));
	            template.process(map,fileWriter);
	            fileWriter.close();
	        }
	
	    }
	
	    private static String readFile(File file) throws IOException {
	        //FileWriter fileWriter = new FileWriter(file);
	        InputStream inputStream = new FileInputStream(file);
	        InputStreamReader inputStreamReader = new InputStreamReader(inputStream,Charset.forName("gbk"));
	        BufferedReader reader  = new BufferedReader(inputStreamReader);
	        String str = null;
	        StringBuilder sb = new StringBuilder();
	        while((str = reader.readLine()) != null){
	            sb.append(str).append("\n\t");
	        }
	        return sb.toString();
	    }
	}
	

```