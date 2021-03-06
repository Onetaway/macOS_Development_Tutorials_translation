# 把你的iOS app搬到macOS上去

#### [原文地址](https://www.raywenderlich.com/161968/porting-your-ios-app-to-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/PortOS-feature.png"
        alt="Porting Your iOS App to macOS" width="250" height="250" class="alignright size-thumbnail bordered">
    </p>
    <p>
        If you’re developing apps for iOS, you already have a particular set of
        skills that you can use to write apps for another platform – macOS!
    </p>
    <p>
        If you’re like most developers, you don’t want to have to write your app
        twice just to ship your app on a new platform, as this can take too much
        time and money. But with a little effort, you can learn how to port iOS
        apps to macOS, reusing a good portion of your existing iOS app, and only
        rewriting the portions that are platform-specific.
    </p>
    <p>
        In this tutorial, you’ll learn how to create an Xcode project that is
        home to both iOS and macOS, how to refactor your code for reuse on both
        platforms, and when it is appropriate to write platform specific code.
    </p>
    <p>
        To get the most out of this tutorial you should be familiar with
        <em>
            NSTableView
        </em>
        . If you need to refresh your knowledge we have an
        <a href="https://www.raywenderlich.com/143828/macos-nstableview-tutorial"
        sl-processed="1">
            introduction
        </a>
        for you.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        For this tutorial, you’ll need to download the starter project
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/BeerTracker-Port_Starter-1.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        The sample project is a version of the BeerTracker app used in previous
        tutorials. It allows you to keep a record of beers you’ve tried, along
        with notes, ratings, and images of the beers. Build and run the app to
        get a feel for how it works.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial-282x500.png"
        alt="Beer Tracker iOS" width="282" height="500" class="aligncenter size-large wp-image-162149 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial-282x500.png 282w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial-180x320.png 180w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial.png 640w"
        sizes="(max-width: 282px) 100vw, 282px">
    </p>
    <p>
        Since the app is only available on iOS, the first step to porting the
        app for macOS is to create a new target. A target simply is a set of instructions
        telling Xcode how to build your application. Currently, you only have an
        iOS target, which contains all the information needed to build your app
        for an iPhone.
    </p>
    <p>
        Select the
        <em>
            BeerTracker
        </em>
        project at the top of the
        <em>
            Project Navigator
        </em>
        . At the bottom of the
        <em>
            Project and Targets
        </em>
        list, click the
        <em>
            +
        </em>
        button.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget-345x320.png"
            alt="" width="345" height="320" class="aligncenter size-medium wp-image-164311"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget-345x320.png 345w, https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget.png 441w"
            sizes="(max-width: 345px) 100vw, 345px">
        </a>
    </p>
    <p>
        This will present a window for you to add a new target to your project.
        At the top of the window, you’ll see tabs representing the different categories
        of platforms supported. Select macOS, then scroll down to
        <em>
            Application
        </em>
        and choose
        <em>
            Cocoa App
        </em>
        . Name the new target
        <em>
            BeerTracker-mac
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection-444x320.png"
            alt="" width="444" height="320" class="aligncenter size-medium wp-image-164312"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection-444x320.png 444w, https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection-650x469.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection.png 731w"
            sizes="(max-width: 444px) 100vw, 444px">
        </a>
    </p>
    <h3>
        Adding the Assets
    </h3>
    <p>
        In the starter app you downloaded, you’ll find a folder named
        <em>
            BeerTracker Mac Icons
        </em>
        . You’ll need to add the App Icons to
        <em>
            AppIcon
        </em>
        in
        <em>
            Assets.xcassets
        </em>
        found under the
        <em>
            BeerTracker-mac
        </em>
        group. Also add
        <em>
            beerMug.pdf
        </em>
        to
        <em>
            Assets.xcassets
        </em>
        . Select
        <em>
            beerMug
        </em>
        , open the
        <em>
            Attributes Inspector
        </em>
        and change the
        <em>
            Scales
        </em>
        to
        <em>
            Single Scale
        </em>
        . This ensures you don’t need to use different scaled images for this
        asset.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/ScaleSelection.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/ScaleSelection.png"
            alt="" width="257" height="318" class="aligncenter size-full wp-image-164313">
        </a>
    </p>
    <p>
        When you’re done, your assets should look like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker_mac-assets-650x360.png"
        alt="Assets for Mac" width="650" height="360" class="aligncenter size-large wp-image-162153 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker_mac-assets-650x360.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker_mac-assets-480x266.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        In the top left of the
        <em>
            Xcode
        </em>
        window, select the
        <em>
            BeerTracker-mac
        </em>
        scheme in the scheme pop-up. Build and run, and you’ll see an empty window.
        Before you can start adding the user interface, you’ll need to make sure
        your code doesn’t have any conflicts between
        <em>
            UIKit
        </em>
        , the framework used on iOS, and
        <em>
            AppKit
        </em>
        , the framework used by macOS.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-Initial.png"
        alt="Mac starting window" width="592" height="404" class="aligncenter size-full wp-image-162150"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-Initial.png 592w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-Initial-469x320.png 469w"
        sizes="(max-width: 592px) 100vw, 592px">
    </p>
    <h2>
        Separation of Powers
    </h2>
    <p>
        The
        <em>
            Foundation
        </em>
        framework allows your app to share quite a bit of code, as it is universal
        to both platforms. However, your UI cannot be universal. In fact, Apple
        recommends that multi-platform applications should not attempt to share
        UI code, as your secondary platform will begin to take on the appearance
        of your initial application’s UI.
    </p>
    <p>
        iOS has some fairly strict
        <em>
            Human Interface Guidelines
        </em>
        that ensure your users are able to read and select elements on their touchscreen
        devices. However, macOS has different requirements. Laptops and desktops
        have a mouse pointer to click and select, allowing elements on the screen
        to be much smaller than would be possible on a phone.
    </p>
    <p>
        Having identified the UI as needing to be different on both platforms,
        it is also important to understand what other components of your code can
        be reused, and which ones need to be rewritten. Keep in mind that there
        isn’t necessarily a definitive right or wrong answer in most of these cases,
        and you will need to decide what works best for your app. Always remember
        that the more code shared, the less code you need to test and debug.
    </p>
    <p>
        Generally, you’ll be able to share models and model controllers. Open
        <em>
            Beer.swift
        </em>
        , and open the
        <em>
            Utilities
        </em>
        drawer in
        <em>
            Xcode
        </em>
        , and select the
        <em>
            File Inspector
        </em>
        . Since both targets will use this model, under
        <em>
            Target Membership
        </em>
        , check
        <em>
            BeerTracker-mac
        </em>
        leaving
        <em>
            BeerTracker
        </em>
        still checked. Do the same thing for
        <em>
            BeerManager.swift
        </em>
        , and
        <em>
            SharedAssets.xcassets
        </em>
        under the
        <em>
            Utilities
        </em>
        group.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership-245x320.png"
            alt="" width="245" height="320" class="aligncenter size-medium wp-image-164314"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership-245x320.png 245w, https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership.png 260w"
            sizes="(max-width: 245px) 100vw, 245px">
        </a>
    </p>
    <p>
        If you try to build and run, you will get a build error. This is because
        <em>
            Beer.swift
        </em>
        is importing
        <em>
            UIKit
        </em>
        . The model is using some platform specific logic to load and save images
        of beers.
    </p>
    <p>
        Replace the import line at the top of the file with the following:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            import
        </span>
        Foundation
    </pre>
    <p>
        If you try to build and run, you’ll see the app no longer compiles due
        to
        <em>
            UIImage
        </em>
        being part of the now removed
        <em>
            UIKit
        </em>
        . While the model portion of this file is shareable between both targets,
        the platform specific logic will need to be separated out. In
        <em>
            Beer.swift
        </em>
        , delete the entire extension marked
        <em>
            Image Saving
        </em>
        . After the
        <code>
            import
        </code>
        statement, add the following protocol:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-class">
            <span class="hljs-keyword">
                protocol
            </span>
            <span class="hljs-title">
                BeerImage
            </span>
        </span>
        { associatedtype
        <span class="hljs-type">
            Image
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                beerImage
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Image
        </span>
        ?
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                saveImage
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                image: Image)
            </span>
        </span>
        }
    </pre>
    <p>
        Since each target will still need access to the beer’s image, and to be
        able to save images, this protocol provides a contract that can be used
        across the two targets to accomplish this.
    </p>
    <h3>
        Models
    </h3>
    <p>
        Create a new file by going to
        <em>
            File/New/File…
        </em>
        , select
        <em>
            Swift File
        </em>
        , and name it
        <em>
            Beer_iOS.swift
        </em>
        . Ensure that only the
        <em>
            BeerTracker
        </em>
        target is checked. After that, create another new file named
        <em>
            Beer_mac.swift
        </em>
        , this time selecting
        <em>
            BeerTracker-mac
        </em>
        as the target.
    </p>
    <p>
        Open
        <em>
            Beer_iOS.swift
        </em>
        , delete the file’s contents, and add the following:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            import
        </span>
        UIKit
        <span class="hljs-comment">
            // MARK: - Image Saving
        </span>
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                Beer
            </span>
            :
            <span class="hljs-title">
                BeerImage
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            typealias
        </span>
        <span class="hljs-type">
            Image
        </span>
        =
        <span class="hljs-type">
            UIImage
        </span>
        <span class="hljs-comment">
            // 2.
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                beerImage
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Image
        </span>
        ? {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        imagePath = imagePath,
        <span class="hljs-keyword">
            let
        </span>
        path =
        <span class="hljs-type">
            NSSearchPathForDirectoriesInDomains
        </span>
        (.documentDirectory, .userDomainMask,
        <span class="hljs-literal">
            true
        </span>
        ).first
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        #imageLiteral(resourceName:
        <span class="hljs-string">
            "beerMugPlaceholder"
        </span>
        ) }
        <span class="hljs-comment">
            // 3.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        pathName = (path
        <span class="hljs-keyword">
            as
        </span>
        <span class="hljs-type">
            NSString
        </span>
        ).appendingPathComponent(
        <span class="hljs-string">
            "BeerTracker/
            <span class="hljs-subst">
                \(imagePath)
            </span>
            "
        </span>
        )
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        image =
        <span class="hljs-type">
            Image
        </span>
        (contentsOfFile: pathName)
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        #imageLiteral(resourceName:
        <span class="hljs-string">
            "beerMugPlaceholder"
        </span>
        ) }
        <span class="hljs-keyword">
            return
        </span>
        image }
        <span class="hljs-comment">
            // 4.
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                saveImage
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                image: Image)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        imgData =
        <span class="hljs-type">
            UIImageJPEGRepresentation
        </span>
        (image,
        <span class="hljs-number">
            0.5
        </span>
        ),
        <span class="hljs-keyword">
            let
        </span>
        path =
        <span class="hljs-type">
            NSSearchPathForDirectoriesInDomains
        </span>
        (.documentDirectory, .userDomainMask,
        <span class="hljs-literal">
            true
        </span>
        ).first
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-keyword">
            let
        </span>
        appPath = (path
        <span class="hljs-keyword">
            as
        </span>
        <span class="hljs-type">
            NSString
        </span>
        ).appendingPathComponent(
        <span class="hljs-string">
            "/BeerTracker"
        </span>
        )
        <span class="hljs-keyword">
            let
        </span>
        fileName =
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(UUID()
            </span>
            .uuidString).jpg"
        </span>
        <span class="hljs-keyword">
            let
        </span>
        pathName = (appPath
        <span class="hljs-keyword">
            as
        </span>
        <span class="hljs-type">
            NSString
        </span>
        ).appendingPathComponent(fileName)
        <span class="hljs-keyword">
            var
        </span>
        isDirectory:
        <span class="hljs-type">
            ObjCBool
        </span>
        =
        <span class="hljs-literal">
            false
        </span>
        <span class="hljs-keyword">
            if
        </span>
        !
        <span class="hljs-type">
            FileManager
        </span>
        .
        <span class="hljs-keyword">
            default
        </span>
        .fileExists(atPath: appPath, isDirectory: &amp;isDirectory) {
        <span class="hljs-keyword">
            do
        </span>
        {
        <span class="hljs-keyword">
            try
        </span>
        <span class="hljs-type">
            FileManager
        </span>
        .
        <span class="hljs-keyword">
            default
        </span>
        .createDirectory(atPath: pathName, withIntermediateDirectories:
        <span class="hljs-literal">
            true
        </span>
        , attributes:
        <span class="hljs-literal">
            nil
        </span>
        ) }
        <span class="hljs-keyword">
            catch
        </span>
        {
        <span class="hljs-built_in">
            print
        </span>
        (
        <span class="hljs-string">
            "Failed to create directory:
            <span class="hljs-subst">
                \(error)
            </span>
            "
        </span>
        ) } }
        <span class="hljs-keyword">
            if
        </span>
        (
        <span class="hljs-keyword">
            try
        </span>
        ? imgData.write(to:
        <span class="hljs-type">
            URL
        </span>
        (fileURLWithPath: pathName), options: [.atomic])) !=
        <span class="hljs-literal">
            nil
        </span>
        { imagePath = fileName } } }
    </pre>
    <p>
        Here’s what’s happening:
    </p>
    <ol>
        <li>
            The
            <em>
                BeerImage
            </em>
            protocol requires the implementing class to define an
            <em>
                associated type
            </em>
            . Think of this as a placeholder name for the type of object you really
            want to use, based on your object’s needs. Since this file is for iOS,
            you’re using
            <em>
                UIImage
            </em>
            .
        </li>
        <li>
            Implement the first protocol method. Here, the
            <em>
                Image
            </em>
            type represents
            <em>
                UIImage
            </em>
            .
        </li>
        <li>
            Another example of how the type alias can be used when initializing an
            image.
        </li>
        <li>
            Implement the second protocol method to save an image.
        </li>
    </ol>
    <p>
        Switch your scheme to
        <em>
            BeerTracker
        </em>
        , then build and run. The application should behave as before.
    </p>
    <p>
        Now that your iOS target is working, you’re ready to add macOS-specific
        code. Open
        <em>
            Beer_mac.swift
        </em>
        , delete all the contents, and add the following code:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            import
        </span>
        AppKit
        <span class="hljs-comment">
            // MARK: - Image Saving
        </span>
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                Beer
            </span>
            :
            <span class="hljs-title">
                BeerImage
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            typealias
        </span>
        <span class="hljs-type">
            Image
        </span>
        =
        <span class="hljs-type">
            NSImage
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                beerImage
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Image
        </span>
        ? {
        <span class="hljs-comment">
            // 2.
        </span>
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        imagePath = imagePath,
        <span class="hljs-keyword">
            let
        </span>
        path =
        <span class="hljs-type">
            NSSearchPathForDirectoriesInDomains
        </span>
        (.applicationSupportDirectory, .userDomainMask,
        <span class="hljs-literal">
            true
        </span>
        ).first
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        #imageLiteral(resourceName:
        <span class="hljs-string">
            "beerMugPlaceholder"
        </span>
        ) }
        <span class="hljs-keyword">
            let
        </span>
        pathName = (path
        <span class="hljs-keyword">
            as
        </span>
        <span class="hljs-type">
            NSString
        </span>
        ).appendingPathComponent(imagePath)
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        image =
        <span class="hljs-type">
            Image
        </span>
        (contentsOfFile: pathName)
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        #imageLiteral(resourceName:
        <span class="hljs-string">
            "beerMugPlaceholder"
        </span>
        ) }
        <span class="hljs-keyword">
            return
        </span>
        image }
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                saveImage
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                image: Image)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 3.
        </span>
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        imgData = image.tiffRepresentation,
        <span class="hljs-keyword">
            let
        </span>
        path =
        <span class="hljs-type">
            NSSearchPathForDirectoriesInDomains
        </span>
        (.applicationSupportDirectory, .userDomainMask,
        <span class="hljs-literal">
            true
        </span>
        ).first
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-keyword">
            let
        </span>
        fileName =
        <span class="hljs-string">
            "/BeerTracker/
            <span class="hljs-subst">
                \(UUID()
            </span>
            .uuidString).jpg"
        </span>
        <span class="hljs-keyword">
            let
        </span>
        pathName = (path
        <span class="hljs-keyword">
            as
        </span>
        <span class="hljs-type">
            NSString
        </span>
        ).appendingPathComponent(fileName)
        <span class="hljs-keyword">
            if
        </span>
        (
        <span class="hljs-keyword">
            try
        </span>
        ? imgData.write(to:
        <span class="hljs-type">
            URL
        </span>
        (fileURLWithPath: pathName), options: [.atomic])) !=
        <span class="hljs-literal">
            nil
        </span>
        { imagePath = fileName } } }
    </pre>
    <p>
        The above code is nearly identical to the previous code, with just a few
        changes:
    </p>
    <ol>
        <li>
            Here, instead of using
            <em>
                UIImage
            </em>
            , you’re using the
            <em>
                AppKit
            </em>
            specific class
            <em>
                NSImage
            </em>
            .
        </li>
        <li>
            On iOS, it’s common to save files in the Documents directory. You usually
            don’t have to worry about cluttering up this directory, since it is specific
            to the app and hidden from the user. On macOS, however, you won’t want
            to not mess up the user’s Documents, so you save the app’s files to the
            Application Support directory.
        </li>
        <li>
            Since
            <em>
                NSImage
            </em>
            doesn’t have the same method for getting image data as
            <em>
                UIImage
            </em>
            , you’re using the supported
            <code>
                tiffRepresentation
            </code>
            .
        </li>
    </ol>
    <p>
        Switch your target to
        <em>
            BeerTracker_mac
        </em>
        , then build and run. Your app now compiles for both platforms, while
        maintaining a standard set of functionality from your model.
    </p>
    <h3>
        Creating the User Interface
    </h3>
    <p>
        Your empty view Mac app isn’t very useful, so it’s time to build the UI.
        From the
        <em>
            BeerTracker-mac
        </em>
        group, open
        <em>
            Main.storyboard
        </em>
        . Start by dragging a
        <em>
            Table View
        </em>
        into your empty view. Now select the
        <em>
            Table View
        </em>
        in the Document Outline.
        <br>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView-650x413.png"
        alt="Adding a table view" width="650" height="413" class="aligncenter size-large wp-image-162919"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView-650x413.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView-480x305.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView.png 1552w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        macOS storyboards sometimes require you to dig down a bit deeper into
        the view hierarchy. This is a change from iOS, where you’re used to seeing
        all template views at the top level.
    </p>
    <h3>
        Configuring the Table View
    </h3>
    <p>
        With the
        <em>
            Table View
        </em>
        selected, make the following changes in the Attributes Inspector:
    </p>
    <ul>
        <li>
            Set
            <em>
                Columns
            </em>
            to 1
        </li>
        <li>
            Uncheck
            <em>
                Reordering
            </em>
        </li>
        <li>
            Uncheck
            <em>
                Resizing
            </em>
        </li>
    </ul>
    <p>
        Select the
        <em>
            Table Column
        </em>
        in the Document Outline and set its Title to
        <em>
            Beer Name
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/Beer-TrackerSelect-Table-View-2.png"
        alt="Selecting the table view" width="268" height="222" class="aligncenter size-medium wp-image-163228"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/Beer-TrackerSelect-Table-View-2.png 537w, https://koenig-media.raywenderlich.com/uploads/2017/05/Beer-TrackerSelect-Table-View-2-387x320.png 387w"
        sizes="(max-width: 268px) 100vw, 268px">
    </p>
    <p>
        In the Document Outline, select the
        <em>
            Bordered Scroll View
        </em>
        (which houses the
        <em>
            Table View
        </em>
        ), and in the Size Inspector find the View section and set the View dimensions
        to the following:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 0
        </li>
        <li>
            <em>
                y
            </em>
            : 17
        </li>
        <li>
            <em>
                width
            </em>
            : 185
        </li>
        <li>
            <em>
                height
            </em>
            : 253
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings-229x320.png"
            alt="" width="229" height="320" class="aligncenter size-medium wp-image-164315"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings-229x320.png 229w, https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings.png 255w"
            sizes="(max-width: 229px) 100vw, 229px">
        </a>
    </p>
    <p>
        Setting the coordinates is going to be slightly different here, as well.
        In macOS, the origin of the UI is not in the top left, but the lower left.
        Here, you’ve set the
        <em>
            y
        </em>
        coordinate to 17, which means 17 points up from the bottom.
    </p>
    <h3>
        Adding a Delegate and Data Source
    </h3>
    <p>
        Next you’ll need to connect your delegate, data source and properties
        for the
        <em>
            Table View
        </em>
        . Again, you’ll need to select the
        <em>
            Table View
        </em>
        from the Document Outline to do this. With it selected, you can
        <em>
            Control-drag
        </em>
        to the
        <em>
            View Controller
        </em>
        item in the Document Outline and click
        <em>
            delegate
        </em>
        . Repeat this for the
        <em>
            dataSource
        </em>
        .
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        in the Assistant Editor,
        <em>
            Control-drag
        </em>
        from the
        <em>
            Table View
        </em>
        and create a new outlet named
        <code>
            tableView
        </code>
        .
    </p>
    <p>
        Before you finish with the
        <em>
            Table View
        </em>
        , there’s one last thing you need to set. Back in the Document Outline,
        find the item named
        <em>
            Table Cell View
        </em>
        . With that selected, open the Identity Inspector, and set the
        <em>
            Identifier
        </em>
        to
        <em>
            NameCell
        </em>
        .
    </p>
    <h3>
        Images and Text
    </h3>
    <p>
        With the
        <em>
            Table View
        </em>
        setup, next comes the “form” section of the UI.
    </p>
    <p>
        First, you’ll add an
        <em>
            Image Well
        </em>
        to the right of the table. Set the frame to the following:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 190
        </li>
        <li>
            <em>
                y
            </em>
            : 188
        </li>
        <li>
            <em>
                width
            </em>
            : 75
        </li>
        <li>
            <em>
                height
            </em>
            : 75
        </li>
    </ul>
    <p>
        An
        <em>
            Image Well
        </em>
        is a convenient object that displays an image, but also allows a user
        to drag and drop a picture onto it. To accomplish this, the
        <em>
            Image Well
        </em>
        has the ability to connect an action to your code!
    </p>
    <p>
        Open the BeerTracker-mac
        <em>
            ViewController.swift
        </em>
        in the Assistant Editor and create an outlet for the
        <em>
            Image Well
        </em>
        named
        <code>
            imageView
        </code>
        . Also create an action for the
        <em>
            Image View
        </em>
        , and name it
        <code>
            imageChanged
        </code>
        . Ensure that you change
        <em>
            Type
        </em>
        to
        <em>
            NSImageView
        </em>
        , as shown:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Image-View-Action-2.png"
        alt="Adding the imageView action." width="300" height="141" class="aligncenter size-full wp-image-163219">
    </p>
    <p>
        While drag and drop is great, sometimes users want to be able to view
        an
        <em>
            Open Dialog
        </em>
        and search for the file themselves. Set this up by dropping a
        <em>
            Click Gesture Recognizer
        </em>
        on the
        <em>
            Image Well
        </em>
        . In the Document Outline, connect an action from the
        <em>
            Click Gesture Recognizer
        </em>
        to
        <em>
            ViewController.swift
        </em>
        named
        <code>
            selectImage
        </code>
        .
    </p>
    <p>
        Add a
        <em>
            Text Field
        </em>
        to the right of the
        <em>
            Image Well
        </em>
        . In the Attributes Inspector, change the
        <em>
            Placeholder
        </em>
        to
        <em>
            Enter Name
        </em>
        . Set the frame to the following:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 270
        </li>
        <li>
            <em>
                y
            </em>
            : 223
        </li>
        <li>
            <em>
                width
            </em>
            : 190
        </li>
        <li>
            <em>
                height
            </em>
            : 22
        </li>
    </ul>
    <p>
        Create an outlet in
        <em>
            ViewController.swift
        </em>
        for the
        <em>
            Text Field
        </em>
        named
        <code>
            nameField
        </code>
        .
    </p>
    <h3>
        Rating a Beer
    </h3>
    <p>
        Next, add a
        <em>
            Level Indicator
        </em>
        below the name field. This will control setting the rating of your beers.
        In the Attributes Inspector, set the following:
    </p>
    <ul>
        <li>
            <em>
                Style
            </em>
            : Rating
        </li>
        <li>
            <em>
                State
            </em>
            : Editable
        </li>
        <li>
            <em>
                Minimum
            </em>
            : 0
        </li>
        <li>
            <em>
                Maximum
            </em>
            : 5
        </li>
        <li>
            <em>
                Warning
            </em>
            : 0
        </li>
        <li>
            <em>
                Critical
            </em>
            : 0
        </li>
        <li>
            <em>
                Current
            </em>
            : 5
        </li>
        <li>
            <em>
                Image
            </em>
            : beerMug
        </li>
    </ul>
    <p>
        Set the frame to the following:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 270
        </li>
        <li>
            <em>
                y
            </em>
            : 176
        </li>
        <li>
            <em>
                width
            </em>
            : 115
        </li>
    </ul>
    <p>
        Create an outlet for the
        <em>
            Level Indicator
        </em>
        named
        <code>
            ratingIndicator
        </code>
        .
    </p>
    <p>
        Add a
        <em>
            Text View
        </em>
        below the rating indicator. Set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 193
        </li>
        <li>
            <em>
                y
            </em>
            : 37
        </li>
        <li>
            <em>
                width
            </em>
            : 267
        </li>
        <li>
            <em>
                height
            </em>
            : 134
        </li>
    </ul>
    <p>
        To create an outlet for the
        <em>
            Text View
        </em>
        , you’ll need to make sure you select
        <em>
            Text View
        </em>
        inside the Document Outline, like you did with the
        <em>
            Table View
        </em>
        . Name the outlet
        <code>
            noteView
        </code>
        . You’ll also need to set the
        <em>
            Text View
        </em>
        ‘s delegate to the
        <em>
            ViewController
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TextView.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TextView.png"
            alt="" width="216" height="84" class="aligncenter size-full wp-image-164317">
        </a>
    </p>
    <p>
        Below the note view, drop in a
        <em>
            Push Button
        </em>
        . Change the title to
        <em>
            Update
        </em>
        , and set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 284
        </li>
        <li>
            <em>
                y
            </em>
            : 3
        </li>
        <li>
            <em>
                width
            </em>
            : 85
        </li>
    </ul>
    <p>
        Connect an action from the button to
        <em>
            ViewController
        </em>
        named
        <code>
            updateBeer
        </code>
        .
    </p>
    <h3>
        Adding and Removing Beers
    </h3>
    <p>
        With that, you have all the necessary controls to edit and view your beer
        information. However, there’s no way to add or remove beers. This will
        make the app difficult to use, even if your users haven’t had anything
        to drink. :]
    </p>
    <p>
        Add a
        <em>
            Gradient Button
        </em>
        to the bottom left of the screen. In the Attributes Inspector, change
        <em>
            Image
        </em>
        to
        <em>
            NSAddTemplate
        </em>
        if it is not already set.
    </p>
    <p>
        In the Size Inspector, set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 0
        </li>
        <li>
            <em>
                y
            </em>
            : -1
        </li>
        <li>
            <em>
                width
            </em>
            : 24
        </li>
        <li>
            <em>
                height
            </em>
            : 20
        </li>
    </ul>
    <p>
        Add an action from the new button named
        <code>
            addBeer
        </code>
        .
    </p>
    <p>
        One great thing about macOS is that you get access to template images
        like the
        <em>
            +
        </em>
        sign. This can make your life a lot simpler when you have any standard
        action buttons, but don’t have the time or ability to create your own artwork.
    </p>
    <p>
        Next, you’ll need to add the remove button. Add another
        <em>
            Gradient Button
        </em>
        directly to the right of the previous button, and change the
        <em>
            Image
        </em>
        to
        <em>
            NSRemoveTemplate
        </em>
        . Set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 23
        </li>
        <li>
            <em>
                y
            </em>
            : -1
        </li>
        <li>
            <em>
                width
            </em>
            : 24
        </li>
        <li>
            <em>
                height
            </em>
            : 20
        </li>
    </ul>
    <p>
        And finally, add an action from this button named
        <code>
            removeBeer
        </code>
        .
    </p>
    <h3>
        Finishing The UI
    </h3>
    <p>
        You’re almost finished building the UI! You just need to add a few labels
        to help polish it off.
    </p>
    <p>
        Add the following labels:
    </p>
    <ul>
        <li>
            Above the name field, titled
            <em>
                Name
            </em>
            .
        </li>
        <li>
            Above the rating indicator titled
            <em>
                Rating
            </em>
            .
        </li>
        <li>
            Above the notes view titled
            <em>
                Notes
            </em>
            .
        </li>
        <li>
            Beneath the table view titled
            <em>
                Beer Count:
            </em>
            .
        </li>
        <li>
            To the right of the beer count label, titled
            <em>
                0
            </em>
            .
        </li>
    </ul>
    <p>
        For each of these labels, in the Attributes Inspector, set the font to
        <em>
            Other – Label
        </em>
        , and the size to 10.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/labelFont.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/labelFont.png"
            alt="" width="196" height="285" class="aligncenter size-full wp-image-164319">
        </a>
    </p>
    <p>
        For the last label, connect an outlet to
        <em>
            ViewController.swift
        </em>
        named
        <code>
            beerCountField
        </code>
        .
    </p>
    <p>
        Make sure your labels all line like so:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2.png"
        alt="Final UI" width="600" height="374" class="aligncenter size-full wp-image-163220"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2-480x299.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        Click the Resolve
        <em>
            Auto Layout Issues
        </em>
        button and in the
        <em>
            All Views in View Controller
        </em>
        section click
        <em>
            Reset to Suggested Constraints
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/AutoLayout-1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/AutoLayout-1.png"
            alt="" width="243" height="197" class="aligncenter size-full wp-image-164423">
        </a>
    </p>
    <h3>
        Adding the Code
    </h3>
    <p>
        Whew! Now you’re ready to code. Open
        <em>
            ViewController.swift
        </em>
        and delete the property named
        <code>
            representedObject
        </code>
        . Add the following methods below
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            private
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                setFieldsEnabled
            </span>
            <span class="hljs-params">
                (enabled: Bool)
            </span>
        </span>
        { imageView.isEditable = enabled nameField.isEnabled = enabled ratingIndicator.isEnabled
        = enabled noteView.isEditable = enabled }
        <span class="hljs-keyword">
            private
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                updateBeerCountLabel
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        { beerCountField.stringValue =
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(BeerManager.sharedInstance.beers.
                <span class="hljs-built_in">
                    count
                </span>
                )
            </span>
            "
        </span>
        }
    </pre>
    <p>
        There are two methods that will help you control your UI:
    </p>
    <ol>
        <li>
            <code>
                setFieldsEnabled(_:)
            </code>
            will allow you to easily turn off and on the ability to use the form controls.
        </li>
        <li>
            <code>
                updateBeerCountLabel()
            </code>
            simply sets the count of beers in the
            <code>
                beerCountField
            </code>
            .
        </li>
    </ol>
    <p>
        Beneath all of your outlets, add the following property:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            var
        </span>
        selectedBeer:
        <span class="hljs-type">
            Beer
        </span>
        ? {
        <span class="hljs-keyword">
            didSet
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        selectedBeer = selectedBeer
        <span class="hljs-keyword">
            else
        </span>
        { setFieldsEnabled(enabled:
        <span class="hljs-literal">
            false
        </span>
        ) imageView.image =
        <span class="hljs-literal">
            nil
        </span>
        nameField.stringValue =
        <span class="hljs-string">
            ""
        </span>
        ratingIndicator.integerValue =
        <span class="hljs-number">
            0
        </span>
        noteView.string =
        <span class="hljs-string">
            ""
        </span>
        <span class="hljs-keyword">
            return
        </span>
        } setFieldsEnabled(enabled:
        <span class="hljs-literal">
            true
        </span>
        ) imageView.image = selectedBeer.beerImage() nameField.stringValue = selectedBeer.name
        ratingIndicator.integerValue = selectedBeer.rating noteView.string = selectedBeer.note!
        } }
    </pre>
    <p>
        This property will keep track of the beer selected from the table view.
        If no beer is currently selected, the setter takes care of clearing the
        values from all the fields, and disabling the UI components that shouldn’t
        be used.
    </p>
    <p>
        Replace
        <code>
            viewDidLoad()
        </code>
        with the following code:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            override
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                viewDidLoad
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        {
        <span class="hljs-keyword">
            super
        </span>
        .viewDidLoad()
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.
        <span class="hljs-built_in">
            count
        </span>
        ==
        <span class="hljs-number">
            0
        </span>
        { setFieldsEnabled(enabled:
        <span class="hljs-literal">
            false
        </span>
        ) }
        <span class="hljs-keyword">
            else
        </span>
        { tableView.selectRowIndexes(
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ), byExtendingSelection:
        <span class="hljs-literal">
            false
        </span>
        ) } updateBeerCountLabel() }
    </pre>
    <p>
        Just like in iOS, you want our app to do something the moment it starts
        up. In the macOS version, however, you’ll need to immediately fill out
        the form for the user to see their data.
    </p>
    <h3>
        Adding Data to the Table View
    </h3>
    <p>
        Right now, the table view isn’t actually able to display any data, but
        <code>
            selectRowIndexes(_:byExtendingSelection:)
        </code>
        will select the first beer in the list. The delegate code will handle
        the rest for you.
    </p>
    <p>
        In order to get the table view showing you your list of beers, add the
        following code to the end of
        <em>
            ViewController.swift
        </em>
        , outside of the
        <code>
            ViewController
        </code>
        class:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                ViewController
            </span>
            :
            <span class="hljs-title">
                NSTableViewDataSource
            </span>
        </span>
        {
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                numberOfRows
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-keyword">
                    in
                </span>
                tableView: NSTableView)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Int
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.
        <span class="hljs-built_in">
            count
        </span>
        } }
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                ViewController
            </span>
            :
            <span class="hljs-title">
                NSTableViewDelegate
            </span>
        </span>
        {
        <span class="hljs-comment">
            // MARK: - CellIdentifiers
        </span>
        <span class="hljs-keyword">
            fileprivate
        </span>
        <span class="hljs-class">
            <span class="hljs-keyword">
                enum
            </span>
            <span class="hljs-title">
                CellIdentifier
            </span>
        </span>
        {
        <span class="hljs-keyword">
            static
        </span>
        <span class="hljs-keyword">
            let
        </span>
        <span class="hljs-type">
            NameCell
        </span>
        =
        <span class="hljs-string">
            "NameCell"
        </span>
        }
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                tableView
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                tableView: NSTableView, viewFor tableColumn: NSTableColumn?, row: Int)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSView
        </span>
        ? {
        <span class="hljs-keyword">
            let
        </span>
        beer =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers[row]
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        cell = tableView.makeView(withIdentifier:
        <span class="hljs-type">
            NSUserInterfaceItemIdentifier
        </span>
        (rawValue:
        <span class="hljs-type">
            CellIdentifier
        </span>
        .
        <span class="hljs-type">
            NameCell
        </span>
        ), owner:
        <span class="hljs-literal">
            nil
        </span>
        )
        <span class="hljs-keyword">
            as
        </span>
        ?
        <span class="hljs-type">
            NSTableCellView
        </span>
        { cell.textField?.stringValue = beer.name
        <span class="hljs-keyword">
            if
        </span>
        beer.name.characters.
        <span class="hljs-built_in">
            count
        </span>
        ==
        <span class="hljs-number">
            0
        </span>
        { cell.textField?.stringValue =
        <span class="hljs-string">
            "New Beer"
        </span>
        }
        <span class="hljs-keyword">
            return
        </span>
        cell }
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            nil
        </span>
        }
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                tableViewSelectionDidChange
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                notification: Notification)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            if
        </span>
        tableView.selectedRow &gt;=
        <span class="hljs-number">
            0
        </span>
        { selectedBeer =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers[tableView.selectedRow] } } }
    </pre>
    <p>
        This code takes care of populating the table view’s rows from the data
        source.
    </p>
    <p>
        Look at it closely, and you’ll see it’s not too different from the iOS
        counterpart found in
        <em>
            BeersTableViewController.swift
        </em>
        . One notable difference is that when the table view selection changes,
        it sends a
        <em>
            Notification
        </em>
        to the
        <em>
            NSTableViewDelegate
        </em>
        .
    </p>
    <p>
        Remember that your new macOS app has multiple input sources — not just
        a finger. Using a mouse or keyboard can change the selection of the table
        view, and that makes handling the change just a little different to iOS.
    </p>
    <p>
        Now to add a beer. Change
        <code>
            addBeer()
        </code>
        to:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                addBeer
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        beer =
        <span class="hljs-type">
            Beer
        </span>
        () beer.name =
        <span class="hljs-string">
            ""
        </span>
        beer.rating =
        <span class="hljs-number">
            1
        </span>
        beer.note =
        <span class="hljs-string">
            ""
        </span>
        selectedBeer = beer
        <span class="hljs-comment">
            // 2.
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.insert(beer, at:
        <span class="hljs-number">
            0
        </span>
        )
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.saveBeers()
        <span class="hljs-comment">
            // 3.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        indexSet =
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ) tableView.beginUpdates() tableView.insertRows(at: indexSet, withAnimation:
        .slideDown) tableView.endUpdates() updateBeerCountLabel()
        <span class="hljs-comment">
            // 4.
        </span>
        tableView.selectRowIndexes(
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ), byExtendingSelection:
        <span class="hljs-literal">
            false
        </span>
        ) }
    </pre>
    <p>
        Nothing too crazy here. You’re simply doing the following:
    </p>
    <ol>
        <li>
            Creating a new beer.
        </li>
        <li>
            Inserting the beer into the model.
        </li>
        <li>
            Inserting a new row into the table.
        </li>
        <li>
            Selecting the row of the new beer.
        </li>
    </ol>
    <p>
        You might have even noticed that, like in iOS, you need to call
        <code>
            beginUpdates()
        </code>
        and
        <code>
            endUpdates()
        </code>
        before inserting the new row. See, you really do know a lot about macOS
        already!
    </p>
    <h3>
        Removing Entries
    </h3>
    <p>
        To remove a beer, add the below code for
        <code>
            removeBeer(_:)
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                removeBeer
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        beer = selectedBeer,
        <span class="hljs-keyword">
            let
        </span>
        index =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.index(of: beer)
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.remove(at: index)
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.saveBeers()
        <span class="hljs-comment">
            // 2
        </span>
        tableView.reloadData() updateBeerCountLabel() tableView.selectRowIndexes(
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ), byExtendingSelection:
        <span class="hljs-literal">
            false
        </span>
        )
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.
        <span class="hljs-built_in">
            count
        </span>
        ==
        <span class="hljs-number">
            0
        </span>
        { selectedBeer =
        <span class="hljs-literal">
            nil
        </span>
        } }
    </pre>
    <p>
        Once again, very straightforward code:
    </p>
    <ol>
        <li>
            If a beer is selected, you remove it from the model.
        </li>
        <li>
            Reload the table view, and select the first available beer.
        </li>
    </ol>
    <h3>
        Handling Images
    </h3>
    <p>
        Remember how
        <em>
            Image Wells
        </em>
        have the ability to accept an image dropped on them? Change
        <code>
            imageChanged(_:)
        </code>
        to:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                imageChanged
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: NSImageView)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        image = sender.image
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        } selectedBeer?.saveImage(image) }
    </pre>
    <p>
        And you thought it was going to be hard! Apple has taken care of all the
        heavy lifting for you, and provides you with the image dropped.
    </p>
    <p>
        On the flip side to that, you’ll need to do a bit more work to handle
        user’s picking the image from within your app. Replace
        <code>
            selectImage()
        </code>
        with:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                selectImage
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        window = view.window
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        openPanel =
        <span class="hljs-type">
            NSOpenPanel
        </span>
        () openPanel.allowsMultipleSelection =
        <span class="hljs-literal">
            false
        </span>
        openPanel.canChooseDirectories =
        <span class="hljs-literal">
            false
        </span>
        openPanel.canCreateDirectories =
        <span class="hljs-literal">
            false
        </span>
        openPanel.canChooseFiles =
        <span class="hljs-literal">
            true
        </span>
        <span class="hljs-comment">
            // 2.
        </span>
        openPanel.allowedFileTypes = [
        <span class="hljs-string">
            "jpg"
        </span>
        ,
        <span class="hljs-string">
            "png"
        </span>
        ,
        <span class="hljs-string">
            "tiff"
        </span>
        ]
        <span class="hljs-comment">
            // 3.
        </span>
        openPanel.beginSheetModal(
        <span class="hljs-keyword">
            for
        </span>
        : window) { (result)
        <span class="hljs-keyword">
            in
        </span>
        <span class="hljs-keyword">
            if
        </span>
        result ==
        <span class="hljs-type">
            NSApplication
        </span>
        .
        <span class="hljs-type">
            ModalResponse
        </span>
        .
        <span class="hljs-type">
            OK
        </span>
        {
        <span class="hljs-comment">
            // 4.
        </span>
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        panelURL = openPanel.url,
        <span class="hljs-keyword">
            let
        </span>
        beerImage =
        <span class="hljs-type">
            NSImage
        </span>
        (contentsOf: panelURL) {
        <span class="hljs-keyword">
            self
        </span>
        .selectedBeer?.saveImage(beerImage)
        <span class="hljs-keyword">
            self
        </span>
        .imageView.image = beerImage } } } }
    </pre>
    <p>
        The above code is how you use
        <code>
            NSOpenPanel
        </code>
        to select a file. Here’s what’s happening:
    </p>
    <ol>
        <li>
            You create an
            <code>
                NSOpenPanel
            </code>
            , and configure its settings.
        </li>
        <li>
            In order to allow the user to choose only pictures, you set the allowed
            file types to your preferred image formats.
        </li>
        <li>
            Present the sheet to the user.
        </li>
        <li>
            Save the image if the user selected one.
        </li>
    </ol>
    <p>
        Finally, add the code that will save the data model in
        <code>
            updateBeer(_:)
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                updateBeer
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        beer = selectedBeer,
        <span class="hljs-keyword">
            let
        </span>
        index =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.index(of: beer)
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        } beer.name = nameField.stringValue beer.rating = ratingIndicator.integerValue
        beer.note = noteView.string
        <span class="hljs-comment">
            // 2.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        indexSet =
        <span class="hljs-type">
            IndexSet
        </span>
        (integer: index) tableView.beginUpdates() tableView.reloadData(forRowIndexes:
        indexSet, columnIndexes:
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        )) tableView.endUpdates()
        <span class="hljs-comment">
            // 3.
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.saveBeers() }
    </pre>
    <p>
        Here’s what you added:
    </p>
    <ol>
        <li>
            You ensure the beer exists, and update its properties.
        </li>
        <li>
            Update the table view to reflect any names changes in the table.
        </li>
        <li>
            Save the data to the disk.
        </li>
    </ol>
    <p>
        You’re all set! Build and run the app, and start adding beers. Remember,
        you’ll need to select
        <em>
            Update
        </em>
        to save your data.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers.png"
        alt="Final UI with some beers added." width="600" height="374" class="aligncenter size-full wp-image-163221"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers-480x299.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <h3>
        Final Touches
    </h3>
    <p>
        You’ve learned a lot about the similarities and differences between iOS
        and macOS development. There’s another concept that you should familiarize
        yourself with:
        <em>
            Settings/Preferences
        </em>
        . In iOS, you should be comfortable with the concept of going into Settings,
        finding your desired app, and changing any settings available to you. In
        macOS, this can be accomplished inside your app through
        <em>
            Preferences
        </em>
        .
    </p>
    <p>
        Build and run the
        <em>
            BeerTracker
        </em>
        target, and in the simulator, navigate to the BeerTracker settings in
        the Settings app. There you’ll find a setting allowing your users to limit
        the length of their notes, just in case they get a little chatty after
        having a few.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-282x500.png"
        alt="Settings - iOS" width="282" height="500" class="aligncenter size-large wp-image-162952"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-282x500.png 282w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-180x320.png 180w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings.png 640w"
        sizes="(max-width: 282px) 100vw, 282px">
    </p>
    <p>
        In order to get the same feature in your mac app, you’ll create a Preferences
        window for the user. In
        <em>
            BeerTracker-mac
        </em>
        , open
        <em>
            Main.storyboard
        </em>
        , and drop in a new
        <em>
            Window Controller
        </em>
        . Select the
        <em>
            Window
        </em>
        , open the Size Inspector, and change the following:
    </p>
    <ol>
        <li>
            Set
            <em>
                Content Size
            </em>
            width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Minimum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Maximum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Full Screen Minimum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Full Screen Maximum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Under
            <em>
                Initial Position
            </em>
            , select
            <em>
                Center Horizontally
            </em>
            and
            <em>
                Center Vertically
            </em>
            .
        </li>
    </ol>
    <p>
        Next, select the View of the empty View Controller, and change the size
        to match the above settings, 380 x 55.
    </p>
    <p>
        Doing these things will ensure your Preferences window is always the same
        size, and opens in a logical place to the user. When you’re finished, your
        new window should look like this in the storyboard:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1.png"
        alt="Preferences - Mac" width="700" height="477" class="aligncenter size-full wp-image-163222"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1-470x320.png 470w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1-650x443.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        At this point, there is no way for a user to open your new window. Since
        it should be tied to the
        <em>
            Preferences
        </em>
        menu item, find the menu bar scene in storyboard. It will be easier if
        you drag it close to the Preferences window for this next part. Once it
        is close enough, do the following:
    </p>
    <ol>
        <li>
            In the menu bar in storyboard, click
            <em>
                BeerTracker-mac
            </em>
            to open the menu.
        </li>
        <li>
            <em>
                Control-drag
            </em>
            from the
            <em>
                Preferences
            </em>
            menu item to the new Window Controller
        </li>
        <li>
            Select
            <em>
                Show
            </em>
            from the dialog
        </li>
    </ol>
    <p>
        Find a
        <em>
            Check Box Button
        </em>
        , and add it to the empty View Controller. Change the text to be
        <em>
            Restrict Note Length to 1,024 Characters
        </em>
        .
    </p>
    <p>
        With the
        <em>
            Checkbox Button
        </em>
        selected, open the Bindings Inspector, and do the following:
    </p>
    <ol>
        <li>
            Expand
            <em>
                Value
            </em>
            , and check
            <em>
                Bind to
            </em>
            .
        </li>
        <li>
            Select
            <em>
                Shared User Defaults Controller
            </em>
            from the drop down.
        </li>
        <li>
            In
            <em>
                Model Key Path
            </em>
            , put
            <em>
                BT_Restrict_Note_Length
            </em>
            .
        </li>
    </ol>
    <p>
        Create a new Swift file in the
        <em>
            Utilities
        </em>
        group named
        <em>
            StringValidator.swift
        </em>
        . Make sure to check both targets for this file.
    </p>
    <p>
        Open
        <em>
            StringValidator.swift
        </em>
        , and replace the contents with the following code:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            import
        </span>
        Foundation
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                String
            </span>
        </span>
        {
        <span class="hljs-keyword">
            private
        </span>
        <span class="hljs-keyword">
            static
        </span>
        <span class="hljs-keyword">
            let
        </span>
        noteLimit =
        <span class="hljs-number">
            1024
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                isValidLength
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-keyword">
            let
        </span>
        limitLength =
        <span class="hljs-type">
            UserDefaults
        </span>
        .standard.bool(forKey:
        <span class="hljs-string">
            "BT_Restrict_Note_Length"
        </span>
        )
        <span class="hljs-keyword">
            if
        </span>
        limitLength {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-keyword">
            self
        </span>
        .characters.
        <span class="hljs-built_in">
            count
        </span>
        &lt;=
        <span class="hljs-type">
            String
        </span>
        .noteLimit }
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            true
        </span>
        } }
    </pre>
    <p>
        This class will provide both targets with the ability to check if a string
        is a valid length, but only if the user default
        <em>
            BT_Restrict_Note_Length
        </em>
        is true.
    </p>
    <p>
        In
        <em>
            ViewController.swift
        </em>
        add the following code at the bottom:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                ViewController
            </span>
            :
            <span class="hljs-title">
                NSTextViewDelegate
            </span>
        </span>
        {
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                textView
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                textView: NSTextView, shouldChangeTextIn affectedCharRange: NSRange, replacementString:
                String?)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        replacementString = replacementString
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            true
        </span>
        }
        <span class="hljs-keyword">
            let
        </span>
        currentText = textView.string
        <span class="hljs-keyword">
            let
        </span>
        proposed = (currentText
        <span class="hljs-keyword">
            as
        </span>
        <span class="hljs-type">
            NSString
        </span>
        ).replacingCharacters(
        <span class="hljs-keyword">
            in
        </span>
        : affectedCharRange, with: replacementString)
        <span class="hljs-keyword">
            return
        </span>
        proposed.isValidLength() } }
    </pre>
    <p>
        Finally, change the names of each
        <em>
            Window
        </em>
        in
        <em>
            Main.storyboard
        </em>
        to match their purpose, and give the user more clarity. Select the initial
        <em>
            Window Controller
        </em>
        , and in the
        <em>
            Attributes Inspector
        </em>
        change the title to
        <em>
            BeerTracker
        </em>
        . Select the
        <em>
            Window Controller
        </em>
        for the Preferences window, and change the title to
        <em>
            Preferences
        </em>
        .
    </p>
    <p>
        Build and run your app. If you select the Preferences menu item, you should
        now see your new Preferences window with your preferences item. Select
        the checkbox, and find some large amount of text to paste in. If this would
        make the note more 1024 characters, the
        <em>
            Text View
        </em>
        will not accept it, just like the iOS app.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM.png"
        alt="Build and Run with Preferences" width="484" height="297" class="alignnone size-full wp-image-164558"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM.png 484w, https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM-480x295.png 480w"
        sizes="(max-width: 484px) 100vw, 484px">
    </p>
    <h2>
        Where to Go From Here?
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses" sl-processed="1">
                <div class="col-wrapper">
                    <div class="col">
                        <img src="https://koenig-assets.raywenderlich.com/wp-content/themes/raywenderlich/images/global/video-yeti@2x.png"
                        alt="yeti holding videos">
                    </div>
                    <div class="col large-col">
                        <span>
                            Want to learn even faster? Save time with our
                            <span>
                                video courses
                            </span>
                        </span>
                    </div>
                </div>
            </a>
        </div>
    </div>
    <p>
        You can download the finished project
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/BeerTracker-Port_Finished-2.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        In this tutorial you learned:
    </p>
    <ul>
        <li>
            How to utilize a current iOS project to host a macOS app.
        </li>
        <li>
            When to separate code based on your platform's needs.
        </li>
        <li>
            How to reuse existing code between both projects.
        </li>
        <li>
            The differences between some of Xcode's behaviors between the two platforms.
        </li>
    </ul>
    <p>
        For more information about porting your apps to macOS, check out
        <a href="https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/OSX_Technology_Overview/MigratingFromCocoaTouch/MigratingFromCocoaTouch.html"
        sl-processed="1">
            Apple's Migrating from Cocoa Touch Overview
        </a>
        .
    </p>
    <p>
        If you have any questions or comments, please join in the forum discussion
        below!
    </p>
</div>