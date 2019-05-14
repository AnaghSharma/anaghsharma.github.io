---
layout: post
title: The State of Stateful UI
description: Adding error and empty views to an existing app can become complex. Considering UI as a set of states and state machines can easily help in having different views. How can you use State Machine to handle different UI states? Find out more in the article.
imageurl: assets/images/sm-previews/pre-home.jpg
keywords: design, side projects, macos, cocoa, xamarin, state design pattern, state machine, user interface
author: Anagh Sharma
read-time: 6m 45s
permalink: '/blog/the-state-of-stateful-ui/'
comments: true
published: false
---

###### **OVERVIEW**
You must be wondering why the title of this post is like this. A couple of months ago I started working on [this macOS app](https://github.com/AnaghSharma/Carol){:target="_blank"}{:.active}. Everything was going fine initially as I had only one UI state which was the one showing content to the user. As I had no prior experience designing and building apps for macOS, I was unaware of any architecture that could ease up the process of showing different UI states. When the time came to incorporate the other UI states namely empty and the error state, I could not do so as I had only one View and an associated ViewController. I did not want to add a separate ViewController for every UI state. What I wanted was a way to load a View into existing ViewController depending on the current UI state.

<br>
It could have been done with the help of dreary if/else conditional statements ladder and a couple of boolean variables. So if the song does not have any lyrics (i.e. it is instrumental), the code must hide everything else (the UI elements for content view and error view) and show only the empty state UI elements.

<br>
To handle this with one View and its associated ViewController, the scenario could have been like this - 
1. Initially Content container is visible. Error and Empty containers are hidden. All of these containers overlap each other but only one is visible at a time. These are loaded at the same time in memory. The only difference is the visibility of each.
<strong>Note</strong> - a container here is a virtual entity which comprises UI elements.
2. Hit API
3. If the song is instrumental, hide Content container and show Empty container.
4. If an error occurred, hide Content Container and show Error container.

Now you can imagine how many if-else conditional statements will be used in this case. The problem with this approach is -
* Not scalable - If you have to add a couple of extra UI states, then you will get bewildered in the nested if-else statements.
* Only one View encompasses all these containers. More the containers, more time will be taken to load the view as this task becomes resource intensive.

<br>
###### **THE NEED FOR A STATE MACHINE**
At this stage, I started looking for all the possible solutions and checked how other devs handle various UI states. A simple (not really 😉) google search suggested that state machines can be used for handling UI states. I found out [this repo](https://github.com/aschuch/StatefulViewController){:target="_blank"}{:.active} which utilises a State Machine to handle the UI states. This library helps you to load the view corresponding to the state e.g. loading, content, etc. It is written in Swift for iOS so I could not use it.

<br>
I had studied about State Machines and Finite State Automata in college but never thought of implementing them. So went through the theory again and looked out for a few examples in C#. There are a lot of good libraries out there but I could not figure out how to use them in association with views of Apple dev environment. After going through a lot of articles I outlined a state machine which could work for my case.

<br>
![a simple state machine]({{ site.url }}/assets/images/posts/sosui-1.jpg){: .slb }

<br>
[The app](https://github.com/AnaghSharma/Carol){:target="_blank"}{:.active} for which I was trying to implement all this is a menu bar app for macOS which identifies the song currently playing and fetches its lyrics. The moment you click on the menu bar icon, a popover opens and the first state is the idle state which swiftly transitions to loading state. Depending on the current player (iTunes & Spotify) state, app hits the lyrics API if a song is playing. If nothing is playing, the empty state is loaded. If the API returns success, the content state is loaded else the error state is loaded.

<br>
###### **IMPLEMENTING THE STATE MACHINE**
Basic steps to implement a state machine are - 
1. Define an abstract base class for the State. 
2. Define different classes for different states inheriting from the abstract base class.
3. Define a state machine class to present a single interface to the outside world and have a pointer to the current state object.
4. To transition to a state, change the pointer to next state object.

To start with I wrote an abstract class `StatefulViewController` which would act as the base class for different states of the state machine. This class has two abstract methods viz. Enter and Exit which as the names suggest provide a way for a subclass (which is a state) to define what should happen when that state is entered/exited. This class also contains `ContainerView` of type `NSView` in which the corresponding view is loaded from a .xib file. The `CurrentDelegate` object helps in getting the ViewController in which the views are to be loaded.

```C#
public abstract class StatefulViewController
    {
        public NSView ContainerView;
        public AppDelegate CurrentDelegate = NSApplication.SharedApplication.Delegate as AppDelegate;
        public abstract void Enter();
        public abstract void Exit();
    }
```

<br>
For every state, I have a class inheriting from `StatefulViewController` e.g. for Loading State
```C#
public class LoadingState : StatefulViewController
    {
        public override void Enter()
        {
            ContainerView = LoadNib.LoadViewFromNib<LoadingView>("LoadingView", CurrentDelegate.controller.View);
            ContainerView.Frame = CurrentDelegate.controller.View.Bounds;
            CurrentDelegate.controller.View.AddSubview(ContainerView, NSWindowOrderingMode.Above, CurrentDelegate.controller.View);
        }

        public override void Exit()
        {
            ContainerView.RemoveFromSuperview();
        }
    }
```

<br>
On entering this state, a view is loaded from the file <strong>LoadingView.xib</strong> and then it is added to the superview associated with the only ViewController that we have in the app. I have added separate .xib files for each state to keep them organised. Having multiple views in a single .xib file might have made the task of getting a particular view complicated.

<br>
![a way to add views]({{ site.url }}/assets/images/posts/sosui-2.jpg){: .slb }

<br>
For point <strong>3</strong>, I wrote another class - `ViewStateMachine`. This is the actual state machine implementation. It has methods which can be called from outside to load the required view. Outside world does not know anything about the states or the transitions apart from these methods.

```C#
public enum States
    {
        Idle,
        Loading,
        Content,
        Empty,
        Error
    }

    public enum Triggers
    {
        Load,
        ShowContent,
        ShowEmpty,
        ThrowError
    }

    public class ViewStateMachine
    {
        private StatefulViewController currentState;
        
        public ViewStateMachine(States initialState)
        {
            if (initialState == States.Idle)
                currentState = new IdleState();
        }

        public void SetupInitialView() => currentState.Enter();

        void TransitionToState(States _currentState, Triggers _trigger)
        {
            currentState.Exit();
            switch(_currentState)
            {
                case States.Idle:
                    if (_trigger == Triggers.Load)
                        currentState = new LoadingState();
                    break;
                case States.Loading:
                    if (_trigger == Triggers.ShowContent)
                        currentState = new ContentState();
                    else if (_trigger == Triggers.ShowEmpty)
                        currentState = new EmptyState();
                    else if (_trigger == Triggers.ThrowError)
                        currentState = new ErrorState();
                    break;
            }
        }
 
        //Loading method which can be called whenever a Loading View is required
        public void StartLoading()
        {
            TransitionToState(States.Idle, Triggers.Load);
            currentState.Enter();
        }

        //Method to load a view when there is content
        public void ShowContent()
        {
            TransitionToState(States.Loading, Triggers.ShowContent);
            currentState.Enter();
        }

        //Method to load a view when there is no content
        public void ShowEmpty()
        {
            TransitionToState(States.Loading, Triggers.ShowEmpty);
            currentState.Enter();
        }

        //Method to load a view whenever there is an error
        public void ShowError()
        {
            TransitionToState(States.Loading, Triggers.ThrowError);
            currentState.Enter();
        }
    }
```
<br>
It has two enums <strong>States</strong> and <strong>Triggers</strong> which helps in transitioning in the function `TransitionToState`.

This state machine appears complex but using it is easy and you can immediately identify its need. In the ViewController - 
```
ViewStateMachine stateMachine = new ViewStateMachine(States.Idle);
stateMachine.SetupInitialView();
```
<br>
Transitioning to any state is as easy as it gets - 
```
stateMachine.StartLoading();
.
.
//Do some work like an API call
.
//If response is a success
stateMachine.ShowContent();
//else
stateMachine.ShowError();
```

<br>
###### **RESULTS**
Since I had a hard time implementing all this, I was sceptical about its scalability. I also thought if I was doing something of an overkill here. But it all turned out to be fine. I was able to add another state - **Empty** and load a corresponding UI view whenever that state is entered.

<br>
![different views added]({{ site.url }}/assets/images/posts/sosui-3.jpg){: .slb }

<br>
The way I approached UI design for this app was not entirely mistaken. Initially, I had only thought of an additional error state which could have been handled by a couple of if-else conditional statements. What I learned from this project is a way to think of UI design as various states of a state machine. From now on, I instinctively consider a UI content screen as having a minimum of 4 states - Empty, Loading, Content and Error.

<br>
All in all, it was a challenging task to implement something that you read as a theory subject in college. State Machines in UI interaction is surely a compelling topic.

<br>
<strong>// KEEP MAKING.<strong>