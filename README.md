Download Link: https://assignmentchef.com/product/solved-project-4-database-programming-ece-650
<br>
<h1>Overview</h1>

In this assignment, you will build a PostgreSQL database. The relation schemas (tables) of the database will be provided, along with the database values. You will implement:

<ol>

 <li>A C++ program to read text files containing the entries (rows) for each table, and build the database by creating each table and adding entries.</li>

 <li>A C++ library (set of functions) which will provide an interface for a program to interact with the database (e.g. add rows to the tables and query for certain information).</li>

</ol>




The database relates to ACC basketball teams, and will allow queries to discover information about things like player statistics, team attributes, etc. The database will have 4 tables, specified as follows (an underlined attribute indicates the primary key for the table):




PLAYER (<u>PLAYER</u>​ _<u>​ ID</u>​ ,​ TEAM_ID, UNIFORM_NUM, FIRST_NAME, LAST_NAME, MPG, PPG,

RPG, APG, SPG, BPG)

TEAM (<u>TEAM</u>​ _​ <u>ID</u>​ , NAME, STATE_ID, COLOR_ID, WINS, LOSSES)​

STATE (<u>STATE_ID</u><u>​ </u>, NAME)​

COLOR (<u>COLOR_ID</u><u>​ </u>, NAME)<u>​ </u>




*Note the following abbreviations: MPG = minutes per game, PPG = points per game, RPG = rebounds per game, APG = assists per game, SPG = steals per game, BGP = blocks per game




<h1>Tips on Working with the Virtual Machine</h1>

When you create your virtual machine and log-in for the first time, you will notice there may be few programs installed (e.g. no gcc, emacs, vim, etc.). You can download your choice of software easily using the command: sudo apt-get install &lt;package name&gt;.  For example:

sudo apt install build-essential emacs




In order to create a PostgreSQL database and interact with the database through a C++ API, you will need to install packages, which can be obtained via git as follows:

sudo apt install libpqxx-dev




<h1>What You Will Implement</h1>

Several skeleton files, and database table information files are provided to get you started. The following describes each file:

<ul>

 <li><strong>Database source text files: player.txt, team.txt, state.txt, color.txt</strong>.​ These files contain table-like information for each entry and each attribute that should be inserted into the respective database table.</li>

 <li><strong>cpp</strong>:​ The main function. Here you should implement code which will setup the database on each execution of the program. Specifically, it should drop (if needed) and add each table to the database (named ACC_BBALL), and then read information from the source text files and add rows to each table as appropriate.</li>

 <li><strong>h and query_funcs.cpp</strong>:​ Here you will implement functions to interact with the database (add new entries and print the results of 5 different queries specified below). You may add new functions to these files if desired (you don’t have to), but you should not change the definitions of the existing functions.</li>

 <li><strong>h and exerciser.cpp</strong>:​ Here you can add code in the exercise() function to test your query functions. The exercise() function is called from main() after the database is initialized.</li>

 <li><strong>Makefile</strong>:​ Will compile all source files into an executable program named “test”</li>

</ul>




Your task is to do the following:

<ul>

 <li>Create a PostgreSQL database named <strong>ACC_BBALL </strong>​ (​ All Caps)</li>

 <li>Create a user for the ACC_BBALL database named “postgres” with password</li>

</ul>

“passw0rd” (see the ppt charts for how to set the password of the postgres user).

<ul>

 <li>Implement support in main.cpp to connect (as user ‘postgres’) to the ACC_BBALL database and initialize its tables and data. Of course, usually a database will live persistently, but for the purposes of evaluating the submissions, the program should re-create the database every time. You should drop tables that may already exist (e.g.</li>

</ul>

from prior runs of your test) before creating an initializing the tables in the program.

<ul>

 <li>Implement the following query functions:</li>

</ul>

○ <strong>query1()</strong>:​ show all attributes of each player with average statistics that fall between the min and max (inclusive) for each enabled statistic

○    <strong>query2()</strong>:​ show the name of each team with the indicated uniform color

○ <strong>query3()</strong>:​ show the first and last name of each player that plays for the indicated team, ordered from highest to lowest ppg (points per game)

○ <strong>query4()</strong>:​ show first name, last name, and jersey number of each player that plays in the indicated state and wears the indicated uniform color

○ <strong>query5()</strong>:​ show first name and last name of each player, and team name and number of wins for each team that has won more than the indicated number of games

○ <strong>Important Note:</strong> Each query function should print its output. The format of this output should be as follows. The first row of output should contain each field name (separated by a single space character. The next rows of output should contain the values returned from the query, each also separated by a single space. The field name and each row of output should appear one line after the next.

<ul>

 <li>You may test your database and query functions by adding calls to the query functions inside the exerciser() function. For the purposes of grading assignments, we will replace the exerciser.cpp file with a new one that will test a variety of query calls.</li>

</ul>




<h1>Example Output and Checking Results</h1>

The following text shows an example output. This output corresponds to <strong>query1</strong>​ which is invoked to show all players with a minimum minutes per game (MPG) of 35 and a maximum minutes per game (MPG) of 40.




PLAYER_ID TEAM_ID UNIFORM_NUM FIRST_NAME LAST_NAME MPG PPG RPG APG SPG BPG

<ul>

 <li>12 3 Andrew WhiteIII 37 19 5 1 1.6 0.4</li>

 <li>12 20 Tyler Lydon 36 13 9 2 1.0 1.4</li>

</ul>

30 3 5 Luke Kennard 36 20 5 3 0.8 0.4

59 5 44 Ben Lammers 35 14 9 2 1.2 3.4

87 7 5 Davon Reed 35 15 5 2 1.3 0.5

98 8 4 Dennis SmithJr. 35 18 5 6 1.9 0.4

130 10 32 Steve Vasturia 35 13 4 3 1.2 0.1




The Unix command ‘diff’ can be used to compare results. For example, if the output above is copied into a file called validation.txt, it can be compared to output for the same query from your program. If your program is in a file called output.txt, the diff command could look as follows:




$ diff -w output.txt validation.txt




Note that the -w indicates that ‘diff’ should not report differences in whitespace (spaces, tabs) in the output. If you want to compare two files character for character, the -w flag can be omitted.




<h1>Detailed Submission Instructions</h1>

Your submission will include the following files:

<ol>

 <li><strong>Source Code   Files:   </strong>cpp,​                      query_funcs.h,            query_funcs.cpp,             exerciser.h,</li>

</ol>

exerciser.cpp

<ol start="2">

 <li><strong>Makefile</strong> – ​ <strong>Even if you have not made changes to the one provided</strong>​</li>

 <li><strong>Database source text files</strong>:​txt, team.txt, state.txt, color.txt</li>

</ol>




You will submit a zip file named “<strong>proj4_netid.zip</strong>​ ” to ​ <strong>Gradescope</strong>​ , e.g.:​

zip proj4_netid.zip Makefile *.h *.cpp *.txt







<h1>Extra Credit (+25%)</h1>

By implementing SQL transactions in C++, you may get a deeper understanding of SQL code and consider it as a common way to use databases. However, a typical use of databases in modern software architecture is using a higher-level framework (e.g. an Object Relational Mapping, or ORM) which obviates the need to worry about transaction details. Specifically, Object-Relational Mapping (ORM) is a technique that allows you to write transactions using an object-oriented paradigm. Many libraries have implemented this technique.




For example, some of you may have used Django to develop web applications. Django contains a default ORM layer to interact with data from relational database management systems like PostgreSQL. You may refer to <em>django.db.models</em>​ for details. And in addition to Django ORM, there are other ORM libraries, such as Hibernate, SQLAlchemy, Doctrine, etc. Choose one ORM library and implement the five queries shown in the previous statement. Submit your code as a zip file named “<strong>proj4_extra_netid.zip</strong>​ ”​ to ​ <strong>Gradescope</strong>​. We will schedule to let you give a demo to TAs for grading.