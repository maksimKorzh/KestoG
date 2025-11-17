# KestoG
Russian draughts engine KestoG v1.1 by Kestutis Gasaitis<br>
that compiles on Linux

# How to compile
gcc -O3 -x c KestoG.C -o KestoG

# Origins
KestoG win32 bit version was running as DLL under CheckerBoard program,
using some text protocol to communicate with GUI which I don't know how
it's called. I turned it into a Linux command line application similar
to UCI chess engines.

# API (use in main(), WINAPI is just ignored)
  - int WINAPI enginecommand (char str[256], char reply[1024]);
  - int WINAPI islegal (int b[8][8], int color, int from, int to,struct CBmove *move);
  - int WINAPI getmove (int board[8][8],int color,double maxtime,char str[1024],int *playnow,int info,int unused,struct CBmove *move)
<br>
<br>
The latter is probably the most useful because this is what gives engine a position to search and returns the best move.
