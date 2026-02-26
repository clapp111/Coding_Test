
## N-Queen (Lv.2)

https://school.programmers.co.kr/learn/courses/30/lessons/12952

### 기록

1. **Back Tracking의 대표 문제**
    
    2~3일간 Back Tracking 문제를 많이 풀게 되었다. 
    
    이 알고리즘의 대표 문제인 N-Queen이 생각나서 풀어보았다. 
    
    예전에 백준에서 풀어본 만큼 빨리 해결할 수 있었다.
    
2. **검사 조건**
    
    퀸이 배치 가능한지 확인하기 위해 같은 열 위, 왼쪽 대각선 위, 오른쪽 대각선 위를 확인해야 한다.
    
    아래쪽으로는 어차피 다 false기 때문에 검사하지 않는다.
    
    검사가 통과하면 해당 위치에 퀸을 배치하고 다음 level로 넘어간다. 만약 검사에서 걸린다면 해당 가지의 탐색을 종료하므로 런타임을 줄일 수 있따.
    

### 제출 코드

```cpp
#include <string>
#include <vector>

using namespace std;

bool checkQueen(const vector<vector<bool>>& board, int x, int y){
    int n = board.size();
    for(int i = x-1; i >= 0; i--){
        if(board[i][y]) return false;
    }
    for(int i = x-1, j = y-1; i >= 0 && j >= 0; i--, j--){
        if(board[i][j]) return false;
    }
    for(int i = x-1, j = y+1; i >= 0 && j < n; i--, j++){
        if(board[i][j]) return false;
    }
    return true;
}

void placeQueens(vector<vector<bool>>& board, int level, int &answer) {
    int n = board.size();
    if (level == n){
        answer++;
        return;
    }
    for(int i = 0; i < n; i++){
        board[level][i] = true;
        if(checkQueen(board, level, i)) placeQueens(board, level+1, answer);
        board[level][i] = false;
    }
}

int solution(int n) {
    int answer = 0;
    vector<vector<bool>> board = vector<vector<bool>>(n, vector<bool>(n, false));
    placeQueens(board, 0, answer);
    return answer;
}
```