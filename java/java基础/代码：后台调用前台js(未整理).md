```javascript
function add(a,b){
	return a + b +number;	
}

function test(){
	return "sss";
}
```

```javascript
			// 获取JS执行引擎
			ScriptEngine se = new ScriptEngineManager().getEngineByName("javascript");
			// 获取变量
			Bindings bindings = se.createBindings();
			bindings.put("number", 3);
			se.setBindings(bindings, ScriptContext.ENGINE_SCOPE);
			Scanner sc = new Scanner(System.in);
			while (sc.hasNextInt()) {
				int a = sc.nextInt();
				int b = sc.nextInt();
				System.out.println("输入的参数【" + a + "】 + 【" + b + "】");
				se.eval(new FileReader("F:\\workspace\\sunon-qis6.2\\amb\\js\\test.js"));
				// 是否可调用
				if (se instanceof Invocable) {
					Invocable in = (Invocable) se;
					String result =  in.invokeFunction("add", a, b).toString();
					System.out.println("获得的结果：" + result);
					
				}
	 
			}
```

```javascript
			//得到ScriptEngine 对象 
			ScriptEngineManager manger = new ScriptEngineManager();
			ScriptEngine engine = manger.getEngineByName("JavaScript");
	        // 读js文件  
	        String jsFile = "F:\\workspace\\sunon-qis6.2\\amb\\js\\workflow-form-0.9.js";  
	        FileInputStream fileInputStream = new FileInputStream(new File(jsFile));
	        Reader scriptReader = new InputStreamReader(fileInputStream, "utf-8"); 
	        try  
	        {  
	            engine.eval(scriptReader);
	            if (engine instanceof Invocable)  
	            {  
	                // 调用JS方法  
	                Invocable invocable = (Invocable)engine;  
	                //test为js中的函数名,也可以在test后边","号分割传参数
	                String result = (String)invocable.invokeFunction("submitForm");
	                System.out.println(result);  
	            }  
	        }  
	        catch (Exception e)  
	        {  
	            e.printStackTrace();  
	        }  
	        finally  
	        {  
	            scriptReader.close();  
	        }
```
