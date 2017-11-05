# Maze-problem

Maze problem

	求迷宫的路径.(深度优先搜索法)
  
【参考程序1】

const

     Road:array[1..8,1..8]of 0..3=((1,0,0,0,0,0,0,0),
     
				   (0,1,1,1,1,0,1,0),
           
				   (0,0,0,0,1,0,1,0),
           
				   (0,1,0,0,0,0,1,0),
           
				   (0,1,0,1,1,0,1,0),
           
				   (0,1,0,0,0,0,1,1),
           
				   (0,1,0,0,1,0,0,0),
           
				   (0,1,1,1,1,1,1,0)); {迷宫数组}
           
  FangXiang:array[1..4,1..2]of -1..1=((1,0),(0,1),(-1,0),(0,-1));{四个移动方向}
  
  WayIn:array[1..2]of byte=(1,1);	 {入口坐标}
  
  WayOut:array[1..2]of byte=(8,8);	 {出口坐标}
  
Var i,j,Total:integer;

Procedure Output;

var i,j:integer;

Begin

     For i:=1 to 8 do begin
     
	 for j:=1 to 8 do begin
   
	     if Road[i,j]=1 then write(#219);	   {1:墙}
       
	     if Road[i,j]=2 then write(' ');       {2:曾走过但不通的路}
       
	     if Road[i,j]=3 then write(#03) ;	   {3:沿途走过的畅通的路}
       
	     if Road[i,j]=0 then write(' ') ;      {0:原本就可行的路}
       
	 end;  writeln;
   
     end; inc(total);  {统计总数}   readln;
     
end;

Function Ok(x,y,i:byte):boolean;  {判断坐标(X,Y)在第I个方向上是否可行}

Var NewX,NewY:shortint;

Begin

     Ok:=True;
     
     Newx:=x+FangXiang[i,1];
     
     Newy:=y+FangXiang[i,2];
     
     If not((NewX in [1..8]) and (NewY in [1..8])) then Ok:=False;  {超界?}
     
     
     If Road[NewX,NewY]=3 then ok:=false;	{是否已走过的路?}
     
     If Road[NewX,NewY]=1 then ok:=false;	{是否墙?}
     
End;

Procedure Howgo(x,y:integer);

Var i,NewX,NewY:integer;

Begin

     For i:=1 to 4 do Begin		 {每一步均有4个方向可选择}
     
	 If Ok(x,y,i) then Begin	 {判断某一方向是否可前进}
   
	    Newx:=x+FangXiang[i,1];	 {前进,产生新的坐标}
      
	    Newy:=y+FangXiang[i,2];
      
	    Road[Newx,Newy]:=3; 	 {来到新位置后,设置已走过标志}
      
	    If (NewX=WayOut[1]) and(NewY=WayOut[2]) Then Output
      
			Else Howgo(Newx,NewY); {如到出口则输出,否则下一步递归}
      
	    Road[Newx,Newy]:=2; 	 {堵死某一方向,不让再走,以免打转}
      
	 end;
   
     end;
     
End;

Begin

     total:=0;
     
     Road[wayin[1],wayin[2]]:=3;		{入口坐标设置已走标志}
     
     Howgo(wayin[1],wayin[2]);			{从入口处开始搜索}
     
     writeln('Total is ',total);                {统计总数}
     
end.
