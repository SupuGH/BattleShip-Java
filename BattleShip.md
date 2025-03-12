```java
import java.util.Scanner;

public class BattleShip {

    static Scanner sca = new Scanner(System.in);

    public static void generateMap(char[][] map, char[][] newMap) {

        /*
        a = water
        b = boat
        */

        char[][] mapBoats = {
            {'a', 'b', 'a', 'a', 'a'},
            {'a', 'b', 'a', 'a', 'a'},
            {'a', 'b', 'a', 'a', 'a'},
            {'a', 'a', 'a', 'a', 'a'},
            {'a', 'a', 'a', 'a', 'a'}
        };

        for (int i = 0; i < mapBoats.length; i++) {
            for (int j = 0; j < mapBoats[0].length; j++) {
                newMap[i][j] = mapBoats[i][j];
            }
        }

    }

    public static void showMap(char[][] map) {

        for (char[] row : map) {
            for (char tile : row) {
                System.out.print(tile + "  ");
            }
            System.out.println("");
        }
        System.out.println();

    }

    public static boolean shoot(char[][] map, char[][] newMap, Boolean[] sink) {

        int row, column;

        System.out.println("Select a row for shooting");
        row = sca.nextInt();

        System.out.println("Select a column for shooting");
        column = sca.nextInt();

        if (newMap[row][column] == 'b') {
            map[row][column] = 't';
            checkAll(sink, map, newMap);
            return true;
        } else {
            map[row][column] = 'a';
            return false;
        }

    }

    public static Boolean checkAll(Boolean[] sink, char[][] map, char[][] newMap) {

        sink[0] = true;

        for (int i = 0; i < map.length; i++) {
            for (int j = 0; j < map[0].length; j++) {
                if (map[i][j] != 't' && newMap[i][j] == 'b') {
                    sink[0] = false;
                }
            }
        }
        return sink[0];
    }

    public static void main(String[] args) {

        Boolean[] sink = {false};

        char[][] map = {
            {'+', '+', '+', '+', '+'},
            {'+', '+', '+', '+', '+'},
            {'+', '+', '+', '+', '+'},
            {'+', '+', '+', '+', '+'},
            {'+', '+', '+', '+', '+'}
        };

        char[][] newMap = new char[5][5];

        generateMap(map, newMap);

        showMap(map);

        do {

            if (shoot(map, newMap, sink)) {
                System.out.println("Hit");
            } else {
                System.out.println("Water");
            }
            showMap(map);

        } while (sink[0] == false);

        System.out.println("And sink! You win");

    }
}
```
