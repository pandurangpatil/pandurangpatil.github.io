+++
title = "Install Eclipse Maven plugin and import maven project"
slug = "2014-03-27-install-eclipse-maven-plugin-and-import-maven-project"
published = 2014-03-27T02:09:00-07:00
author = "Pandurang Patil"
tags = [ "eclipse", "m2e", "GWT", "maven",]
+++
With new versions of `Eclipse` old `m2e` plugins have become absolute now you need to install `eclipse` plugins from `eclipse` market place. Follow below steps to install `m2e` plugins along with required `GWT` plugins. I have tried below steps with `Eclipse (Kepler)`

1. Install `GWT` `eclipse` plugin `Help` -> `Eclipse Marketplace`. Search with string `GWT` install `Google Plugin for eclipse 4.3`.
2. Install maven plugin open `Eclipse Marketplace` and search for `m2e-wtp` look for `Maven Integration for Eclipse WTP Juno (1.0.1)` and install it
3. Other maven integration plugins open `Eclipse marketplace` and search for `m2e` look for `APT M2E Connector` and `GWT M2E Connector` install both the plugins.

  
With above plugins installed before importing your maven project. I tend to make sure I use same maven installation and configuration that I use for command line maven build. When you install `m2e` `eclipse` plugin for maven it comes with default maven installation. To change your maven installation to same as that of command line maven. Follow below steps.

1. Open `Window` -> `Preferences` "Preferences" window will be open.
2. Expand `Maven` label on left side panel.
3. Select `Installations` on right hand side panel you will see `embedded` maven installation selected.
4. Click on `Add` button directory window will be prompted. Select home folder of your maven installation and click `Ok`.
5. With addition of your installed maven installation. Make sure check mark is marked on your installed maven installation and then click on `OK`

To import your maven project inside `eclipse` follow below steps.

Note: Before importing your `eclipse` projects make sure you make a complete build from command prompt.

1. Select `File` -> `Import`
2. Expand `Maven` and select `Existing Maven Projects` and click on `Next`.
3. Click on `Browse` button on next screen folder explorer will appear.
4. Select your project's parent folder which contains the `pom.xml`.
5. Next follow next screens as next screens varies based on maven plugins used in your project. Sometimes it may take some time, but be patient and allow `eclipse` to complete it (in some cases where you are using maven plugin in your `pom.xml` `m2e` will try to locate respective `eclipse` plugin to achieve same task from `eclipse`. If it fails to find one it will try to locate in `eclipse` market place and if it is there user will be prompted to install the same).
