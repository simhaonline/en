## API Reference

### Methods
```javascript
sdkbox.PluginInMobi.init();
```
>  initialize the plugin instance.

```javascript
sdkbox.PluginInMobi.setListener(listener);
```
> Set listener to listen for inmobi events

```javascript
sdkbox.PluginInMobi.getVersion();
```
> Use this to get the version of the SDK.
@return The version of the SDK.

```javascript
sdkbox.PluginInMobi.setLogLevel(desiredLogLevel);
```
> Set the log level for SDK's logs

```javascript
sdkbox.PluginInMobi.addIdForType(identifier, type);
```
> Register a user specific id with the SDK

```javascript
sdkbox.PluginInMobi.removeIdType(type);
```
> Deregister a particular set of Ids

```javascript
sdkbox.PluginInMobi.setAge(age);
```
> Provide the user's age to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setAreaCode(areaCode);
```
> Provide the user's area code to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setAgeGroup(ageGroup);
```
> Provide the user's age group to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setYearOfBirth(yearOfBirth);
```
> Provide a user's date of birth to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setEducation(education);
```
> Provide the user's education status to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setEthnicity(ethnicity);
```
> Provide the user's ethnicity to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setGender(gender);
```
> Provide the user's gender to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setHouseholdIncome(income);
```
> Provide the user's household income to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setIncome(income);
```
> Provide the user's income to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setInterests(interests);
```
> Provide the user's interests to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setLanguage(language);
```
> Provide the user's preferred language to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setLocation(city, state, country);
```
> Provide the user's location to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setLocation(latitude, longitude);
```
> Provide the user's location to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setNationality(nationality);
```
> Provide the user's nationality to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.setPostalCode(postalcode);
```
> Provide the user's postal code to the SDK for targeting purposes.

```javascript
sdkbox.PluginInMobi.shouldAutoRefresh(refresh);
```
> Control if the banner should auto-refresh ad content.

```javascript
sdkbox.PluginInMobi.setRefreshInterval(interval);
```
> Specify the refresh interval for the banner ad.

```javascript
sdkbox.PluginInMobi.loadBanner();
```
> Submit a request to load banner ad content.

```javascript
sdkbox.PluginInMobi.disableHardwareAccelerationForBanner();
```
> Turn off hardware acceleration on the underlying views.
vaild on android

```javascript
sdkbox.PluginInMobi.setBannerAnimationType(animationType);
```
> Set the animation preference on the banner views during ad refresh.

```javascript
sdkbox.PluginInMobi.setBannerKeywords(keywords);
```
> Set comma delimited keywords for targeting purpose

```javascript
sdkbox.PluginInMobi.hideBanner();
```
> Hide Banner

```javascript
sdkbox.PluginInMobi.loadInterstitial(ad);
```
> Submit a request to load interstitial ad content.

```javascript
sdkbox.PluginInMobi.isInterstitialReady(ad);
```
> Returns true if the interstitial was loaded successfully and in ready to be shown.

```javascript
sdkbox.PluginInMobi.showInterstitial(ad);
```
> Displays the interstitial on the screen

```javascript
sdkbox.PluginInMobi.showInterstitial(type, ad);
```
> Displays the interstitial on the screen
valid on ios

```javascript
sdkbox.PluginInMobi.showInterstitial(enterAnimationResourcedId,
                                      exitAnimationResourceId,
                                      ad);
```
> Displays the interstitial on the screen
valid on android

```javascript
sdkbox.PluginInMobi.disableHardwareAccelerationForInterstitial(ad);
```
> Disable hardware acceleration on the underlying views.
valid on android

```javascript
sdkbox.PluginInMobi.setInterstitialKeywords(keywords, ad);
```
> Set comma delimited keywords for targeting purpose


### Listeners
```javascript
bannerDidFinishLoading();
```
> Notifies the delegate that the banner has finished loading

```javascript
bannerDidFailToLoadWithError(code, description);
```
> Notifies the delegate that the banner has failed to load with some error.

```javascript
bannerDidInteractWithParams(params);
```
> Notifies the delegate that the banner was interacted with.

```javascript
userWillLeaveApplicationFromBanner();
```
> Notifies the delegate that the user would be taken out of the application context.

```javascript
bannerWillPresentScreen();
```
> Notifies the delegate that the banner would be presenting a full screen content.

```javascript
bannerDidPresentScreen();
```
> Notifies the delegate that the banner has finished presenting screen.

```javascript
bannerWillDismissScreen();
```
> Notifies the delegate that the banner will start dismissing the presented screen.

```javascript
bannerDidDismissScreen();
```
> Notifies the delegate that the banner has dismissed the presented screen.

```javascript
bannerRewardActionCompletedWithRewards(rewards);
```
> Notifies the delegate that the user has completed the action to be incentivised with.

```javascript
interstitialDidFinishLoading();
```
> Notifies the delegate that the interstitial has finished loading

```javascript
interstitialDidFailToLoadWithError(code, description);
```
> Notifies the delegate that the interstitial has failed to load with some error.

```javascript
interstitialWillPresent();
```
> Notifies the delegate that the interstitial would be presented.

```javascript
interstitialDidPresent();
```
> Notifies the delegate that the interstitial has been presented.

```javascript
interstitialDidFailToPresentWithError(code, description);
```
> Notifies the delegate that the interstitial has failed to present with some error.

```javascript
interstitialWillDismiss();
```
> Notifies the delegate that the interstitial will be dismissed.

```javascript
interstitialDidDismiss();
```
> Notifies the delegate that the interstitial has been dismissed.

```javascript
interstitialDidInteractWithParams(params);
```
> Notifies the delegate that the interstitial has been interacted with.

```javascript
interstitialRewardActionCompletedWithRewards(rewards);
```
> Notifies the delegate that the user has performed the action to be incentivised with.

```javascript
userWillLeaveApplicationFromInterstitial();
```
> Notifies the delegate that the user will leave application context.


