Download Link: https://assignmentchef.com/product/solved-ai-project2-multi-agent-pacman
<br>
In this project, you will design agents for the classic version of Pacman, including ghosts. Along the way, you will implement both minimax and expectimax search and try your hand at evaluation function design.

<strong>The code base has not changed much from the previous project, but please start with a fresh installation, rather than intermingling files from project 1.</strong>

As in project 1, this project includes an autograder for you to grade your answers on your machine. This can be run on all questions with the command: python autograder.py

It can be run for one particular question, such as q2, by:

python autograder.py -q q2

It can be run for one particular test by commands of the form: python autograder.py -t test_cases/q2/0-small-tree

By default, the autograder displays graphics with the -t option, but doesn’t with the -q option. You can force graphics by using the –graphics flag, or force no graphics by using the –no-graphics flag.

<strong>Evaluation:</strong> Your code will be autograded for technical correctness. Please <em>do not</em> change the names of any provided functions or classes within the code, or you will wreak havoc on the autograder. However, the correctness of your implementation — not the autograder’s judgements — will be the final judge of your score. If necessary, we will review and grade assignments individually to ensure that you receive due credit for your work.

<strong>Academic Dishonesty:</strong> We will be checking your code against other submissions in the class for logical redundancy. If you copy someone else’s code and submit it with minor changes, we will know. These cheat detectors are quite hard to fool, so please don’t try. We trust you all to submit your own work only; <em>please</em> don’t let us down. If you do, we will pursue the strongest consequences available to us.

<strong>Getting Help:</strong> You are not alone! If you find yourself stuck on something, contact the course staff for help. Office hours, classes, and the discussion forum are there for your support; please use them.  We want these projects to be rewarding and instructional, not frustrating and demoralizing. But, we don’t know when or how to help unless you ask.

<strong>Discussion:</strong> Please be careful not to post spoilers.

<strong>Questions: </strong>We will post for each project a document like this containing all questions you have to work on. Although our course is based upon the CS188 AI class at Berkeley, <strong>we might change, add or remove tasks</strong>! Thus, make always sure to read this document.

<strong>Files to Edit and Submit:</strong> You will fill in portions of  multiagents.py during the assignment. You should submit this file with your code and comments. Please <em>do not</em> change the other files in this distribution or submit any of our original files other than this file. Submit the file via Blackboard.

<strong>Files you’ll edit:</strong>

<table width="635">

 <tbody>

  <tr>

   <td colspan="2" width="635"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/multiAgents.html">multiAgents.py</a><u>            </u>Where all of your multi-agent search agents will reside.<strong>Files you should read but NOT edit:</strong></td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/pacman.html">pacman.py</a></td>

   <td width="380">The main file that runs Pacman games. This file also describes a Pacman GameState type, which you will use extensively in this project</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/game.html">game.py</a></td>

   <td width="380">The logic behind how the Pacman world works. This file describes several supporting types like AgentState, Agent, Direction, and Grid.</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/util.html">util.py</a><strong>Files you can ignore:</strong></td>

   <td width="380">Useful data structures for implementing search algorithms.</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/graphicsDisplay.html">graphicsDisplay.py</a></td>

   <td width="380">Graphics for Pacman</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/graphicsUtils.html">graphicsUtils.py</a></td>

   <td width="380">Support for Pacman graphics</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/textDisplay.html">textDisplay.py</a></td>

   <td width="380">ASCII graphics for Pacman</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/ghostAgents.html">ghostAgents.py</a></td>

   <td width="380">Agents to control ghosts</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/keyboardAgents.html">keyboardAgents.py</a></td>

   <td width="380">Keyboard interfaces to control Pacman</td>

  </tr>

  <tr>

   <td width="254"><a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/layout.html">layout.py</a></td>

   <td width="380">Code for reading layout files and storing their contents</td>

  </tr>

 </tbody>

</table>

<a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/autograder.html">autograder.py</a><u>              </u>Project autograder

<a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/testParser.html">testParser.py</a> Parses autograder test and solution files <a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/testClasses.html">testClasses.py</a><u>   </u>General autograding test classes test_cases/ Directory containing the test cases for each question <a href="https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/docs/multiagentTestClasses.html">multiagentTestClasses.py</a> Project 2 specific autograding test classes

<h1>Multi-Agent Pacman</h1>

First, play a game of classic Pacman: python pacman.py

Now, run the provided ReflexAgent in multiAgents.py: python pacman.py -p ReflexAgent

Note that it plays quite poorly even on simple layouts:

python pacman.py -p ReflexAgent -l testClassic

Inspect its code (in multiAgents.py) and make sure you understand what it’s doing.

<h1>1.   Question (4 points): Reflex Agent</h1>

Improve the ReflexAgent in multiAgents.py to play respectably. The provided reflex agent code provides some helpful examples of methods that query the GameState for information. A capable reflex agent will have to consider both food locations and ghost locations to perform well. Your agent should easily and reliably clear the testClassic layout: python pacman.py -p ReflexAgent -l testClassic

Try out your reflex agent on the default mediumClassic layout with one ghost or two (and animation off to speed up the display):

python pacman.py –frameTime 0 -p ReflexAgent -k 1 python pacman.py –frameTime 0 -p ReflexAgent -k 2

How does your agent fare? It will likely often die with 2 ghosts on the default board, unless your evaluation function is quite good.

<em>Note:</em> As features, try the reciprocal of important values (such as distance to food) rather than just the values themselves.

<em>Note:</em> The evaluation function you’re writing is evaluating state-action pairs; in later parts of the project, you’ll be evaluating states.

<em>Options:</em> Default ghosts are random; you can also play for fun with slightly smarter directional ghosts using -g DirectionalGhost. If the randomness is preventing you from telling whether your agent is improving, you can use -f to run with a fixed random seed (same random choices every game). You can also play multiple games in a row with -n. Turn off graphics with -q to run lots of games quickly.

<em>Grading:</em> we will run your agent on the openClassic layout 10 times. You will receive 0 points if your agent times out, or never wins. You will receive 1 point if your agent wins at least 5 times, or 2 points if your agent wins all 10 games. You will receive an addition 1 point if your agent’s average score is greater than 500, or 2 points if it is greater than 1000. You can try your agent out under these conditions with python autograder.py -q q1

To run it without graphics, use:

python autograder.py -q q1 –no-graphics

Don’t spend too much time on this question, though, as the meat of the project lies ahead.

<h1>2.   Question (5 points): Minimax</h1>

Now you will write an adversarial search agent in the provided MinimaxAgent class stub in multiAgents.py. Your minimax agent should work with any number of ghosts, so you’ll have to write an algorithm that is slightly more general than what you’ve previously seen in lecture. In particular, your minimax tree will have multiple min layers (one for each ghost) for every max layer.

Your code should also expand the game tree to an arbitrary depth. Score the leaves of your minimax tree with the supplied self.evaluationFunction, which defaults to

scoreEvaluationFunction. MinimaxAgent extends MultiAgentSearchAgent, which

gives access to self.depth and self.evaluationFunction. Make sure your minimax code makes reference to these two variables where appropriate as these variables are populated in response to command line options.

<em>Important:</em> A single search ply is considered to be one Pacman move and all the ghosts’ responses, so depth 2 search will involve Pacman and each ghost moving two times.

<em>Grading</em>: We will be checking your code to determine whether it explores the correct number of game states. This is the only way reliable way to detect some very subtle bugs in implementations of minimax. As a result, the autograder will be <em>very</em> picky about how many times you call

GameState.generateSuccessor. If you call it any more or less than necessary, the autograder will complain. To test and debug your code, run python autograder.py -q q2

This will show what your algorithm does on a number of small trees, as well as a pacman game. To run it without graphics, use:

python autograder.py -q q2 –no-graphics

<h2>Hints and Observations</h2>

<ul>

 <li>The correct implementation of minimax will lead to Pacman losing the game in some tests. This is not a problem: as it is correct behaviour, it will pass the tests.</li>

 <li>The evaluation function for the pacman test in this part is already written</li>

</ul>

(self.evaluationFunction). You shouldn’t change this function, but recognize that now we’re evaluating *states* rather than actions, as we were for the reflex agent. Look-ahead agents evaluate future states whereas reflex agents evaluate actions from the current state.

<ul>

 <li>The minimax values of the initial state in the minimaxClassic layout are 9, 8, 7, -492 for depths 1, 2, 3 and 4 respectively. Note that your minimax agent will often win (665/1000 games for us) despite the dire prediction of depth 4 minimax.</li>

</ul>

python pacman.py -p MinimaxAgent -l minimaxClassic -a depth=4

<ul>

 <li>Pacman is always agent 0, and the agents move in order of increasing agent index.</li>

 <li>All states in minimax should be GameStates, either passed in to getAction or generated via generateSuccessor. In this project, you will not be abstracting to simplified states.</li>

 <li>On larger boards such as openClassic and mediumClassic (the default), you’ll find Pacman to be good at not dying, but quite bad at winning. He’ll often thrash around without making progress. He might even thrash around right next to a dot without eating it because he doesn’t know where he’d go after eating that dot. Don’t worry if you see this behavior, question 5 will clean up all of these issues.</li>

 <li>When Pacman believes that his death is unavoidable, he will try to end the game as soon as possible because of the constant penalty for living. Sometimes, this is the wrong thing to do with random ghosts, but minimax agents always assume the worst: python pacman.py -p MinimaxAgent -l trappedClassic -a depth=3</li>

</ul>

Make sure you understand why Pacman rushes the closest ghost in this case.

<h1>3.   Question (5 points): Alpha-Beta Pruning</h1>

Make a new agent that uses alpha-beta pruning to more efficiently explore the minimax tree, in

AlphaBetaAgent. Again, your algorithm will be slightly more general than the pseudocode from lecture, so part of the challenge is to extend the alpha-beta pruning logic appropriately to multiple minimizer agents.

You should see a speed-up (perhaps depth 3 alpha-beta will run as fast as depth 2 minimax). Ideally, depth 3 on smallClassic should run in just a few seconds per move or faster. python pacman.py -p AlphaBetaAgent -a depth=3 -l smallClassic

The AlphaBetaAgent minimax values should be identical to the MinimaxAgent minimax values, although the actions it selects can vary because of different tie-breaking behavior. Again, the minimax values of the initial state in the minimaxClassic layout are 9, 8, 7 and -492 for depths 1, 2, 3 and 4 respectively.

<em>Grading</em>: Because we check your code to determine whether it explores the correct number of states, it is important that you perform alpha-beta pruning without reordering children. In other words, successor states should always be processed in the order returned by GameState.getLegalActions. Again, do not call GameState.generateSuccessor more than necessary.

<strong>You must <em>not</em> prune on equality in order to match the set of states explored by our autograder.</strong> (Indeed, alternatively, but incompatible with our autograder, would be to also allow for pruning on equality and invoke alpha-beta once on each child of the root node, but this will <em>not</em> match the autograder.)

The pseudo-code below represents the algorithm you should implement for this question.

To test and debug your code, run python autograder.py -q q3

This will show what your algorithm does on a number of small trees, as well as a pacman game. To run it without graphics, use:

python autograder.py -q q3 –no-graphics

The correct implementation of alpha-beta pruning will lead to Pacman losing some of the tests. This is not a problem: as it is correct behaviour, it will pass the tests.

<h1>4.   Question (5 points): Expectimax</h1>

Minimax and alpha-beta are great, but they both assume that you are playing against an adversary who makes optimal decisions. As anyone who has ever won tic-tac-toe can tell you, this is not always the case. In this question you will implement the ExpectimaxAgent, which is useful for modeling probabilistic behavior of agents who may make suboptimal choices.

As with the search and constraint satisfaction problems covered so far in this class, the beauty of these algorithms is their general applicability. To expedite your own development, we’ve supplied some test cases based on generic trees. You can debug your implementation on small the game trees using the command: python autograder.py -q q4

Debugging on these small and manageable test cases is recommended and will help you to find bugs quickly. <strong>Make sure when you compute your averages that you use floats.</strong> Integer division in Python truncates, so that 1/2 = 0, unlike the case with floats where 1.0/2.0 = 0.5.

Once your algorithm is working on small trees, you can observe its success in Pacman. Random ghosts are of course not optimal minimax agents, and so modeling them with minimax search may not be appropriate. ExpectimaxAgent, will no longer take the min over all ghost actions, but the expectation according to your agent’s model of how the ghosts act. To simplify your code, assume you will only be running against an adversary which chooses amongst their getLegalActions uniformly at random.

To see how the ExpectimaxAgent behaves in Pacman, run: python pacman.py -p ExpectimaxAgent -l minimaxClassic -a depth=3

You should now observe a more cavalier approach in close quarters with ghosts. In particular, if Pacman perceives that he could be trapped but might escape to grab a few more pieces of food, he’ll at least try. Investigate the results of these two scenarios:

python pacman.py -p AlphaBetaAgent -l trappedClassic -a depth=3 -q -n 10

python pacman.py -p ExpectimaxAgent -l trappedClassic -a depth=3 -q -n 10

You should find that your ExpectimaxAgent wins about half the time, while your

AlphaBetaAgent always loses. Make sure you understand why the behavior here differs from the minimax case.

The correct implementation of expectimax will lead to Pacman losing some of the tests. This is not a problem: as it is correct behaviour, it will pass the tests.

<h1>5.   Question (6 points): Evaluation Function</h1>

Write a better evaluation function for pacman in the provided function

betterEvaluationFunction. The evaluation function should evaluate states, rather than actions like your reflex agent evaluation function did. You may use any tools at your disposal for evaluation, including your search code from the last project. With depth 2 search, your evaluation function should clear the smallClassic layout with one random ghost more than half the time and still run at a reasonable rate (to get full credit, Pacman should be averaging around 1000 points when he’s winning). python autograder.py -q q5

Grading: the autograder will run your agent on the smallClassic layout 10 times. We will assign points to your evaluation function in the following way:

<ul>

 <li>If you win at least once without timing out the autograder, you receive 1 points. Any agent not satisfying these criteria will receive 0 points.</li>

 <li>+1 for winning at least 5 times, +2 for winning all 10 times</li>

 <li>+1 for an average score of at least 500, +2 for an average score of at least 1000 (including scores on lost games)</li>

 <li>+1 if your games take on average less than 30 seconds on the autograder machine. The autograder is run on EC2, so this machine will have a fair amount of resources, but your personal computer could be far less performant (netbooks) or far more performant (gaming rigs).</li>

 <li>The additional points for average score and computation time will only be awarded if you win at least 5 times.</li>

</ul>

<strong>Hints and Observations</strong>

<ul>

 <li>As for your reflex agent evaluation function, you may want to use the reciprocal of important values (such as distance to food) rather than the values themselves.</li>

 <li>One way you might want to write your evaluation function is to use a linear combination of features. That is, compute values for features about the state that you think are important, and then combine those features by multiplying them by different values and adding the results together. You might decide what to multiply each feature by based on how important you think it is.</li>

</ul>