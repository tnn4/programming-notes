
{https://stackoverflow.com/questions/467557/what-is-meant-by-the-term-hook-in-programming

Hooks are a category of function that allows base code to call extension code. This can be useful in situations in which a core developer wants to offer extensibility without exposing their code.

One usage of hooks is in video game mod development. A game may not allow mod developers to extend base functionality, but hooks can be added by core mod library developers. With these hooks, independent developers can have their custom code called upon any desired event, such as game loading, inventory updates, entity interactions, etc.

A common method of implementation is to give a function an empty list of callbacks, then expose the ability to extend the list of callbacks. The base code will always call the function at the same and proper time but, with an empty callback list, the function does nothing. This is by design.

A third party, then, has the opportunity to write additional code and add their new callback to the hook's callback list. With nothing more than a reference of available hooks, they have extended functionality at minimal risk to the base system.

Hooks don't allow developers to do anything that can't be done with other structures and interfaces. They are a choice to be made with consideration to the task and users (third-party developers).

For clarification: a hook allows the extension and may be implemented using callbacks. Callbacks are generally nothing more than a function pointer; the computed address of a function. There appears to be confusion in other answers/comments.

Implementation example:

callbacks are references to functions

list of callbacks
list_of_callbacks = [callback1, callback2, callback3, ..., callbackN]

injected function calls list of callback at injection point

users can add custom functions by adding a new callback to the list

hooks_fn(callback_list) // runs list of new mod functions

original source code <-- not modified




Simple said:

A hook is a means of executing custom code (function) either before, after, or instead of existing code. For example, a function may be written to "hook" into the login process in order to execute a Captcha function before continuing on to the normal login process.


example:
harmony patch

`Harmony uses a variation of hooking and focuces only on runtime changes that ... '


Essentially it's a place in code that allows you to tap in to a module to either provide different behavior 
or to react when something happens.

Card game example:

OnStartTurn : hook at start of turn
OnDrawPhase : hook at draw phase
OnMainPhase : hook at main phase
}

{
https://www.reddit.com/r/gamedev/comments/fjr3n/advice_for_developing_a_card_game_rules_engine/
A finite state machine and event hub (Observer pattern) is probably the way to go. With those and a few other supporting systems such as an event queue, you can model just about anything.

You might also provide a number of appropriate hooks like OnPrePlayed(), OnPlayed(), OnPostPlayed() for your Card objects.
}