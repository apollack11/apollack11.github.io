---
layout: inner
title: 'Localizing a Quadcopter using the HTC Vive'
date: 2017-06-04 16:30:00
categories: python ros
tags: localization
featured_image: '/assets/vive_logo.png'
lead_text: 'Final Project for MSR Program'
---

Currently working on setting up localization using Vive Lighthouses and Vive Tracker

### Summary  
The goal of this project is to implement a relatively cheap localization setup for a quadcopter using the HTC Vive. This project was proposed by Professor Michael Rubenstein and is intended to be an add-on to his course focused on the creation of a quadcopter from start to finish. The initial plan is to attach a Vive Tracker to one of the quadcopters and try and stabilize the vehicle's position in space.

### Background
The HTC Vive system consists of a main headset unit, two lighthouses, and two controllers. The lighthouses are the core element of this system because they track the other three components. Equipped with IR blasters, each lighthouse helps to locate the IR receivers on each of the Vive devices. Using these lighthouses, a system can be created to allow sub-millimeter localization.

### Progress  
Initial progress so far has been slow due to an initial lack of the required components for the system. The MSR program initially purchased an HTC Vive but our attempts to connect it to our existing computers were unsuccessful as they did not have the required graphics card for use with the Vive. Since discovering this problem, we have purchased a computer with a high-end GPU to run the Vive and it is now up and running. We have also purchased a Vive Tracker to attach to the quadcopter. With these components ready, I can now begin to extract the (x,y) location of the Vive Tracker in space.

### Related Work  
Once I have established localization of the quadcopter, I would like to be able to control its position in space and track trajectories based on its position. In preparation for this concept, I focused the efforts of my project in ME454: Optimal Control of Non-Linear Systems on controlling a 2D quadcopter. Below is a brief description and the results of this project.

#### Optimal Control of a 2D Quadcopter  

**Description:**  
This system consists of a rectangular object in two dimensions which has controllable forces at both ends. It can be pictured as a viewing a quadcopter from the side. It is under-actuated (2 controls, 3 degrees of freedom) and therefore I thought it would be a good problem for which to utilize optimal control.  

**Dynamics:**  
ddx = (1 / m) * [(F1 + F2) * Sin(theta[t])]  
ddy = (1 / m) * [(F1 + F2) * Cos(theta[t]) – g]  
ddtheta = (1 / rotInertia) * [F2 * length/2 – F1 * length/2]  

The dynamics of the system were straightforward and were determined by drawing a free body diagram of the quadcopter. The mass, the length, the height, and the rotational inertia of the quadcopter was determined by looking at the specs of a DJI Mavic quadcopter.  

**Results:**  
<div style="text-align: center;">
  <img src="/assets/2d_quadcopter_control.gif" alt="2D Quadcopter Control" style="width: 80%; max-width: 650px; padding: 10px"/>
  <p>2D Quadcopter tracking the following trajectory: Travel to (1,2), draw a circle with a 1m radius, travel back to origin</p>
</div>

The end result of my efforts to create a 2D quadcopter system was a piece of code which takes xcenter and ycenter as inputs, moves to the (x,y) location defined by these points, tracks a circle with a 1m radius at that point, and returns to the origin. This works robustly for any points within the range x = [-1,1] and y = [-2,2]. Outside of this range, there were problems with computation and the result ends up diverging. I believe it may be possible to fix this by varying the amount of time for each movement. I will explore this concept further when applying this to a 3D quadcopter for the localization project.
