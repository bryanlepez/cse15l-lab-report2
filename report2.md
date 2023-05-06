## Part 2: Choosing A Bug From Lab 3
The buggy program that I will be using is the `averageWithoutLowest` method. The buggy version of this program looks like this:
```
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
  
  ```
  This program is supposed to take the mean of the numbers(doubles) within the array. However, it is supposed to take the mean without including the lowest
  number within the array. The program should also return 0 if there are no elements in the array or if there is only 1 element in the array. However the bug
  within this program is that it doesn't account for the possiblity of there being duplicates of the lowest number within the array. The program does 
  `return sum / (arr.ength - 1);` but it should do `return sum / (arr.length - #the amount of the lowest number in the array)`.
  
  Due to the nature of this buggy program, if we have a duplicate `lowest` within the array it will fail to do the task correctly. An example of a
  failure-inducing test would be:
  ```
  @Test 
  public void testAverage(){
    double[] input1 = {1.0, 2.0, 3.0, 1.0};
    assertEquals(2.5, ArrayExamples.averageWithoutLowest(input1), 0.001);

    
  }
  
  ```
  This test makes the program fail because it has duplicate `lowest` numbers, which are equal to 1.0. The program fails to return the correct mean of the
  array because when it does the calculation `return sum / (arr.length - 1);` it only accounts for one of the `lowest` numbers within the array instead of both.
  This results in the calculation being `5 / (4 - 1)` which = `5 / 3` = `1.666666666667`.
  
  The program works fine when there is only one `lowest` number within the array. An example of a test that does not induce a failure would be:
  ```
    @Test
  public void testAverage2(){
    double[] input1 = {1.0, 2.0, 3.0};
    assertEquals(2.5, ArrayExamples.averageWithoutLowest2(input1), 0.001);
  }
  ```
  The test passes with the buggy program because there is only one of the `lowest` numbers within the array which is `1`. Since there is only one of the `lowest` values in the array the calculation would be `5 / (3 - 1)` whihch = `5 / 2` = `2.5`. This is the correct average without the lowest value in the array. It is correct because in this case, since there is only one `lowest` value then the `- 1` in the calculation is correct because there is only one `lowest` value within the array.
  
 ### Picture of Symptoms with Both Tests
 ![Image](symptoms.png)
  
