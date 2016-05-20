Email源码
入口Activity：com.android.email2.ui.MailActivityEmail
AuthenticatorSetupIntentHelper的actionNewAccountWithResultIntent方法，构建建立账户的流程Intent
MailActivityEmail的父类为MailActivity
MailActivity onCreate ControllerFactory.forActivity方法,这里选择UI界面是适配手机还是平板。
return isTabletDevice ? new TwoPaneController(activity, viewMode)
        : new OnePaneController(activity, viewMode);

这里手机选择的是OnePaneController，实现了AbstractActivityController

第一次进入应用时，进入帐号设置流程，具体是EmailAccountCacheProvider.getNoAccountsIntent方法

AbstractActivityController里，AccountLoads是一个Loader,他的onLoadFinished方法里调用到这个方法。
if (accountsLoaded) {
     final Intent noAccountIntent = MailAppProvider.getNoAccountIntent
     (mContext);
     if (noAccountIntent != null) {
         mActivity.startActivityForResult(noAccountIntent,
              ADD_ACCOUNT_REQUEST_CODE);
     }
}

AccountSetupFinal账户设置的Activity

SetupDataFragment: Headless fragment to hold setup data for the account setup or settings flows
