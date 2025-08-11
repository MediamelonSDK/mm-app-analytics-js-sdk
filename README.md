# MediaMelon App Analytics SDK

A comprehensive JavaScript SDK for tracking user behavior, video engagement, monetization events, and application analytics in web applications.

## Features

- 🎯 **Core Analytics**: User tracking, screen tracking, app state monitoring
- 🎥 **Video Analytics**: Video engagement, quality tracking, user interactions
- 💰 **Monetization Tracking**: Subscription management, payment tracking, ad analytics
- 🔬 **Experiment & Feature Tracking**: A/B testing, feature flags, user segmentation
- 🤖 **Auto-Collection**: Automatic event capture, performance monitoring, error tracking
- 🌳 **Tree Shaking Support**: Optimized for bundle size reduction

## Installation

### NPM Installation

```bash
npm install mm-app-analytics-js-sdk
```

### CDN Installation

```html
<!-- ES Module (Recommended for modern bundlers) -->
<script type="module">
  import { MMAppAnalyticsSDK } from 'https://unpkg.com/mm-app-analytics-js-sdk@1.0.0/mm-app-analytics-js-sdk.min.js';
</script>

<!-- Browser Bundle (IIFE) - Modern browsers -->
<script src="https://unpkg.com/mm-app-analytics-js-sdk@1.0.0/mm-app-analytics-js-sdk.min.js"></script>

<!-- ES5 Bundle - Legacy browsers (IE 11+) -->
<script src="https://unpkg.com/mm-app-analytics-js-sdk@1.0.0/mm-app-analytics-js-sdk.es5.min.js"></script>
```

### Browser Compatibility

The SDK provides multiple builds for different browser environments:

- **`mm-app-analytics-js-sdk.min.js`** - Modern ES6+ build (Chrome 50+, Firefox 50+, Safari 10+, Edge 14+)
- **`mm-app-analytics-js-sdk.es5.min.js`** - ES5 compatible build (IE 11+, older browsers)
- **`mm-app-analytics-js-sdk.esm.js`** - ES Module build for bundlers

Choose the appropriate build based on your browser support requirements.

## Quick Start

### NPM Usage

```javascript
import { MMAppAnalyticsSDK } from 'mm-app-analytics-js-sdk';

// Initialize the SDK
const analytics = new MMAppAnalyticsSDK();

// Initialize with required parameters
await analytics.initialize(
    'your-customer-id',
    'your-app-id', 
    'Your App Name',
    '1.0.0'
);

// Track events
analytics.reportVideoStart({
    videoId: "1234",
    title: "Sample Video",
    duration: 2400,
    quality: "1080p"
});
```

### HTML Usage

```html
<!DOCTYPE html>
<html>
<head>
    <title>Analytics Demo</title>
</head>
<body>
    <!-- Include the SDK -->
    <script src="https://unpkg.com/mm-app-analytics-js-sdk@1.0.0/mm-app-analytics-js-sdk.min.js"></script>
    
    <script>
        // Initialize the SDK
        const analytics = new MMAppAnalyticsSDK();
        
        // Initialize with required parameters
        analytics.initialize(
            'your-customer-id',
            'your-app-id', 
            'Your App Name',
            '1.0.0'
        ).then(() => {
            console.log('SDK initialized successfully');
            
            // Track events
            analytics.reportVideoStart({
                videoId: "1234",
                title: "Sample Video",
                duration: 2400,
                quality: "1080p"
            });
        });
    </script>
</body>
</html>
```

### ES5 Usage (Legacy Browsers)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Analytics Demo - ES5</title>
</head>
<body>
    <!-- Include the ES5 SDK -->
    <script src="https://unpkg.com/mm-app-analytics-js-sdk@1.0.0/mm-app-analytics-js-sdk.es5.min.js"></script>
    
    <script>
        // Initialize the SDK (ES5 compatible)
        var analytics = new MMAppAnalyticsSDK();
        
        // Initialize with required parameters
        analytics.initialize(
            'your-customer-id',
            'your-app-id', 
            'Your App Name',
            '1.0.0'
        ).then(function() {
            console.log('SDK initialized successfully');
            
            // Track events
            analytics.reportVideoStart({
                videoId: "1234",
                title: "Sample Video",
                duration: 2400,
                quality: "1080p"
            });
        }).catch(function(error) {
            console.error('SDK initialization failed:', error);
        });
    </script>
</body>
</html>
```

## Advanced Configuration

### With User Information

```javascript
const userInfo = {
    userId: "user123",
    email: "user@example.com",
    phoneNumber: "+1234567890",
    demographics: {
        age: 25,
        gender: "female",
        region: "US-West"
    }
};

const sdkConfig = {
    debug: true,
    logLevel: 'info',
    offlineQueueSize: 1000,
    batchSize: 50,
    batchIntervalMs: 5000,
    autoCollect: {
        enabled: true,
        session: true,
        navigation: true,
        clicks: true,
        scrolls: true
    }
};

await analytics.initialize(
    'your-customer-id',
    'your-app-id', 
    'Your App Name',
    '1.0.0',
    userInfo,
    sdkConfig
);
```

## API Reference

# MediaMelon App Analytics JS SDK - API Reference Table

| API | Parameters | Example Code |
|-----|------------|--------------|
| **reportVideoStart(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br>- `data.assetName` (string): Video asset name<br>- `data.duration` (number): Video duration in seconds<br>- `data.position` (number): Starting position in seconds<br>- `data.quality` (string): Video quality<br>- `data.reason` (string): Reason for video start<br><br>**Optional:**<br>- `data.genre` (string): Video genre<br>- `data.metadata` (object): Additional metadata<br>- `data.playbackSpeed` (number): Playback speed<br>- `data.bufferingTime` (number): Buffering time in milliseconds<br>- `data.bitrate` (number): Video bitrate<br>- `data.resolution` (string): Video resolution<br>- `data.playerVersion` (string): Player version<br>- `data.playerType` (string): Player type | ```javascript<br>mmAnalytics.reportVideoStart({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  duration: 3600,<br>  position: 0,<br>  quality: "1080p",<br>  reason: "user_click",<br>  genre: "action",<br>  playbackSpeed: 1.0,<br>  metadata: {<br>    category: "movies",<br>    language: "en"<br>  }<br>});<br>``` |
| **reportVideoPause(data)** | **Mandatory:** Same as `reportVideoStart` | ```javascript<br>mmAnalytics.reportVideoPause({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  duration: 3600,<br>  position: 120,<br>  quality: "1080p",<br>  reason: "user_pause"<br>});<br>``` |
| **reportVideoResume(data)** | **Mandatory:** Same as `reportVideoStart` | ```javascript<br>mmAnalytics.reportVideoResume({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  duration: 3600,<br>  position: 120,<br>  quality: "1080p",<br>  reason: "user_resume"<br>});<br>``` |
| **reportVideoEnd(data)** | **Mandatory:** Same as `reportVideoStart` | ```javascript<br>mmAnalytics.reportVideoEnd({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  duration: 3600,<br>  position: 3600,<br>  quality: "1080p",<br>  reason: "video_complete"<br>});<br>``` |
| **reportVideoSkip(data)** | **Mandatory:** Same as `reportVideoStart` | ```javascript<br>mmAnalytics.reportVideoSkip({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  duration: 3600,<br>  position: 300,<br>  quality: "1080p",<br>  reason: "user_skip"<br>});<br>``` |
| **reportVideoStop(data)** | **Mandatory:** Same as `reportVideoStart` | ```javascript<br>mmAnalytics.reportVideoStop({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  duration: 3600,<br>  position: 180,<br>  quality: "1080p",<br>  reason: "user_stop"<br>});<br>``` |
| **reportVideoQuality(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br>- `data.oldQuality` (string): Previous quality<br>- `data.newQuality` (string): New quality<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportVideoQuality({<br>  assetId: "video_123",<br>  oldQuality: "720p",<br>  newQuality: "1080p",<br>  metadata: {<br>    reason: "bandwidth_improvement"<br>  }<br>});<br>``` |
| **reportVideoBuffering(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br>- `data.duration` (number): Buffering duration in milliseconds<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportVideoBuffering({<br>  assetId: "video_123",<br>  duration: 2000,<br>  metadata: {<br>    reason: "network_issue"<br>  }<br>});<br>``` |
| **reportVideoShared(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br><br>**Optional:**<br>- `data.assetName` (string): Video asset name<br>- `data.sharedTo` (string): Platform shared to<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportVideoShared({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  sharedTo: "facebook",<br>  metadata: {<br>    shareType: "social"<br>  }<br>});<br>``` |
| **reportVideoBookmarked(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br><br>**Optional:**<br>- `data.assetName` (string): Video asset name<br>- `data.type` (string): Bookmark type<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportVideoBookmarked({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  type: "favorite",<br>  metadata: {<br>    listName: "my_favorites"<br>  }<br>});<br>``` |
| **reportVideoLiked(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br><br>**Optional:**<br>- `data.assetName` (string): Video asset name<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportVideoLiked({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  metadata: {<br>    likeType: "thumbs_up"<br>  }<br>});<br>``` |
| **reportVideoComment(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br><br>**Optional:**<br>- `data.assetName` (string): Video asset name<br>- `data.comment` (string): Comment text<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportVideoComment({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  comment: "Great video!",<br>  metadata: {<br>    commentType: "user_review"<br>  }<br>});<br>``` |
| **reportVideoRating(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br><br>**Optional:**<br>- `data.assetName` (string): Video asset name<br>- `data.rating` (number): Rating value (1-5)<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportVideoRating({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  rating: 5,<br>  metadata: {<br>    ratingType: "star_rating"<br>  }<br>});<br>``` |
| **reportVideoQualityChange(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br>- `data.assetName` (string): Video asset name<br>- `data.quality` (string): Current quality<br>- `data.reason` (string): Reason for quality change<br><br>**Optional:**<br>- `data.oldQuality` (string): Previous quality<br>- `data.newQuality` (string): New quality<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportVideoQualityChange({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  quality: "1080p",<br>  reason: "auto_adjustment",<br>  oldQuality: "720p",<br>  newQuality: "1080p"<br>});<br>``` |
| **reportVideoPlaybackSpeedChange(data)** | **Mandatory:**<br>- `data.assetId` (string): Video asset identifier<br><br>**Optional:**<br>- `data.assetName` (string): Video asset name<br>- `data.oldSpeed` (number): Previous playback speed<br>- `data.newSpeed` (number): New playback speed<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportVideoPlaybackSpeedChange({<br>  assetId: "video_123",<br>  assetName: "Sample Video",<br>  oldSpeed: 1.0,<br>  newSpeed: 1.5<br>});<br>``` |
| **reportScreenView(screenView)** | **Mandatory:**<br>- `screenView.screenName` (string): Screen name<br>- `screenView.screenId` (string): Screen identifier<br><br>**Optional:**<br>- `screenView.timestamp` (number): Event timestamp<br>- `screenView.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportScreenView({<br>  screenName: "Home Screen",<br>  screenId: "home_screen_001",<br>  timestamp: Date.now(),<br>  metadata: {<br>    source: "navigation"<br>  }<br>});<br>``` |
| **reportScreenExit(data)** | **Mandatory:**<br>- `data.screenName` (string): Screen name<br>- `data.screenId` (string): Screen identifier<br>- `data.duration` (number): Time spent on screen in milliseconds<br><br>**Optional:**<br>- `data.timestamp` (number): Event timestamp<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportScreenExit({<br>  screenName: "Home Screen",<br>  screenId: "home_screen_001",<br>  duration: 45000,<br>  timestamp: Date.now(),<br>  metadata: {<br>    exitMethod: "back_button"<br>  }<br>});<br>``` |
| **reportAppState(appState)** | **Mandatory:**<br>- `appState.state` (string): App state ("foreground" or "background")<br><br>**Optional:**<br>- `appState.timestamp` (number): Event timestamp<br>- `appState.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportAppState({<br>  state: "foreground",<br>  timestamp: Date.now(),<br>  metadata: {<br>    trigger: "user_interaction"<br>  }<br>});<br>``` |
| **reportAppError(error)** | **Mandatory:**<br>- `error.errorType` (string): Type of error<br>- `error.message` (string): Error message<br><br>**Optional:**<br>- `error.stack` (string): Error stack trace<br>- `error.source` (string): Error source file<br>- `error.line` (number): Error line number<br>- `error.column` (number): Error column number<br>- `error.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportAppError({<br>  errorType: "network_error",<br>  message: "Failed to fetch data",<br>  stack: error.stack,<br>  source: "api.js",<br>  line: 45,<br>  column: 12,<br>  metadata: {<br>    endpoint: "/api/data"<br>  }<br>});<br>``` |
| **reportPerformanceMetrics(data)** | **Mandatory:**<br>- `data` (object): Performance metrics data<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportPerformanceMetrics({<br>  loadTime: 1200,<br>  renderTime: 800,<br>  memoryUsage: 45.6,<br>  metadata: {<br>    page: "dashboard"<br>  }<br>});<br>``` |
| **reportUserInfo(userInfo)** | **Mandatory:**<br>- `userInfo` (object): User information object<br><br>**Optional:**<br>- Additional user data (key-value pairs) | ```javascript<br>mmAnalytics.reportUserInfo({<br>  userId: "user_123",<br>  email: "user@example.com",<br>  name: "John Doe",<br>  age: 25,<br>  location: "New York"<br>});<br>``` |
| **reportUserSignUp(data)** | **Mandatory:**<br>- `data.userId` (string): User identifier<br>- `data.email` (string): User email address<br><br>**Optional:**<br>- `data.name` (string): User name<br>- `data.age` (number): User age<br>- `data.source` (string): Sign up source<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserSignUp({<br>  userId: "user_123",<br>  email: "user@example.com",<br>  name: "John Doe",<br>  age: 25,<br>  source: "email_campaign",<br>  metadata: {<br>    referralCode: "REF123"<br>  }<br>});<br>``` |
| **reportUserSignIn(data)** | **Mandatory:**<br>- `data.userId` (string): User identifier<br>- `data.email` (string): User email address<br><br>**Optional:**<br>- `data.method` (string): Sign in method<br>- `data.device` (string): Device type<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserSignIn({<br>  userId: "user_123",<br>  email: "user@example.com",<br>  method: "email_password",<br>  device: "mobile",<br>  metadata: {<br>    ipAddress: "192.168.1.1"<br>  }<br>});<br>``` |
| **reportUserSignOut(data)** | **Mandatory:**<br>- `data.userId` (string): User identifier<br>- `data.email` (string): User email address<br><br>**Optional:**<br>- `data.reason` (string): Sign out reason<br>- `data.sessionDuration` (number): Session duration in milliseconds<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserSignOut({<br>  userId: "user_123",<br>  email: "user@example.com",<br>  reason: "user_logout",<br>  sessionDuration: 3600000,<br>  metadata: {<br>    logoutMethod: "button_click"<br>  }<br>});<br>``` |
| **reportUserIdentification(data)** | **Mandatory:**<br>- `data` (object): User identification data<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserIdentification({<br>  anonymousId: "anon_456",<br>  userId: "user_123",<br>  email: "user@example.com",<br>  metadata: {<br>    identificationMethod: "login"<br>  }<br>});<br>``` |
| **reportUserSessionStart(data)** | **Mandatory:**<br>- `data` (object): User session data<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserSessionStart({<br>  sessionId: "session_789",<br>  userId: "user_123",<br>  timestamp: Date.now(),<br>  metadata: {<br>    source: "app_launch"<br>  }<br>});<br>``` |
| **reportUserSessionEnd(data)** | **Mandatory:**<br>- `data` (object): User session data<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserSessionEnd({<br>  sessionId: "session_789",<br>  userId: "user_123",<br>  duration: 1800000,<br>  metadata: {<br>    reason: "app_close"<br>  }<br>});<br>``` |
| **reportUserPreferenceChange(data)** | **Mandatory:**<br>- `data` (object): User preference data<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserPreferenceChange({<br>  userId: "user_123",<br>  preference: "theme",<br>  oldValue: "light",<br>  newValue: "dark",<br>  metadata: {<br>    changeSource: "settings_page"<br>  }<br>});<br>``` |
| **reportUserProfileUpdate(data)** | **Mandatory:**<br>- `data.userId` (string): User identifier<br>- `data.updatedFields` (array): List of updated fields<br><br>**Optional:**<br>- Additional profile data (key-value pairs) | ```javascript<br>mmAnalytics.reportUserProfileUpdate({<br>  userId: "user_123",<br>  updatedFields: ["name", "avatar"],<br>  name: "Jane Doe",<br>  avatar: "avatar_url",<br>  metadata: {<br>    updateSource: "profile_edit"<br>  }<br>});<br>``` |
| **reportUserClick(metadata)** | **Mandatory:**<br>- `metadata.elementId` (string): Element identifier<br>- `metadata.elementType` (string): Element type<br>- `metadata.pageUrl` (string): Page URL<br>- `metadata.position` (object): Click position<br>- `metadata.timestamp` (number): Event timestamp<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserClick({<br>  elementId: "btn_subscribe",<br>  elementType: "button",<br>  pageUrl: "https://example.com/pricing",<br>  position: {<br>    x: 150,<br>    y: 200<br>  },<br>  timestamp: Date.now(),<br>  metadata: {<br>    buttonText: "Subscribe Now"<br>  }<br>});<br>``` |
| **reportUserScroll(metadata)** | **Mandatory:**<br>- `metadata.scrollDepth` (number): Scroll depth in pixels<br>- `metadata.scrollPercentage` (number): Scroll percentage (0-100)<br>- `metadata.pageUrl` (string): Page URL<br>- `metadata.timestamp` (number): Event timestamp<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportUserScroll({<br>  scrollDepth: 800,<br>  scrollPercentage: 75,<br>  pageUrl: "https://example.com/article",<br>  timestamp: Date.now(),<br>  metadata: {<br>    scrollDirection: "down"<br>  }<br>});<br>``` |
| **reportSubscriberInfo(data)** | **Mandatory:**<br>- `data.subscriberId` (string): Unique subscriber ID<br>- `data.planType` (string): Subscription plan type<br>- `data.segment` (string): User segment<br>- `data.profileId` (string): Profile ID<br><br>**Optional:**<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportSubscriberInfo({<br>  subscriberId: "sub_123",<br>  planType: "premium",<br>  segment: "power_user",<br>  profileId: "profile_456",<br>  metadata: {<br>    subscriptionDate: "2024-01-15"<br>  }<br>});<br>``` |
| **reportReferralInfo(data)** | **Mandatory:**<br>- `data.referralId` (string): Unique referral ID<br>- `data.source` (string): Referral source<br>- `data.medium` (string): Referral medium<br>- `data.campaign` (string): Referral campaign<br><br>**Optional:**<br>- `data.term` (string): Search term<br>- `data.content` (string): Content identifier<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportReferralInfo({<br>  referralId: "ref_789",<br>  source: "google",<br>  medium: "cpc",<br>  campaign: "summer_sale",<br>  term: "video streaming",<br>  content: "banner_ad_001",<br>  metadata: {<br>    landingPage: "/welcome"<br>  }<br>});<br>``` |
| **reportSubscriptionStart(data)** | **Mandatory:**<br>- `data.subscriptionId` (string): Subscription identifier<br>- `data.planId` (string): Plan identifier<br>- `data.planName` (string): Plan name<br>- `data.amount` (number): Subscription amount<br>- `data.currency` (string): Currency code<br>- `data.duration` (number): Duration value<br>- `data.measure` (string): Duration measure<br>- `data.status` (string): Subscription status<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata<br>- `data.paymentMethod` (string): Payment method<br>- `data.autoRenew` (boolean): Auto-renewal status<br>- `data.trialPeriod` (number): Trial period in days<br>- `data.startDate` (string): Start date | ```javascript<br>mmAnalytics.reportSubscriptionStart({<br>  subscriptionId: "sub_123",<br>  planId: "premium_monthly",<br>  planName: "Premium Monthly",<br>  amount: 9.99,<br>  currency: "USD",<br>  duration: 1,<br>  measure: "month",<br>  status: "active",<br>  paymentMethod: "credit_card",<br>  autoRenew: true,<br>  trialPeriod: 7,<br>  startDate: "2024-01-15",<br>  metadata: {<br>    source: "pricing_page"<br>  }<br>});<br>``` |
| **reportSubscriptionRenewal(data)** | **Mandatory:** Same as `reportSubscriptionStart` | ```javascript<br>mmAnalytics.reportSubscriptionRenewal({<br>  subscriptionId: "sub_123",<br>  planId: "premium_monthly",<br>  planName: "Premium Monthly",<br>  amount: 9.99,<br>  currency: "USD",<br>  duration: 1,<br>  measure: "month",<br>  status: "renewed",<br>  metadata: {<br>    renewalNumber: 3<br>  }<br>});<br>``` |
| **reportSubscriptionCancellation(data)** | **Mandatory:** Same as `reportSubscriptionStart` | ```javascript<br>mmAnalytics.reportSubscriptionCancellation({<br>  subscriptionId: "sub_123",<br>  planId: "premium_monthly",<br>  planName: "Premium Monthly",<br>  amount: 9.99,<br>  currency: "USD",<br>  duration: 1,<br>  measure: "month",<br>  status: "cancelled",<br>  metadata: {<br>    reason: "too_expensive"<br>  }<br>});<br>``` |
| **reportSubscriptionUpgrade(data)** | **Mandatory:** Same as `reportSubscriptionStart` | ```javascript<br>mmAnalytics.reportSubscriptionUpgrade({<br>  subscriptionId: "sub_123",<br>  planId: "premium_yearly",<br>  planName: "Premium Yearly",<br>  amount: 99.99,<br>  currency: "USD",<br>  duration: 12,<br>  measure: "month",<br>  status: "upgraded",<br>  metadata: {<br>    previousPlan: "premium_monthly"<br>  }<br>});<br>``` |
| **reportSubscriptionDowngrade(data)** | **Mandatory:** Same as `reportSubscriptionStart` | ```javascript<br>mmAnalytics.reportSubscriptionDowngrade({<br>  subscriptionId: "sub_123",<br>  planId: "basic_monthly",<br>  planName: "Basic Monthly",<br>  amount: 4.99,<br>  currency: "USD",<br>  duration: 1,<br>  measure: "month",<br>  status: "downgraded",<br>  metadata: {<br>    previousPlan: "premium_monthly"<br>  }<br>});<br>``` |
| **reportSubscriptionViewed(data)** | **Mandatory:**<br>- `data.planId` (string): Plan identifier<br><br>**Optional:**<br>- `data.planName` (string): Plan name<br>- `data.price` (number): Plan price<br>- `data.duration` (string): Plan duration<br>- Additional metadata (key-value pairs) | ```javascript<br>mmAnalytics.reportSubscriptionViewed({<br>  planId: "premium_monthly",<br>  planName: "Premium Monthly",<br>  price: 9.99,<br>  duration: "1 month",<br>  metadata: {<br>    page: "pricing"<br>  }<br>});<br>``` |
| **reportPaymentInitiation(data)** | **Mandatory:**<br>- `data.paymentId` (string): Payment identifier<br>- `data.amount` (number): Payment amount<br>- `data.currency` (string): Currency code<br>- `data.paymentMethod` (string): Payment method<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata<br>- `data.transactionId` (string): Transaction identifier<br>- `data.orderId` (string): Order identifier<br>- `data.customerId` (string): Customer identifier | ```javascript<br>mmAnalytics.reportPaymentInitiation({<br>  paymentId: "pay_123",<br>  amount: 9.99,<br>  currency: "USD",<br>  paymentMethod: "credit_card",<br>  transactionId: "txn_456",<br>  orderId: "order_789",<br>  customerId: "cust_123",<br>  metadata: {<br>    source: "subscription_payment"<br>  }<br>});<br>``` |
| **reportPaymentSuccess(data)** | **Mandatory:** Same as `reportPaymentInitiation` | ```javascript<br>mmAnalytics.reportPaymentSuccess({<br>  paymentId: "pay_123",<br>  amount: 9.99,<br>  currency: "USD",<br>  paymentMethod: "credit_card",<br>  transactionId: "txn_456",<br>  metadata: {<br>    processingTime: 1500<br>  }<br>});<br>``` |
| **reportPaymentFailure(data)** | **Mandatory:**<br>- `data.paymentId` (string): Payment identifier<br>- `data.amount` (number): Payment amount<br>- `data.currency` (string): Currency code<br>- `data.paymentMethod` (string): Payment method<br>- `data.errorType` (string): Error type<br>- `data.message` (string): Error message<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportPaymentFailure({<br>  paymentId: "pay_123",<br>  amount: 9.99,<br>  currency: "USD",<br>  paymentMethod: "credit_card",<br>  errorType: "insufficient_funds",<br>  message: "Insufficient funds in account",<br>  metadata: {<br>    retryCount: 1<br>  }<br>});<br>``` |
| **reportPaymentRefund(data)** | **Mandatory:**<br>- `data.paymentId` (string): Payment identifier<br>- `data.amount` (number): Refund amount<br>- `data.currency` (string): Currency code<br>- `data.refundReason` (string): Refund reason<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportPaymentRefund({<br>  paymentId: "pay_123",<br>  amount: 9.99,<br>  currency: "USD",<br>  refundReason: "customer_request",<br>  metadata: {<br>    refundType: "full_refund"<br>  }<br>});<br>``` |
| **reportAdImpression(data)** | **Mandatory:**<br>- `data.adId` (string): Ad identifier<br>- `data.adType` (string): Ad type<br><br>**Optional:**<br>- `data.duration` (number): Ad duration in seconds<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportAdImpression({<br>  adId: "ad_123",<br>  adType: "banner",<br>  duration: 30,<br>  metadata: {<br>    position: "top_banner"<br>  }<br>});<br>``` |
| **reportAdClick(data)** | **Mandatory:** Same as `reportAdImpression` | ```javascript<br>mmAnalytics.reportAdClick({<br>  adId: "ad_123",<br>  adType: "banner",<br>  metadata: {<br>    clickPosition: { x: 150, y: 200 }<br>  }<br>});<br>``` |
| **reportAdStart(data)** | **Mandatory:** Same as `reportAdImpression` | ```javascript<br>mmAnalytics.reportAdStart({<br>  adId: "ad_123",<br>  adType: "preroll",<br>  duration: 15,<br>  metadata: {<br>    videoId: "video_456"<br>  }<br>});<br>``` |
| **reportAdComplete(data)** | **Mandatory:** Same as `reportAdImpression` | ```javascript<br>mmAnalytics.reportAdComplete({<br>  adId: "ad_123",<br>  adType: "preroll",<br>  duration: 15,<br>  metadata: {<br>    completionRate: 100<br>  }<br>});<br>``` |
| **reportAdSkip(data)** | **Mandatory:** Same as `reportAdImpression` | ```javascript<br>mmAnalytics.reportAdSkip({<br>  adId: "ad_123",<br>  adType: "preroll",<br>  duration: 5,<br>  metadata: {<br>    skipReason: "user_skip"<br>  }<br>});<br>``` |
| **reportAdError(data)** | **Mandatory:**<br>- `data.adId` (string): Ad identifier<br>- `data.adType` (string): Ad type<br>- `data.errorType` (string): Error type<br>- `data.message` (string): Error message<br><br>**Optional:**<br>- `data.duration` (number): Ad duration in seconds<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportAdError({<br>  adId: "ad_123",<br>  adType: "preroll",<br>  errorType: "load_failed",<br>  message: "Ad failed to load",<br>  metadata: {<br>    errorCode: "AD_LOAD_ERROR"<br>  }<br>});<br>``` |
| **reportExperimentExposure(data)** | **Mandatory:**<br>- `data.experimentId` (string): Experiment identifier<br>- `data.experimentName` (string): Experiment name<br>- `data.variantId` (string): Variant identifier<br>- `data.variantName` (string): Variant name<br>- `data.timestamp` (number): Event timestamp<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata<br>- `data.exposureType` (string): Exposure type<br>- `data.source` (string): Exposure source<br>- `data.context` (object): Exposure context | ```javascript<br>mmAnalytics.reportExperimentExposure({<br>  experimentId: "exp_123",<br>  experimentName: "New UI Layout",<br>  variantId: "variant_a",<br>  variantName: "Control",<br>  timestamp: Date.now(),<br>  exposureType: "page_view",<br>  source: "homepage",<br>  context: {<br>    userSegment: "new_users"<br>  },<br>  metadata: {<br>    sessionId: "session_789"<br>  }<br>});<br>``` |
| **reportExperimentActivation(data)** | **Mandatory:** Same as `reportExperimentExposure` | ```javascript<br>mmAnalytics.reportExperimentActivation({<br>  experimentId: "exp_123",<br>  experimentName: "New UI Layout",<br>  variantId: "variant_a",<br>  variantName: "Control",<br>  timestamp: Date.now(),<br>  exposureType: "feature_activation",<br>  source: "user_interaction",<br>  metadata: {<br>    activationTrigger: "button_click"<br>  }<br>});<br>``` |
| **reportFeatureFlagEvaluation(data)** | **Mandatory:**<br>- `data.featureId` (string): Feature identifier<br>- `data.featureName` (string): Feature name<br>- `data.enabled` (boolean): Feature enabled status<br>- `data.timestamp` (number): Event timestamp<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata<br>- `data.evaluationContext` (object): Evaluation context<br>- `data.source` (string): Evaluation source | ```javascript<br>mmAnalytics.reportFeatureFlagEvaluation({<br>  featureId: "feature_123",<br>  featureName: "Dark Mode",<br>  enabled: true,<br>  timestamp: Date.now(),<br>  evaluationContext: {<br>    userType: "premium"<br>  },<br>  source: "app_startup",<br>  metadata: {<br>    evaluationTime: 50<br>  }<br>});<br>``` |
| **reportExperimentResults(data)** | **Mandatory:**<br>- `data.experimentId` (string): Experiment identifier<br>- `data.experimentName` (string): Experiment name<br>- `data.variantId` (string): Variant identifier<br>- `data.variantName` (string): Variant name<br>- `data.results` (object): Experiment results<br>- `data.timestamp` (number): Event timestamp<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata<br>- `data.resultType` (string): Result type<br>- `data.metrics` (object): Metrics data<br>- `data.context` (object): Result context | ```javascript<br>mmAnalytics.reportExperimentResults({<br>  experimentId: "exp_123",<br>  experimentName: "New UI Layout",<br>  variantId: "variant_a",<br>  variantName: "Control",<br>  results: {<br>    conversionRate: 0.15,<br>    engagementTime: 300<br>  },<br>  timestamp: Date.now(),<br>  resultType: "conversion",<br>  metrics: {<br>    clicks: 45,<br>    impressions: 300<br>  },<br>  context: {<br>    userSegment: "new_users"<br>  },<br>  metadata: {<br>    sessionDuration: 1800<br>  }<br>});<br>``` |
| **reportEvent(event)** | **Mandatory:**<br>- `event` (object): Event data object<br><br>**Optional:**<br>- Additional event data (key-value pairs) | ```javascript<br>mmAnalytics.reportEvent({<br>  eventName: "custom_action",<br>  eventType: "user_interaction",<br>  timestamp: Date.now(),<br>  userId: "user_123",<br>  metadata: {<br>    action: "button_click",<br>    page: "dashboard"<br>  }<br>});<br>``` |
| **reportFeatureUsage(data)** | **Mandatory:**<br>- `data.featureId` (string): Feature identifier<br>- `data.featureName` (string): Feature name<br>- `data.action` (string): Feature action<br>- `data.timestamp` (number): Event timestamp<br><br>**Optional:**<br>- `data.metadata` (object): Additional metadata | ```javascript<br>mmAnalytics.reportFeatureUsage({<br>  featureId: "feature_123",<br>  featureName: "Search Function",<br>  action: "search_executed",<br>  timestamp: Date.now(),<br>  metadata: {<br>    searchTerm: "video streaming",<br>    resultsCount: 15<br>  }<br>});<br>``` |

- **Modern Browsers**: Chrome 50+, Firefox 50+, Safari 10+, Edge 14+
- **Legacy Browsers**: IE 11+ (using ES5 build)
- **Mobile Browsers**: iOS Safari 10+, Android Chrome 50+

## Node.js Support

- Node.js 14.0.0+

## License

MIT License

## Support

For support and questions:
- Documentation: [GitHub Repository](https://github.com/mediamelon/mm-app-analytics-js-sdk)
- Issues: [GitHub Issues](https://github.com/mediamelon/mm-app-analytics-js-sdk/issues)
- Contact: [MediaMelon Support](mailto:support@mediamelon.com)

## Changelog

### v1.0.0
- Initial release
- Core analytics functionality
- Video tracking
- User tracking
- Monetization tracking
- Experiment tracking
- Auto-collection
- Tree shaking support