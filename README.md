package Task1;
public class detectduplicates {
	static char detectduplicates(char arr[], int n)
    {
        if (n == 0 || n == 1)
            return (char) n;
        char[] temp = new char[n];
        char j = 0;
        for (char i = 0; i < n - 1; i++)
           
            if (arr[i] != arr[i + 1])
                temp[j++] = arr[i];
        temp[j++] = arr[n - 1];
        for (char i = 0; i < j; i++)
            arr[i] = temp[i];
        return j;
    }
  
    public static void main(String[] args)
    {
        char arr[] = { 'k', 'k', 'j', 'j','d', };
        char n = (char) arr.length;
        n = detectduplicates(arr, n);
            for (char i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}







package Task2;
import java.util.Arrays;
public class sameset {

    public static void main(String[] args) {
        int[] arr1 = {4, 7, 2, 1, 9, 5, 3, 8};
        int[] arr2 = {2, 8, 5, 1, 7, 9, 3, 4};
        boolean sameSet = samesett(arr1, arr2);
        System.out.println(sameSet ? "The arrays have the same set" : "The arrays don't the same set");
    }
    public static boolean samesett(int[] arr1, int[] arr2) {
        if (arr1.length != arr2.length) {
            return false;
        }
        Arrays.sort(arr1);
        Arrays.sort(arr2);

        for (int i = 0; i < arr1.length; i++) {
            if (arr1[i] != arr2[i]) {
                return false;
            }
        }
        return true;
    }
}





package Task3;
public class task3 {
    private int[] array;
    private int red;
    private int blue;
    public task3(int capacity) {
        array = new int[capacity];
        red = -1;
        blue = capacity;
    }
    public void pushRed(int item) {
        if (red + 1 >= blue) {
            throw new RuntimeException("full red stack");
        }
        array[++red] = item;
    }
    public void pushBlue(int item) {
        if (blue - 1 <= red) {
            throw new RuntimeException("full blue stack");
        }
        array[--blue] = item;
    }
    public int popRed() {
        if (red == -1) {
            throw new RuntimeException("empty red stack");
        }
        return array[red--];
    }
    public int popBlue() {
        if (blue == array.length) {
            throw new RuntimeException("empty blue stack");
        }
        return array[blue++];
    }
    public boolean isRedEmpty() {
        return red == -1;
    }
    public boolean isBlueEmpty() {
        return blue == array.length;
    }
    public boolean isRedFull() {
        return red + 1 >= blue;
    }
    public boolean isBlueFull() {
        return blue - 1 <= red;
    }
    public static void main(String[] args) {
        task3 stack = new task3(10);
        stack.pushRed(8);
        stack.pushRed(9);
        stack.pushBlue(7);
        stack.pushBlue(2);
        System.out.println(stack.popRed());
        System.out.println(stack.popBlue());
        System.out.println(stack.popRed());
        System.out.println(stack.popBlue());
    }
}





package Task7;
import java.util.ArrayList;
import java.util.Arrays;
public class heapsort {

    public static void main(String[] args) {
        int[] arr = {9, 7, 5, 4, 6, 3, 8};
        System.out.println("Before sorting: " + Arrays.toString(arr));
        heapSort(arr);
        System.out.println("After sorting: " + Arrays.toString(arr));
    }
    public static void heapSort(int[] arr) {
    int x = arr.length;
    
        for (int i = x / 2 - 1; i >= 0; i--) {
            heapify(arr, x, i);
        }

        for (int i = x - 1; i >= 0; i--) {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            heapify(arr, i, 0);
        }
    }

    private static void heapify(int[] arr, int x, int i) {
        int least = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < x && arr[left] < arr[least]) {
            least = left;
        }

        if (right < x && arr[right] < arr[least]) {
            least = right;
        }

        if (least != i) {
            int temp = arr[i];
            arr[i] = arr[least];
            arr[least] = temp;
            heapify(arr, x, least);
        }
    }
}


    
    
    
    package Task8;
import java.util.*;

public class RoutingTableBuilder {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Get input for number of nodes
        System.out.print("Enter the number of nodes: ");
        int numNodes = scanner.nextInt();
        scanner.nextLine();

        // Initialize the network graph
        Map<String, List<String>> networkGraph = new HashMap<>();

        // Get input for node connectivity lists
        for (int i = 1; i <= numNodes; i++) {
            System.out.print("Enter the connectivity list for node " + i + ": ");
            String input = scanner.nextLine();
            String[] connectivityList = input.split(":");
            String node = connectivityList[0].trim();

            if (!networkGraph.containsKey(node)) {
                networkGraph.put(node, new ArrayList<>());
            }

            for (String connectedNode : connectivityList[1].split(",")) {
                networkGraph.get(node).add(connectedNode.trim());
            }
        }

        // Build routing tables for each node
        for (String node : networkGraph.keySet()) {
            Map<String, String> routingTable = new HashMap<>();

            Queue<String> queue = new LinkedList<>();
            queue.add(node);
            Set<String> visited = new HashSet<>();
            visited.add(node);
            int distance = 0;

            while (!queue.isEmpty()) {
                int levelSize = queue.size();
                for (int i = 0; i < levelSize; i++) {
                    String currentNode = queue.poll();

                    if (!routingTable.containsKey(currentNode) && !currentNode.equals(node)) {
                        routingTable.put(currentNode, queue.peek());
                    }

                    for (String connectedNode : networkGraph.get(currentNode)) {
                        if (!visited.contains(connectedNode)) {
                            queue.add(connectedNode);
                            visited.add(connectedNode);
                        }
                    }
                }
                distance++;
            }

            // Print the routing table for the current node
            System.out.println("Routing table for node " + node + ":");
            for (String destNode : routingTable.keySet()) {
                System.out.println(destNode + " : " + routingTable.get(destNode));
            }
            System.out.println();
        }
    }
}
