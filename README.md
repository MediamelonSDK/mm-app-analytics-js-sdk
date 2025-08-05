# MediaMelon Application Analytics SDK Integration Guide

This guide provides comprehensive documentation for integrating the MediaMelon App Analytics SDK into your web application. It enables detailed user behavior tracking, analytics, and monetization tracking capabilities.

## Step 1: Add SDK to Your Website

**Purpose:** Load the SDK into your application.

**Method 1: NPM Installation (Recommended for modern applications)**

```bash
npm install mm-app-analytics-js-sdk
```

Then import in your JavaScript:

```javascript
import { MMAppAnalyticsSDK } from 'mm-app-analytics-js-sdk';
```

**Method 2: HTML Script Tag (For direct browser usage)**

Add the following script tag at the top of the `<body>` section of your HTML:

```html
<!-- Add this at the start of the <body> tag -->
<!-- Browser Bundle (IIFE) for direct usage -->
<script src="https://unpkg.com/mm-app-analytics-js-sdk@1.0.0/mm-app-analytics-js-sdk.min.js"></script>
```

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

### Video Tracking

```javascript
// Video events
analytics.reportVideoStart({ videoId: "1234", title: "Video", duration: 2400 });
analytics.reportVideoPause({ videoId: "1234", currentTime: 540 });
analytics.reportVideoResume({ videoId: "1234", currentTime: 540 });
analytics.reportVideoEnd({ videoId: "1234", duration: 2400, completed: true });
analytics.reportVideoSkip({ videoId: "1234", fromTime: 100, toTime: 400 });
analytics.reportVideoStop({ videoId: "1234", currentTime: 1800 });
```

### User Engagement

```javascript
// User interaction events
analytics.reportVideoShared({ videoId: "1234", platform: "WhatsApp" });
analytics.reportVideoBookmarked({ videoId: "1234", type: "WatchLater" });
analytics.reportVideoLiked({ videoId: "1234" });
analytics.reportUserClick({ elementId: "cta-button", elementType: "button" });
analytics.reportUserScroll({ scrollDepth: window.scrollY, scrollPercentage: 50 });
```

### User Authentication

```javascript
// Authentication events
analytics.reportUserSignUp({ userId: "user123", email: "user@example.com" });
analytics.reportUserSignIn({ userId: "user123", email: "user@example.com" });
analytics.reportUserSignOut({ userId: "user123", email: "user@example.com" });
```

### Monetization

```javascript
// Subscription events
analytics.reportSubscriptionViewed({ planId: "basic", duration: "6", measure: "months" });
analytics.reportSubscriptionStart({ subscriptionId: "sub123", planId: "basic", amount: 9.99 });
analytics.reportPaymentSuccess({ paymentId: "pay123", amount: 9.99, currency: "USD" });

// Ad events
analytics.reportAdStart({ adId: "ad123", adType: "pre-roll", duration: 30 });
analytics.reportAdComplete({ adId: "ad123", adType: "pre-roll", duration: 30 });
analytics.reportAdError({ adId: "ad123", adType: "pre-roll", errorType: "NETWORK_FAILURE" });
```

### Screen Views

```javascript
// Screen tracking
analytics.reportScreenView("HomePage");
analytics.reportScreenView("SearchResults");
analytics.reportScreenView("ContentDetailsPage");
```

### App State

```javascript
// App state tracking
analytics.reportAppState("Foreground");
analytics.reportAppState("Background");
analytics.reportAppError({ errorType: "PlaybackFailure", message: "DRM Error", code: 101 });
```

### Experiments

```javascript
// A/B testing events
analytics.reportExperimentExposure({ experimentId: "exp123", variantId: "var456" });
analytics.reportExperimentActivation({ experimentId: "exp123", variantId: "var456" });
analytics.reportFeatureFlagEvaluation({ flagId: "flag123", value: true });
```

## Tree Shaking

The SDK is optimized for tree shaking to reduce bundle size. Import only what you need:

```javascript
// Full SDK
import { MMAppAnalyticsSDK } from 'mm-app-analytics-js-sdk';

// Core SDK only (smaller bundle)
import { MMAppAnalyticsSDK, Config, Logger } from 'mm-app-analytics-js-sdk';

// Specific features only
import { VideoTracker, UserTracker } from 'mm-app-analytics-js-sdk';
```

### Bundle Size Comparison

| Import Type | Bundle Size | Features Included |
|-------------|-------------|-------------------|
| Full SDK | ~200KB | All features |
| Core SDK | ~50KB | Core functionality only |
| Video Tracking | ~30KB | Video tracking only |
| Monetization | ~25KB | Monetization only |
| User Tracking | ~20KB | User tracking only |

## Configuration Options

### SDK Configuration

```javascript
const sdkConfig = {
    // Debug settings
    debug: false,
    logLevel: 'info', // 'debug' | 'info' | 'warn' | 'error'
    
    // Queue settings
    offlineQueueSize: 1000,
    batchSize: 50,
    batchIntervalMs: 5000,
    
    // Retry settings
    maxRetries: 3,
    retryBackoffMs: 1000,
    
    // Auto-collection settings
    autoCollect: {
        enabled: true,
        session: true,
        navigation: true,
        clicks: true,
        scrolls: true,
        experiments: true,
        featureUsage: true
    }
};
```

### User Information

```javascript
const userInfo = {
    userId: "user123",
    email: "user@example.com",
    phoneNumber: "+1234567890",
    sessionId: "session123",
    preferences: { theme: "dark", language: "en" },
    demographics: {
        age: 25,
        gender: "female",
        region: "US-West",
        language: "en"
    }
};
```

## Error Handling

```javascript
// Set up error handlers
analytics.onError('video', (error) => {
    console.error('Video error:', error);
});

analytics.onError('network', (error) => {
    console.error('Network error:', error);
});

// Get error history
const errors = analytics.getErrorHistory();
```

## Logging

```javascript
// Set log level
analytics.setLogLevel('debug');

// Enable/disable logging
analytics.setLoggingEnabled(true);

// Set up log callbacks
analytics.onLog('info', (log) => {
    console.log('SDK Log:', log);
});

// Get log history
const logs = analytics.getLogHistory();
```

## Performance Monitoring

```javascript
// Get performance metrics
const metrics = analytics.getPerformanceMetrics();

// Get session information
const session = analytics.getSessionInfo();

// Get navigation information
const navigation = analytics.getNavigationInfo();
```

## Cleanup

```javascript
// Clean up SDK resources
analytics.destroy();
```

## Browser Support

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

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