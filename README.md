Download Link: https://assignmentchef.com/product/solved-csci1200-data-structures-homework-2-league-of-legends-classes
<br>
In this assignment you will parse, compute, and study statistics from an obscure video-based endeavor called “League of Legends”. As it is unlikely that you know anyone who has played this sport, we will summarize all of the rules that you need to know to complete this homework. <em>We certainly do not recommend you engage in such activities before you have completed your homework!</em>

A head-to-head <em>match </em>in League of Legends consists of two <em>teams </em>of 5 <em>players</em>. At the start of the match, each player selects a <em>champion </em>from a list of (currently) 134 champions, each with their own abilities. Players may coordinate to select champions with complementary strengths to improve the performance of their team in the match. During the match, each player controls his or her champion character and battles with players on the opposite team and also computer-controlled <em>minion </em>characters. When combat results in the <em>death </em>of a champion, that player must wait a small period of time before their champion <em>re-spawns </em>and they can re-join the match. Credit for the <em>kill </em>of a champion character is given to the appropriate player on the other team, or in some cases to a general game minion. One or more of the teammates may also be given credit for <em>assisting</em>. The game ends when one team destroys the other team’s <em>Nexus</em>.

More details on the game are available here: <a href="https://en.wikipedia.org/wiki/League_of_Legends">https://en.wikipedia.org/wiki/League_of_Legends</a><a href="https://en.wikipedia.org/wiki/League_of_Legends">.</a> Data for this homework comes from actual gameplay, made publicly available by the game author, <em>Riot Games,</em>

<em>Inc.</em>: <a href="https://developer.riotgames.com/docs/getting-started">https://developer.riotgames.com/docs/getting-started</a><a href="https://developer.riotgames.com/docs/getting-started">.</a> We have heavily reduced these very large and detailed datasets to a minimum set of information.

Here is an example of the input format for this homework (some event lines are omitted for space):

MATCH ID 1778973240

LOSING TEAM iTcnRKaneki playing champion Syndra T1Zed playing champion Kalista

IamZevahc playing champion Thresh

SushiNChopstix playing champion Riven

BattlecastLulu playing champion Udyr

WINNING TEAM

Dopy playing champion Graves komimatt playing champion Brand

SRVaRiaX playing champion Lissandra

Diddydan playing champion Zac

Jrazo playing champion Blitzcrank

EVENTS

@ 277230 BattlecastLulu [ SushiNChopstix ] killed SRVaRiaX

@ 432589 Dopy [ Jrazo ] killed T1Zed

@ 444272 SushiNChopstix [ T1Zed IamZevahc ] killed Dopy

@ 448804 minion killed SushiNChopstix @ 519016 T1Zed [ IamZevahc ] killed Dopy

. . .

@ 2410278 Dopy [ komimatt SRVaRiaX Jrazo ] killed BattlecastLulu END

First we see the MATCH ID, then the players and champions for each team are listed. The teams are labeled “WINNING” and “LOSING”, indicating the final result of the match. The highlights of all <em>champion kill </em>events are listed chronologically. Each of these events begins with the ’@’ character, then a timestamp (in milliseconds from the start of the match), the name of the player given primary credit for the kill, the assistants (if any) listed in square brackets, and finally the name of the victim. At the end of the events list is the keyword “END”. An input file will contain one or more matches.

<h1>File I/O and Command Line Arguments</h1>

Your program will expect 3 required command line arguments. The first and second are the names of the input and output files, respectively. The third argument is the name of the output table that should be printed, one of “players”, “champions”, or “custom”. For example, here are some valid command lines to your program:

./lol_stats.out input_simple.txt output_simple_players.txt                         players

./lol_stats.out input_small.txt                       output_small_champions.txt champions

./lol_stats.out input_medium.txt output_medium_custom.txt custom <strong>Statistics Collected and Output</strong>

The output will be one of three different tables, as specified on the command line.

First, we study the “players” table, containing all players who participated in one or more matches in the input file. Each row contains the number of kills credited to this player, the number of times they died and re-spawned during the match, the <em>kill-to-death ratio </em>(KDR), and the names of the champion(s) used by that player. <em>NOTE: To avoid divide by zero, if a player’s deaths is zero, then the KDR is equal to the kills. </em>If a player played more than one champion in different matches, the names of the champions should be sorted alphabetically, separated by commas (without duplicates). Overall, the rows of this table are sorted by KDR. If two players are tied in KDR, they are sorted by kills (highest first), then by deaths, and if tied in all of the above, they should be alphabetically by player name. <em>Note: We will simply use the less than &lt; operator on STL strings, which places numbers before capital letters, and capital letters before lowercase letters.</em>

Here is an example of this output:

<table width="488">

 <tbody>

  <tr>

   <td width="160">PLAYER NAME</td>

   <td colspan="2" width="119">KILLS DEATHS</td>

   <td width="49">KDR</td>

   <td width="160">PLAYED WITH CHAMPION(S)</td>

  </tr>

  <tr>

   <td width="160">squirT0T</td>

   <td width="77">6</td>

   <td width="42">1</td>

   <td width="49">6.00</td>

   <td width="160">Amumu</td>

  </tr>

  <tr>

   <td width="160">komimatt</td>

   <td width="77">7</td>

   <td width="42">2</td>

   <td width="49">3.50</td>

   <td width="160">Brand</td>

  </tr>

  <tr>

   <td width="160">KelloggsBRNFLKZ</td>

   <td width="77">10</td>

   <td width="42">3</td>

   <td width="49">3.33</td>

   <td width="160">Sejuani</td>

  </tr>

  <tr>

   <td width="160">Diddydan</td>

   <td width="77">3</td>

   <td width="42">1</td>

   <td width="49">3.00</td>

   <td width="160">Zac</td>

  </tr>

  <tr>

   <td width="160">AntiToro</td>

   <td width="77">13</td>

   <td width="42">6</td>

   <td width="49">2.17</td>

   <td width="160">Tristana</td>

  </tr>

  <tr>

   <td width="160">Dopy</td>

   <td width="77">10</td>

   <td width="42">6</td>

   <td width="49">1.67</td>

   <td width="160">Graves</td>

  </tr>

  <tr>

   <td width="160">Jrazo</td>

   <td width="77">4</td>

   <td width="42">3</td>

   <td width="49">1.33</td>

   <td width="160">Blitzcrank</td>

  </tr>

  <tr>

   <td width="160">alittlemido</td>

   <td width="77">5</td>

   <td width="42">4</td>

   <td width="49">1.25</td>

   <td width="160">Thresh</td>

  </tr>

  <tr>

   <td width="160">OMGLeiChen</td>

   <td width="77">9</td>

   <td width="42">10</td>

   <td width="49">0.90</td>

   <td width="160">Graves</td>

  </tr>

  <tr>

   <td width="160">Jovone</td>

   <td width="77">7</td>

   <td width="42">8</td>

   <td width="49">0.88</td>

   <td width="160">Nasus</td>

  </tr>

  <tr>

   <td width="160">SRVaRiaX</td>

   <td width="77">6</td>

   <td width="42">7</td>

   <td width="49">0.86</td>

   <td width="160">Lissandra</td>

  </tr>

  <tr>

   <td width="160">iTcnRKaneki</td>

   <td width="77">6</td>

   <td width="42">7</td>

   <td width="49">0.86</td>

   <td width="160">Syndra</td>

  </tr>

  <tr>

   <td width="160">Stylether</td>

   <td width="77">10</td>

   <td width="42">12</td>

   <td width="49">0.83</td>

   <td width="160">LeBlanc</td>

  </tr>

  <tr>

   <td width="160">SushiNChopstix</td>

   <td width="77">6</td>

   <td width="42">8</td>

   <td width="49">0.75</td>

   <td width="160">Riven</td>

  </tr>

  <tr>

   <td width="160">T1Zed</td>

   <td width="77">6</td>

   <td width="42">8</td>

   <td width="49">0.75</td>

   <td width="160">Kalista</td>

  </tr>

  <tr>

   <td width="160">Indovaasion</td>

   <td width="77">5</td>

   <td width="42">10</td>

   <td width="49">0.50</td>

   <td width="160">Fizz</td>

  </tr>

  <tr>

   <td width="160">Zraotic</td>

   <td width="77">4</td>

   <td width="42">9</td>

   <td width="49">0.44</td>

   <td width="160">Warwick</td>

  </tr>

  <tr>

   <td width="160">BattlecastLulu</td>

   <td width="77">1</td>

   <td width="42">3</td>

   <td width="49">0.33</td>

   <td width="160">Udyr</td>

  </tr>

  <tr>

   <td width="160">IamZevahc</td>

   <td width="77">0</td>

   <td width="42">5</td>

   <td width="49">0.00</td>

   <td width="160">Thresh</td>

  </tr>

  <tr>

   <td width="160">Zyyke</td>

   <td width="77">0</td>

   <td width="42">7</td>

   <td width="49">0.00</td>

   <td width="160">Taric</td>

  </tr>

 </tbody>

</table>

Next, we study the “champions” table, which contains all champions that were used in one or more matches in the input file. This table contains the number of wins &amp; losses, the corresponding win percentage, and the number of times that champion was killed not by another champion, but by a minion (rather embarrassing if you think about it…). Overall this table is sorted by win percentage, highest first. If tied in win percentage, champions should be sorted by wins, then by losses, and finally by name if all of the above are equal.

And here is an example of this type of table:

2

CHAMPION NAME                          WINS LOSSES           WIN%      MINION DEATHS

Amumu                                                  1                0          1.00                                    0

Blitzcrank                                          1                0          1.00                                    0

Brand                                                    1                0          1.00                                    0

LeBlanc                                                1                0          1.00                                    1

Lissandra                                            1                0          1.00                                    0

Sejuani                                                1                0          1.00                                    0

Tristana                                              1                0          1.00                                    0

Zac                                                        1                0          1.00                                    0

Graves                                                  1                1          0.50                                    0

Thresh                                                  1                1          0.50                                    0

Fizz                                                       0                1          0.00                                    0

Kalista                                                 0                1          0.00                                    0

Nasus                                                    0                1          0.00                                    0

Riven                                                    0                1          0.00                                    1

Syndra                                                  0                1          0.00                                    0

Taric                                                     0                1          0.00                                    0

Udyr                                                      0                1          0.00                                    0

Warwick                                               0                1          0.00                                    0

Finally, the “custom” table is a chance for you to be creative. You will collect, organize, and output some other statistic from the provided match data. Notice that the earlier tables didn’t use the event timestamp, or the champion kill assists. You may be interested in exploring that data. Can you identify champions who are good <em>supporting </em>team members (many assists, but not many kills)? Can you identify the best <em>carry </em>players, who are strong late in the match and help carry the team to victory? Or perhaps you can study pairs of champions who are more successful when they play on a team together. Or find champions who are particularly susceptible to a team with a specific enemy champion.

The most important task for this part of the assignment is to write a concise description (∼ 100 words) of your new statistic. What is your hypothesis for the patterns that might emerge from your statistic? Put this description in your README.txt along with any other notes for the grader. Be sure to tell the grader which dataset best demonstrates your new statistic. You may also create your own dataset and include it and your program’s output for that test case with your submission. Extra credit will be awarded to particularly interesting statistics that require clever programming.

<h1>Useful Code</h1>

To control the formatting of your tables, you’ll want to read up on the various iomanipulators: std::setw(int), std::setprecision(int), std::fixed, std::left, and std::right. And don’t forget about the sort function that can be used to order the contents of a vector.

We encourage you to use the &lt;&lt; input stream function for strings to implement all of the parsing necessary for this assignment. Be sure to study the more complex parsing example on this website: <a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/other_information.php">Misc. C++ </a><a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/other_information.php">Programming Information</a><a href="http://www.cs.rpi.edu/academics/courses/spring17/ds/other_information.php">.</a> <em>Note: You do not need to use </em>getline <em>or </em>eof<em>. In fact, your code should not rely on the position of newlines or whitespace within the input file.</em>

<h1>Program Requirements &amp; Submission Details</h1>

Your program should involve the definition of <em>at least one well-designed C++ class </em>that has its own .h and .cpp files, named appropriately.


