# Leetcode---2462
Total Cost to Hire K Workers
//code in java
import java.util.PriorityQueue;

public class Solution {
    public long totalCostToHireKWorkers(int[] costs, int k, int candidates) {
        int n = costs.length;
        PriorityQueue<Integer> lowCostWorkers = new PriorityQueue<>();
        PriorityQueue<Integer> highCostWorkers = new PriorityQueue<>();

        for (int i = 0; i < candidates; i++) {
            lowCostWorkers.offer(costs[i]);
            highCostWorkers.offer(costs[n - 1 - i]);
        }

        long totalCost = 0;
        int left = candidates;
        int right = n - 1 - candidates;

        for (int i = 0; i < k; i++) {
            if (lowCostWorkers.peek() <= highCostWorkers.peek()) {
                totalCost += lowCostWorkers.poll();
                if (left <= right) {
                    lowCostWorkers.offer(costs[left++]);
                }
            } else {
                totalCost += highCostWorkers.poll();
                if (left <= right) {
                    highCostWorkers.offer(costs[right--]);
                }
            }
        }

        return totalCost;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] costs = {17, 12, 10, 2, 7, 2, 11, 20, 8};
        int k = 3;
        int candidates = 4;
        long result = solution.totalCostToHireKWorkers(costs, k, candidates);
        System.out.println("The total cost to hire " + k + " workers is: " + result);
    }
}
