#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<int> findMissingAndRepeatedValues(vector<vector<int>>& grid) {
        map<int, int> mp;
        int n = grid.size();  

        for (auto& row : grid) {
            for (auto& num : row) {
                mp[num]++;
            }
        }

        int repeated = -1, missing = -1;
        
        // Find the repeated value
        for (auto [num, freq] : mp) {
            if (freq == 2) {
                repeated = num;
                break;
            }
        }

        // Find the missing value
        for (int i = 1; i <= n * n; i++) {
            if (mp.find(i) == mp.end()) {
                missing = i;
                break;
            }
        }

        return {repeated, missing};
    }
};

int main() {
    int n;
    cout << "Enter grid size (n): ";
    cin >> n;

    vector<vector<int>> grid(n, vector<int>(n));
    cout << "Enter the " << n * n << " elements of the grid:\n";

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }

    Solution sol;
    vector<int> result = sol.findMissingAndRepeatedValues(grid);
    
    cout << "Repeated: " << result[0] << ", Missing: " << result[1] << endl;
    return 0;
}
