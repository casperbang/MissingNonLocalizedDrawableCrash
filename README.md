# MissingNonLocalizedDrawableCrash
Demo project showing what happens when you don't provide non-localized fall-back drawables (crashes!)

Neither Android Studio nor Lint will flag this. As a result, it's easy to end up with production error reports like this:

android.content.res.Resources$NotFoundException: Resource ID #0x7f02005d
	at android.content.res.Resources.getValue(Resources.java:1343)
	at android.content.res.Resources.getDrawable(Resources.java:819)
	at android.content.res.Resources.getDrawable(Resources.java:799)
	at android.content.Context.getDrawable(Context.java:403)
	
This happens because some users can have a device language which does not match an apps localized drawables. The algorithm for resource selection falls back to using non-localized resources so Android Studio or Lint really should try to catch this problem up-front.

This demo application includes a drawable for Danish so everything compiles, with no Lint warnings and no Google Play deployment warnings - yet it crashes horrible on anything but a Danish device.
