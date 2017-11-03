# 大标题交互封装（BigTitleContainer）使用说明


---


## BigTitleContainer
大标题滑动交互封装，是一个布局容器
### 容器布局
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/root_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <android.support.design.widget.AppBarLayout
        android:id="@+id/appbar_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <android.support.design.widget.CollapsingToolbarLayout
            android:id="@+id/collapsing_toolbar_layout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:fitsSystemWindows="false"
            app:contentScrim="#00000000"
            app:layout_scrollFlags="scroll|exitUntilCollapsed|snap">

            <android.support.v7.widget.Toolbar
                android:id="@+id/tool_bar"
                android:layout_width="match_parent"
                android:layout_height="@dimen/common_toolbar_height"
                app:contentInsetStart="0dp"
                app:layout_collapseMode="pin">
            </android.support.v7.widget.Toolbar>

            <LinearLayout
                android:id="@+id/header_layout"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="@dimen/common_toolbar_height"
                android:background="#fff"
                android:gravity="bottom"
                android:orientation="vertical">

                <TextView
                    android:id="@+id/header_tv"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginBottom="15dp"
                    android:layout_marginLeft="15dp"
                    android:layout_marginRight="15dp"
                    android:layout_marginTop="30dp"
                    android:background="#fff"
                    android:gravity="center"
                    tools:text="标题"
                    android:textColor="#333"
                    android:textSize="32sp"/>

            </LinearLayout>

        </android.support.design.widget.CollapsingToolbarLayout>

    </android.support.design.widget.AppBarLayout>

    <LinearLayout
        android:id="@+id/nested_scrolling_child_container"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_behavior="@string/appbar_scrolling_view_behavior">

    </LinearLayout>
</android.support.design.widget.CoordinatorLayout>


```

### 涉及到相关方法

```
public Toolbar toolBar; //标题栏容器
public LinearLayout headerLayout;//大标题容器
public TextView headerTv; //大标题TextView
public LinearLayout contentContainer;//内容容器


//设置大标题
public void setBigTitle(String title)

//设置titleBar上标题大小（单位sp）
public void setTitleBarSizeSp()

//设置TitleBar上标题大小（单位px）
public void setTitleBarSizePx()

//设置大标题大小（单位sp）
public void setBigTitleSizeSp()

//设置大标题大小（单位px）
public void setBigTitleSizePx()

//设置titleBar大小（放在一个Toolbar里面）
public void setTitleBar(View view)

//设置页面具体内容
public View setContentView(int resource)

//设置页面具体内容
public void setContentView(View view)

//设置二级tab导航栏
public void setTabView(View view)
```

## SimpleBigTitleActivity
是个抽象类，继承于MBaseActivity<V, T>，是对Activity中使用BigTitleContainer的简单封装

```
protected BigTitleContainer mBigTitleContainer;
protected TitleBar mTitleBar;
protected View mainView;


//设置标题内容
public abstract String getBigTitle();

//设置页面具体内容的布局
public abstract int getContentLayoutId();
 
 //设置标题栏，默认已经包含一个公共标题栏
 
 public void setTitleBar(View titleBar)
```

## SimpleBigTitleFragment 
是个抽象类，继承于MBaseFragment<V, T>，是对Fragment中使用BigTitleContainer的简单封装

```
protected BigTitleContainer mBigTitleContainer;
protected TitleBar mTitleBar;
protected View mainView;

//设置标题内容
public abstract String getBigTitle();

//设置页面具体内容的布局
public abstract int getContentLayoutId();
 
 //设置标题栏，默认已经包含一个公共标题栏
 
 public void setTitleBar(View titleBar)

```

## TitleBar
TitleBar是根据绿城app旧版本顶部标题栏布局做的标题栏封装，内部布局文件view_title_bar.xml跟绿城head_save_view.xml一模一样
### head_save_view.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="wrap_content"
              android:background="@color/common_color_back_white"
              android:orientation="vertical">

    <FrameLayout
        android:layout_width="fill_parent"
        android:layout_height="@dimen/common_toolbar_height"
        android:orientation="vertical">

        <LinearLayout
            android:id="@+id/ler_back"
            android:layout_width="65dp"
            android:layout_height="fill_parent"
            android:layout_marginLeft="15dp"
            android:gravity="center_vertical"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/iv_back"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <TextView
                android:id="@+id/head_left_tv"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:singleLine="true"
                android:textColor="@color/common_color_font_black"
                android:textSize="15sp"/>
        </LinearLayout>

        <TextView
            android:id="@+id/title_text"
            android:layout_width="wrap_content"
            android:layout_height="fill_parent"
            android:layout_gravity="center"
            android:layout_marginLeft="10dp"
            android:layout_marginRight="10dp"
            android:ellipsize="end"
            android:maxLines="1"
            android:textColor="@color/common_color_font_black"
            android:textSize="@dimen/common_font_title"
            android:textStyle="normal"
            android:visibility="visible"/>

        <LinearLayout
            android:id="@+id/ler_save"
            android:layout_width="wrap_content"
            android:layout_height="fill_parent"
            android:layout_gravity="right|center_vertical"
            android:layout_marginRight="10dp"
            android:gravity="right|center_vertical"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/head_info"
                android:layout_width="25dp"
                android:layout_height="25dp"/>

            <TextView
                android:id="@+id/head_right_tv"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:textColor="@color/common_color_font_black"
                android:textSize="15sp"/>
        </LinearLayout>
    </FrameLayout>

    <View
        android:layout_width="fill_parent"
        android:layout_height="@dimen/common_divide_line"
        android:background="@color/common_color_divideline_color"/>

</LinearLayout>
```
### TitleBar内部一些主要的属性方法
```
    //左边布局
    public LinearLayout leftLayout;
    //左边返回按钮
    public ImageView backIv;
    //左边文字
    public TextView leftTv;
    //中间标题
    public TextView titleTv;
    //右边布局
    public LinearLayout rightLayout;
    //右边图标
    public ImageView rightIv;
    //右边文字
    public TextView rightTv;
    //是否有返回按钮标识
    private boolean hasBack = true;
    
    //设置是否有左边返回按钮
    public void setHasBack(boolean hasBack)
    customStyleWithLeft()
    customStyleWithRight()
    customStyleWithBoth()
    ...
    这些方法跟绿城旧的标题工具类StyleUtil类统一
```

### **使用注意**:
绿城旧版本的标题栏，大部分是通过在布局里inclue添加head_save_view.xml，
结合StyleUtil工具类来实现的，有部分页面未使用StyleUtil工具类，自己获取相应的View来定义。
这次修改时，如果使用了BigTitleContainer，结合TitleBar，则不再需要head_save_view.xml，
可以将head_save_view.xml内部view全部去掉既可，这样感觉改动比较小
  


