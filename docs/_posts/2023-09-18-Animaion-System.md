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
  caption: "A character animated by the system."
#   actions:
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

{% include gallery id="photo1" caption="Animation system demonstrated with a walk/run cycle and movement-speed combined blend. Also shown with Inverse Kinematics on the hand." %}

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