实验四：扩展的Activity
============  
实验内容 
-----------
使用PrefereceFragment实现设置页面  
设置项说明  
总共四组设置项  
1.In-line preferences:CheckBoxPreference  

2.Dialog-based preferences:EditTextPreference、ListPreference  

3.Launch preferences:  
    (1)PreferenceScreen: 跳转到另一个PreferenceScreen  
    (2)PreferenceScreen: 启动一个网页  
    
4.Preference attributes:  
    (1)CheckBox: 父选项  
    (2)CheckBox: 子选项，当父选项勾选时呈现 

关键代码
-------- 
1.preferences.xml
```  
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">

    <PreferenceCategory
        android:key="Inline_settings"
        android:title="In-line preferences">
        <CheckBoxPreference
            android:key="checkbox"
            android:summary="This is a checkbox"
            android:title="Checkbox preference"
            android:defaultValue="true"/>
    </PreferenceCategory>

    <PreferenceCategory
        android:key="Dialog_settings"
        android:title="Dialog-based preferences">
        <EditTextPreference
            android:key="editText"
            android:title="Edit text preference"
            android:summary="An example that uses an edit text dialog"
            android:dialogTitle="Enter your favorite animal"/>

        <ListPreference
            android:key="list"
            android:title="List preferences"
            android:dialogTitle="choose one"
            android:summary="An example that uses a list dialog"
            android:entries="@array/entries_list_preference"
            android:entryValues="@array/entryValues_list_preference"/>
    </PreferenceCategory>

    <PreferenceCategory
        android:key="Launch_settings"
        android:title="Launch preferences">
        <PreferenceScreen
            android:key="screen preference"
            android:summary="shows another screen of preferences"
            android:title="Screen preference" >
            <!-- 你可以在这里放置更多的首选项内容，将被在下一个页面呈现出来 -->
            <CheckBoxPreference
                android:key="next screen checkbox preference"
                android:summary="Preference that is on the next screen but same hierarchy"
                android:title="Toggle preference" />
        </PreferenceScreen>

        <PreferenceScreen
            android:key="intent_preference"
            android:summary="launches an Activity from an Intent"
            android:title="intent preference" >
            <intent
                android:action="android.intent.action.VIEW"
                android:data="http://www.baidu.com" />
        </PreferenceScreen>
    </PreferenceCategory>

    <PreferenceCategory
        android:key="Attributes_settings"
        android:title="Preference attributes">
        <CheckBoxPreference
            android:key="parent checkbox preference"
            android:summary="This is visually a parent"
            android:title="parent checkbox preference" />

        <CheckBoxPreference
            android:dependency="parent checkbox preference"
            android:key="child_checkbox_preference"
            android:layout="?android:attr/preferenceLayoutChild"
            android:summary="This is visually a child"
            android:title="parent checkbox preference" />
    </PreferenceCategory>

</PreferenceScreen>

```  

2.preFragment.java  
```  
public class PreFragment extends PreferenceFragment {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        addPreferencesFromResource(R.xml.preferences);
    }
}  
```  
3.MainActivity.java  
```  
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        getFragmentManager().beginTransaction().replace(android.R.id.content,new PreFragment()).commit();
    }
}  
```  
结果截图  
---------------  
![image](https://github.com/grapeyu/PreferenceFragment/blob/master/img2/4.1.jpg)  

![image](https://github.com/grapeyu/PreferenceFragment/blob/master/img2/4.2.jpg)  

![image](https://github.com/grapeyu/PreferenceFragment/blob/master/img2/4.3.jpg)  

![image](https://github.com/grapeyu/PreferenceFragment/blob/master/img2/4.4.jpg)  

![image](https://github.com/grapeyu/PreferenceFragment/blob/master/img2/4.5.jpg)  

![image](https://github.com/grapeyu/PreferenceFragment/blob/master/img2/4.6.jpg)  



