---
title: "Firelight"
date: 2019-01-27
last_modified_at: 2023-06-01
categories:
  - Project-Postmortems
tags:
  - Game
  - Game-Jam
  - C#
  - Unity
  - Engine-Learning
header:
  overlay_image: /assets/images/Projects/Firelight/F1-3.jpg
  teaser: /assets/images/Projects/Firelight/FTitle-1.jpg
  og_image: /assets/images/Projects/Firelight/FTitle-1.jpg
  caption: "Firelight from above"
  actions: 
   - label: "Play Firelight"
     url: "https://probablyjay.itch.io/firelight"
excerpt: "Learning Unity: Making a game about staying warm and finding friends."
tagline: "Learning Unity: Making a game about staying warm and finding friends."
photo1:
  - url: "/assets/images/Projects/Firelight/F2.png"
    image_path: "/assets/images/Projects/Firelight/F2.png"
    alt: "Firelight Screenshot"
    title: "Firelight Gameplay"
---
# Firelight
> *The world is a dark and cold place. While a few fires light up the jagged rocks, 
they are few and far between. You, and the people you meet, won't survive out in the dark. 
The fires are going out, it won't be long before there is no light left at all. 
Unless you find some other source of warmth in this unforgiving world, 
your death is almost certain.*

Firelight was our submission for Global Game Jam 2019. Made alongside my good friend *Matt Stark*, this was my first global game 
jam and only my second foray into Unity's game engine.

You play as a lost soul wandering between campfires, 
trying to weather a freezing cold storm. The people you meet are all similarly lost and alone, 
but if you manage to convince them to come along with you then you all might just survive.  

{% include gallery id="photo1" caption="Firelight Gameplay" %}

Taking place on Abertay’s campus, this was a really nice chance to get to grips developing something from scratch 
in only a couple of days. I had only written in C# a handful of times since first learning the language 
during my NC with with [*XNA MonoGame*](https://www.monogame.net). 

My role in this project was mostly gameplay programming, writing the logic for the main *warmth* mechanic in the game, 
player movement, as well as designing the layout of the level. I also took the chance to dip my toe in other disciplines, 
writing the story and dialogue, and recording the sound effects used thought the game. This turned out to be great practice 
in using teammate’s modules, implementing dialogue in the module written by my partner.

````csharp
protected override IEnumerator ChatCoroutine()
{
    Cutscene.Instance.StartCutscene();
 
    // move camera to cutscene view 
    Cutscene.Instance.Transition(GameController.Instance.Player.transform.position);
    while (Cutscene.Instance.IsTransitionInProgress()) { yield return null; }
    
    ...
    
    // dialogue choice
    Cutscene.Instance.DialogueDecision("Who are you?", "I’m a friend.", "I can’t remember.", true);
    while (Cutscene.Instance.IsDialogueInProgress()) { yield return null; }

    Cutscene.Instance.Transition(GameController.Instance.Player.transform.position);
    while (Cutscene.Instance.IsTransitionInProgress()) { yield return null; }

    // choice A
    if (Cutscene.Instance.GetDecisionOutcome())
    {
        Cutscene.Instance.Dialogue("I’m a friend.", true);
        while (Cutscene.Instance.IsDialogueInProgress()) { yield return null; }
    }
    else // choice B
    {
        Cutscene.Instance.Dialogue("I can’t remember.", true);
        while (Cutscene.Instance.IsDialogueInProgress()) { yield return null; }
    }
    ...
}

````
<figcaption>Snippet from a dialogue file</figcaption>

Despite the tight deadline, we finished the game with plenty of time to show it off. 
It was popular at the Jam, earning us both a Unity t-shirt from our Uni's rep, which he insisted were 
*“not prizes, as the Jam wasn't a competition”*. 

Overall, I really like this game and I’m glad we had the chance to make it.

### Watch a full play-through here:

{% include video id="LCdt8rgqWDE" provider="youtube" %}
