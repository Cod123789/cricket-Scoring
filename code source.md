#include <iostream>
#include <string>
#include <fstream>
using namespace std;

string teamName(int);
string playerName(int);
int toss(int&);
int activePlayers(int&,string[],string[],int&);
int innings1(int[],int[],int[],int[],string[],string[],int[],int[],int[],float[],int[],int[],int[],int[]);
int innings2(int,int[],int[],int[],int[],string[],string[],int[],int[],int[],float[],int[],int[],int[],int[]);
void scoreCard(string[],string[],int[],int[],int[],int[],int[],int[],int[],float[],int[]);
void strikeRotate(int[],int[],string[],int[],int[]);
void outHow(int[],int);
void fileHandling(string[],string[],int[],int[],int[],int[],int[],int[],int[], int[],float[],float[],int,int,float,float,int,int);

int playerSize=11,striker,non_striker,bowler,totalOvers,runOut,totalScore1=0,totalScore2=0;
int fallOfWickets1=0,fallOfWickets2=0,extra=0,extra2=0,targetScored,targetAchieved;
float overs=0.0;
float overs2=0.0;
string team[2];
int wtoss,tcheck,cont,stupid=0;


int main()
{
    
    int *batsman1Runs=new int[playerSize];
    int *batsman2Runs=new int[playerSize];
    int *batsman1Balls=new int[playerSize];
    int *batsman2Balls=new int[playerSize];
    int *bowler1Runs=new int[playerSize];
    int *bowler2Runs=new int[playerSize];
   	int *bowler1Wickets=new int[playerSize];
	int *bowler2Wickets=new int[playerSize];
	float *bowler1Overs=new float[playerSize];
	float *bowler2Overs=new float[playerSize];
	int *wicket1Manner=new int[playerSize];
	int *wicket2Manner=new int[playerSize];
	int *remainingBatsman=new int[playerSize];
	int *activeBowler=new int[playerSize];
	int *four1=new int[playerSize];
	int *four2=new int[playerSize];
	int *six1=new int[playerSize];
	int *six2=new int[playerSize];
	int *maiden1=new int[playerSize];
	int *maiden2=new int[playerSize];
	int *temp=new int[playerSize];
	
	                                                                  
	string team1Player[playerSize],team2Player[playerSize];
	
	cout<<endl <<"\t\t\tCricket Scroing System";
	cout<<endl <<"\t\t\t______________________\n\n";
	
	for(int i=0;i<2;i++)
	team[i]=teamName(i);
	
	for(int i=0;i<2;i++)
	cout<<"\t\t\tTeam " <<i+1 <<" : " <<team[i] ;
	
	do
	{
      cout<<endl <<"\n\t\t\tEnter Total Number Of Players: ";
	  cin>>playerSize;
	} while(playerSize<2||playerSize>11);
	system("cls");
	
	cin.ignore(1000,'\n');
	
	cout<<"\n\n\t\t\t\tTeam " <<team[0] <<endl;
	for(int i=0;i<playerSize;i++)
	team1Player[i]=playerName(i);
	
	cout<<"\n\n\t\t\t\tTeam " <<team[1] <<endl;
	for(int i=0;i<playerSize;i++)
	team2Player[i]=playerName(i);
	
	system("cls");
	cout<<"\n\n\t\t\t\tTeam " <<team[0] <<"\t\t\tTeam " <<team[1];
	cout<<endl;
	
	for(int i=0;i<playerSize;i++)
	cout<<"\t\t\t\t" <<team1Player[i] <<"\t\t\t\t" <<team2Player[i] <<endl;
	
	cout<<endl <<"Number Overs To Be Played: ";
	cin>>totalOvers;
	
	wtoss=toss(tcheck);
	
	non_striker=activePlayers(striker,team1Player,team2Player,bowler);
	
	
  
    
	
	
	if((wtoss==1&&tcheck==1)||(wtoss==2&&tcheck==2))
	{
	      targetScored=innings1(batsman1Runs,batsman1Balls,bowler2Runs,wicket1Manner,team1Player,team2Player,bowler2Wickets,remainingBatsman,activeBowler,bowler2Overs,four1,six1,maiden2,temp);
	      scoreCard(team1Player,team2Player,batsman1Runs,batsman1Balls,four1,six1,wicket1Manner,bowler2Runs,bowler2Wickets,bowler2Overs,maiden2);
	      do{
		  cout<<endl <<"\n\t\tPress 1 To Start The Next Innings: ";
	      cin>>cont;}while(cont!=1);
		  targetAchieved=innings2(targetScored,batsman2Runs,batsman2Balls,bowler1Runs,wicket2Manner,team2Player,team1Player,bowler1Wickets,remainingBatsman,activeBowler,bowler1Overs,four2,six2,maiden1,temp);
          scoreCard(team2Player,team1Player,batsman2Runs,batsman2Balls,four2,six2,wicket2Manner,bowler1Runs,bowler1Wickets,bowler1Overs,maiden1);
		  
		  if(targetAchieved>targetScored)
	      cout<<endl <<" \a\n\t\t\t" <<team[1] <<" Has Won The Match By " <<playerSize-fallOfWickets2 <<" wickets.";
		  
		  else if(targetAchieved==targetScored)
		  cout<<endl <<"\a\n\t\t\t Match Has Been Drawn.";
		  
		  else 
		  cout<<endl <<" \a\n\t\t\t" <<team[0] <<" Has Won The Match By " <<targetScored-targetAchieved <<" runs.";    
		  
		  int x=1, y=0;
		  
		  fileHandling(team1Player,team2Player,batsman1Runs,batsman2Runs,batsman1Balls,batsman2Balls,bowler2Wickets,bowler1Wickets,bowler2Runs,bowler1Runs,bowler2Overs,bowler1Overs,x,y,overs,overs2,fallOfWickets1,fallOfWickets2);
	      
	}
	else
	{
	      targetScored=innings1(batsman2Runs,batsman2Balls,bowler1Runs,wicket2Manner,team2Player,team1Player,bowler1Wickets,remainingBatsman,activeBowler,bowler1Overs,four2,six2,maiden1,temp);
	      scoreCard(team2Player,team1Player,batsman2Runs,batsman2Balls,four2,six2,wicket2Manner,bowler1Runs,bowler1Wickets,bowler1Overs,maiden1);
		  do{
		  cout<<endl <<"\n\t\tPress 1 To Start The Next Innings: ";
	      cin>>cont;}while(cont!=1);
		  targetAchieved=innings2(targetScored,batsman1Runs,batsman1Balls,bowler2Runs,wicket1Manner,team1Player,team2Player,bowler2Wickets,remainingBatsman,activeBowler,bowler2Overs,four1,six1,maiden2,temp); 
          scoreCard(team1Player,team2Player,batsman1Runs,batsman1Balls,four1,six1,wicket1Manner,bowler2Runs,bowler2Wickets,bowler2Overs,maiden2);
		  
		  if(targetAchieved>targetScored)
	      cout<<endl <<" \a\n\t\t\t" <<team[0] <<" Has Won The Match By " <<playerSize-fallOfWickets1 <<" wickets.";
		  
		  else if(targetAchieved==targetScored)
		  cout<<endl <<"\a\n\t\t\t Match Has Been Drawn.";
		  
		  else 
		  cout<<endl <<" \a\n\t\t\t" <<team[1] <<" Has Won The Match By " <<targetScored-targetAchieved <<" runs.";
		  
		  int x=1, y=0;
		  
		  fileHandling(team2Player,team1Player,batsman2Runs,batsman1Runs,batsman2Balls,batsman1Balls,bowler1Wickets,bowler2Wickets,bowler1Runs,bowler2Runs,bowler1Overs,bowler2Overs,x,y,overs2,overs,fallOfWickets2,fallOfWickets1);
	}
	
	
	

	
	
	
	
	
	return 0;
	
	
}

string teamName(int i)
{
		string name;
	
	cout<<"Enter Name Of Team " <<i+1 <<" :";
	getline(cin,name);
	cout<<endl;
	
	return name;
}

string playerName(int i)
{
	string playerName;
	cout<<endl <<"\nEnter Name Of Player " <<i+1 <<" : ";
    getline(cin,playerName);

	return playerName;
}

int toss(int &tcheck)
{
	int i=0;
	int teamcheck;
	
	while(tcheck!=1&&tcheck!=2)
	{
	   cout<<endl <<"TOSS Won By (Press '1' For " <<team[0] <<" Press '2' For " <<team[1] <<"): ";
	   cin>>tcheck;
	   i++;
    }
	
	if(tcheck==1)
	{
	    cout<<endl <<"\n\t\t" <<team[0] <<" Has Won The Toss!";
  
     	while(teamcheck!=1&&teamcheck!=2)
     	{
	       cout<<endl <<"Press '1' To Bat or Press '2' to Bowl: ";
	       cin>>teamcheck;
	       i++;
                       }
        system("cls");
       	if(teamcheck==1)
    	cout<<endl <<"\t\t" <<team[0] <<" Has Elected To Bat First.\n";
	
	    else 
	    cout<<endl <<"\t\t" <<team[0] <<" Has Elected To Bowl First.\n";
        }

	else 
    {
	    cout<<endl <<"\n\t\t" <<team[1] <<" Has Won The Toss!\n";
	    
	    while(teamcheck!=1&&teamcheck!=2)
     	{
	       cout<<endl <<"Press '1' To Bat or Press '2' to Bowl: ";
	       cin>>teamcheck;
	       i++;
                       }
        system("cls");
       	if(teamcheck==1)
    	cout<<endl <<"\t\t" <<team[1] <<" Has Elected To Bat First.\n";
	
	    else 
	    cout<<endl <<"\t\t" <<team[1] <<" Has Elected To Bowl First.\n";
        }

	return teamcheck;
	
}

int activePlayers(int &striker,string team1Player[],string team2Player[],int &bowler)
{
	int nStriker;
	
	if((tcheck==1&&wtoss==1)||(tcheck==2&&wtoss==2))
	{
        do
        {
		cout<<endl;
		cout<<"\n\t\t\t" <<team[0] <<endl <<endl;
		for(int i=0;i<playerSize;i++)
		cout<<"\t\t" <<i+1 <<".) " <<team1Player[i] <<endl;
		cout<<endl <<"Team " <<team[0] <<" Enter No. Of The Batsman On Strike: ";
		cin>>striker;
		}while(striker<=0||striker>playerSize);
		
		do
		{
		cout<<"Enter No. Of Non-Striker: ";
		cin>>nStriker;
	    }while(nStriker<=0||nStriker>playerSize);
		
		do
		{
		cout<<endl;
		cout<<"\n\t\t\t" <<team[1] <<endl <<endl;
		for(int i=0;i<playerSize;i++)
		cout<<"\t\t" <<i+1 <<".) " <<team2Player[i] <<endl;
		cout<<endl <<"Team " <<team[1] <<" Enter No. Of The Bowler: ";
		cin>>bowler;
	    }while(bowler<=0||bowler>playerSize);
		return nStriker;
	}
	
	else
	{
		do
		{
		cout<<endl;
		cout<<"\n\t\t\t" <<team[1] <<endl <<endl;
		for(int i=0;i<playerSize;i++)
		cout<<"\t\t" <<i+1 <<".) " <<team2Player[i] <<endl;
		cout<<endl <<"Team " <<team[1] <<" Enter No. Of The Batsman On Strike: ";
		cin>>striker;}while(striker<=0||striker>playerSize);
		
		do
		{
		cout<<"Enter No. Of Non-Striker: ";
		cin>>nStriker;
	    }while(nStriker<=0||nStriker>playerSize);
		
		do
		{
		cout<<endl;
		cout<<"\n\t\t\t" <<team[0] <<endl <<endl;
		for(int i=0;i<playerSize;i++)
		cout<<"\t\t" <<i+1 <<".) " <<team1Player[i] <<endl;
		cout<<endl <<"Team " <<team[0] <<" Enter No. Of The Bowler: ";
		cin>>bowler;}while(bowler<=0||bowler>playerSize);

		return nStriker;
	}
	
	
}

int innings1(int batsmanxRuns[],int batsmanxBalls[],int bowleryRuns[],int wicketxManner[],string teamxPlayer[],string teamyPlayer[],int bowleryWickets[],int remainingBatsman[],int activeBowler[],float bowleryOvers[],int fourx[],int sixx[],int maideny[],int temp[])
{
	int x,y,ballRun,remBatsmanSize;
	remBatsmanSize=playerSize;
	
    if((wtoss==1&&tcheck==1)||(wtoss==2&&tcheck==2))  //could be avoided
    { 
	     x=0;
	     y=1;
    }
    
    else 
    {
    	x=1;
    	y=0;
	}
	
	for(int i=0;i<playerSize;i++)
	{
	   batsmanxRuns[i]=0;
	   batsmanxBalls[i]=0;
	   bowleryWickets[i]=0;
	   bowleryRuns[i]=0;
	   wicketxManner[i]=0;
	   remainingBatsman[i]=0;
	   activeBowler[i]=0;
	   bowleryOvers[i]=0.0;
	   fourx[i]=0;
	   sixx[i]=0;
	   maideny[i]=0;
	   temp[i]=0;
    }


	int a=0;
	while(a<totalOvers)
	{
	   activeBowler[bowler]=0;
	   
	   for(int j=0;j<6;j++)
	{
		      system("cls");	
	cout<<endl <<endl <<team[x] <<" " <<totalScore1 <<"-" <<fallOfWickets1 <<"\t\t\tOvers " <<overs <<"(" <<totalOvers <<")" <<"RR: " <<totalScore1/overs  <<"\t\t\tExtras: " <<extra;
	cout<<endl <<endl <<"Batsman \t\t\t\t\t Bowler";
	cout<<endl <<teamxPlayer[striker-1]  <<"* " <<batsmanxRuns[striker-1] <<"(" <<batsmanxBalls[striker-1] <<")";
	cout<<"\t\t\t\t\t\t" <<teamyPlayer[bowler-1] << " " <<bowleryWickets[bowler-1] <<"-" <<bowleryRuns[bowler-1] <<"(" <<bowleryOvers[bowler-1] <<")";
 	cout<<endl <<teamxPlayer[non_striker-1] <<"  " <<batsmanxRuns[non_striker-1] <<"(" <<batsmanxBalls[non_striker-1] <<")";
 	 
 	
 	remainingBatsman[non_striker-1]=1;
	remainingBatsman[striker-1]=1;
	 
    do
    {
	cout<<endl <<endl <<"\t\tWhat Happened On The Current Delivery";
	cout<<"\n\t\tPress The Corresponding Digit For Runs";
	cout<<"\n\t\tPress 7 For Leg-Byes";
	cout<<"\n\t\tPress 8 For Wide Or No Ball";
	cout<<"\n\t\tPress 9 For Dissmisal";
	cout<<"\n\t\tPress 10 For Byes";
	cout<<"\n\t\tPress 11 To Declare Innings";
	cout<<"\n\t\tEnter: ";
	cin>>ballRun;}while(ballRun<0||ballRun>11);
	
	batsmanxBalls[striker-1]++;
	
	if(ballRun<=6)
	{
	
	  batsmanxRuns[striker-1]=batsmanxRuns[striker-1]+ballRun;
	  bowleryRuns[bowler-1]=bowleryRuns[bowler-1]+ballRun;
      totalScore1=totalScore1+ballRun;
    
      if(ballRun%2!=0)
	  strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	  
	  if(ballRun==4)
	  fourx[striker-1]++;
	  
	  if(ballRun==6)
	  sixx[striker-1]++;
	  
	} 
    
	else if(ballRun==7||ballRun==10) //leg-byes
	{
		cout<<"\n\t\tHow Many Runs Were Scored: ";
		cin>>ballRun;
		totalScore1=totalScore1+ballRun;
		extra=extra+ballRun;
		
		if(ballRun%2!=0)
	    strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	}
	
	else if(ballRun==8)
	{
		cout<<"\n\t\tHow Many Extra Runs Were Scored: ";
		cin>>ballRun;
		batsmanxBalls[striker-1]--;
		bowleryOvers[bowler-1]=bowleryOvers[bowler-1]-0.1;
		totalScore1=totalScore1+ballRun+1;
		bowleryRuns[bowler-1]=bowleryRuns[bowler-1]+ballRun+1;
		extra=extra+ballRun+1;
		overs=overs-0.1;
		j--;
		if(ballRun%2!=0)
	    strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	    
		if(ballRun==4)
	    fourx[striker-1]++;
	  
	    else if(ballRun==6)
	    sixx[striker-1]++;
	}

	else if(ballRun==9) //wicket
    {
    	do
    	{
		cout<<"\n\t\tMeans Of Dissmisal";
    	cout<<"\n\t\tPress 1 for Bowled";
    	cout<<"\n\t\tPress 2 for Caught ";
	    cout<<"\n\t\tPress 3 for Run Out";
	    cout<<"\n\t\tPress 4 for Retired Hurt";
	    cout<<"\n\t\tPress 5 for LBW";
	    cout<<"\n\t\tPress 6 for Stumped";
	    cout<<"\n\t\tEnter: ";
	    cin>>wicketxManner[striker-1];}while(wicketxManner[striker-1]<1||wicketxManner[striker-1]>6);
	    
	    remBatsmanSize--;
	    fallOfWickets1++;
	    
		if(remBatsmanSize<=1)
		{
        system("cls");		
		cout<<endl<<"\n" <<team[x] <<" " <<totalScore1 <<"-" <<fallOfWickets1 <<" (All Out)" <<"\t\t\tOvers " <<overs <<"(" <<totalOvers <<")" <<"RR: " <<totalScore1/overs <<"\t\t\tExtras: " <<extra;
		cout<<"\n\n\t\tTarget To Win: " <<totalScore1+1;
		cout<<"\n\t\tEnd Of Innings.";
		return totalScore1;
		}
		
	    
	    if(wicketxManner[striker-1]==1||wicketxManner[striker-1]==5||wicketxManner[striker-1]==6)
	    {
	    	bowleryWickets[bowler-1]++;
	    	
	    	do
	    	{
			cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
	    	for(int i=0;i<playerSize;i++)
	    	{
	    		if(remainingBatsman[i]==0)
			    cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
			}
			
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;}while(striker<=0||striker>playerSize);
	    }
	    
	    if(wicketxManner[striker-1]==4)
	    {
	    	remBatsmanSize++;
	    	fallOfWickets1--;
	    	do
	    	{
			cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
	    	for(int i=0;i<playerSize;i++)
	    	{
	    		if(remainingBatsman[i]==0)
			    cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
			}
			
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;}while(striker<=0||striker>playerSize);
	    	
		}
	    
	    
		if(wicketxManner[striker-1]==3)
	    {
			cout<<"\n\t\tHow Many Runs Were Scored: ";
			cin>>ballRun;
		    batsmanxRuns[striker-1]=batsmanxRuns[striker-1]+ballRun;
	        bowleryRuns[bowler-1]=bowleryRuns[bowler-1]+ballRun;
            totalScore1=totalScore1+ballRun;
			cout<<"\n\t\tWho Was Run Out?";
	    	cout<<"\n\t\tPress 1 for Striker";
	    	cout<<"\n\t\tPress 2 for Non-Striker";
	    	cin>>runOut;
	    	
	    	
	    	
			if(runOut==2)
	    	{
	    		wicketxManner[non_striker-1]=3;
	    		wicketxManner[striker-1]=0;
	    		cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
	    		for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
				   cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
				   cout<<"\n\t\tEnter No. Of New Non-Striker Batsman: ";
	    	       cin>>non_striker;
			}
			else 
			{
				cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
				for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
			        cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
			
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;
			}
	}
		else if(wicketxManner[striker-1]==2)
		{
			bowleryWickets[bowler-1]++;
			int cross;
			cout<<"\n\t\tDid The Batsmen Cross?";
			cout<<"\n\t\tPress 1 for Yes";
	    	cout<<"\n\t\tPress 2 for No";
	    	cout<<"\n\t\tEnter: ";
	    	cin>>cross;
	    	
	    	if(cross==1)
	    	{
	    		striker=striker+non_striker;
	    		non_striker=striker-non_striker;
	    		striker=striker-non_striker;
				
				cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
                for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
					cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
			        cout<<"\n\t\tEnter No. Of New Non-Striker Batsman: ";
			        cin>>non_striker;
		    }
		    
		    else
            {
            	cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
				for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
				    cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;
			}
		}
			
	}
	    else if(ballRun==11)
	    {
	        system("cls");
			cout<<"\n\t\tInnings Have Been Declared!";
	    	cout<<endl<<"\n" <<team[x] <<" " <<totalScore1 <<"-" <<fallOfWickets1 <<"\t\t\tOvers " <<overs <<"(" <<totalOvers <<")" <<"RR: " <<totalScore1/overs <<"\t\t\tExtras: " <<extra;
	     	cout<<"\n\n\t\tTarget To Win: " <<totalScore1+1; 
	    	cout<<"\n\t\tEnd Of Innings.";
	    	batsmanxBalls[striker-1]--;
	    	return totalScore1;
	    	
		}
	            bowleryOvers[bowler-1]=bowleryOvers[bowler-1]+0.1;
				overs=overs+0.1;
	}
	   system("cls");
	    bowleryOvers[bowler-1]=bowleryOvers[bowler-1]+0.4;
	    overs=overs+0.4;
	    
		if(temp[bowler-1]==bowleryRuns[bowler-1])
	    maideny[bowler-1]++;
	    
	    temp[bowler-1]=bowleryRuns[bowler-1];
	    
	cout<<endl <<endl <<team[x] <<" " <<totalScore1 <<"-" <<fallOfWickets1 <<"\t\t\tOvers " <<overs <<"(" <<totalOvers <<")" <<"RR: " <<totalScore1/overs <<"\t\t\tExtras: " <<extra;
	cout<<endl <<endl <<"Batsman \t\t\t\t\t Bowler";
	cout<<endl <<teamxPlayer[striker-1]  <<"* " <<batsmanxRuns[striker-1] <<"(" <<batsmanxBalls[striker-1] <<")";
	cout<<"\t\t\t\t\t\t" <<teamyPlayer[bowler-1] << " " <<bowleryWickets[bowler-1] <<"-" <<bowleryRuns[bowler-1] <<"(" <<bowleryOvers[bowler-1] <<")";
 	cout<<endl <<teamxPlayer[non_striker-1] <<"  " <<batsmanxRuns[non_striker-1] <<"(" <<batsmanxBalls[non_striker-1] <<")";
	
		strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	    
		activeBowler[bowler-1]=1;   
		a++;
		if(a<totalOvers)
		{
		 cout<<endl; 	
		cout<<"\n\t\t\t" <<team[y] <<endl <<endl;
		for(int i=0;i<playerSize;i++)
		{
		     if(activeBowler[i]==0)
	         cout<<"\t\t" <<i+1 <<".) " <<teamyPlayer[i] <<endl;
	    }
		activeBowler[bowler-1]=0;
		cout<<endl <<"Team " <<team[y] <<" Enter No. Of The Bowler: ";
		cin>>bowler;
	}
   
    }
        system("cls");
		cout<<endl<<"\n" <<team[x] <<" " <<totalScore1 <<"-" <<fallOfWickets1 <<"\t\t\tOvers " <<overs <<"(" <<totalOvers <<")" <<"RR: " <<totalScore1/overs <<"\t\t\tExtras: " <<extra;
		cout<<"\n\n\t\tTarget To Win: " <<totalScore1+1; 
		cout<<"\n\t\tEnd Of Innings.";
		return totalScore1;
    }

int innings2(int targetScored,int batsmanxRuns[],int batsmanxBalls[],int bowleryRuns[],int wicketxManner[],string teamxPlayer[],string teamyPlayer[],int bowleryWickets[],int remainingBatsman[],int activeBowler[],float bowleryOvers[],int fourx[],int sixx[],int maideny[],int temp[])
{
	int x,y,ballRun,remBatsmanSize;
	remBatsmanSize=playerSize;
	
    if((wtoss==2&&tcheck==1)||(wtoss==1&&tcheck==2))  //could be avoided
    {
	     x=0;
	     y=1;
    }
    
    else 
    {
    	x=1;
    	y=0;
	}
	
	for(int i=0;i<playerSize;i++)
	{
	   batsmanxRuns[i]=0;
	   batsmanxBalls[i]=0;
	   bowleryWickets[i]=0;
	   bowleryRuns[i]=0;
	   wicketxManner[i]=0;
	   remainingBatsman[i]=0;
	   activeBowler[i]=0;
	   bowleryOvers[i]=0.0;
	   fourx[i]=0;
	   sixx[i]=0;
	   maideny[i]=0;
	   temp[i]=0;
    }
       system("cls");
	    cout<<endl <<"\n\t\t\tStart Of 2nd Innings";
        cout<<endl <<"\t\t\t____________________";
        cout<<endl;
        cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
	    for(int i=0;i<playerSize;i++)   //could be avoided
		cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
		cout<<endl <<"Team " <<team[x] <<" Enter No. Of The Batsman On Strike: ";
		cin>>striker;
		cout<<"Enter No. Of Non-Striker: ";
		cin>>non_striker;
		
		cout<<endl;
		cout<<"\n\t\t\t" <<team[y] <<endl <<endl;
		for(int i=0;i<playerSize;i++)
		cout<<"\t\t" <<i+1 <<".) " <<teamyPlayer[i] <<endl;
		cout<<endl <<"Team " <<team[y] <<" Enter No. Of The Bowler: ";
		cin>>bowler;
    
	int a=0; 
	while(a<totalOvers)
	{
	   activeBowler[bowler]=0;
	   
	   for(int j=0;j<6;j++)
	{
	system("cls");
	cout<<endl <<endl <<team[x] <<" " <<totalScore2 <<"-" <<fallOfWickets2 <<"\t\t\tOvers " <<overs2 <<"(" <<totalOvers <<")" <<"\t\t\tTarget: " <<targetScored <<"\t\tRRR: " <<targetScored/(totalOvers-overs2) <<"\t\t\tExtras: " <<extra2;
	cout<<endl <<endl <<"Batsman \t\t\t\t\t Bowler";
	cout<<endl <<teamxPlayer[striker-1]  <<"* " <<batsmanxRuns[striker-1] <<"(" <<batsmanxBalls[striker-1] <<")";
	cout<<"\t\t\t\t\t\t" <<teamyPlayer[bowler-1] << " " <<bowleryWickets[bowler-1] <<"-" <<bowleryRuns[bowler-1] <<"(" <<bowleryOvers[bowler-1] <<")";
 	cout<<endl <<teamxPlayer[non_striker-1] <<"  " <<batsmanxRuns[non_striker-1] <<"(" <<batsmanxBalls[non_striker-1] <<")";
 	 
 	
 	remainingBatsman[non_striker-1]=1;
	remainingBatsman[striker-1]=1;
	 
	do
	{
	cout<<endl <<endl <<"\t\tWhat Happened On The Current Delivery";
	cout<<"\n\t\tPress The Corresponding Digit For Runs";
	cout<<"\n\t\tPress 7 For Leg-Byes";
	cout<<"\n\t\tPress 8 For Wide Or No Ball";
	cout<<"\n\t\tPress 9 For Dissmisal";
	cout<<"\n\t\tPress 10 For Byes";
	cout<<"\n\t\tPress 11 To Declare Innings";
	cout<<"\n\t\tEnter: ";
	cin>>ballRun;}while(ballRun<0||ballRun>11);
	
	batsmanxBalls[striker-1]++;
	
	if(ballRun<=6)
	{
	
	  batsmanxRuns[striker-1]=batsmanxRuns[striker-1]+ballRun;
	  bowleryRuns[bowler-1]=bowleryRuns[bowler-1]+ballRun;
      totalScore2=totalScore2+ballRun;
    
      if(ballRun%2!=0)
	  strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	  
	  if(ballRun==4)
	  fourx[striker-1]++;
	  
	  else if(ballRun==6)
	  sixx[striker-1]++;
	} 
    
	else if(ballRun==7||ballRun==10) //leg-byes
	{
		cout<<"\n\t\tHow Many Runs Were Scored: ";
		cin>>ballRun;
		totalScore2=totalScore2+ballRun;
		extra2=extra2+ballRun;
		
		if(ballRun%2!=0)
	    strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	}
	
	else if(ballRun==8)
	{
		cout<<"\n\t\tHow Many Extra Runs Were Scored: ";
		cin>>ballRun;
		batsmanxBalls[striker-1]--;
		bowleryOvers[bowler-1]=bowleryOvers[bowler-1]-0.1;
		totalScore2=totalScore2+ballRun+1;
		bowleryRuns[bowler-1]=bowleryRuns[bowler-1]+ballRun+1;
		extra2=extra2+ballRun+1;
		overs2=overs2-0.1;
		j--;
		if(ballRun%2!=0)
	    strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	    
	    if(ballRun==4)
	    fourx[striker-1]++;
	  
	    else if(ballRun==6)
	    sixx[striker-1]++;
	}

	else if(ballRun==9) //wicket
    {
    	cout<<"\n\t\tMeans Of Dissmisal";
    	cout<<"\n\t\tPress 1 for Bowled";
    	cout<<"\n\t\tPress 2 for Caught ";
	    cout<<"\n\t\tPress 3 for Run Out";
	    cout<<"\n\t\tPress 4 for Retired Hurt";
	    cout<<"\n\t\tPress 5 for LBW";
	    cout<<"\n\t\tPress 6 for Stumped";
	    cout<<"\n\t\tEnter: ";
	    cin>>wicketxManner[striker-1];
	    
	    remBatsmanSize--;
	    fallOfWickets2++;
	    
		if(remBatsmanSize<=1)
		{
		system("cls");
		cout<<endl<<"\n" <<team[x] <<" " <<totalScore2 <<"-" <<fallOfWickets2 <<"\t\t\tOvers " <<overs2 <<"(" <<totalOvers <<")" <<"\t\t\tTarget: " <<targetScored  <<"\t\t\tExtras: " <<extra2;
		cout<<"\n\t\tEnd Of Innings.";
		return totalScore2;
		}
		
	    
	    if(wicketxManner[striker-1]==1||wicketxManner[striker-1]==5||wicketxManner[striker-1]==6)
	    {
	    	bowleryWickets[bowler-1]++;
	    	cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
	    	for(int i=0;i<playerSize;i++)
	    	{
	    		if(remainingBatsman[i]==0)
			    cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
			}
			
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;
	    }
	    
	    if(wicketxManner[striker-1]==4)
	    {
	    	remBatsmanSize++;
	    	fallOfWickets2--;
	    	cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
	    	for(int i=0;i<playerSize;i++)
	    	{
	    		if(remainingBatsman[i]==0)
			    cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
			}
			
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;
	    	
		}
	    
	    
		if(wicketxManner[striker-1]==3)
	    {
			cout<<"\n\t\tHow Many Runs Were Scored: ";
			cin>>ballRun;
		    batsmanxRuns[striker-1]=batsmanxRuns[striker-1]+ballRun;
	        bowleryRuns[bowler-1]=bowleryRuns[bowler-1]+ballRun;
            totalScore2=totalScore2+ballRun;
			cout<<"\n\t\tWho Was Run Out?";
	    	cout<<"\n\t\tPress 1 for Striker";
	    	cout<<"\n\t\tPress 2 for Non-Striker";
	    	cin>>runOut;
	    	
	    	
	    	
			if(runOut==2)
	    	{
	    		wicketxManner[non_striker-1]=3;
	    		wicketxManner[striker-1]=0;
	    		cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
	    		for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
				   cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
				   cout<<"\n\t\tEnter No. Of New Non-Striker Batsman: ";
	    	       cin>>non_striker;
			}
			else 
			{
				cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
				for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
			        cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
			
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;
			}
	}
		else if(wicketxManner[striker-1]==2)
		{
			bowleryWickets[bowler-1]++;
			int cross;
			cout<<"\n\t\tDid The Batsmen Cross?";
			cout<<"\n\t\tPress 1 for Yes";
	    	cout<<"\n\t\tPress 2 for No";
	    	cout<<"\n\t\tEnter: ";
	    	cin>>cross;
	    	
	    	if(cross==1)
	    	{
	    		striker=striker+non_striker;
	    		non_striker=striker-non_striker;
	    		striker=striker-non_striker;
				
				cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
                for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
					cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
			        cout<<"\n\t\tEnter No. Of New Non-Striker Batsman: ";
			        cin>>non_striker;
		    }
		    
		    else
            {
				cout<<"\n\t\t\t" <<team[x] <<endl <<endl;
				for(int i=0;i<playerSize;i++)
	    		{
	    			if(remainingBatsman[i]==0)
				    cout<<"\t\t" <<i+1 <<".) " <<teamxPlayer[i] <<endl;
				}
				cout<<"\n\t\tEnter No. Of New On Strike Batsman: ";
				cin>>striker;
			}
		}
			
	}
	    else if(ballRun==11)
	    {
	    	system("cls");
			cout<<"\n\t\tInnings Have Been Declared!";
	    	cout<<endl<<"\n" <<team[x] <<" " <<totalScore2 <<"-" <<fallOfWickets2 <<"\t\t\tOvers " <<overs2 <<"(" <<totalOvers <<")" <<"\t\t\tTarget: " <<targetScored  <<"\t\t\tExtras: " <<extra2;
	     	cout<<"\n\t\tEnd Of Innings.";
	     	batsmanxBalls[striker-1]--;
	     	return totalScore2;
	    	
		}
	            bowleryOvers[bowler-1]=bowleryOvers[bowler-1]+0.1;
				overs2=overs2+0.1;
		if(totalScore2>targetScored)
 	    {  
 	    	system("cls");
 	    	cout<<endl<<"\n" <<team[x] <<" " <<totalScore2 <<"-" <<fallOfWickets2 <<"\t\t\tOvers " <<overs2 <<"(" <<totalOvers <<")" <<"\t\t\tTarget: " <<targetScored  <<"\t\t\tExtras: " <<extra2;
			cout<<"\n\t\tEnd Of Innings!";
 	    	return totalScore2;
		}
	}
	    bowleryOvers[bowler-1]=bowleryOvers[bowler-1]+0.4;
	    overs2=overs2+0.4;
	    
		if(temp[bowler-1]==bowleryRuns[bowler-1])
	    maideny[bowler-1]++;
	    
	    temp[bowler-1]=bowleryRuns[bowler-1];
		
		system("cls");
	cout<<endl <<endl <<team[x] <<" " <<totalScore2 <<"-" <<fallOfWickets2 <<"\t\t\tOvers " <<overs2 <<"(" <<totalOvers <<")" <<"\t\t\tTarget: " <<targetScored <<"\t\tRRR: " <<targetScored/(totalOvers-overs2) <<"\t\t\tExtras: " <<extra2;
	cout<<endl <<endl <<"Batsman \t\t\t\t\t Bowler";
	cout<<endl <<teamxPlayer[striker-1]  <<"* " <<batsmanxRuns[striker-1] <<"(" <<batsmanxBalls[striker-1] <<")";
	cout<<"\t\t\t\t\t\t" <<teamyPlayer[bowler-1] << " " <<bowleryWickets[bowler-1] <<"-" <<bowleryRuns[bowler-1] <<"(" <<bowleryOvers[bowler-1] <<")";
 	cout<<endl <<teamxPlayer[non_striker-1] <<"  " <<batsmanxRuns[non_striker-1] <<"(" <<batsmanxBalls[non_striker-1] <<")";
 	
 	    strikeRotate(batsmanxRuns,batsmanxBalls,teamxPlayer,fourx,sixx);
	    
		activeBowler[bowler-1]=1;   
		a++;
		if(a<totalOvers)
		{
		cout<<endl; 
		cout<<"\n\t\t\t" <<team[y] <<endl <<endl;	
		for(int i=0;i<playerSize;i++)
		{
		     if(activeBowler[i]==0)
	         cout<<"\t\t" <<i+1 <<".) " <<teamyPlayer[i] <<endl;
	    }
		activeBowler[bowler-1]=0;
		cout<<endl <<"Team " <<team[y] <<" Enter No. Of The Bowler: ";
		cin>>bowler;
	    }
   
    }
        system("cls");
	    cout<<endl<<"\n" <<team[x] <<" " <<totalScore2 <<"-" <<fallOfWickets2 <<"\t\t\tOvers " <<overs2 <<"(" <<totalOvers <<")" <<"\t\t\tTarget: " <<targetScored  <<"\t\t\tExtras: " <<extra2;
		cout<<"\n\t\tEnd Of Innings.";
		return totalScore2;
    }

void scoreCard(string teamxPlayer[],string teamyPlayer[],int batsmanxRuns[],int batsmanxBalls[],int fourx[],int sixx[],int wicketxManner[],int bowleryRuns[],int bowleryWickets[],float bowleryOvers[],int maideny[])
{
	int x,y;
	if(stupid==0)
	if((wtoss==1&&tcheck==1)||(wtoss==2&&tcheck==2))  //could be avoided
    { 
	     x=0;
	     y=1;
    }
    
    else 
    {
    	x=1;
    	y=0;
	}
	
	 cout<<endl <<endl <<"\t\t\t\t" <<team[x] <<" Innings" <<endl <<endl;
	 cout<<"\tBatting " <<"\t\t\tRuns\t\tBalls\t\t4s\t\t6s\n\n";
	 
	 for(int i=0;i<playerSize;i++)
	{
	 cout<<"\t" <<teamxPlayer[i] <<"     ";
	 outHow(wicketxManner,i); 
	 cout<<"\t\t\t" <<batsmanxRuns[i] <<"\t\t\t" <<batsmanxBalls[i] <<"\t" <<fourx[i] <<"\t\t" <<sixx[i] <<endl;}
	 
	 cout<<endl <<endl <<"\t\t\t\t" <<team[y] <<" Bowling" <<endl <<endl;
	 cout<<"\tBowling" <<"\t\tOvers\tMaidens\tRuns\tWickets\t\tEconomy\n\n";
	 for(int i=0;i<playerSize;i++)
	 cout<<"\t" <<teamyPlayer[i] <<"\t\t" <<bowleryOvers[i] <<"\t" <<maideny[i] <<"\t" <<bowleryRuns[i] <<"\t" <<bowleryWickets[i] <<"\t\t" <<bowleryRuns[i]/bowleryOvers[i] <<endl;
	 stupid++;
	 
}

void outHow(int wicketxManner[],int i)
{
	if(wicketxManner[i]==0)
	cout<<"Not Out";
	
	else if(wicketxManner[i]==1)
	cout<<"Bowled";
	
	else if(wicketxManner[i]==2)
	cout<<"Caught";
	
	else if(wicketxManner[i]==3)
	cout<<"Run Out";
	
	else if(wicketxManner[i]==4)
	cout<<"Retired Hurt";
	
	else if(wicketxManner[i]==5)
	cout<<"LBW";
	
	else if(wicketxManner[i]==6)
	cout<<"Stumped";
	
	
}

void strikeRotate(int x[],int y[],string z[],int a[],int b[])
{
	x[striker-1]=x[striker-1] + x[non_striker-1];
    x[non_striker-1]=x[striker-1] - x[non_striker-1];
    x[striker-1]=x[striker-1] - x[non_striker-1];
    
    y[striker-1]=y[striker-1] + y[non_striker-1];
    y[non_striker-1]=y[striker-1] - y[non_striker-1];
    y[striker-1]=y[striker-1] - y[non_striker-1];
    
    string temp;
    temp=z[striker-1];
	z[striker-1]=z[non_striker-1];
	z[non_striker-1]=temp; 
	
	a[striker-1]=a[striker-1] + a[non_striker-1];
    a[non_striker-1]=a[striker-1] - a[non_striker-1];
    a[striker-1]=a[striker-1] - a[non_striker-1];
    
    b[striker-1]=b[striker-1] + b[non_striker-1];
    b[non_striker-1]=b[striker-1] - b[non_striker-1];
    b[striker-1]=b[striker-1] - b[non_striker-1];
    
}

void fileHandling(string teamxPlayer[],string teamyPlayer[],int batsmanxRuns[],int batsmanyRuns[],int batsmanxBalls[],int batsmanyBalls[],int bowleryWickets[],int bowlerxWickets[],int bowleryRuns[], int bowlerxRuns[],float bowleryOvers[],float bowlerxOvers[],int x,int y,float oversx,float oversy,int fallOfWicketsx,int fallOfWicketsy)
{
	int topBatsman1Runs,topBatsman1Balls,topBatsman2Runs,topBatsman2Balls,topBowler2Wickets;
	int topBowler2Runs,topBowler1Wickets,topBowler1Runs;
	string topBatsman1Name,topBatsman2Name,topBowler2Name,topBowler1Name;
	float topBowler1overs,topBowler2overs;
	ofstream fout("Match Summary.txt");
	
	fout<<"\n\t\t\t\tMatch Summary";
	fout<<"\n\t\t\t\t_____________\n";
	
	if(tcheck==1)
	{
	   fout<<"\n\t\t\t\tToss Won By " <<team[0];
       if(wtoss==1)
	   fout<<" And Elected To Bat First.";
	   
	   else
	   fout<<" And Elected To Bowl First.";
    }  	
	
	else
	{
       fout<<"\n\t\t\t\tToss Won By " <<team[1];
       
	   if(wtoss==1)
       fout<<" And Elected To Bat First.";
       
	   else
	   fout<<" And Elected To Bowl First.";
    }
     
     
     topBatsman1Runs= batsmanxRuns[0];
     topBowler2Wickets= bowleryWickets[0];
     topBatsman1Balls=batsmanxBalls[0];
 	 topBatsman1Name=teamxPlayer[0];
 	 topBowler2overs=bowleryOvers[0];
     topBowler2Name=teamyPlayer[0];
   	 topBowler2Runs=bowleryRuns[0];
 
            for(int i=1;i<playerSize;i++)
            {
			  if(batsmanxRuns[i]>topBatsman1Runs)
			{
			    
				topBatsman1Runs=batsmanxRuns[i];
				topBatsman1Balls=batsmanxBalls[i];
				topBatsman1Name=teamxPlayer[i];
			}
			
			if(bowleryWickets[i]>topBowler2Wickets)
			{
				topBowler2Wickets=bowleryWickets[i];
				topBowler2overs=bowleryOvers[i];
				topBowler2Name=teamyPlayer[i];
				topBowler2Runs=bowleryRuns[i];
			}
		}
	        topBatsman2Runs=batsmanyRuns[0];
	        topBatsman2Balls=batsmanyBalls[0];
			topBatsman2Name=teamyPlayer[0];
		    topBowler1Wickets=bowlerxWickets[0];
		    topBowler1Runs=bowlerxRuns[0];
			topBowler1overs=bowlerxOvers[0];
			topBowler1Name=teamxPlayer[0];
		    
            for (int i=1;i<playerSize;i++)
            {
			if(batsmanyRuns[i]>topBatsman2Runs)
			{
			
				topBatsman2Runs=batsmanyRuns[i];
				topBatsman2Balls=batsmanyBalls[i];
				topBatsman2Name=teamyPlayer[i];
			}
			
			if(bowlerxWickets[i]>topBowler1Wickets)
			{
				topBowler1Wickets=bowlerxWickets[i];
				topBowler1Runs=bowlerxRuns[i];
				topBowler1overs=bowlerxOvers[i];
				topBowler1Name=teamxPlayer[i];
				}
		}

	fout<<endl <<endl;
    
	fout<<"\t" <<team[x] <<"\t\tOvers: " <<oversx <<"(" <<totalOvers <<")" <<"\t\t" <<targetScored <<"-" <<fallOfWicketsx;
	fout<<"\n\n\tTop Batsman\n\t" <<topBatsman1Name <<"\t" <<topBatsman1Runs <<"(" <<topBatsman1Balls <<")" <<endl <<endl;
	fout<<"\tTop Bowler\n\t"  <<topBowler2Name  <<"\t" <<topBowler2Wickets <<"-" <<topBowler2Runs <<"(" <<topBowler2overs <<")";
	
	fout<<endl <<endl;
    
	fout<<"\n\n\t" <<team[y] <<"\t\tOvers: " <<oversy <<"(" <<totalOvers <<")" <<"\t\t" <<targetAchieved <<"-" <<fallOfWicketsy;
	fout<<"\n\n\tTop Batsman\n\t" <<topBatsman2Name <<"\t" <<topBatsman2Runs <<"(" <<topBatsman2Balls <<")" <<endl <<endl;
	fout<<"\tTop Bowler\n\t"  <<topBowler1Name  <<"\t" <<topBowler1Wickets <<"-" <<topBowler1Runs <<"(" <<topBowler1overs <<")"<<endl <<endl <<"\t\t\t\t";
	
	     
		  if(targetAchieved>targetScored)
	      fout<<endl <<" \n\t\t\t" <<team[x] <<" Has Won The Match By " <<playerSize-fallOfWickets1 <<" wickets.";
		  
		  else if(targetAchieved==targetScored)
		  fout<<endl <<"\a\n\t\t\t Match Has Been Drawn.";
		  
		  else 
		  fout<<endl <<" \a\n\t\t\t" <<team[y] <<" Has Won The Match By " <<targetScored-targetAchieved <<" runs.";
	   
       
}
