# SDK/API
## 百度SDK
### 百度sdk初始化
androidStudio查看sha1

![enter description here][1]

![enter description here][2]

其中test2的appkey为我电脑的（每台电脑不同）
下载SDK
http://wiki.lbsyun.baidu.com/cms/androidsdk/all/v4.1.1/BaiduMap_AndroidSDK_v4.1.1_All.zip
填写AppKey:
```
<application
        android:name=".Application">
         <meta-data
            android:name="com.baidu.lbsapi.API_KEY"
            android:value="申请的AppKey" />
            </application>
```
application:
```
SDKInitializer.initialize(this);
```
gradle_app
```
android {
 sourceSets {
        main {
            jniLibs.srcDir 'libs'
        }
    }
}
```
权限
```
uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="com.android.launcher.permission.READ_SETTINGS" />
    <uses-permission android:name="android.permission.WAKE_LOCK"/>
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.GET_TASKS" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
```
### 百度地图
layout:
```
<FrameLayout
        android:id="@+id/map"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```
```
@SuppressWarnings("unused")
    SupportMapFragment map;
private void initMap() {
        Intent intent = getIntent();
        MapStatus.Builder builder = new MapStatus.Builder();
        if (intent.hasExtra("x") && intent.hasExtra("y")) {
            // 当用intent参数时，设置中心点为指定点
            Bundle b = intent.getExtras();
            LatLng p = new LatLng(b.getDouble("y"), b.getDouble("x"));
            builder.target(p);
        }
        builder.overlook(-20).zoom(15);
        BaiduMapOptions bo = new BaiduMapOptions().mapStatus(builder.build())
                .compassEnabled(false).zoomControlsEnabled(false);
        map = SupportMapFragment.newInstance(bo);
        FragmentManager manager = getSupportFragmentManager();
        manager.beginTransaction().add(R.id.map, map, "map_fragment").commit();
    }
```

## 讯飞语音识别SDK
sdk下载地址http://www.xfyun.cn/sdk/dispatcher
![enter description here][3]
导入libs里的文件

armeab/libmsc.so
Msc.jar
导入assets里的文件夹iflytek至项目assets中(麦克风对话框所需)

修改gradle_app的jniLibs目录
```
android {
 sourceSets {
        main {
            jniLibs.srcDir 'libs'
        }
    }
}
```
权限:
```
<!--连接网络权限，用于执行云端语音能力 -->
    <uses-permission android:name="android.permission.INTERNET"/>
    <!--获取手机录音机使用权限，听写、识别、语义理解需要用到此权限 -->
    <uses-permission android:name="android.permission.RECORD_AUDIO"/>
    <!--读取网络信息状态 -->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <!--获取当前wifi状态 -->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <!--允许程序改变网络连接状态 -->
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/>
    <!--读取手机信息权限 -->
    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
    <!--读取联系人权限，上传联系人需要用到此权限 -->
    <uses-permission android:name="android.permission.READ_CONTACTS"/>
```
Application所需添加/
```
SpeechUtility.createUtility(this, SpeechConstant.APPID +"=583eaf20");
```
```
import org.json.JSONArray;
import org.json.JSONObject;
import org.json.JSONTokener;

/**
 * Json结果解析类
 */
public class JsonParser {

	public static String parseIatResult(String json) {
		StringBuffer ret = new StringBuffer();
		try {
			JSONTokener tokener = new JSONTokener(json);
			JSONObject joResult = new JSONObject(tokener);

			JSONArray words = joResult.getJSONArray("ws");
			for (int i = 0; i < words.length(); i++) {
				// 转写结果词，默认使用第一个结果
				JSONArray items = words.getJSONObject(i).getJSONArray("cw");
				JSONObject obj = items.getJSONObject(0);
				ret.append(obj.getString("w"));
//				如果需要多候选结果，解析数组其他字段
//				for(int j = 0; j < items.length(); j++)
//				{
//					JSONObject obj = items.getJSONObject(j);
//					ret.append(obj.getString("w"));
//				}
			}
		} catch (Exception e) {
			e.printStackTrace();
		} 
		return ret.toString();
	}
	
	public static String parseGrammarResult(String json) {
		StringBuffer ret = new StringBuffer();
		try {
			JSONTokener tokener = new JSONTokener(json);
			JSONObject joResult = new JSONObject(tokener);

			JSONArray words = joResult.getJSONArray("ws");
			for (int i = 0; i < words.length(); i++) {
				JSONArray items = words.getJSONObject(i).getJSONArray("cw");
				for(int j = 0; j < items.length(); j++)
				{
					JSONObject obj = items.getJSONObject(j);
					if(obj.getString("w").contains("nomatch"))
					{
						ret.append("没有匹配结果.");
						return ret.toString();
					}
					ret.append("【结果】" + obj.getString("w"));
					ret.append("【置信度】" + obj.getInt("sc"));
					ret.append("\n");
				}
			}
		} catch (Exception e) {
			e.printStackTrace();
			ret.append("没有匹配结果.");
		} 
		return ret.toString();
	}
	
	public static String parseLocalGrammarResult(String json) {
		StringBuffer ret = new StringBuffer();
		try {
			JSONTokener tokener = new JSONTokener(json);
			JSONObject joResult = new JSONObject(tokener);

			JSONArray words = joResult.getJSONArray("ws");
			for (int i = 0; i < words.length(); i++) {
				JSONArray items = words.getJSONObject(i).getJSONArray("cw");
				for(int j = 0; j < items.length(); j++)
				{
					JSONObject obj = items.getJSONObject(j);
					if(obj.getString("w").contains("nomatch"))
					{
						ret.append("没有匹配结果.");
						return ret.toString();
					}
					ret.append("【结果】" + obj.getString("w"));
					ret.append("\n");
				}
			}
			ret.append("【置信度】" + joResult.optInt("sc"));

		} catch (Exception e) {
			e.printStackTrace();
			ret.append("没有匹配结果.");
		} 
		return ret.toString();
	}
}
```
```
@Bind(R.id.button)
    Button mButton;
    @Bind(R.id.editText)
    EditText mEditText;
    @Override
    public void initViews(Bundle bundle) {
        initXunFei();
    }
    private InitListener mInitListener = new InitListener() {

        @Override
        public void onInit(int code) {
            Log.d(TAG, "SpeechRecognizer init() code = " + code);
            if (code != ErrorCode.SUCCESS) {
                Toast.makeText(XunFeiActivity.this,"初始化失败，错误码：" + code, Toast.LENGTH_SHORT).show();
            }
        }
    };
    private RecognizerDialogListener mRecognizerDialogListener = new RecognizerDialogListener() {
        public void onResult(RecognizerResult results, boolean isLast) {
            printResult(results);
        }
        public void onError(SpeechError error) {
            Toast.makeText(XunFeiActivity.this,error.getPlainDescription(true), Toast.LENGTH_SHORT).show();
        }

    };
    private HashMap<String, String> mIatResults = new LinkedHashMap<String, String>();

    private void printResult(RecognizerResult results) {
        String text = JsonParser.parseIatResult(results.getResultString());

        String sn = null;
        // 读取json结果中的sn字段
        try {
            JSONObject resultJson = new JSONObject(results.getResultString());
            sn = resultJson.optString("sn");
        } catch (JSONException e) {
            e.printStackTrace();
        }
        mIatResults.put(sn, text);
        StringBuffer resultBuffer = new StringBuffer();
        for (String key : mIatResults.keySet()) {
            resultBuffer.append(mIatResults.get(key));
        }

        mEditText.setText(resultBuffer.toString());
        mEditText.setSelection(mEditText.length());
    }
    private void initXunFei() {
        mButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //1.创建SpeechRecognizer对象，第二个参数：本地听写时传InitListener
                RecognizerDialog iatDialog = new RecognizerDialog(XunFeiActivity.this, mInitListener);
                //2.设置听写参数，同上节
                //3.设置回调接口
                iatDialog.setListener(mRecognizerDialogListener);
                //4.开始听写
                iatDialog.show();
            }
        });
    }
    @Override
    public void initToolBar() {

    }
```

## IjkPlayerView
Bilibili的开源视频播放器组件，含弹幕组件
库以及，弹幕资源已放入内部文件夹
如需修改播放器，请自行修改，如加载进度条、等待进度条在color资源文件修改
### 正确食用姿势：
1.小屏/全屏可任意切换
```
private static final String VIDEO_URL = "http://flv2.bn.netease.com/videolib3/1611/28/GbgsL3639/SD/movie_index.m3u8";
    private static final String VIDEO_HD_URL = "http://flv2.bn.netease.com/videolib3/1611/28/GbgsL3639/HD/movie_index.m3u8";
    private static final String IMAGE_URL = "http://vimg2.ws.126.net/image/snapshot/2016/11/I/M/VC62HMUIM.jpg";
    private IjkPlayerView mPlayerView;
	private void initIjkPlayerView() {
	//请使用注解
        mPlayerView = (IjkPlayerView) findViewById(R.id.IjkPlayerView);
        Glide.with(this).load(IMAGE_URL).fitCenter().into(mPlayerView.mPlayerThumb);
        mPlayerView.init()
                .setTitle("这是个跑马灯TextView，标题要足够长才会跑。-(゜ -゜)つロ 乾杯~")
                //各种质量视频地址
                .setVideoSource(null, VIDEO_URL, VIDEO_HD_URL, null, null)
                //从上次记录1分钟开始播放
                .setSkipTip(1000*60*1)
                //播放高质量的视频，第3个
                .setMediaQuality(IjkPlayerView.MEDIA_QUALITY_HIGH)
                //启用弹幕库
                .enableDanmaku()
                .setDanmakuSource(getResources().openRawResource(R.raw.bili));
    }
	@Override
    public void onConfigurationChanged(Configuration newConfig) {
        super.onConfigurationChanged(newConfig);
        mPlayerView.configurationChanged(newConfig);
    }
```

layout:
```
<com.dl7.player.media.IjkPlayerView
        android:id="@+id/IjkPlayerView"
        android:layout_width="match_parent"
        android:layout_height="200dp"/>
```
onCreate函数中
        initIjkPlayerView();
2.全屏模式
```
 private static final String VIDEO_URL = "http://flv2.bn.netease.com/videolib3/1611/28/nNTov5571/SD/nNTov5571-mobile.mp4";
    private static final String IMAGE_URL = "http://vimg3.ws.126.net/image/snapshot/2016/11/C/T/VC628QHCT.jpg";
    IjkPlayerView mPlayerView;
    private void initIjkPlayerView() {
        mPlayerView = new IjkPlayerView(this);
        Glide.with(this).load(IMAGE_URL).fitCenter().into(mPlayerView.mPlayerThumb);
        mPlayerView.init()
                .setTitle("这是个跑马灯TextView，标题要足够长才会跑。-(゜ -゜)つロ 乾杯~")
                .setVideoPath(VIDEO_URL)
                .alwaysFullScreen()
                .enableOrientation()
                .enableDanmaku()
                .setDanmakuSource(getResources().openRawResource(R.raw.bili))
                .start();
    }
```
onCreate函数中
setContentView(mPlayerView);
        initIjkPlayerView();
		
以上代码均使用第一种弹幕方式				
以下代码上述方式皆需要
```
    @Override
    protected void onResume() {
        super.onResume();
        mPlayerView.onResume();
    }

    @Override
    protected void onPause() {
        super.onPause();
        mPlayerView.onPause();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        mPlayerView.onDestroy();
    }

    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {
        if (mPlayerView.handleVolumeKey(keyCode)) {
            return true;
        }
        return super.onKeyDown(keyCode, event);
    }

    @Override
    public void onBackPressed() {
        if (mPlayerView.onBackPressed()) {
            return;
        }
        super.onBackPressed();
    }
```
### 弹幕
onCreate:
```
mIvSend.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //发射弹幕
                mPlayerView.sendDanmaku(mEditText.getText().toString(), false);
                mEditText.setText("");
                _closeSoftInput();
            }
        });
        mEditText.setOnFocusChangeListener(new View.OnFocusChangeListener() {
            @Override
            public void onFocusChange(View view, boolean isFocus) {
                if (isFocus) {
                    mPlayerView.editVideo();
                }
                mIsFocus = isFocus;
            }
        });
```
```
 @Override
    public boolean dispatchTouchEvent(MotionEvent ev) {
        View view = getCurrentFocus();
        if (_isHideSoftInput(view, (int) ev.getX(), (int) ev.getY())) {
            _closeSoftInput();
            return true;
        }
        return super.dispatchTouchEvent(ev);
    }

    private void _closeSoftInput() {
        mEditText.clearFocus();
        SoftInputUtils.closeSoftInput(this);
        mPlayerView.recoverFromEditVideo();
    }

    private boolean _isHideSoftInput(View view, int x, int y) {
        if (view == null || !(view instanceof EditText) || !mIsFocus) {
            return false;
        }
        return x < mEtLayout.getLeft() ||
                x > mEtLayout.getRight() ||
                y < mEtLayout.getTop();
    }
```
#### 第二种弹幕
```
InputStream stream = null;
        try {
            stream = getAssets().open("custom.json");
        } catch (IOException e) {
            e.printStackTrace();
        }
        Glide.with(this).load(IMAGE_URL).fitCenter().into(mPlayerView.mPlayerThumb);
        mPlayerView.init()
                .setTitle("这是个跑马灯TextView，标题要足够长才会跑。-(゜ -゜)つロ 乾杯~")
                .enableDanmaku()
//                .setDanmakuCustomParser(new AcFunDanmakuParser(), AcFunDanmakuLoader.instance(), null)
                // 注意 setDanmakuCustomParser() 要在 setDanmakuSource() 前调用
                .setDanmakuCustomParser(new DanmakuParser(), DanmakuLoader.instance(), DanmakuConverter.instance())
                .setDanmakuSource(stream)
                .setVideoPath(VIDEO_URL)
                .setDanmakuListener(new OnDanmakuListener<DanmakuData>() {
                    @Override
                    public boolean isValid() {
                        // TODO: 这里可以控制全屏模式下的是否可以发射弹幕，返回 true 才能发射，可判断用户是否登录
                        Log.w("CustomDanmakuActivity", "准备发射弹幕");
                        return true;
                    }

                    @Override
                    public void onDataObtain(DanmakuData data) {
                        // 添加个人信息
                        data.userName = "LONG";
                        data.userLevel = 2;
                        // 这个转换的数据格式 DanmakuData 需要配合 DanmakuConverter 来实现，如果没有设置转换器则默认返回 BaseDanmaku
                        Log.e("CustomDanmakuActivity", data.toString());
                        // GsonHelper.object2JsonStr(data)转换为Json字符串，可以直接保存到文件或服务器，参考{assets/custom.json}文件
                        Log.e("CustomDanmakuActivity", GsonHelper.object2JsonStr(data));
                    }
                });
```

RecyclerView中设置播放视频超出视野外时右下角弹出view播放视频
```
videoList.addOnChildAttachStateChangeListener(new RecyclerView.OnChildAttachStateChangeListener() {
            @Override
            public void onChildViewAttachedToWindow(View view) {
                int index = videoList.getChildAdapterPosition(view);
                view.findViewById(R.id.showview).setVisibility(View.VISIBLE);
                if (index == postion) {
                    FrameLayout frameLayout = (FrameLayout) view.findViewById(R.id.layout_video);
                    frameLayout.removeAllViews();
                    if (videoItemView != null &&
                            ((videoItemView.isPlay()) || videoItemView.VideoStatus() == IjkVideoView.STATE_PAUSED)) {
                        view.findViewById(R.id.showview).setVisibility(View.GONE);
                    }

                    if (videoItemView.VideoStatus() == IjkVideoView.STATE_PAUSED) {
                        if (videoItemView.getParent() != null)
                            ((ViewGroup) videoItemView.getParent()).removeAllViews();
                        frameLayout.addView(videoItemView);
                        return;
                    }

                    if (smallLayout.getVisibility() == View.VISIBLE && videoItemView != null && videoItemView.isPlay()) {
                        smallLayout.setVisibility(View.GONE);
                        videoLayout.removeAllViews();
                        videoItemView.setShowContoller(true);
                        frameLayout.addView(videoItemView);
                    }
                }
            }

            @Override
            public void onChildViewDetachedFromWindow(View view) {
                int index = videoList.getChildAdapterPosition(view);
                if (index == postion) {
                    FrameLayout frameLayout = (FrameLayout) view.findViewById(R.id.layout_video);
                    frameLayout.removeAllViews();
                    if (smallLayout.getVisibility() == View.GONE && videoItemView != null
                            && videoItemView.isPlay()) {
                        videoLayout.removeAllViews();
                        videoItemView.setShowContoller(true);
                        videoLayout.addView(videoItemView);
                        smallLayout.setVisibility(View.VISIBLE);
                    }
                }
            }
        });
    }
```

  [1]: ./images/1480438421636.jpg "1480438439355.jpg"
  [2]: ./images/1480438439355.jpg "1480438421636.jpg"
  [3]: ./images/1480507419140.jpg "1480507419140.jpg"