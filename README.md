# dijstraAlgorithm
dijkstra by using priority queue
vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
       //using priority queue
      priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>>pq;
      vector<int>dist(V);
      for(int i=0;i<V;i++)
      {
          dist[i]=1e9;
      }
      dist[S]=0;
      pq.push({0,S});
      while(!pq.empty())
      {
          int dis=pq.top().first;
          int node=pq.top().second;
          pq.pop();
          for(auto it:adj[node])
          {
              int edgeW=it[1];
              int adjNode=it[0];
              if(edgeW+dis<dist[adjNode])
              {
                  dist[adjNode]=dis+edgeW;
                  pq.push({dist[adjNode],adjNode});
              }
          }
      }
      return dist;
      }
      dijkstra by using set
      set<pair<int,int>>st;
    vector<int>dist(V,1e9);
    st.insert({0,S});
    dist[S]=0;
    while(!st.empty())
    {
        auto it=*(st.begin());
        int node=it.second;
        int dis=it.first;
        st.erase(it);
        for(auto it:adj[node])
        {
            int adjNode=it[0];
            int adjW=it[1];
            if(dis+adjW<dist[adjNode])
            {
                if(dist[adjNode]!=1e9)
                {
                    st.erase({dist[adjNode],adjNode});
                    dist[adjNode]=dis+adjW;
                    st.insert({dist[adjNode],adjNode});
                }
            }
        }
    }
    return dist;
    }
