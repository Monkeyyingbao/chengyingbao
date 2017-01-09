下拉级联是我们在开发中经常会遇到的问题，下面结合单选选择监听，动态控制下级下拉框内容的渲染，通过一个实例进行说明如何实现这一需求。

1.布局文件：

	<?xml version="1.0" encoding="utf-8"?>
	<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent">
	
	    <Spinner
	        android:id="@+id/spinner_season"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content" />
	    <Spinner
	        android:id="@+id/spinner_month"
	        android:layout_width="wrap_content"
	        android:prompt="@string/month"
	        android:layout_toRightOf="@+id/spinner_season"
	        android:layout_height="wrap_content" />
	</RelativeLayout>

2.MainActivity 代码：

	public class MainActivity extends Activity {
	    private Spinner spinner_season,spinner_month;
	    ArrayAdapter <String> adapter_season,adapter_month;
	    private List<String> list_season;
	    String   months[][]={{"一月","二月","三月"},{"四月","五月","六月"},{"七月","八月","九月"},{"十月","十一月","十二月"}};
	
	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);
	        spinner_season=(Spinner)findViewById(R.id.spinner_season);
	        spinner_month=(Spinner)findViewById(R.id.spinner_month);
	        spinner_season.setPrompt("请选择季节");
	        initDatas();
	        adapter_season=new ArrayAdapter<String>(this,android.R.layout.simple_list_item_1,list_season);
	        spinner_season.setAdapter(adapter_season);
	        spinner_season.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
	            @Override
	            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
	                adapter_month=new ArrayAdapter<String>(MainActivity.this,android.R.layout.simple_list_item_1,months[position]);//通过二维数组及position的值动态决定下级菜单的数据源
	                adapter_month.setDropDownViewResource(android.R.layout.simple_list_item_single_choice);//设置下拉显示样式
	                spinner_month.setAdapter(adapter_month);
	            }
	
	            @Override
	            public void onNothingSelected(AdapterView<?> parent) {
	
	            }
	        });
	
	    }
	
	    private void initDatas() {
	        list_season=new ArrayList<String>();
	        list_season.add("春季");
	        list_season.add("夏季");
	        list_season.add("秋季");
	        list_season.add("冬季");
	
	    }
	}

这里定义了一个二维数组，在覆写的onItemSelected方法中根据传入的position的值动态决定下级列表框的数据源，从而实现数据级联的效果。这里还利用Spinner的setDropDownViewResource方法设置了下拉显示样式