iOSUtils
========

UpdateStoryBoardStrings.sh
--------------------------
Given a usual project setup for Project P

P.xcodeproj
P (folder)

You'll need to issue this command as follows:

$ UpdateStoryboardStrings.sh P

UpdateCodeStrings.sh
--------------------
You need to issue this from the project folder. This command does NOT update the Localizable.strings in your base.lproj folder. It only takes the new strings from your .m code files and generates them into all the existing language files. It does not provide support for parametrizable messages, as based on the following code:

    NSString *s = [NSString stringWithFormat:NSLocalizedString(@"sales", @"Comment for sales text"), @(123)];

It will generate

    /* Comment for sales text */
    "sales" = "Comment for sales text";

Whereas you would want something like:

    "sellertext" = "You have sold %1@ apps yesterday.";

Which is not very helpful to be honest. 

I've modified the original script so it takes a default value and a comment, separated by ';' as seen here:

    NSString *s = [NSString stringWithFormat:NSLocalizedString(@"sellertext", 
                            @"You have sold %1$i apps yesterday;Comment for seller text"), @(123)];

If you define the localizable strings like below, the UpdateCodeStrings.sh will generate this:


    /*  Comment for seller text" */
    "sellertext" = "You have sold %1$i apps yesterday;

If you do not want to specify a comment you will need to close the string with a ';' - yes annoying, but I have no time now to fiddle with this... and anyway, comments are good! :)

Original project (for the two shell scripts): https://github.com/AppliedIS/iOSL10n
