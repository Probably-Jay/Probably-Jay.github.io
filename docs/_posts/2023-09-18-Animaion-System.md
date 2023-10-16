---
title: "Animation System"
date: 2023-01-05
last_modified_at: 2023-09-18
categories:
  - Project-Postmortems
tags:
  - Coursework
  - C&#8203++
  - Animation
header:
  overlay_image: /assets/images/Projects/Animation-System/Picture3.png
  overlay_filter: rgba(0, 0, 0, 0.5)
  teaser: /assets/images/Projects/Animation-System/Squareish-transformed.png
  og_image: /assets/images/Projects/Animation-System/Squareish-transformed.png
  # caption: "A character animated by the system."
  actions:
  - label: "Source"
    url: "https://github.com/Probably-Jay/AnimationSystem/tree/master"
  - label: "Documentation"
    url: "https://jaybretherton.xyz/AnimationSystemDocumentation/annotated.html"
#    - label: "Download exe"
#      url: "/download/Animation-System.zip"
# excerpt: "Procedurally generating a game's soundtrack. Markov Chains meet Functional harmony."
# tagline: "Procedurally generating a game's soundtrack. Markov Chains meet Functional harmony."
photo1:
  - url: "/assets/images/Projects/Animation-System/Animation.gif"
    image_path: "/assets/images/Projects/Animation-System/Animation.gif"
    alt: "An animated character smoothly transitioning from walking to running while her hand points at the cursor."
    title: "Animated character controlled by the animation blending and IK systems." 

---
# Anmation System 

A part of a university module on game engine animaiton systems. My goal with this software was to create a system with the best possible API and with minimum depencance on platform being used, so that the module could be easily inserted into any project.

What was created was a pretty powerful 2D sprite & skeletal, and 3D blend-node based skeletal animation system, with suport for IK as well as a methods for loading in the animation data. 

The system was created to be used with a propriety C++ engine, which is what is running the demonstration gifs, but care was taken to minimise dependancy on this framework.


{% include gallery id="photo1" caption="Animation system demonstrated with a walk/run cycle and movement-speed combined blend. Also shown with Inverse Kinematics on the hand." %}


There were two areas of intrest for me in this project. The first being 


````cpp
AnimationSystem::PureResult AnimatedMeshApp::LoadMeshAndAnimation()
{
   // create an animated object, returns Value/Error discriminated union
   auto createPlayerResult = animation_system_->CreateAnimatedObject("Player", 
                                                                     "xbot/xbot.scn") ;

   // early return the error if there is one 
   if(createPlayerResult.IsError())
      return createPlayerResult.ToPureResult();


   // move player from result to member variable
   player_ = createPlayerResult.Take();


   // load the animations, configure with delegates, return early in the case of error
   if(auto animationResult =
      animation_system_->CreateAnimationFor(*player_,
                                          "Walk","xbot/xbot@walking_inplace.scn","",
                                          [](IAnimatorConfig& animPlayer)
                                          {
                                             animPlayer.SetAnimationTime(0);
                                             animPlayer.SetLooping(true);
                                          });
      animationResult.IsError())
   {
      return animationResult;
   }

   if(auto animationResult =
      animation_system_->CreateAnimationFor(*player_,
                                             "Run","xbot/xbot@running_inplace.scn","",
                                             [](IAnimatorConfig& animPlayer)
                                             {
                                                animPlayer.SetAnimationTime(0);
                                                animPlayer.SetLooping(true);
                                             });
      animationResult.IsError())
   {
      return animationResult;
   }


   // set the player's animation state
   if(auto result = player_->Animator().SetAnimation("Walk"); result.IsError())
      return result;


   // return OK
   return AnimationSystem::PureResult::OK();
}
````
<figcaption>Snippet showing the API for creating animation objects.</figcaption>