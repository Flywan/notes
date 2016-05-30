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
AccountSetupNoteDialogFragment: 账户设置过程中的提醒对话框
AccountCreationFragment: This retained headless fragment acts as a container for the multi-step task of creating the AccountManager account and saving our account object to the database, as well as some misc related background tasks.
AccountCheckSettingsFragment:
/**
 * Check incoming or outgoing settings, or perform autodiscovery.
 *
 * There are three components that work together.  1. This fragment is retained and non-displayed,
 * and controls the overall process.  2. An AsyncTask that works with the stores/services to
 * check the accounts settings.  3. A stateless progress dialog (which will be recreated on
 * orientation changes).
 *
 * There are also two lightweight error dialogs which are used for notification of terminal
 * conditions.
 */

SecurityRequiredDialogFragment: Exchange账户安全策略控制对话框
CheckSettingsErrorDialogFragment: 设置账户时发生错误对话框，比如无法连接至服务器等
CheckSettingsProgressDialogFragment：Simple dialog that shows progress as we work through the settings checks.
AccountSetupTypeFragment: 选择账户的类型(POP3, IMAP 和 EXCHANGE)
AccountSetupNamesFragment：设置账户发件的姓名和账户名称
AccountSetupOptionsFragment: 账户选项设置
AccountSetupBasicsFragment:填入邮箱账户的界面
AccountServerBaseFragment: 帐号服务器设置的base class。AccountSetupIncomingFragment和AccountSetupOutgoingFragment继承了它。
AccountSetupCredentialsFragment：账户凭证设置界面
DuplicateAccountDialogFragment：提示用户名已被使用的对话框
AccountSetupABFragment: 确认账户的类型，当用户的protocol选择和providers.xml里指示的不一样之时。
AccountSetupFragment: 账户设置流程的父类，保存着一个代表当前的状态mState，方便后退操作

