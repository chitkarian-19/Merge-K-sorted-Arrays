# Merge-K-sorted-Arrays
Practise Link: https://practice.geeksforgeeks.org/problems/merge-k-sorted-arrays/1


Given K sorted arrays arranged in the form of a matrix of size K*K. The task is to merge them into one sorted array.

Thq question is looking for a sorted unidirectional array,from a 2d matrix which is already sorted in some special manner. We could have used sorting algorithm, the time and space complexity would be O(nlogn) and O(n^2) where n=k.
We used heap in order to save the space however time comeplxity remains the same. Here are the steps that i used
1. Push all the first col elements in the priority queue with the row and column number, here we are using a min heap
2. After that, run a while loop with a condition that the heap is not empty
3. In the while loop pop out the top element from the heap, get the row and col num , check if the col_num is the last colum or not
4. If col_num is the last column number i.e. k-1, then repeatedly pop the elements from the heap, until col_num is the last column.
5. When the program comes out of the while loop, check that still the col_num is the last column or not.
6. If it is not then push the element present at the row_num and col_num +1 in the heap.
7. When popping the element from the heap, add the item in the output list.


Here is the working code.
````

class Item{
    int row_num;
    int col_num;
    int value;
    Item(){
        
    }
    Item(int row_num,int col_num,int value){
        this.row_num = row_num;
        this.col_num = col_num;
        this.value = value;
    }
}
class Solution
{
    //Function to merge k sorted arrays.
    public static ArrayList<Integer> mergeKArrays(int[][] arr,int k) 
    {
        // Write your code here.
        PriorityQueue<Item> pq = new PriorityQueue<Item>(new Comparator<Item>(){
            public int compare(Item i1,Item i2){
                return i1.value-i2.value;
            }
        });
        
        for(int i=0;i<k;i++){
         
          pq.add(new Item(i,0,arr[i][0]));   
         
        }
        
        ArrayList<Integer> op = new ArrayList<Integer>();
        while(!pq.isEmpty()){
          
          Item item = pq.poll();
          int row_num = item.row_num;
          int col_num = item.col_num;
          op.add(item.value);
          while(!pq.isEmpty()&&col_num==k-1){
              item = pq.poll();
              row_num = item.row_num;
              col_num = item.col_num;
              op.add(item.value);
          }
          
          if(col_num !=k-1){
              pq.add(new Item(row_num,col_num+1,arr[row_num][col_num+1]));
          }
          
        }
        
        return op;
        
        
    }
}

```````
