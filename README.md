public List<List<String>> solveNQueens(int n) {
    List<List<String>> result = new ArrayList<>();
    char[][] board = new char[n][n];
    for (char[] row : board) Arrays.fill(row, '.');
    backtrack(0, board, result);
    return result;
}

private void backtrack(int row, char[][] board, List<List<String>> result) {
    if (row == board.length) {
        result.add(construct(board));
        return;
    }
    for (int col = 0; col < board.length; col++) {
        if (isValid(board, row, col)) {
            board[row][col] = 'Q';
            backtrack(row + 1, board, result);
            board[row][col] = '.';
        }
    }
}

private boolean isValid(char[][] board, int row, int col) {
    for (int i = 0; i < row; i++)
        if (board[i][col] == 'Q' || (col - (row - i) >= 0 && board[i][col - (row - i)] == 'Q') || 
            (col + (row - i) < board.length && board[i][col + (row - i)] == 'Q')) return false;
    return true;
}

private List<String> construct(char[][] board) {
    List<String> result = new ArrayList<>();
    for (char[] row : board) result.add(new String(row));
    return result;
}
