### Initialize HMS
Initialize the plugin where appropriate in your code. We recommend to do this in the `AppDelegate::applicationDidFinishLaunching()` or `AppController:didFinishLaunchingWithOptions()`. Make sure to include the appropriate headers:
```cpp
#include "PluginHMS/PluginHMS.h"
AppDelegate::applicationDidFinishLaunching()
{
     sdkbox::PluginHMS::init();
}
```

### Login

HMS provides three way to login.

* Signing In with HUAWEI ID(ID Token)

```cpp
sdkbox::PluginHMS::login(1);
```

* Signing In with HUAWEI ID(Authorization Code)

```cpp
sdkbox::PluginHMS::login(2);
```

* Silently Signing In With HUAWEI ID

Authorization is required only at the first sign-in to your app using a HUAWEI ID. Subsequent sign-ins using the same HUAWEI ID does not require any authorization.

```cpp
sdkbox::PluginHMS::login(0);
```

> `onLogin` will be triggered when HMS AccountKit reruns the login response.

HMS offical [documentation](https://developer.huawei.com/consumer/en/doc/development/HMS-Guides/account-guide-v4)

### Logout

```cpp
sdkbox::PluginHMS::logout();
```

### Request Managed Products

```cpp
sdkbox::PluginHMS::iapRequestProducts();
```
this method will trigger `onIAPProducts` event

### Purchase Managed Product

```cpp
sdkbox::PluginHMS::iapPurchase("coin");
```
this method will trigger `onIAPPurchase` event

### Purchase Unmanaged Product

```cpp
const std::string productInfo = R"(
{
  "priceType": 0, //0:consumable 1:non-consumable 2:subscription
  "productName": "product name",
  "productId": "product id",
  "amount": "1.00",
  "currency": "CNY",
  "country": "CN",
  "sdkChannel": "1", // sdkChannel size must be between 0 and 4
  "serviceCatalog": "X58",
  "reservedInfor": "{\"a\": 1, \"b\":\"s\"}", // reservedInfor must be json string
  "developerPayload": "payload1"
}
)";
sdkbox::PluginHMS::iapPurchaseWithPrice(productInfo);
```
this method will trigger `onIAPPurchase` event

### request owned purchase

will return current user own products, include non-consumable, subscription product and consumable product which have not be consumed.

```cpp
sdkbox::PluginHMS::iapRequestOwnedPurchases();
```
this method will trigger `onIAPOwnedPurchases` event

### consume product

```cpp
sdkbox::PluginHMS::iapConsume(purchaseToken);
```
this method will trigger `onIAPPConsume` event

### request owned purchase record

request current user's all purchase records.
```cpp
sdkbox::PluginHMS::iapRequestOwnedPurchaseRecords(purchaseToken);
```
this method will trigger `onIAPOwnedPurchaseRecords` event

### Player Info

#### GetPlayer Info

will trigger listener event `onPlayerInfo`
```cpp
sdkbox::PluginHMS::playerRequestInfo();
```

#### GetPlayer ExtraInfo

Will return follow info of current player: isadult, playtime and so on
will trigger listener event `onPlayerExtraInfo`
```cpp
sdkbox::PluginHMS::playerRequestInfo();
```

#### Submit GameBegin

submit player game begin event. if your game will sell in china, you should submit game begin event.
will trigger listener event `onPlayerGameBegin`
```cpp
sdkbox::PluginHMS::playerSubmitGameBegin();
```

#### Submit GameEnd

submit player game begin event. if your game will sell in china, you should submit game end event.

will trigger listener event `onPlayerGameEnd`

```cpp
sdkbox::PluginHMS::playerSubmitGameEnd();
```

### Achievement

#### Request Achievement List

request achivement list, then you can show achievement list by yourself

will trigger listener event `onAchievementList`

```cpp
sdkbox::PluginHMS::achievementRequestList();
```

#### AchievementShow

show achivement with hms default ui

will trigger listener event `onAchievementShow`

```cpp
sdkbox::PluginHMS::achievementShow();
```

#### achievementVisualize

will trigger listener event `onAchievementVisualize`
```cpp
sdkbox::PluginHMS::achievementVisualize();
```

#### achievementGrow

will trigger listener event `onAchievementGrow`
```cpp
sdkbox::PluginHMS::achievementGrow();
```

#### achievementMakeSteps

will trigger listener event `onAchievementMakeSteps`
```cpp
sdkbox::PluginHMS::achievementMakeSteps();
```

#### achievementReach

```cpp
sdkbox::PluginHMS::achievementReach();
```

### Event

#### eventGrow

```cpp
sdkbox::PluginHMS::eventGrow();
```

#### eventRequestList

will trigger listener event `onEventList`
```cpp
sdkbox::PluginHMS::eventRequestList();
```

### Ranking

#### Check ranking switch status

before invoke ranking related api, you must make sure player is allow to open score.

will trigger listener event `onRankingSwitchStatus`
```cpp
sdkbox::PluginHMS::rankingRequestSwitchStatus();
```

will trigger listener event `onRankingSetSwitchStatus`
```cpp
sdkbox::PluginHMS::rankingSetSwitchStatus();
```

#### submit score

will trigger listener event `onRankingSubmitScore`

```cpp
sdkbox::PluginHMS::rankingSubmitScore(rankingName, score, score_unit);
```

#### Show ranking

show ranking by self.

will trigger listener event `onRankingList`

```cpp
bool realtime = true; // true, will request data from hms server; false, will use local cache data
sdkbox::PluginHMS::rankingRequestList(realtime, rankingName);
```

show with hms default ui

will trigger listener event `onRankingShow`

```cpp
int timeDimension = 2; // 0-> day, 1-> week, 2-> all time
sdkbox::PluginHMS::rankingShow(timeDimension, rankingName);
```

#### get scores

current player score

will trigger listener event `onRankingCurPlayerScore`

```cpp
int timeDimension = 2; // 0-> day, 1-> week, 2-> all time
sdkbox::PluginHMS::rankingRequestCurPlayerScore(rankingName, timeDimension);
```

request player centered score

will trigger listener event `onRankingPlayerCenteredScores`

```cpp
int timeDimension = 2; // 0-> day, 1-> week, 2-> all time
sdkbox::PluginHMS::rankingRequestPlayerCenteredScores(rankingName, timeDimension, realtime);
```

### Archive

add archive

will trigger listener event `onArchiveAdd`

```cpp
sdkbox::PluginHMS::archiveAdd(playedTime, progress, description, supportCache,
                               bmBytes, bmBytesLen, bmBytesType,
                               dataBytes, dataBytesLen);
```

update archive

will trigger listener event `onArchiveUpdate`

```cpp
sdkbox::PluginHMS::archiveUpdate(archiveId,
                          playedTime, progress, description,
                          bmBytes, bmBytesLen, bmBytesType,
                          dataBytes, dataBytesLen);
```

load archive

will trigger listener event `onArchiveLoad`

```cpp
int conflictPolicy = 3;
//-1 -> hms willn't hand conflict, 
//1  -> hms will resolved conflict by played time, 
//2  -> hms will resolved conflict by progress,
//3  -> hms will resolved conflict by last update time
sdkbox::PluginHMS::archiveLoad(archiveId, conflictPolicy);
```

### BUOY

if you game sell in china, you should show buoy
```cpp
sdkbox::PluginHMS::buoyShow();
//or
sdkbox::PluginHMS::buoyHide();
```

### Advertisement

caceh ad

```cpp
sdkbox::PluginHMS::adCache(adName);
```

show ad

```cpp
if (sdkbox::PluginHMS::adIsAvailable(adName)) {
    sdkbox::PluginHMS::adShow(adName);
}
```

hide banner

```cpp
sdkbox::PluginHMS::adHide(adName);
```

ad request settings (Optional)

```cpp
/*
  * adContentClassification:
  *   "W"->Content suitable for toddlers and older audiences;
  *  "PI"->Content suitable for kids and older audiences
  *   "J"->Content suitable for teenagers and older audiences.
  *   "A"->Content suitable only for adults.
  *    ""->Unknown rating.
  */
sdkbox::PluginHMS::adSetAdContentClassification("A");

/*
  * tagForUnderAgeOfPromise:
  *  0->Do not process ad requests as directed to users under the age of consent;
  *  1->Process ad requests as directed to users under the age of consent;
  * -1->Whether to process ad requests as directed to users under the age of consent is not specified;
  */
sdkbox::PluginHMS::adSetTagForUnderAgeOfPromise(0);

/*
* tagForChildProtection:
*  0->Do not process ad requests according to the COPPA;
*  1->Process ad requests according to the COPPA;
* -1->Whether to process ad requests according to the COPPA is not specified;
*/
sdkbox::PluginHMS::adSetTagForChildProtection(0);

/*
* nonPersonalizedAd
*  0->Request both personalized and non-personalized ads (default);
*  1->Request only non-personalized ads;
*/
sdkbox::PluginHMS::adSetNonPersonalizedAd(0);
```

reward ad setting (Optional)

reward data must be URL-encoded and length must be less than 1024

```cpp
// reward ad custom data
sdkbox::PluginHMS::adSetRewardData("cdata");

// uid for reward ad
sdkbox::PluginHMS::adSetRewardUserId("uid666");
```


### Handling HMS Events
This allows you to catch the `HMS` events so that you can perform operations based upon the response from your players and HMS servers.

all listener include code param, you can find code in follow url:

* https://developer.huawei.com/consumer/cn/doc/development/HMS-References/game-return-code-v4
* https://developer.huawei.com/consumer/cn/doc/development/HMS-References/hms-error-code

here we list a specific code:

- 7020: havn't find data in local cache
- 7022: is not adult
- 7024: `huawei mobile market` app is not installed
- 7218: huawei game services is not enabled, or user cancel
- 7204: need install the last application assist
- 7013: not login or archive is not enabled (make sure archive is true in sdkbox_config.json).

* Allow your class to extend `sdkbox::HMSListener`:
```cpp
#include "PluginHMS/PluginHMS.h"
class MyClass : public sdkbox::HMSListener {
private:
  // Account
  virtual void onLogin(int code, const std::string &msg) override;

  // Player Info
  virtual void onPlayerInfo(int code, const std::string& errorOrJson) override;
  virtual void onPlayerExtraInfo(int code, const std::string& errorOrJson) override;
  virtual void onPlayerGameBegin(int code, const std::string& errorOrJson) override;
  virtual void onPlayerGameEnd(int code, const std::string& errorOrJson) override;

  // IAP
  virtual void onIAPReady(int code, const std::string& msg) override;
  virtual void onIAPProducts(int code, const std::string& errorOrJson) override;
  virtual void onIAPPurchase(int code, const std::string& errorOrJson) override;
  virtual void onIAPPConsume(int code, const std::string& errorOrJson) override;
  virtual void onIAPOwnedPurchases(int code, const std::string& errorOrJson) override;
  virtual void onIAPOwnedPurchaseRecords(int code, const std::string& errorOrJson) override;

  // Achievement
  virtual void onAchievementList(int code, const std::string& errorOrJson) override;
  virtual void onAchievementShow(int code, const std::string& errorOrJson) override;
  virtual void onAchievementVisualize(int code, const std::string& errorOrJson) override;
  virtual void onAchievementGrow(int code, const std::string& errorOrJson) override;
  virtual void onAchievementMakeSteps(int code, const std::string& errorOrJson) override;

  // Event
  virtual void onEventList(int code, const std::string& errorOrJson) override;

  // Ranking
  virtual void onRankingSwitchStatus(int code, const std::string& errorOrJson) override;
  virtual void onRankingSetSwitchStatus(int code, const std::string& errorOrJson) override;
  virtual void onRankingSubmitScore(int code, const std::string& errorOrJson) override;
  virtual void onRankingShow(int code, const std::string& errorOrJson) override;
  virtual void onRankingList(int code, const std::string& errorOrJson) override;
  virtual void onRankingCurPlayerScore(int code, const std::string& errorOrJson) override;
  virtual void onRankingPlayerCenteredScores(int code, const std::string& errorOrJson) override;
  virtual void onRankingMoreScores(int code, const std::string& errorOrJson) override;
  virtual void onRankingTopScores(int code, const std::string& errorOrJson) override;

  // Archive
  virtual void onArchiveLimitThumbnailSize(int code, const std::string& errorOrJson) override;
  virtual void onArchiveLimitDetailsSize(int code, const std::string& errorOrJson) override;
  virtual void onArchiveAdd(int code, const std::string& errorOrJson) override;
  virtual void onArchiveShow(int code, const std::string& errorOrJson) override;
  virtual void onArchiveSummaryList(int code, const std::string& errorOrJson) override;
  virtual void onArchiveSelect(int code, const std::string& errorOrJson) override;
  virtual void onArchiveThumbnail(int code, const std::string& errorOrJson, unsigned char* coverData, unsigned int coverDataLen) override;
  virtual void onArchiveUpdate(int code, const std::string& errorOrJson) override;
  virtual void onArchiveLoad(int code, const std::string& errorOrJson, unsigned char* contentData, unsigned int contentDataLen) override;
  virtual void onArchiveRemove(int code, const std::string& errorOrJson) override;

  // Game Stats
  virtual void onGamePlayerStats(int code, const std::string& errorOrJson) override;
  virtual void onGameSummary(int code, const std::string& errorOrJson) override;

  // Ad
  virtual void onAdClose(int code, const std::string& errorOrJson) override;
  virtual void onAdFail(int code, const std::string& errorOrJson) override;
  virtual void onAdLeave(int code, const std::string& errorOrJson) override;
  virtual void onAdOpen(int code, const std::string& errorOrJson) override;
  virtual void onAdLoad(int code, const std::string& errorOrJson) override;
  virtual void onAdClick(int code, const std::string& errorOrJson) override;
  virtual void onAdImpression(int code, const std::string& errorOrJson) override;
  virtual void onAdReward(int code, const std::string& errorOrJson) override;

}
```

* Create a __listener__ that handles callbacks:
```cpp
sdkbox::PluginHMS::setListener(listener);
```
