# java-To-Do-List-Application-with-DSA-implementation
Implemented CRUD operations, search and sorting algorithms to manage student records efficiently
import java.util.*;

class Task {
    String name;
    int priority;

    Task(String name, int priority) {
        this.name = name;
        this.priority = priority;
    }
}

public class TodoListDSA {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        PriorityQueue<Task> pq = new PriorityQueue<>(Comparator.comparingInt(t -> t.priority));
        HashMap<String, Task> taskMap = new HashMap<>();

        while(true){
            System.out.println("\n1. Add Task\n2. Remove Task\n3. Show Tasks\n4. Exit");
            System.out.print("Enter choice: ");
            int ch = sc.nextInt();
            sc.nextLine(); // consume newline

            switch(ch){
                case 1:
                    System.out.print("Task Name: ");
                    String name = sc.nextLine();
                    System.out.print("Priority (1=High, 5=Low): ");
                    int prio = sc.nextInt();
                    sc.nextLine();
                    Task t = new Task(name, prio);
                    pq.add(t);
                    taskMap.put(name, t);
                    System.out.println("Task Added!");
                    break;

                case 2:
                    System.out.print("Task Name to remove: ");
                    String removeName = sc.nextLine();
                    Task taskToRemove = taskMap.get(removeName);
                    if(taskToRemove != null){
                        pq.remove(taskToRemove);
                        taskMap.remove(removeName);
                        System.out.println("Task Removed!");
                    } else {
                        System.out.println("Task not found!");
                    }
                    break;

                case 3:
                    if(pq.isEmpty()){
                        System.out.println("No tasks!");
                        break;
                    }
                    System.out.println("Tasks by Priority:");
                    PriorityQueue<Task> temp = new PriorityQueue<>(pq);
                    while(!temp.isEmpty()){
                        Task tsk = temp.poll();
                        System.out.println(tsk.name + " - Priority " + tsk.priority);
                    }
                    break;

                case 4:
                    System.out.println("Exiting...");
                    sc.close();
                    return;

                default:
                    System.out.println("Invalid choice!");
            }
        }
    }
}
