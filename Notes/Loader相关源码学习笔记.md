最近项目用到了LoaderManager+Loader加载数据，同时在阅读Android源码时发现其中使用LoaderManager+Loader加载数据的情况数不胜数，于是趁热打铁，学习一下相关源码。

首先根据源码简单画一下LoaderManager+Loader的大致框架（水平尚待提高，如有错误望指点）
![Loader概要](http://img.blog.csdn.net/20160522235354315)

源码位置：
frameworks/base/core/java/android/content
frameworks/base/core/java/android/app

>Google官方实例中的注释
>// Prepare the loader.  Either re-connect with an existing one, or start a new one.
getLoaderManager().initLoader()

一个Activity中维护了一个ArrayMap：mAllLoaderManagers ，其中维护着Activity自己的和Activity中Fragment各自的一个LoaderManager，而每个LoaderManager又管理着自己创建的一个或多个Loader。在Activity配置变化时会保存mAllLoaderManagers，并根据情况使用其中LoaderManager来对Loader进行管理，这个是Loader能在Activity配置变化时自动处理的原理。

AsyncTaskLoader是Loader的封装抽象类，使用一个AsyncTask来加载数据，如果要加载自己数据类型一般需要继承该类实现自己的Loader。
CursorLoader实现了AsyncTaskLoader，加载sqlite数据库时使用，这是开发中最常使用的两种方式。

ForceLoadContentObserver
>An implementation of a ContentObserver that takes care of connecting it to the Loader to have the loader re-load its data when the observer is told it has changed. You do not normally need to use this yourself; it is used for you by CursorLoader to take care of executing an update when the cursor's backing data changes.

使用Cursor的时候可以用到这个，当后台数据更新时Loader可以reload，在CursorLoader中返回结果的Cursor直接注册了这个观察者，经过Google的封装，在使用CursorLoader加载数据时就十分的简洁了。自定义的Loader方面，源码中的AccountLoader是一个自定义的Loader，根据不同的数据类型加载账户信息，比CursorLoader实现更灵活，更有利于对象的封装。

参考链接：
实例：[alexjlockwood/AppListLoader](https://github.com/alexjlockwood/AppListLoader)
源码具体讲解和使用技巧：[ 工匠若水：Android应用Loaders全面详解及源码浅析](http://blog.csdn.net/yanbober/article/details/48861457)