beanstalk-play
==============

Install [Play! Framework](http://www.playframework.org/)
via homebrew or other means, per your platform.

    $ brew install play

Check your play version...

    $ play
           _            _ 
     _ __ | | __ _ _  _| |
    | '_ \| |/ _' | || |_|
    |  __/|_|\____|\__ (_)
    |_|            |__/ 
             
    play! 2.0.2, http://www.playframework.org
    
    This is not a play application!
    
    Use `play new` to create a new Play application in the current directory, 
    or go to an existing application and launch the development console using `play`.
    
    You can also browse the complete documentation at http://www.playframework.org.

Create a new Play! app...


Then make a new directory for a new app, then initialize a new play app

    $ play new new-play
           _            _ 
     _ __ | | __ _ _  _| |
    | '_ \| |/ _' | || |_|
    |  __/|_|\____|\__ (_)
    |_|            |__/ 
             
    play! 2.0.2, http://www.playframework.org
    
    The new application will be created in /Users/travis/src/new-play
    
    What is the application name? 
    > new-play
    
    Which template do you want to use for this new application? 
    
      1 - Create a simple Scala application
      2 - Create a simple Java application
      3 - Create an empty project
    
    > 2
    
    OK, application new-play is created.

    Have fun!

    $ 

Modify `project/plugins.sbt` to include the `war` generating plugin...

    // Comment to get more information during initialization
    logLevel := Level.Warn

    // The Typesafe repository
    resolvers ++= Seq(
      "Typesafe repository" at "http://repo.typesafe.com/typesafe/releases/",
      "Play2war plugins release" at "http://repository-play-war.forge.cloudbees.com/release/"
    )

    // Use the Play sbt plugin for Play projects
    addSbtPlugin("play" % "sbt-plugin" % "2.0.2")

    addSbtPlugin("com.github.play2war" % "play2-war-plugin" % "0.6")

And the `project/Build.scala` file as well...

    import sbt._
    import Keys._
    import PlayProject._

    object ApplicationBuild extends Build {
    
        val appName         = "new-play"
        val appVersion      = "1.0-SNAPSHOT"

        val appDependencies = Seq(
          // Add your project dependencies here,
          "com.github.play2war" %% "play2-war-core" % "0.6"
        )

        val main = PlayProject(appName, appVersion, appDependencies, mainLang = JAVA).settings(
          // Add your own project settings here
          resolvers += "Play2war plugins release" at "http://repository-play-war.forge.cloudbees.com/release/"
        )

    }

Then executing `play war` will create a new war file in `target/`.
