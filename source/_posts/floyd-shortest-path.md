---
title: Floyd最短路径算法
tags:
  - floyd
  - shortest path
id: 25
categories:
  - Programming
date: 2007-12-19 02:11:00
---

2006-10-20, by leon_jlu
     在图论中经常会遇到这样的问题，在一个有向图里，求出任意两个节点之间的最短距离。我们在离散数学、数据结构课上都遇到过这个问题，在计算机网络里介绍网络层的时候好像也遇到过这个问题，记不请了... 但是书本上一律采取的是Dijkstra算法，通过Dijkstra算法可以求出单源最短路径，然后逐个节点利用Dijkstra算法就可以了。不过在这里想换换口味，采取Robert Floyd提出的算法来解决这个问题。下面让我们先把问题稍微的形式化一下：

<!--more-->
      如果有一个矩阵D=[d(ij)]，其中d(ij)&gt;0表示i城市到j城市的距离。若i与j之间无路可通，那么d(ij)就是无穷大。又有d(ii)=0。编写一个程序，通过这个距离矩阵D，把任意两个城市之间的最短与其行径的路径找出来。
     我们可以将问题分解，先找出最短的距离，然后在考虑如何找出对应的行进路线。如何找出最短路径呢，这里还是用到动态规划的知识，对于任何一个城市而言，i到j的最短距离不外乎存在经过i与j之间的k和不经过k两种可能，所以可以令k=1，2，3，...，n(n是城市的数目)，在检查d(ij)与d(ik)+d(kj)的值；在此d(ik)与d(kj)分别是目前为止所知道的i到k与k到j的最短距离，因此d(ik)+d(kj)就是i到j经过k的最短距离。所以，若有d(ij)&gt;d(ik)+d(kj)，就表示从i出发经过k再到j的距离要比原来的i到j距离短，自然把i到j的d(ij)重写为d(ik)+d(kj)，每当一个k查完了，d(ij)就是目前的i到j的最短距离。重复这一过程，最后当查完所有的k时，d(ij)里面存放的就是i到j之间的最短距离了。所以我们就可以用三个for循环把问题搞定了，但是有一个问题需要注意，那就是for循环的嵌套的顺序：我们可能随手就会写出这样的程序，但是仔细考虑的话，会发现是有问题的。

                     for(int i=0; i&lt;n; i++)
                           for(int j=0; j&lt;n; j++)
                                for(int k=0; k&lt;n; k++)  

     问题出在我们太早的把i-k-j的距离确定下来了，假设一旦找到了i-p-j最短的距离后，i到j就相当处理完了，以后不会在改变了，一旦以后有使i到j的更短的距离时也不能再去更新了，所以结果一定是不对的。所以应当象下面一样来写程序：

                    for(int k=0; k&lt;n; k++)
                         for(int i=0; i&lt;n; i++)
                              for(int j=0; j&lt;n; j++)

    这样作的意义在于固定了k，把所有i到j而经过k的距离找出来，然后象开头所提到的那样进行比较和重写，因为k是在最外层的，所以会把所有的i到j都处理完后，才会移动到下一个k，这样就不会有问题了，看来多层循环的时候，我们一定要当心，否则很容易就弄错了。
     接下来就要看一看如何找出最短路径所行经的城市了，这里要用到另一个矩阵P，它的定义是这样的：p(ij)的值如果为p，就表示i到j的最短行经为i-&gt;...-&gt;p-&gt;j，也就是说p是i到j的最短行径中的j之前的最后一个城市。P矩阵的初值为p(ij)=i。有了这个矩阵之后，要找最短路径就轻而易举了。对于i到j而言找出p(ij)，令为p，就知道了路径i-&gt;...-&gt;p-&gt;j；再去找p(ip)，如果值为q，i到p的最短路径为i-&gt;...-&gt;q-&gt;p；再去找p(iq)，如果值为r，i到q的最短路径为i-&gt;...-&gt;r-&gt;q；所以一再反复，到了某个p(it)的值为i时，就表示i到t的最短路径为i-&gt;t，就会的到答案了，i到j的最短行径为i-&gt;t-&gt;...-&gt;q-&gt;p-&gt;j。因为上述的算法是从终点到起点的顺序找出来的，所以输出的时候要把它倒过来。
     但是，如何动态的回填P矩阵的值呢？回想一下，当d(ij)&gt;d(ik)+d(kj)时，就要让i到j的最短路径改为走i-&gt;...-&gt;k-&gt;...-&gt;j这一条路，但是d(kj)的值是已知的，换句话说，就是k-&gt;...-&gt;j这条路是已知的，所以k-&gt;...-&gt;j这条路上j的上一个城市(即p(kj))也是已知的，当然，因为要改走i-&gt;...-&gt;k-&gt;...-&gt;j这一条路，j的上一个城市正好是p(kj)。所以一旦发现d(ij)&gt;d(ik)+d(kj)，就把p(kj)存入p(ij)。
   下面是具体的C代码：
   #include            
   #include            
   #include            
   #define   MAXSIZE   20        

   void  floyd(int [][MAXSIZE], int [][MAXSIZE], int);
   void  display_path(int [][MAXSIZE], int [][MAXSIZE], int);
   void  reverse(int [], int);
   void  readin(int [][MAXSIZE], int *);

   #define   MAXSUM(a, b)   (((a) != INT_MAX &amp;&amp; (b) != INT_MAX) ?
                          ((a) + (b)) : INT_MAX)

   void floyd(int dist[][MAXSIZE], int path[][MAXSIZE], int n)
   {
       int  i, j, k;
       for (i = 0; i &lt; n; i++)  
           for (j = 0; j &lt; n; j++)
               path[i][j] = i;
       for (k = 0; k &lt; n; k++)  
           for (i = 0; i &lt; n; i++)
               for (j = 0; j &lt; n; j++)  
                    if (dist[i][j] &gt; MAXSUM(dist[i][k], dist[k][j]))
                    {
                         path[i][j] = path[k][j];
                         dist[i][j] = MAXSUM(dist[i][k], dist[k][j]);
                    }
   }

   void display_path(int dist[][MAXSIZE], int path[][MAXSIZE], int n)
   {
       int  *chain;
       int  count;
       int  i, j, k;
       printf("nnOrigin-&gt;Dest   Dist   Path");
       printf(  "n-----------------------------");
       chain = (int *) malloc(sizeof(int)*n);
       for (i = 0; i &lt; n; i++)
           for (j = 0; j &lt; n; j++)
           {
               if (i != j)
               {  
                    printf("n%6d-&gt;%d    ", i+1, j+1);
                    if (dist[i][j] == INT_MAX)
                         printf("  NA    ");
                    else
                    {
                         printf("%4d    ", dist[i][j]);
                         count = 0;  
                         k = j;
                         do
                         {
                             k = chain[count++] = path[i][k];
                         } while (i != k);
                         reverse(chain, count);
                         printf("%d", chain[0]+1);
                         for (k = 1; k &lt; count; k++)
                              printf("-&gt;%d", chain[k]+1);
                         printf("-&gt;%d", j+1);
                    }
               }
           }
       free(chain);            
   }

   #define SWAP(a, b)  { temp = a; a = b; b = temp; }

   void reverse(int x[], int n)
   {
       int  i, j, temp;
       for (i = 0, j = n-1; i &lt; j; i++, j--)
            SWAP(x[i], x[j]);
   }

   void readin(int dist[][MAXSIZE], int *number)
   {
       int  origin, dest, length, n;
       int  i, j;
       char line[100];
       gets(line);              
       sscanf(line, "%d", &amp;n);
       *number = n;
       for (i = 0; i &lt; n; i++)
       {
           for (j = 0; j &lt; n; j++)
                dist[i][j] = INT_MAX;
           dist[i][i] = 0;    
       }
       gets(line);              
       sscanf(line, "%d%d%d", &amp;origin, &amp;dest, &amp;length);
       while (origin != 0 &amp;&amp; dest != 0 &amp;&amp; length != 0)
       {
          dist[origin-1][dest-1] = length;
          gets(line);        
          sscanf(line, "%d%d%d", &amp;origin, &amp;dest, &amp;length);
       }
   }
     测试程序如下所示：
   int main(void)
   {
       int dist[MAXSIZE][MAXSIZE];
       int path[MAXSIZE][MAXSIZE];
       int n;
       printf("nInput the path information:");
       printf("n----------------------------n");
       readin(dist, &amp;n);
       floyd(dist, path, n);
       display_path(dist, path, n);
       getchar();
   }
     其中readin函数规定了输入的格式，第一列是指出有多少个城市；第二列以后每行三个数；第一个和第二个是一条路径的起点和终点，第三个数是路径的长度，最后以三个0作为输入结束条件。下面是一个输入的例子：
              Input the path information:
            --------------------------------------
              4
              1          2          5
              2          1          50
              2          3          15
              2          4          5
              3          1          30
              3          4          15
              4          1          15
              4          3          5
              0          0          0
   对应的输出结果为：
     Origin-&gt;Dest      Dist          Path
  ----------------------------------------------
        1-&gt;2             5           1-&gt;2
        1-&gt;3            15          1-&gt;2-&gt;4-&gt;3
        1-&gt;4            10          1-&gt;2-&gt;4
        2-&gt;1            20          2-&gt;4-&gt;1
        2-&gt;3            10          2-&gt;4-&gt;3
        2-&gt;4             5           2-&gt;4
        3-&gt;1            30          3-&gt;1
        3-&gt;2            35          3-&gt;1-&gt;2
        3-&gt;4            15          3-&gt;4
        4-&gt;1            15          4-&gt;1
        4-&gt;2            20          4-&gt;1-&gt;2
        4-&gt;3             5           4-&gt;3