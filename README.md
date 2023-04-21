# Practice-Project
Practice Group in GitHub
import java.util.Scanner;

public class Monticalvo_E3 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter a number to compute its factorial: ");
        int number = scanner.nextInt();

        FactorialThread factorialThread = new FactorialThread(number);
        MatrixMultiplicationThread matrixMultiplicationThread = new MatrixMultiplicationThread();
        PrimeNumberThread primeNumberThread = new PrimeNumberThread();

        factorialThread.start();
        matrixMultiplicationThread.start();
        primeNumberThread.start();
    }
}

class FactorialThread extends Thread {
    private int number;

    public FactorialThread(int number) {
        this.number = number;
    }

    @Override
    public void run() {
        int result = 1;
        for (int i = 1; i <= number; i++) {
            result *= i;
        }
        System.out.println("Factorial of " + number + " is " + result);
    }
}

class MatrixMultiplicationThread extends Thread {
    @Override
    public void run() {
        int[][] matrix1 = { {1, 2}, {3, 4}, {5, 6} };
        int[][] matrix2 = { {1, 2, 3}, {4, 5, 6} };
        int[][] result = new int[matrix1.length][matrix2[0].length];

        for (int i = 0; i < matrix1.length; i++) {
            for (int j = 0; j < matrix2[0].length; j++) {
                for (int k = 0; k < matrix2.length; k++) {
                    result[i][j] += matrix1[i][k] * matrix2[k][j];
                }
            }
        }

        System.out.println("Result of matrix multiplication:");
        for (int i = 0; i < result.length; i++) {
            for (int j = 0; j < result[0].length; j++) {
                System.out.print(result[i][j] + " ");
            }
            System.out.println();
        }
    }
}

class PrimeNumberThread extends Thread {
    @Override
    public void run() {
        int count = 0;
        int number = 2;

        System.out.println("First 100 prime numbers:");
        while (count < 100) {
            boolean isPrime = true;

            for (int i = 2; i <= Math.sqrt(number); i++) {
                if (number % i == 0) {
                    isPrime = false;
                    break;
                }
            }

            if (isPrime) {
                System.out.print(number + " ");
                count++;
            }

            number++;
        }

        System.out.println();
    }
}
