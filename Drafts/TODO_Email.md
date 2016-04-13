Email源码
入口Activity：com.android.email2.ui.MailActivityEmail
AuthenticatorSetupIntentHelper的actionNewAccountWithResultIntent方法，构建建立账户的流程Intent

EmailAccountCacheProvider.getNoAccountsIntent方法

AbstractActivityController AccountLoads的onLoadFinished方法
if (accountsLoaded) {
     final Intent noAccountIntent = MailAppProvider.getNoAccountIntent
     (mContext);
     if (noAccountIntent != null) {
         mActivity.startActivityForResult(noAccountIntent,
              ADD_ACCOUNT_REQUEST_CODE);
     }
}

OnePaneController继承AbstractActivityController
