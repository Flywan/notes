�����Ŀ�õ���LoaderManager+Loader�������ݣ�ͬʱ���Ķ�AndroidԴ��ʱ��������ʹ��LoaderManager+Loader�������ݵ��������ʤ�������ǳ��ȴ�����ѧϰһ�����Դ�롣

���ȸ���Դ��򵥻�һ��LoaderManager+Loader�Ĵ��¿�ܣ�ˮƽ�д���ߣ����д�����ָ�㣩
![Loader��Ҫ](http://img.blog.csdn.net/20160522235354315)

Դ��λ�ã�
frameworks/base/core/java/android/content
frameworks/base/core/java/android/app

>Google�ٷ�ʵ���е�ע��
>// Prepare the loader.  Either re-connect with an existing one, or start a new one.
getLoaderManager().initLoader()

һ��Activity��ά����һ��ArrayMap��mAllLoaderManagers ������ά����Activity�Լ��ĺ�Activity��Fragment���Ե�һ��LoaderManager����ÿ��LoaderManager�ֹ������Լ�������һ������Loader����Activity���ñ仯ʱ�ᱣ��mAllLoaderManagers�����������ʹ������LoaderManager����Loader���й��������Loader����Activity���ñ仯ʱ�Զ������ԭ��

AsyncTaskLoader��Loader�ķ�װ�����࣬ʹ��һ��AsyncTask���������ݣ����Ҫ�����Լ���������һ����Ҫ�̳и���ʵ���Լ���Loader��
CursorLoaderʵ����AsyncTaskLoader������sqlite���ݿ�ʱʹ�ã����ǿ������ʹ�õ����ַ�ʽ��

ForceLoadContentObserver
>An implementation of a ContentObserver that takes care of connecting it to the Loader to have the loader re-load its data when the observer is told it has changed. You do not normally need to use this yourself; it is used for you by CursorLoader to take care of executing an update when the cursor's backing data changes.

ʹ��Cursor��ʱ������õ����������̨���ݸ���ʱLoader����reload����CursorLoader�з��ؽ����Cursorֱ��ע��������۲��ߣ�����Google�ķ�װ����ʹ��CursorLoader��������ʱ��ʮ�ֵļ���ˡ��Զ����Loader���棬Դ���е�AccountLoader��һ���Զ����Loader�����ݲ�ͬ���������ͼ����˻���Ϣ����CursorLoaderʵ�ָ����������ڶ���ķ�װ��

�ο����ӣ�
ʵ����[alexjlockwood/AppListLoader](https://github.com/alexjlockwood/AppListLoader)
Դ����彲���ʹ�ü��ɣ�[ ������ˮ��AndroidӦ��Loadersȫ����⼰Դ��ǳ��](http://blog.csdn.net/yanbober/article/details/48861457)