# miniproject
small project in c

#include<stdio.h>

struct tosort
{
    int bt;
    int p;
    int pr;
};
int partition(struct tosort ob[],int low,int high)
{
int p=ob[low].pr;
int i=low+1;
int j=high;
struct tosort temp;
while(low<high)
{
  while(ob[i].pr < p && i<high)
  i++;
  while(ob[j].pr > p && j>low)
  j--;
  if(i<j)
  {
    temp=ob[i];
    ob[i]=ob[j];
    ob[j]=temp;
  }
  else
  {
    temp=ob[low];
    ob[low]=ob[j];
    ob[j]=temp;
    return j;
  }
}
return j;
}
void qsort(struct tosort ob[],int low,int high)
{
if(low<high)
{
  int s=partition(ob,low,high);
  qsort(ob,low,s-1);
  qsort(ob,s+1,high);
}
}

int main()
{
    int wt[20],tat[20],i,j,n,total=0,pos,temp,avg_wt,avg_tat;
    struct tosort ob[20];
    printf("Enter Total Number of Process:");
    scanf("%d",&n);
    printf("\nEnter Burst Time and Priority\n");
    for(i=0;i<n;i++)
    {
        printf("\nP[%d]\n",i+1);
        printf("Burst Time:");
        scanf("%d",&ob[i].bt);
        printf("Priority:");
        scanf("%d",&ob[i].pr);
        ob[i].p=i+1;
    }
    qsort(ob,0,n-1);

    wt[0]=0;
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
            wt[i]+=ob[j].bt;

        total+=wt[i];
    }
    avg_wt=total/n;

