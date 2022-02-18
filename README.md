# Kickstart-practice-problem-solving
Code for questions in practice session of Google Kickstart 2022.
//kickstart practice problems;
#include<iostream>
#include<stack>
#include<math.h>
#include<vector>
#include<vector>

using namespace std;

//sample problem
/*void check(stack<char>v,string str,int x)
{
    
    char s = tolower(v.top());
    if(s=='a'||s=='e'||s=='i'||s=='o'||s=='u')
    {
        cout<<"Case #"<<x+1<<": "<<str<<" is ruled by Alice"<<endl;
    }
    else if(s=='y')
    {
        cout<<"Case #"<<x+1<<": "<<str<<" is ruled by nobody"<<endl;
    }
    else
      cout<<"Case #"<<x+1<<": "<<str<<" is ruled by Bob"<<endl;
}
int main()
{
    int t;
    cin>>t;
    
    vector<string>s(t);
    vector<stack<char>> v(t);
    for(int i=0;i<t;i++)
    {
        cin>>s[i];
    }
    
    for(int i=0;i<t;i++)
    {
        int j=0;
      while(j<s[i].size())
         {
            v[i].push(s[i][j]);
            j++;
         }
         
         check(v[i],s[i],i);
         
    }
    
}*/

//centauri

/*int main()
{
    int t;
    cin>>t;
    int n[t];
    int m[t];
    
    int total[t] = {0};
    for(int k=0;k<t;k++)
    {
        cin>>n[k]>>m[k];
        int c[n[k]];
        
        for(int i = 0;i<n[k];i++)
      {
         cin>>c[i];
         total[k] += c[i];
      }
    }
    
    for(int i=0;i<t;i++)
    {
        cout<<"Case #"<<i+1<<": "<<total[i]%m[i]<<endl;
    }
    
    
}*/

//Milk tea

#include<iostream>
#include<unordered_map>
#include<vector>
#include<stack>
#include<queue>
#include<math.h>
#include<string>

using namespace std;
bool sortbysec(const pair<int,int> &a,
              const pair<int,int> &b)
{
    return (a.second < b.second);
}
string change(string s,int index)
{
    
        if(s[index]=='0')
        {
            s[index]='1';
        }
        else
         {
             s[index]='0';
         }
         
    return s;
}
bool pass(vector<string>v,string s)
{
  for(int i=0;i<v.size();i++)
  {
      if(v[i]==s)
      {
          return false;
      }
  }
  return true;
}
string buildorder(vector<pair<int,int>>mp,vector<string>na)
{
    string str;
    vector<pair<int ,int>>v(mp.size());
    for(int i=0;i<mp.size();i++)
    {
        v[i].first = i;
        v[i].second = max(mp[i].first,mp[i].second)-min(mp[i].first,mp[i].second);
        if(mp[i].first>mp[i].second)
        {
            str = str + '0';
        }
        else{
            str = str + '1';
        }
    }
    sort(v.begin(), v.end(), sortbysec);
    int n = 0;
    
    if(pass(na,str))
    {
        return str;
    }
    
    while(!pass(na,str))
    {
        str = change(str,v[n].first);
        n++;
    }
    return str;

}
vector<int>count0(vector<string> s)
{
    int count[s.size()] = 0;
    
    for(int k=0;k<s[0].size();k++)
    {
       for(int i=0;i<s.size();i++)
      {
           if(s[i][k]=='0')
           {
               count[k]++;
           }
      } 
    }
    
    return count;
}
vector<int> count1(vector<string> s)
{
    int count[s.size()] = 0;
    
    for(int k=0;k<s[0].size();k++)
    {
       for(int i=0;i<s.size();i++)
      {
           if(s[i][k]=='1')
           {
               count[k]++;
           }
      } 
    }
    
    return count;
}

int findcomplaints(vector<string>v,string s)
{
    int count = 0;
    for(int i=0;i<v.size();i++)
    {
        for(int j=0;j<s.size();j++)
        {
            if(v[i][j]!=s[j])
            {
                count++;
            }
            else
             continue;
        }
    }
    return count;
}

int main()
{
    int t;
    int n;
    int m;
    int ans[t];
    
    cin>>t;
    cin>>n>>m;
    for(int i=0;i<t;i++)
    {
        vector<string> fr[n];
        vector<string> na[m];
        for(int x=0;x<n;x++)
        {
            cin>>fr[x];
        }
    
        for(int j=0;j<m;j++)
        {
            cin>>na[j];
        }
        
       vector<int> c0[fr[0].size()] = count0(fr);
       vector<int> c1[fr[0].size()] = count1(fr);
       vector<pair<int,int>>mp(fr[0].size());
       
       for(int i=0;i<fr[0].size();i++)
       {
           mp[i].first = c0[i];
           mp[i].second= c1[i];
       }
        
       string s = buildorder(mp,na);
       ans[i] = findcomplaints(fr,s);
    }
       
       for(int i=0;i<t;i++)
       {
            cout<<"Case #"<<i+1<<": "<<ans[i]<<endl;
       }

}
