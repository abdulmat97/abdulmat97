import java.util.Scanner;

public class tictactoe {
    char tictactoe[][] = new char[3][3];

    public static void display(char tictactoe[][]) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                System.out.print(tictactoe[i][j] + " ");
            }
            System.out.println();
        }
    }

    static void replace(char arr[][], char find, char replace) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (arr[i][j] == find) {
                    arr[i][j] = replace;
                    return;
                }
            }
        }
    }

    public boolean checkForWin() {
        return (checkForRow() || checkForColomn() || checkForDiagnol());
    }

    public boolean check(char c1, char c2, char c3) {
        return ((c1 == c2) && (c2 == c3));
    }

    public boolean checkForRow() {
        for (int i = 0; i < 3; i++) {
            if (check(tictactoe[i][0], tictactoe[i][1], tictactoe[i][2]) == true)
                return true;
        }
        return false;
    }

    public boolean checkForColomn() {
        for (int i = 0; i < 3; i++) {
            if (check(tictactoe[0][i], tictactoe[1][i], tictactoe[2][0]) == true)
                return true;
        }
        return false;
    }

    public boolean checkForDiagnol() {
        return ((check(tictactoe[0][0], tictactoe[1][1], tictactoe[2][2]) == true)
                || (check(tictactoe[0][2], tictactoe[1][1], tictactoe[2][0]) == true));
    }

    // main Function
    public static void main(String[] args) {
        tictactoe game = new tictactoe();
        Scanner sc = new Scanner(System.in);

        String user1, user2;
        char user1mark, user2mark;
        System.out.print("Enter Player one Name: ");
        user1 = sc.nextLine();
        System.out.print("Enter Player two Name: ");
        user2 = sc.nextLine();

        System.out.println(user1 + " Select Your Marker (X or O): ");

        user1mark = sc.next().charAt(0);
        while (user1mark != 'X' && user1mark != 'x' && user1mark != 'O' && user1mark != 'o') {
            System.out.print("Invalid Input (Select X or O): ");
            user1mark = sc.next().charAt(0);
        }
        if (user1mark == 'X' || user1mark == 'x')
            user2mark = 'O';
        else
            user2mark = 'X';

        int counter = 0;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                game.tictactoe[i][j] = Character.forDigit(++counter, 10);
            }
        }

        display(game.tictactoe);

        char input;
        for (int i = 0; i < 4; i++) {
            System.out.print(user1 + " Turn: ");
            input = sc.next().charAt(0);
            replace(game.tictactoe, input, user1mark);
            display(game.tictactoe);
            System.out.print(user2 + " Turn: ");
            input = sc.next().charAt(0);
            replace(game.tictactoe, input, user2mark);
            display(game.tictactoe);
        }
        System.out.print("User " + user1 + ": ");
        input = sc.next().charAt(0);
        replace(game.tictactoe, input, user1mark);
        display(game.tictactoe);

        if (game.checkForWin())
            System.out.print("We have a Winner");
        else
            System.out.print("Match is Draw");
    }
}
