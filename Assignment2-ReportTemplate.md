**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#2 – Requirements-Based Test Generation**

| Group \#:      |     |
| -------------- | --- |
| Student Names: |  Nuha Shaikh     |
|                |  Huda Abbas      |
|                |  Lubaba Sheikh   |
|                |  Rajpreet Gill   |

# 1 Introduction

This lab enabled the team to concentrate on fully grasping the principles of automated unit testing, especially unit testing based on a set requirements criterion for each unit of code. The lab provided an opportunity for all group members to become acquainted with the widely used unit testing tool for Java, JUnit framework, which is part of the XUnit framework family. Upon completion of the lab, all team members were equipped with the knowledge to develop automated test code in JUnit along with other similar testing environments used in the industry. The lab also allowed us to utilize and work with mock objects in test-code development and further gave us an opportunity to employ the notion of mocking in various unit tests.

Along with the fundamental automation testing knowledge the lab provided, it also gave us an essence into the strength and influence teamwork offers. Through strong collaboration and cooperation as well as by employing effective teamwork capabilities, we all ensured to maximize our expertise by taking part in active discussions throughout the lab and providing each other guidance and feedback frequently. Overall, this lab was a success, and the following report captures all test cases performed, the reasoning as well as a detailed conclusion regarding the findings.


# 2 Detailed description of unit test strategy

*2.1 Testing Plan*

Our general testing plan to design and develop our test cases for all 10 methods is first we will partition the input variables using the requirements specified in the documentation, splitting them into valid and invalid inputs using the domain for each input. This will help us determine our equivalent classes where we can create test cases using one sample from each class and one sample at every boundary between the classes following ECT and BVT principles.

*2.2 Test-Case Design Strategy*

Below are the input partitions designed for the methods in the _DataUtilities_ class:

__calculateColumnTotal(Values2D data, int column):double__
 * Invalid data
    * Values2D data is null
    * Column index less than 0
    * Column index larger than data size
 * Equivalent class
    * For int column variable (-inf, 0) (0, data column count - 1) (data column count -1, inf)
 * Boundary
    * int column = 0
    * int column = column size - 1

__calculateColumnTotal(Values2D data, int column, int[] validRows):double__
* Invalid data
   * Values2D data is null
   * Column index less than 0
   * Column index larger than data size
   * Negative or larger than row size number in rows array
* Equivalent class
   * For int column variable (-inf, 0) (0, data column count - 1) (data column count - 1, inf)
   * For int[] validRows each integer in the array has 3 distinct classes (-inf, 0) (0, data row count - 1) (data row count - 1, inf)
* Boundary
   * int column = 0
   * int column = column size - 1
   * int[] validRows = {0,..}
   * int[] validRows = {row size - 1,..}

__calculateRowTotal(Values2D, int row): double__
* Invalid data
   * Values2D data is null
   * Row index less than 0
   * Row index larger than data size
* Equivalent class
   * For int row variable (-inf, 0) (0, data row count - 1) (data row count - 1, inf)
* Boundary
   * int row = 0
   * int row = column size - 1

__calculateRowTotal(Values2D data, int row, int[] validCols): double__
Invalid data
Values2D data is null
Row index less than 0
Rowindex larger than data size
Negative or larger than column size number in column array
Equivalent class
For int row variable (-inf, 0) (0, data row count - 1) (data row count - 1, inf)
For int[] validColumn each integer in the array has 3 distinct classes (-inf, 0) (0, data column count - 1) (data column count - 1, inf)
Boundary
int row = 0
int row = row size - 1
Int[] validColumn = {0,..}
Int[] validColumn = {column size - 1,..}
createNumberArray(double[]): Number[]
Array of double -> array of Number objects (returns array of Number)
Invalid data (null, missing, empty…)
double[] data is null
Valid input data (part of equivalent class input data)
For the double[] data, can be anything from -inf to +inf
Boundary analysis (part of equivalent class input data)
None
createNumberArray2D(double[][]): Number[][]
Array of array of type doubles -> array of arrays of Number objects (returns 2-D array of Number)
Invalid data (null, missing, empty…)
Double[][] data is null
Valid input data (part of equivalent class input data)
For the double[][] data, can be anything from -inf to inf
Boundary analysis (part of equivalent class input data)
None
getCumulativePercentage(KeyedValues): KeyedValues
Invalid data (null, missing, empty…)
KeyedValues data is null
KeyedValues data is non-unique
Valid input data (part of equivalent class input data)
Values in the KeyedValues data are between 0.0 and 1.0
Boundary analysis (part of equivalent class input data)
KeyedValues containing values such as 0.0 and 1.0

__Below are the input partitions designed for the methods in the _Range_ class:__

__scale(Range, double): Range__
* One dimensional equivalent classes
* Invalid Data
   * Base is null
   * Factor is a negative number
* Valid Data
   * Range is not null
   * Factor is a positive number
* Boundary
   * Factor is 0

__constrain(double): double__
* Invalid Data
   * All values are valid for value
* Can test 3 different partitions
   * One dimensional equivalent classes
   * Inputs: lower is lower bound, upper is upper bound
   * (-inf, lower) (lower, upper) (upper, +inf)
* Boundary
   * Select the boundary values upper and lower bounds: lower and upper

__contains(double): double__
* Invalid Data
   * All values are valid for value
* Can test 3 different partitions
   * One dimensional equivalent classes
   * Inputs: lower is lower bound, upper is upper bound
   * (-inf, lower) (lower, upper) (upper, +inf)
* Boundary
   * Select the boundary values upper and lower bounds: lower and upper
intersects(double b0, double b1): boolean
b0 - the lower bound (should be <= b1).
b1 - the upper bound (should be >= b0).
One dimensional partitioning
Input variables b0:
Valid Data: (-inf, b1]
Invalid Data: (b1, +inf)
Input variables b1:
Valid Data: [b0, +inf)
Invalid Input: (-inf, b0)
intersects(Range): boolean
Invalid data
Range = null
Can test \_ different partitions
Boundary intersections
Upper bound of input Range argument is equivalent to upper bound of Range class object
Lower bound of input Range argument is equivalent to lower bound of Range class object
Both upper and lower bounds of Range argument are equivalent to upper & lower bounds of Range object
Partitions
One dimensional equivalent classes
Inputs: lower is lower bound, upper is upper bound
(-inf, lower) (lower, upper) (upper, +inf)
Both bound within the Range object
Both bounds out of range object


# 3 Test cases developed

Values2D data is the following 3x3 array for all the below methods unless otherwise specified
|   1.5   |  2   |   3.5  |
| ---- | --- | --- |
| 2    |  4    |  5
| 3   |  6     |  1.5

__calculateColumnTotal(Values2D data, int column):double__
* test_calculatedColumnTotal_invalidData()
   * Input: Values2D data = null
   * Output: IllegalArgumentException.class
   * Covers the invalid class/partition for first input variable
* test_calculatedColumnTotal_negativeColumn()
   * Input: int column = -1
   * Output: 0
   * Invalid class for second input variable, nothing to sum column is null
* test_calculatedColumnTotal_OutOfBoundsColumn()
   * Input: int column = 3
   * Output: 0
   * Invalid class for second input variable where column index larger than data size, nothing to sum column is null
* test_calculatedColumnTotal_ColumnZero()
   * Input: int column = 0
   * Output: 1.5 + 2 + 3 = 6.5
   * Valid input for second variable but at boundary of valid and invalid
* test_calculatedColumnTotal_ValidColumn()
   * Input: int column = 1
   * Output: 2 + 4 + 6 = 12
   * Valid input for second variable, one sample within equivalence class not at boundary
* test_calculatedColumnTotal_ColumnAtSize()
   * Input: int column = 2
   * Output: 3.5 + 5 + 1.5 = 10
   * Valid input for second variable but at boundary of valid and invalid, index right at the maximum size of the data

__calculateColumnTotal(Values2D data, int column, int[] validRows):double__
* test_calculatedColumnTotal_negativeIntForRows()
   * Input: int[] validRows = [-1] int column = 1
   * Output: 0
   * Invalid class for third input variable, negative row number
* test_calculatedColumnTotal_OutOfBoundsRow()
   * Input: int[] validRows = [3] int column = 1
   * Output: 0
   * Invalid class for third input variable where row index in valid rows is larger than data size
* test_calculatedColumnTotal_RowZero()
   * Input: int[] validRows = [0] int column = 1
   * Output: 2
   * Valid input for third variable but at boundary of valid and invalid
* test_calculatedColumnTotal_allValidRows()
   * Input: int[] validRows = [1, 2] int column = 1
   * Output: 4 + 6 = 10
   * Valid input for third variable, one sample within equivalence class not at boundary
* test_calculatedColumnTotal_RowAtSize()
   * Input: int[] validRows = [2] int column = 1
   * Output: 6
   * Valid input for third variable but at boundary of valid and invalid, index right at the maximum size of the data

__calculateRowTotal(Values2D data, int row): double__
* test_calculatedRowTotal_invalidData()
   * Input: Values2D data = null
   * Output: IllegalArgumentException.class
   * Covers the invalid class/partition for first input variable
* test_calculatedRowTotal_negativeRow()
   * Input: int row = -1
   * Output: 0
   * Invalid class for second input variable
* test_calculatedRowTotal_outOfBoundsRow()
   * Input: int row = 3
   * Output: 0
   * Invalid class for second input variable where row index larger than data size
* test_calculatedRowTotal_rowZero()
   * Input: int row = 0
   * Output: 1.5 + 2 + 3.5 = 7
   * Valid input for second variable but at boundary of valid and invalid
* test_calculatedRowTotal_validRow()
   * Input: int row = 1
   * Output: 2 + 4 + 5 = 11
   * Valid input for second variable, one sample within equivalence class not at boundary
* test_calculatedRowTotal_rowAtSize()
   * Input: int row = 2
   * Output: 3 + 6 + 1.5 = 10.5
   * Valid input for second variable but at boundary of valid and invalid, index right at the maximum size of the data
   
calculateRowTotal(Values2D data, int row, int[] validColumn): double
test_calculatedRowTotal_negativeIntForValidColumn()
Input: int[] validColumn = [-1] int row = 1
Output: 0.0
Invalid class for second input variable, negative column number
test_calculatedRowTotal_OutOfBoundsColumn()
Input: int[] validColumn = [3] int row = 1
Output: 0.0
Invalid class for second input variable where column index in valid columns is larger than data size
test_calculatedRowTotal_ColumnZero()
Input: int[] validColumn = [0] int row = 1
Output: 5.0
Valid input for second variable but at boundary of valid and invalid
test_calculatedRowTotal_allValidColumns()
Input: int[] validColumns = [1, 2] int row = 1
Output: 9.0
Valid input for second variable, one sample within equivalence class not at boundary
test_calculatedRowTotal_ColumnAtSize()
Input: int[] validColumn = [2] int row = 1
Output: 2.0
Valid input for third variable but at boundary of valid and invalid, index right at the maximum size of the data

__createNumberArray(double[]): Number[]__
* test_createNumberArray_invalidData()
    * Input: null
    * Output: an exception should be thrown
    * Checks a null entry into the double[] data parameter
* test_createNumberArray_validData()
    * Input: double[] = {4.14, 9.14, 10.0}
    * Output: Number [] = {4.14, 9.14, 10.0}
    * Checks a valid entry of double[] data parameter

__createNumberArray2D(double[][]): Number[][]__
* test_createNumberArray2D_invalidData()
    * Input: null
    * Output: an exception should be thrown
    * Checks an invalid entry of double[][] data parameter
* test_createNumberArray2D_validData()__
    * Input: double[][] data = {{4.14,9.14,10.0}, {4.15, 9.15, 10.01}}
    * Output: Number[][] data = {{4.14,9.14,10.0}, {4.15, 9.15, 10.01}}
    * Checks a valid entry of double[][] data parameter

__getCumulativePercentage(KeyedValues): KeyedValues__
* test_getCumulativePercentage_invalidData()
    * Input: null
    * Output: an exception should be thrown
    * Checks an invalid entry of KeyedValues data parameter
* test_getCumulativePercentage_validData()
    * Input: KeyedValues object, index=0;value=1, index=1;value=1
    * Output: KeyedValues object, index=0;value=0.5, index=1;value=1.0
    * Checks a valid entry of KeyedValues data parameter

*3.2 Test Cases for org.jfree.data.Range*

intersects(double b0, double b1): boolean
test_intersects_invalidData_b0()
Range input @setup: -10, 10
Function call Input: 11, 10
Output: false
checks: the behavior of the function when an illegal range is provided, when the lower bound is greater than the upper bound
test_intersects_invalidData_b1()
Range input @setup: -10, 10
Function call Input: 11, 8
Output: false
Checks: the behavior of the function when an illegal range is provided, when upper bound is less than the lower bound
test_intersects_edge_b0()
Range input @setup: -10, 10
Function call Input: -10, 12
Output: true
Checks: the behavior of the function at the edges of the Range variable
test_intersects_edge_b1()
Range input @setup: -11, 11
Function call Input: -10, 11
Output:
Checks: the behavior of the function at the edges of the Range variable
test_intersects_bothIntersects()
Range input @setup: -11, 11
Function call Input: -11, 11
Output:
Checks: the behavior of the function at the edges of the Range variable
test_intersects_validData()
Range input @setup: -11, 11
Function call Input: -10, 10
Output:
Checks: the behavior of the function at the edges of the Range variable
intersects(Range): boolean
test_intersects_invalidData_b0()
Range input @setup: -10, 10
Function call Input: Range(11, 10)
Output:
checks: the behavior of the function when an illegal range is provided, when the lower bound is greater than the upper bound
test_intersects_invalidData_b1()
Range input @setup: -10, 10
Function call Input: Range(11, 8)
Output:
Checks: the behavior of the function when an illegal range is provided, when upper bound is less than the lower bound
test_intersects_edge_b0()
Range input @setup: -10, 10
Function call Input: Range(-10, 12)
Output:
Checks: the behavior of the function at the edges of the Range variable
test_intersects_edge_b1()
Range input @setup: -11, 11
Function call Input: Range(10, 11)
Output:
Checks: the behavior of the function at the edges of the Range variable
test_intersects_bothIntersects()
Range input @setup: -11, 11
Function call Input: Range(-11, 11)
Output:
Checks: the behavior of the function at the edges of the Range variable
test_intersects_validData()
Range input @setup: -11, 11
Function call Input: Range(-10, 10)
Output:
Checks: the behavior of the function at the edges of the Range variable

__The methods below used the following valid Range:__

Lower bound: 4

Upper bound: 10

__scale(Range, double): Range__
* test_scale_invalidData_base()
   * Input: Null base Range
   * Output: Throws exception
   * Checks if an exception is thrown when an invalid Range object is provided, EC invalid input

* test_scale_invalidData_factor()
   * Input: factor = -2
   * Output: Throws exception
   * Checks if an exception is thrown when an invalid Range factor is provided, EC invalid input

* test_scale_invalidData_factorBoundary()
   * Input: factor = 0
   * Output
      * Range: lower = 0, upper = 0
   * Checks behavior of function when the boundary value of factor is provided, test’s boundary value

* test_scale_validData()
   * Input:
      * Valid base range: lower = 4, upper = 10
      * factor = 2
   * Output: lower = 8, upper = 20
   * Checks behavior of function if both input arguments are valid, EC valid inputs

__constrain(double): double__
* test_constrain_valueBelowLower()
   * Input: value = -2
   * Output: 4
   * Checks behavior of function when a value below the lower bound is provided, EC valid input partition
* test_constrain_valueBetweenRange()
   * Input: value = 9
   * Output: 9
   * Checks behavior of function when a value between the range is provided, EC valid input partition
* test_constrain_valueAboveUpper()
   * Input: value = 20
   * Output: 10
   * Checks behavior of function when a value above the upper bound is provided, EC valid input partition
* test_constrain_valueAtLower()
   * Input: value = 4
   * Output: 4
   * Checks behavior of function when a value at the boundary of the lower bound is provided, boundary value test
* test_constrain_valueAtUpper()
   * Input: value = 10
   * Output: 10
   * Checks behavior of function when a value at the boundary of the upper bound is provided, boundary value test
__contains(double): double__
* test_contains_valueBelowLower()
   * Input: value = 1
   * Output: false
   * Checks behavior of function when a value below the lower bound is provided, EC valid input partition
* test_contains_valueBetweenRange()
   * Input: value = 5
   * Output: true
   * Checks behavior of function when a value between the range is provided, EC valid input partition
* test_contains_valueAboveUpper()
   * Input: value = 15
   * Output: false
   * Checks behavior of function when a value above the upper bound is provided, EC valid input partition
* test_contains_valueAtLower()
   * Input: value = 4
   * Output: true
   * Checks behavior of function when a value at the boundary of the lower bound is provided, boundary value test
* test_contains_valueAtUpper()
   * Input: value = 10
   * Output: true
   * Checks behavior of function when a value at the boundary of the upper bound is provided, boundary value test

*3.3 Benefits and Drawbacks about using Mocking*

_Benefits:_ mocking allows us to instantiate a fake object and watch the interactions between the objects to determine if a unit test has passed or failed. It is a more reliable way of testing as it allows us to isolate the tests from external dependencies. This reduces the scope of the unit tests which creates more focused tests.

_Disadvantages:_ Since the use of mocking involves knowing how the method under test is implemented, it can lead to more tests failing due to misinterpretation of the function implementation.


# 4 How the team work/effort was divided and managed

Initially, all team members came together to develop a consistent test strategy for all methods and selected the 5 methods to be tested from the Range class. The functions that were to be tested were divided among the team members. Each team member created tests for 3 functions (this includes overloaded functions). After we finished creating all the test cases, we reviewed each other’s tests to ensure there were no inconsistencies or defects. By familiarizing ourselves with each other's tests we were able to manage the team work and divide it evenly, while also keeping each other accountable and providing constructive criticism on input partitioning, test case design and unit test development. All source code, equivalent class planning and boundary analysis that was divided was shared with the entire team in the end.


# 5 Difficulties encountered, challenges overcome, and lessons learned

When the work was divided, maintaining version control and ensuring all parties had the same files and the most up to date version was difficult since Eclipse does not have an easy to install seamless integration with GitHub and a lot of conflicts occured with libraries when sharing over git. In the end, we decided to come together and manually share and explain our unit tests. This allowed us to compare, provide valid criticism and integrate each other's unit tests together. Deciding what type of strategy to use for the specific classes was also complicated, we encountered difficulties with input variable partitioning as the documentation did not have a lot of restrictions or ranges specified. In the end we learned how to collaborate and share unit tests, different test strategies and how to partition input variables for black box testing using available invalid and valid information. Another big challenge was setting up our Eclipse IDE for the project as each team member had their own individual errors which made it hard to troubleshoot as a team.


# 6 Comments/feedback on the lab itself

Overall, the lab taught us a-lot about black box testing, developing well-commented and through JUnit tests and using mocking to aid with external dependencies in methods. The lab repository had some errors in files given like with the hamcrest.jar file provided there was an error being thrown when trying to use JMock however, after some troubleshooting we imported the hamcrest-all.jar file which fixed our issue. Additionally, there were some discrepancies in the JChartFree code jars attached in d2L versus the one in the repository which made testing confusing as we were not sure which was the correct set. Additionally, the document was out of date in some areas as DataUtilties had more than five methods in its documentation, so we were unsure whether we were meant to do them all, include overloaded methods just once, or test them all.

