#include<bits/stdc++.h>

using namespace std;

struct Process
{
    int id,art,bt,ct,wt,tat,rem_time;
};

bool cmp(Process a ,Process b)
{
    return (a.art < b.art);
}
bool cmp2(Process a,Process b)
{
    return (a.rem_time > b.rem_time );
}
int main()
{
    int n;
    cout<<"Enter no of Process\n";
    cin>>n;
    vector<Process> ranjan;
    for(int i=1;i<=n;i++)
    {
        int x,y;
        cout<<"Enter arrival time of "<<i<<" Process\n";
        cin>>x;
        cout<<"Enter burst time of "<<i<<" Process\n";
        cin>>y;
        Process code;
        code.art=x;
        code.bt=y;
        code.id=i;
        code.tat=0;
        code.wt=0;
        code.rem_time=code.bt;
        ranjan.push_back(code);
    }
    sort(ranjan.begin(),ranjan.end(),cmp);
    int t=0;
    for(int j=6;j<=10;j+=4)
    {


        for(int i=0;i<ranjan.size();i++)
        {
            if(ranjan[i].art > t)
            continue;
            if(ranjan[i].rem_time > j)
            {
                t+=j;
                ranjan[i].rem_time=ranjan[i].rem_time-j;
            }
            else
            {
                t+=ranjan[i].rem_time;
                ranjan[i].wt=t-ranjan[i].bt;
                ranjan[i].rem_time=0;
            }
        }
    }
    sort(ranjan.begin(),ranjan.end(),cmp2);
    vector<Process> amit;
    cout<<"T is "<<t<<endl;
    int i;
    for( auto i:ranjan)
    {
        i.ct=t+i.rem_time;
        cout<<"i.ct is "<<i.ct<<endl;
        i.tat=i.ct-i.art;
        i.wt=i.tat-i.bt;
        t=i.ct;
        amit.push_back(i);
    }
    cout<<"ID "<<" AT "<<" BT "<<" CT "<<" TAT "<<" WT "<<endl;
    for(int i=0;i<amit.size();i++)
    {
        cout<< amit[i].id<<"  "<< amit[i].art<<"  "<< amit[i].bt<<"  "<< amit[i].ct<<"  "<< amit[i].tat<<"  "<< amit[i].wt<<endl;
    }
    cout<<"Average waiting time : "<<((amit[i].wt)/n);

}
