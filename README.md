# KestoG
Russian draughts engine KestoG v1.1 by Kestutis Gasaitis<br>
that compiles on Linux

# Origins
KestoG win32 bit version was running as DLL under CheckerBoard program,
using undergoing DLL calls to communicate with GUI. I turned it into a
Linux command line application where developer can manually call these functions.

# API
  - int WINAPI enginecommand (char str[256], char reply[1024]);
  - int WINAPI islegal (int b[8][8], int color, int from, int to,struct CBmove *move);
  - int WINAPI getmove (int board[8][8],int color,double maxtime,char str[1024],int *playnow,int info,int unused,struct CBmove *move)
<br>
The latter is probably the most useful because this is what gives engine a position to search and returns the best move.
I also provided functions move_from_initial_position() and perft_test() as an example.

# Search move
     cmk@cmk:~/KestoG$ make && ./KestoG 
     gcc -O3 -x c KestoG.C -o KestoG
     
     Before:
    
     6  0  6  0  0  0  5  0 
     0  6  0  0  0  5  0  5 
     6  0  6  0  0  0  5  0 
     0  6  0  0  0  5  0  5 
     6  0  6  0  0  0  5  0 
     0  6  0  0  0  5  0  5 
     6  0  6  0  0  0  5  0 
     0  6  0  0  0  5  0  5 
    
    
    [thinking] [depth 3] [move 24-19] [time 0.00] [eval -1] [nodes 216], [pv ]
    [thinking] [depth 4] [move 24-19] [time 0.00] [eval 3] [nodes 494], [pv ]
    [thinking] [depth 5] [move 24-19] [time 0.00] [eval -3] [nodes 1096], [pv ]
    [thinking] [depth 6] [move 24-19] [time 0.00] [eval 1] [nodes 2236], [pv ]
    [thinking] [depth 7] [move 24-19] [time 0.00] [eval -1] [nodes 6087], [pv ]
    [thinking] [depth 8] [move 24-19] [time 0.00] [eval 2] [nodes 11995], [pv ]
    [thinking] [depth 9] [move 24-19] [time 0.01] [eval -1] [nodes 24881], [pv ]
    [thinking] [depth 10] [move 22-17] [time 0.02] [eval 2] [nodes 61637], [pv ]
    [thinking] [depth 11] [move 22-17] [time 0.03] [eval 0] [nodes 114877], [pv ]
    [thinking] [depth 12] [move 22-18] [time 0.06] [eval 3] [nodes 235571], [pv ]
    [thinking] [depth 13] [move 22-18] [time 0.12] [eval -2] [nodes 499295], [pv ]
    [thinking] [depth 14] [move 22-18] [time 0.26] [eval 2] [nodes 1045261], [pv ]
    [thinking] [depth 15] [move 22-18] [time 0.58] [eval 0] [nodes 2402710], [pv ]
    [thinking] [depth 16] [move 22-18] [time 1.24] [eval 3] [nodes 5096615], [pv ]
    [done] [depth 16] [move 22-18] [time 1.24] [eval 3] [nodes 5096615] [PV 22-18 10-14 25-22 11-16 24-20  8-11 28-24  6-10 22-17  4- 8]Status: [done] [depth 16] [move 22-18] [time 1.24] [eval 3] [nodes 5096615] [PV 22-18 10-14 25-22 11-16 24-20  8-11 28-24  6-10 22-17  4- 8]
    Move from (5,5) to (4,4)
    Old piece: 5, New piece: 5
    
     After:
    
     6  0  6  0  0  0  5  0 
     0  6  0  0  0  5  0  5 
     6  0  6  0  0  0  5  0 
     0  6  0  0  0  5  0  5 
     6  0  6  0  5  0  5  0 
     0  6  0  0  0  0  0  5 
     6  0  6  0  0  0  5  0 
     0  6  0  0  0  5  0  5 

# Perft test
    cmk@cmk:~/KestoG$ make && ./KestoG 
    gcc -O3 -x c KestoG.C -o KestoG
    
     8 . x . x . x . x
     7 x . x . x . x .
     6 . x . x . x . x
     5 . . . . . . . .
     4 . . . . . . . .
     3 o . o . o . o .
     2 . o . o . o . o
     1 o . o . o . o .
       a b c d e f g h
    
     Perft test, depth 10:
    
     Move: g3-f4, nodes: 48601093
     Move: g3-g4, nodes: 65135691
     Move: e3-d4, nodes: 56974563
     Move: e3-f4, nodes: 56818265
     Move: c3-b4, nodes: 64503403
     Move: c3-d4, nodes: 56524808
     Move: a3-b4, nodes: 57961671
    
        Depth: 10
        Nodes: 406519494
         Time: 7070
