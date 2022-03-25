def queen_promoted(matrix, row):
    if row == 0 or row == len(matrix) - 1:
        return True
    else:
        return False

def is_inside(matrix, row, col):
    if 0 <= row < len(matrix) and 0 <= col < len(matrix):
        return True
    return False

def white_can_capture(matrix, white_row, white_col):
    if is_inside(matrix, white_row-1, white_col-1):
        if matrix[white_row-1][white_col-1] == "b":
            return "Left"
    if is_inside(matrix, white_row-1, white_col+1):
        if matrix[white_row-1][white_col+1] == "b":
            return "Right"
    return False

def square_calculator(row, col):
    cols = ["a","b","c","d","e","f","g","h"]
    rows = [8, 7, 6,5,4,3,2,1]
    return f"{cols[col]}{rows[row]}"



def black_can_capture(matrix, black_row, black_col):
    if is_inside(matrix, black_row+1, black_col-1):
        if matrix[black_row+1][black_col-1] == "w":
            return "Left"
    if is_inside(matrix, black_row+1, black_col+1):
        if matrix[black_row+1][black_col+1] == "w":
            return "Right"
    return False


matrix = []
white_row = None
white_col = None
black_row = None
black_col = None
for row in range(0, 8):
    columns = input().split()
    matrix.append(columns)
    for col in range(len(columns)):
        if columns[col] == "w":
            white_row = row
            white_col = col
        elif columns[col] == "b":
            black_row = row
            black_col = col

while True:

    if white_can_capture(matrix, white_row, white_col) == "Left":
        matrix[white_row-1][white_col-1] = "w"
        matrix[white_row][white_col] = "-"
        print(f"Game over! White win, capture on {square_calculator(white_row-1, white_col-1)}.")
        break

    elif white_can_capture(matrix, white_row, white_col) == "Right":
        matrix[white_row-1][white_col+1] = "w"
        matrix[white_row][white_col] = "-"
        print(f"Game over! White win, capture on {square_calculator(white_row-1, white_col+1)}.")
        break

    else:
        white_row -= 1
        matrix[white_row+1][white_col] = "-"
        matrix[white_row][white_col] = "w"
        if queen_promoted(matrix, white_row):
            print(f"Game over! White pawn is promoted to a queen at {square_calculator(white_row, white_col)}.")
            break

    if black_can_capture(matrix, black_row, black_col) == "Left":
        matrix[black_row+1][black_col-1] = "b"
        matrix[black_row][black_col] = "-"
        print(f"Game over! Black win, capture on {square_calculator(black_row+1, black_col-1)}.")
        break
    elif white_can_capture(matrix, white_row, white_col) == "Right":
        matrix[black_row][black_col+1] = "b"
        matrix[black_row][black_col] = "-"
        print(f"Game over! Black win, capture on {square_calculator(black_row+1, black_col+11)}.")
        break

    else:
        black_row += 1
        matrix[black_row-1][black_col] = "-"
        matrix[black_row][black_col] = "b"
        if queen_promoted(matrix, black_row):
            print(f"Game over! Black pawn is promoted to a queen at {square_calculator(black_row, black_col)}.")
            break
            
