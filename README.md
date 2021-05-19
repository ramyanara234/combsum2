# combsum2
class Solution {
  set<vector<int> > vec_set;

public:
  void dfs(vector<int>& candidates, vector<int> path, int start, int target) {
    if(target == 0){
      vec_set.insert(path);
      return;
    }
    for(int k=start; k<candidates.size(); k++) {
      int cur = candidates[k];
      if(cur > target) break;

      int remain = target - cur;
      path.push_back(cur);
      // Note: k+1 is to increment the index in next loop
      dfs(candidates, path, k+1, remain); 
      path.pop_back();
    }
  }

  vector<vector<int> > combinationSum2(vector<int>& candidates, int target) {
    sort(candidates.begin(), candidates.end());
    vector<int> path;
    vector<vector<int> > ans;
    dfs(candidates, path, 0, target);
    for(set<vector<int> >::iterator it = vec_set.begin(); it != vec_set.end(); ++it)
      ans.push_back(*it);

    return ans;
  }
