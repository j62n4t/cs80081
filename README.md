java c
Tower   of   Hanoi   Puzzle
COMP   273,   Fall   2024,   Assignment   4
IntroductionThis   assignment   will give you   more   practice with functions   and   recursion   in   MIPS.   In   addition,   it gives you some experience of   how to   make your   code   efficient,   both   in terms   of   the   number   of   instructions   as well as with   the   use   of the   cache.All   the   functions   you   write   in   this   assignment      must      respect      register   conventions.   Your   code   must   also   include   useful   comments to   make   it   readable. You   will   need to   use two   MARS tools   in this   assignment:
•    Data    Cache      Simulator:      This      tool    allows      you      to      set    different    cache      sizes    and      types,    and   measures the   number of   memory   accesses, and cache   misses.
• Instruction Counter: This tool counts the number of true MIPS assembly   instructions that   are   executed   during your   program.Each    tool    needs    to      be    connected    to      MARS,      and      you    will      want      to      use      a      combination      of   breakpoints   and   the   reset   button   on   each   tool   to      make   careful      measurements   of   your   code   performance. you should go over   them   in   "MARs   tutorial   3"
Assignment   Objectives   (40   marks total)
Provided code will   help you get started with this   assignment.   The   code   lets   you   run   2   different   tests   by   changing AlgorithmType   in the   .data section   at the top   of the   code.
-                Algorithm Type   0 will   help you   test the   first   objective   of   this   assignment   (Tower   of   Hanoi   -recursive   method).
-          Algorithm   Type    1    will    help    you   test   the    second    objective      of   this      assignment      (Tower      of   Hanoi -non-recursive   method).
1-    Tower   of      Hanoi -recursive   method    (20      marks)
The tower   of    Hanoi    is    a    puzzle    invented    by    French      mathematician      E(´)douard      Lucas.       The   puzzleconsists   of three   rods: A,   B   and   C,   and   n   disks   (labeled   with   numbers   1..n)   with   different   radii   stacked on pod A. The disks are arranged from top to bottom in the   order   of decreasing   radius.   Figure   1shows   an   example   with three   disks. You   can   move the   diskbetween   rods,   but   smaller   disks   have to   be   on top   of   bigger   disks,   and you   can   only   moveone   disk   at   one time. The   goal   is   to   move all the disks from   rod A to   rod   C with the   minimal   number   of    moves.
   
Figure   1:   An   example   of the tower   of   Hanoi   with   n =   3Alice is trying to solve this   puzzle (with 3 disks). She   cannot solve   it   directly, so she   asks   Bob   to      move   disk      1   and   2   from      rod   A   to   B,   then   she   can   simply      move   disk   3   fromA to   C,   and   ask   Bob   again to   move two   disks from   B      to   C,   and   solve the   problem!      These   two   tasks    are      still      a      bit      difficult   for    Bob,      so   for   the   first   task,    he      asks      Charlie   to    move   the   smallest   disk from A to   C so that   he   can   move   the   second   disk   from   A   to   B,   and   then   ask   Charlie to   move the smallest   disk from   C to   B. Similar for the   second   task,   he   asks   Charlie   to   move the   smallest   disk from   B to A   before   he   moves the   second   disk   from   B   to   C,   and   asks   Charlie   to      move   the   smallest   disk   from   A   to   C.   All   the   tasks   for   Charlie   are   simple   enough so he doesn’t need help from others. By asking others to solve   the sub-problems, Alice   successfully   solves   the   puzzle:
1.    Charlie    moves   disk   1   from A   to   C;
2.      Bob   moves   disk   2   from A   to   B;
3.    Charlie    moves   disk   1   from   C   to   B;
4.    Alice   moves   disk   3   from A   to   C;
5.    Charlies   moves   disk   1   from   B   to A;
6.      Bob   moves   disk   2   from   B   to   C
7.    Charlies    moves   disk   1   from A   to   C.This   idea can   be formalized   using a   recursive algorithm shown   in Algorithm1,   which   gives   the   solution to   move   n   disks from the source   rod   to   the   target   rod,   with   the   help   of   the   auxiliary   rod.
Algorithm    1    Recursive    algorithm    for    the   tower    of    Hanoi
procedure      MOVE   (n,   source,   target,   auxiliary)      :   if      n=1   then
move   disk   1   from   source   to   target
else
MOVE(n         - 1,   source,      auxiliary,      target)   move   disk   n   from source   to   target
MOVE(n         - 1,      auxiliary,      target,   source)
end   if
end      procedureImplement    the    recursive    algorithm    described    above      in    the      provided      hanoi.asm.    The      program   should   read   an   integer   n   (already   implemented),   i.e.,   the   number   of   disks.   The   output   should   be   the   steps to solve the   problem,   one step   per   line,   printed   to the   standard   output.    Each   line should
have the format   of:                                                                                                                                                                                                                                                                                                                                                                                                                                                
Step i: move disk    from      to   .               Here   is   an   example   of   the   output   for   the   problem   with   n   =   3:
S代 写COMP 273, Fall 2024, Assignment 4 Tower of Hanoi PuzzleR
代做程序编程语言tep   1:   move disk   1 from      A      to      C   Step   2:   move disk   2 from    A      to      B   Step   3:   move disk   1 from   C   to   B            Step 4:   move disk   3   from    A      to      C   Step   5:   move disk   1 from      B      to      A   Step   6:   move disk   2 from      B      to      C   Step   7:   move disk   1 from   A   to   C
You   can   assume that the   input   nisa valid   integer and   1   ≤    n    ≤   15.          Make sure you   strictly   follow   the   output   format!
2-    Tower   of      Hanoi -   non-recursive   method      (15      marks)Write    a    non-recursive    algorithm    for    the    tower    of    Hanoi    which      replacing      the      above      recursion   algorithm with a   loop. You   have the same   input   assumption   and   output   requirements   as   indicated   for the   recursion   algorithm   in   1.
3-   Measure cache performance   (5   marks)
Complete and submit the   provided   .csv   (comma-separated values) file with   entries   summarizing   the cache   performance   (i.e.,   number of cache   misses   and   hit   rate) and the   instruction   count   of
the   recursive and   non-recursive versions   of the Tower of   Hanoi algorithms   implemented   in   1   and   2, for an   input   n   (number   of   disks)   =15.For   both   solutions, fix the   cache size at   1024   bytes   and examine   performance   by   varying   the   block   size   and   number   of   blocks   (with   a   fixed   cache   size).   Include   results   for   at   least   two   configurations   of   block   size   and   number   of   blocks   for   each   solution.   Use   LRU   as   a   replacement   policy   for   all   the   tested configurations.
Collect data only from the final version   of your   implementation,   which   you   will   submit   for   grading.
Ensure that   you do not   modify   your   code once data collection begins, as the TA will verify accuracy   and may deduct marks if the   data collected is inaccurate.The filename   must   have the form      .csv, that   is,   it   should   consist   of your student   number   and   have the file extension   .csv, for   instance,   “260123456.csv”   . To   best ensure you   respect the file   format,   rename   and   edit the   provided   csv file.    You   may   include   comments   in the file   by   starting   a   line with “#”, but otherwise complete the entries in the provided file with comma separated values,   or fields,   on   each   line.    These fields   consist   of your   student   number, the   test   name,   the   block   size,   number   of   blocks,   the   instruction   count,   the   number   of   memory   accesses,   the   number   of   cache   misses,   and the   hit   rate.
The file should   only   contain ASCII. You   can   use the   MARS   text   editor   to   load   and   edit   the   provided   csv file.    Take care to write   your   student   ID   on   each   line   of the   provided   csv   file.
Follow the following steps to   measure the   required   performance of your Tower of   Hanoi   solutions:
1.          Set two   breakpoints   at the   locations   specified   in the   comments   within the   provided   .asm   file for   each   implemented algorithm.
2.          Ensure the   cache   simulator   is   configured   correctly, then   connect   it   to   MIPS.
3.          Ensure the   instruction   counter   is   connected   to   MIPS.
4.               Run your code   up to the   first   breakpoint.
5.          Press   thereset   button   on   the   cache   simulator.
6.          Press   thereset   button   on   the   instruction   counter.
7.               Press the run   button to continue   execution.
8.          Once the simulation   stops   at the   second   breakpoint just   before   exiting the   program,   make   note of the   instruction   count, and the cache   performance.
9.          Repeat step   1 to   8   for   each   algorithm   and   chosen   cache   configuration   (i.e.,   block   size   and   number of   blocks).
To evaluate cache   performance, you   must   record the   memory access   count, the   number   of   cache   misses, and the   hit   rate. The file contains four   entries   to   demonstrate these   measurements   for the two algorithms   of the Tower of   Hanoi   puzzle, with   at   least   two   different   configurations   for      the   block size   for   each.
Submission      Instructions
Submit   exactly two files that   includes your “   hanoi.asm”   and   “.csv”   file   containing   the measurements.   Do   not   use a   zip file or any   other   kind   of   archive.      Include your   name   and   student   number   in all files submitted   as   instructed above.    Add   to   comments   at   the top   of   the   provided   hanoi.asm file anything you would want the TAs   to   know   (i.e., treat   the   comments   at   the top   of   the asm file as   a   README, that also   should      include   a   request to   apply   the   one-time   penalty waiver for this   submission   if it   has   not   been   used   before).
All work   must   be your   own   and   must   be submitted   by   MyCourses.   Double check that you   have   correctly submitted the correct version of your   assignment   as   you   will   NOT   receive   marks   for            work   incorrectly submitted.
HOWIT WILL   BE GRADED
•               Your   program   must execute   to   be graded.
•          The grader   should   test your   code   against   different   values   of   n   input   for   both   implemented   algorithms   and compare the   output with the expected   one   (partial   marks will   be   given).
•               Not following the submission   instruction will   result   in   losing 3   marks.
•               Not following   MIPs   register   convention will   result   in   losing   5   marks.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
