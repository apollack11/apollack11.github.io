---
layout: inner
title: 'Shape Stream'
date: 2016-10-13 12:07:00
categories: java git
tags: software shape stream
featured_image: '/assets/feature_screen.png'
lead_text: 'iOS: <a href="https://itunes.apple.com/td/app/shape-stream/id1095099500?mt=8">App Store</a> -- Android: <a href="https://play.google.com/store/apps/details?id=com.tea.game&hl=en">Google Play Store</a>'
---

Shape Stream is a cross-platform mobile game for Android and iOS created in Java. The game was released in April 2016 and has over 400 total downloads.

I began working on Shape Stream in January 2016 with Tyler Carrara and Eric Robinson, two friends from high school. We wanted to learn how to bring an application from idea to completion and thought that creating a mobile game would be an effective way to do so. None of us majored in Computer Science, but we were all familiar with programming and willing to learn the object-oriented programming necessary to produce the game. The project began with an idea of having the user interact with shapes falling from the top of the screen. Building on this idea, we brainstormed exactly what we wanted to include in the game. We determined how the user would score points, how they would lose lives, when the game would end, what power-ups we should include, and more.

<div style="text-align: center;">
  <p style="font-weight: bold">Shape Stream Initial Concept Images</p>
</div>
<div style="text-align: center;">
  <img src="/assets/concept-image1.png" alt="Shape Stream Concept 1" style="width: 300px; padding: 10px"/>
  <img src="/assets/concept-image2.png" alt="Shape Stream Concept 2" style="width: 300px; padding: 10px"/>
  <img src="/assets/concept-image3.png" alt="Shape Stream Concept 3" style="width: 300px; padding: 10px"/>
</div>
<br/>

After sketching out a broad concept and listing features, we began laying out a plan for programming the application. We conducted research to figure out what resources we wanted to use to create the game. Because I already had an intermediate knowledge of Java, we chose to use LibGDX as our game engine and RoboVM to port the game from Android to iOS. These technologies allowed us to focus development all in Java and still create a product which could be released in both app marketplaces. Tyler and I were the ones focused on programming, with Tyler learning Java from scratch and me taking my intermediate knowledge of Java and learning how to apply it to the LibGDX game engine and RoboVM.

Once we had a basic idea of how the programming was going to work, we created a project and a git repository to store our code and collaborate. Using GitHub, we were able to simultaneously make changes to the project and then merge them together. The basic structure of our project consists of a core directory which contains all code related directly to the game. The core directory includes all menus, text overlays, settings, and the game itself. The project also has desktop, android, and ios directories which allow the game to be instantiated on different devices. The desktop version was used for testing new features related directly to the game, and we used Android and iOS devices to test ads, in-app purchases, and the functionality of the game on touch platforms.

After three months of work including working through spring break, we launched Shape Stream for Android and iOS on April 16th, 2016. On April 15th, 2016, we participated in the MobiLEHIGH game creation competition at Lehigh University and won first prize by choice of the judges.

Shape Stream involved combining a wide set of skills in order to move from concept to product. In addition to the code, we also created every asset from scratch including music, sound effects, logos, and sprites. I learned an immense amount about game design, project planning, Java programming, bug fixing, and testing while working on this project.

We received great feedback from a number of friends and are currently working on a new version to improve upon the original concept. If you want to checkout Shape Stream, links to both app stores are at the top of the post.

<div style="text-align: center;">
  <p style="font-weight: bold">Shape Stream Final Images</p>
</div>
<div style="text-align: center;">
  <img src="/assets/ShapeStreamScreenshot1.png" alt="Shape Stream Screenshot 1" style="width: 300px; padding: 10px"/>
  <img src="/assets/ShapeStreamScreenshot3.png" alt="Shape Stream Screenshot 2" style="width: 300px; padding: 10px"/>
  <img src="/assets/ShapeStreamScreenshot4.png" alt="Shape Stream Screenshot 3" style="width: 300px; padding: 10px"/>
  <img src="/assets/ShapeStreamScreenshot5.png" alt="Shape Stream Screenshot 4" style="width: 300px; padding: 10px"/>
</div>
<br/>

iOS: [App Store](https://itunes.apple.com/td/app/shape-stream/id1095099500?mt=8) <br/>
Android: [Google Play Store](https://play.google.com/store/apps/details?id=com.tea.game&hl=en)
