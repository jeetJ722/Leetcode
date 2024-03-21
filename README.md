# Leetcode
Functions go easy to solve 
1.Arrays
--Move zeroes to the end of an array:
class Solution {
    public int[] moveZeroes(int[] nums) {
    int j=-1;
    for(int i=0;i<nums.length;i++)
    {
        if(nums[i]==0)
        {
            j=i;
            break;
        }
    }  
    if (j==-1) return nums;  
    for(int i=j+1;i<nums.length;i++)
    {
        if(nums[i]!=0)
        {
            int temp=nums[i];
            nums[i]=nums[j];
            nums[j]=temp;
            j++;
        }
    }
    return nums;
}

    public void main(String[] args){
        int[] nums={0,1,0,3,12};
        int[] ans=moveZeroes(nums);
        for(int i=0;i<nums.length;i++)
        {
            System.out.println(ans[i]+" ");
        }
        
    }
}
--Leetcode:1295. Find Numbers with Even Number of Digits:-
class Solution {
    public int findNumbers(int[] nums) {
        int digits=0;
        for(int i=0;i<nums.length;i++)
        {
            if(nums[i]>9 && nums[i]<100 || nums[i]>999 && nums[i]<10000 || nums[i]==100000)
            {
                digits++;
            }
           
        }
return digits;
}
}

--Leetcode:1672.Richest Customer Wealth:-
class Solution {
    public int maximumWealth(int[][] accounts) {
        int ans=Integer.MIN_VALUE;
        for(int row=0;row<accounts.length;row++)
        
        {
            int wealth=0;
            for(int col=0;col<accounts[row].length;col++)
            {
                wealth=accounts[row][col]+wealth;
            }
            if(wealth>ans)
            {
                ans=wealth;
            }

        }
        return ans;
    }
}

--Leetcode:189. Rotate Array:-
class Solution {
    public void rotate(int[] nums,int k) {
        k=k%nums.length;
        reverse(nums,0,nums.length-k-1);
        reverse(nums,nums.length-k,nums.length-1);
        reverse(nums,0,nums.length-1);
      
    }
    
    public void reverse(int[] nums,int start,int end)
    {
       while(start<=end)
       {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
       }
    }
} 
--Leetcode:744. Find Smallest Letter Greater Than Target:-(Ceiling of Number using BS approach)
class Solution {
    public char nextGreatestLetter(char[] arr, char target) {
       
        int start = 0;
        int end = arr.length-1;
        while(start<=end)
        {
            int mid=start +(end - start)/2;
            if(target<arr[mid])
            {
                end = mid-1;
            }
            else{
                start = mid + 1;
            }
            

        }
        return arr[start% arr.length];
    }
}
--Leetcode Problem:852. Peak Index in a Mountain Array:-(A mountain array is a sorted array but in parts where one part is incresing order and one decreasin left and right respectively)
int[] mountainArrayExample={1,3,5,7,4,2,0};and thus find max element in this:
class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int start = 0;
        int end = arr.length - 1;
        while(start < end)
    {
        int mid = start + (end - start)/2;
        if(arr[mid] > arr[mid + 1])//IF YES THAN WE ARE AT THE DECREASING PART THUS THE MAX ELEMENT WOULD BE EITHER MID OR AT THE LEFT SIDE:
        {
           end = mid;
        }
        else{
            //The max element is yet on right side:
            start = mid + 1;
        }
     //as start and end would be equal in the end due to above conditions thus return anyone as keeping on checking in the above ranges
    }
     return start;
    }
}
--Leetcode Problem:410. Split Array Largest Sum:-BS:
class Solution {
    public int splitArray(int[] nums, int m) {  
        int start = 0;
        int end = 0;
        for(int i =0 ; i < nums.length;i++){
           start = Math.max(start, nums[i]);//Max element from the array
           end+=nums[i];//Sum of all the values
        }
        //Now we have start and end we will apply binary search
        while(start <end) {
            //try middle for potential answer
            int mid = start + (end - start) / 2;
            int sum = 0;
            int pieces = 1;//Atleast one piece
            for (int num : nums) {
                    if (sum + num > mid)
                    {
                       //then create new subarray:
                        sum = num;
                        pieces++;
                    }
                    else {
                        sum += num;
                    }
                }
            if(pieces > m)
            {
                start = mid + 1;
            }
            else{
                end = mid;
            }
        }
        return end;
    }
}
--Leetcode Problem:74. Search a 2D Matrix:-
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int r=matrix.length;
        int c=matrix[0].length;
        // the idea is to think of the matrix as a 1D array
        // so the start index is
        int low=0;
        // and the last index is (since there are r*c items)
        int high=r*c-1;
        // now that we have a 1D array we can perform binary search
        while(low<=high){
            int mid=low+(high-low)/2; // to avoid integer overflow
            //but how can we derive the ith index (row) and jth index (col)
            int row=mid / c;
            int col=mid % c;
            // actual search
            if(matrix[row][col]==target)
                return true;
            else if(matrix[row][col]<target)
                low=mid+1;
            else
                high=mid-1;
        }
        return false;
    }
}

--Leetcode Problem:35. Search Insert Position:-
class Solution {
    public int searchInsert(int[] nums, int target) {
       int start = 0;
       int end = nums.length - 1;
       while(start <= end)
       {
        int mid = start +(end - start)/2;
        if(nums[mid] == target){
            return mid;
        }
        else if(target < nums[mid]){
        end = mid -1;    
        }     
        else{
            start = mid + 1;
        }
    }
  return start;  
}
}


