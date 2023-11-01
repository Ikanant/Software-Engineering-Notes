Star Match Game

Wednesday, May 01, 2019

2:35 PM

<https://jscomplete.com/playground/rgs3.1>

\^\^\^ Starting point for our code

Note: Using too many components in an application or too few is always a problem. We need to focus carefully into what should be converted. One pointer to make this identification is: Every time in the UI that we have many items that share similar DATA or behavior: that\'s a candidate for an item component.

On our game example we know that the play numbers will have the exact same behavior. Each click on a number will invoke logic to determine if that click is good or bad. Numbers are going to invoke the behavior with different data, but the nature of the behavior will remain constant.

**Note**: (Summary from above) - Every time we are dealing with an item that shares similar **Data** or **Behavior** is a great candidate for isolating into its own component

![const Number = props ( \<button 2 const StarMatch = const \[stars, setStars\] return ( div \<div Pick I or \*\'re numbers that sum to the number of stars e/ div, \<div \<div {uttls. range(l, stars) .map(starld \<div •div {utns.range(l, CNumber e/ divs \<div Remaining: 1 ](003_Star_Match_Game_000.png)

\^\^\^ The image above shows how we have extracted the NUMBER input as its own REACT component... what\'s the problem though? Well, we named the new Component Number... essentially clashing with the native Number class that usually converts strings into numbers... BUT, looking at line 6 above... now that is not going to work anymore. *We should always be aware of the top level JS code and be sure not to override them. Nice rule of thumb is to name our components 2 word names.*

![const PlayNumber = props \<button console. log( \'Num\' , props.number)Y {props. c/button\> 7 • const Starmatch z const \[stars, setStars\] useState(utiIs. random(l, 9)); return ( \<div Pick 1 or more numbers that sum to the number of stars 2 5 8 3 6 9 Group similz Cons o t e cleared 4 7 ediv Pick I or mre numbers ediv •div that sun to the number Of stars Time Remaining: 10 {utus. range(l, stars) -map(starld div Question : handlers (Pause and What JavaScript concept to report their numbers thi nk) enabled 9 di fferent click ](003_Star_Match_Game_001.png)

How come we have essentially created 9 top functions and 9 handler functions in them and they still print out one at a time when a button is clicked?

**Answer:** Closures. Each onClick() function closes over the scope of its owner number and give us access to its props

**View Function State =\> UI**

For every behavior we are trying to implement in any REACT application, there are 2 aspects to it:

1.  App logic to change state

2.  UI logic to describe stae

So in our example, when we click on a number, we are going to have to change its color based on its new state.

So let\'s think about the possible numbers we need to store in the state of our application?

-   candidateNumbers

-   wrongeNumbers

-   usedNumbers

-   availableNumbers

The general advice in REACT stateful components is to minimize the state. Don\'t place on the state ANYTHING that can be computed from the other things we place on the state.

For example: wrongNumbers can be computed from the candidateNumbers (since we have the count of stars and we could just sum the candidateNumbers and know if they are greater than that count). Used numbers and available numbers are just the inverse of each other, so we could use one or the other.

Here we will only end up using

-   candidateNumbers

-   availableNumbers

<https://jscomplete.com/playground/rgs3.4>

\^\^\^ The link above will display the state of the project in which we have only modified and set ready the UI elements and their behavior. NOT done any calculations yet.

[https://jscomplete.com/playground/rgs3.5](https://jscomplete.com/playground/rgs3.4)

\^\^\^ We have now a playable game!

![•div {availableNuns.Iength G ? ( «pIayAgatn eStarsDispIay ](003_Star_Match_Game_002.png)

Now let\'s consider the case in which we want to display a GAME OVER screen or something that will allow our players to restart the game... it would be tempting to do something like the code above... just have a computation before using whatever REACT component we want... BUT we should try to stay away from these type of behaviors.... This is because readability can be a problem if we have logic like that spread around our JSX. Instead we should always try to do these computations before the return statement.

![19• const Starmatch z const \[stars, setStars\] = useState(utiIs. random(l, 9)); Const z const (candidateNums, setCandidateNumsJ z useState(t\]); 9)); 27. ) stars; const ganeIsDone avaLLabIeNums . length Const number Status number If (!avaitabIeNums. includes(nunber)) return •used\'; If (candidateNums. includes(nunber)) return candidatesAreHrong ? •wrong • : \'candidate\'; ](003_Star_Match_Game_003.png)

\^\^\^ These is way more elegant

**Note:** The structure of a REACT component should always be \*similar\*. The first few lines should be any hooks into the state or side effects for this component... THEN after that any computations based on the state... THEN we have the return statement with the description of the UI based on all the states and computations out of that state.

**Side Effect Hooks**

The only react Hook we have used so far is the useState() hook. REACT has a few other hooks at our disposal and one of them is useEffect

This useEffect hook is a tool real offers to introduce some side effects to our component. It takes in a function AND it will run this function EVERY TIME the owner component renders itself.

![25 • const Starhatch C) const \[stars, setstarsl 9)); const \[availableUuns, setAvauabLeNumsJ Const \[candidateUuns, setCandtdateNumsl useState(Cl); const \[secondsLeft, setSecondsLeftJ useState(10); 31 setSecOndsLeft(secondsLeft - I) ](003_Star_Match_Game_004.png)

Now my first thought when looking at the method above I think, oh this is fine, it will run the useEffect function whenever it re-renders the component, which in our case is when the user changes the state of some of the properties after doing some clicking around..... Well, the interesting thing here is that we are in fact changing the state of the properties when we do a setSecondsLeft call.... SO, we will re-render the component every one second. So this, works!

What\'s our problem then? WELL, considering we will have the useEffect trigger every time the user clicks on something on the page, there component is going to end up re-rendering way more times that we expect... AND each time the useEffect runs is essentially creating a timer... so it will just create and create and create those functions unnecessarily.

The useEffect hooks has a mechanism to CLEAN the side effect when is no longer needed. This cleaner option is found in the return value of this callback function within the sideEffect. We can return a function when REACT is about to unmount the component.

[https://jscomplete.com/playground/rgs3.7](https://jscomplete.com/playground/rgs3.4)

**Unmount & Remount Components**

So we know that when dealing with a component we could manually reset the property values of the component in order to make it restart... but there is a better way... we can unmount the component all together and that will essentially clear out any cached data we have had for that component and its children.

Now **how** do we identify what components need to be unmounted? - Easy, we use the key attribute that REACT uses to identify an element.

So if we place a key at the Game parent level and change it when we click to play again REACT will unmount game 1 and mount a new component that\'s game 2.... AND when react unmounts game one...it will reset everything about game 1... including side effects.

<https://jscomplete.com/playground/rgs3.8>,

The Game component is HUGE. It has states, the initial values of the state, it has effects, it has computations, it has functions to transact on the state AND it also has its own render logic... The reason why this is the case is because we have this component be the only state manager in this application. It has the responsibility of managing AND rendering the game tree... while this works... there is a better way to split this responsibilities:

**Custom hooks:**

In order to split out all the logic that we have to prepare the state of our game component, we will build a custom hook... which starts by making our separate special function. We are going to make a stateful function. We are going to extract logic that is basically React hooks: useState && useEffects and we are going to group them.

**Note:** Because these are custom hooks, it is often suggested that we name this functions **use**Something.

***The Rule of Hooks***

You always use the REACT hooks functions in the SAME order. We cannot call hooks inside loop or conditions. (We can inside of the hooks)

Custom hooks can return anything.

![const setGameState = (newCandtdateNums) - if stars) { setCandtdateNums(newCandtdateNums); } else { const newAvatIabIeNums = availableNums \_ filter ( n !newCandtdateNums \_tncludes(n) sets tars(u tus \_ randonSumIn(newAvatIabIeNums , setAvatla bleNums ( newAvatIa bleNums) ; setCandtdateNums(C\]); g)); return { stars, availableNums , candida teNums , secondsLeft, setGameState } ; 62 const Game = const { stars, props = availableNums , candida teNums , secondsLeft, setGameState , } = useGameState(); ](003_Star_Match_Game_005.png)

<https://jscomplete.com/playground/rgs3.9>
