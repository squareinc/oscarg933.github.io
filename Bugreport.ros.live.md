Skip to content
 
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 @oscarg933 Sign out
You are over your private repository plan limit (4 of 0). Please upgrade your plan, make private repositories public, or remove private repositories so that you are within your plan limit.
Your private repositories have been locked until this is resolved. Thanks for understanding. You can contact support with any questions.
0
0 138 Maxprofs/BugshotKit
forked from marcoarment/BugshotKit
 Code  Pull requests 0  Projects 0  Wiki  Insights  Settings
iOS in-app bug reporting for developers and testers, with annotated screenshots and the console log.
 73 commits
 1 branch
 1 release
 15 contributors
 MIT
 Objective-C 99.5%	 Ruby 0.5%
 Pull request   Compare This branch is even with marcoarment:master.
@marcoarment
marcoarment Merge pull request marcoarment#41 from operator/master  …
Latest commit bfa7fc2  on Feb 17
Type	Name	Latest commit message	Commit time
BugshotKit.xcodeproj	Fix minor build issues, including marcoarment#17	5 years ago
BugshotKit	Fix iOS 8 deprecation warnings	3 years ago
Resources	Removed the need for icon resources	5 years ago
Test Project	Adding new files to test project	5 years ago
.gitignore	Fix minor build issues, including marcoarment#17	5 years ago
BugshotKit.podspec	Preparing for Cocoapods submission ("finally")	5 years ago
LICENSE	Initial commit	5 years ago
README.md	Shipped Overcast	5 years ago
example-screenshot.png	Yeah, that screenshot was way too big.	5 years ago
 README.md
BugshotKit
iOS in-app bug reporting for developers and testers, with annotated screenshots and the console log. By Marco Arment.

(tl;dr: Embedded Bugshot plus NSLog() collection for beta testing.)

Just perform a gesture of your choice — shake, two-finger swipe-up, three-finger double-tap, swipe from right screen edge, etc. — from anywhere in the app, and the Bugshot report window slides up:

Screenshot

It automatically screenshots whatever you were just seeing in the app, and it includes a live NSLog() console log with no dependencies. (Also compatible with CocoaLumberjack and anything else capable of outputting to the standard system log, or you can add messages manually.)

Tapping the screenshot brings up an embedded version of the Bugshot app: draw bold orange arrows and boxes to annotate, or blur out sensitive information.

Tapping the console brings up a full-screen live console, useful in debugging even when you're not submitting a bug report.

Tap the respective green checkmarks to omit the screenshot or log if you'd like, and then simply compose an email with all of the relevant information already filled in and attached.

For development and beta tests only!
BugshotKit is made for development and ad-hoc beta testing. Please do not ship it in App Store builds.

To help prevent accidentally shipping your app with BugshotKit, I've included a helpful private API call that should cause immediate validation failure upon submitting. If you somehow ship it anyway, it will attempt to detect App Store builds at runtime and disable itself.

These safeguards aren't guaranteed. Please don't rely on them. Remove BugshotKit from your App Store builds.

Setup
The easiest way to be sure you're not going to build BugshotKit into your App Store builds is to link to it just in your Debug and Ad-Hoc builds. To do that:

Build a static library from the BugshotKit Xcode project.
Put that library, and the header files that come with it, somewhere in your project folder.
Make sure your app build settings' Library Search Paths and Header Search Paths include the path to where you put these.
Add -lBugshotKit to the Other Linker Flags setting, but only for the Debug and Ad-Hoc builds.
Use a conditional macro (e.g. "#if defined(DEBUG) || defined(ADHOC)"..."#endif") around the BugshotKit import and the invocation, below.
Usage
Simply invoke [BugshotKit enableWithNumberOfTouches:...] from your application:didFinishLaunchingWithOptions::

#import "BugshotKit.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [BugshotKit enableWithNumberOfTouches:1 performingGestures:BSKInvocationGestureSwipeUp feedbackEmailAddress:@"your@app.biz"];
}
That's it, really. Console tracking begins immediately, and on the next run-loop pass, it'll look for a UIWindow with a rootViewController and attach its gesture handlers (if any).

Bugshot can also be shown when the user shakes the device, by using BSKWindow in place of UIWindow in your application delegate:

self.window = [[BSKWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
If you don't want to use gesture triggers, you can invoke it manually (from a button, maybe):

[BugshotKit show];
BugshotKit's emails include an info.json file containing basic info in JSON:

{
  "appName" : "TestBugshotKit",
  "appVersion" : "1.0",
  "systemVersion" : "7.1",
  "deviceModel" : "iPhone6,1"
}
To add custom keys to this, set a block with [BugshotKit setExtraInfoBlock:] that returns an NSDictionary, and they'll be merged in.

To customize the email subject, set a block with [BugshotKit setEmailSubjectBlock:]. It receives the full dictionary as a parameter, with any keys you added with the extra info block, so you can do something like:

[BugshotKit setExtraInfoBlock:^NSDictionary *{
    return @{
        @"userID" : @(1),
        @"colorScheme" : @"dark"
    };
}];

[BugshotKit setEmailSubjectBlock:^NSString *(NSDictionary *info) {
    return [NSString stringWithFormat:@"Bug report from version %@, user %@", info[@"appVersion"], info[@"userID"]];
}];
License
See the included LICENSE file. (It's the MIT license.)

If you use BugshotKit, please consider supporting my bill-paying projects:

Marco.org
Accidental Tech Podcast
Overcast
Thanks.

Inconsolata font
BugshotKit includes Inconsolata, a free monospace programming font released under the SIL Open Font License, to make its console look nicer.

Add it to your application's resources to use it. If it's absent, BugshotKit will fall back to Courier New, but its console will look worse.

© 2018 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
Press h to open a hovercard with more details.
