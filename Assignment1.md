# INF502 HW1
```python  
#Question 1: 
import math
def pythagoreanTheorem(length_a, length_b):
 hypotenuse_square = math.pow(length_a,2)+math.pow(length_b,2)
 hypotenuse = math.sqrt(hypotenuse_square )
 return hypotenuse
>>> hytenuse1_len = pythagoreanTheorem (1,1)
>>> print (hytenuse1_len)
1.4142135623730951
>>> hytenuse2_len = pythagoreanTheorem (3,4)
>>> print (hytenuse2_len)
5.0
>>> hytenuse3_len = pythagoreanTheorem (9,16)
>>> print (hytenuse3_len)
18.35755975068582

#Question 2
def list_mangler(list_in):
    for element in list_in:
      if element%2==0:
       new_element = element **2
      else:
        new_element = element **3
      newlist.append(new_element)
    print (newlist)
>>> newlist = []
>>> list_mangler ([1,2,3,4])
[1, 4, 27, 16]
>>> newlist = []
>>> list_mangler ([5,6,7,8])
[125, 36, 343, 64]
>>> newlist = []
>>> list_mangler ([9,0,3,4])
[729, 0, 27, 16]
## description: 
#  if element devided by 2 remainder is 0,it's even and be squrared by multiplying element by itself 2 times. 
#  if it is not even, it is odd and it will be tripled by multiplying element by element 3 times by ** operator. 
#  for each element, we calculate new_element
#  Finally, append to append each calculate new_element to the newlist

## Question 3
def grade_calc(grades_in, to_drop):
    grades_in.sort(reverse=True)
    #print(grades_in)
    Length = len(grades_in) - to_drop
    avg = 0
    summation = 0
    for grades in range(Length):
        summation = summation + grades_in[grades]
    avg = summation / Length
    #print(avg)
    if avg >= 90:
        return "A"
    elif avg >= 80:
        return "B"
    elif avg >= 70:
        return "C"
    else:
        return "F"
>>> result = grade_calc([100, 90, 80, 95], 2)
>>> print(result)
A
>>> result = grade_calc([72, 72, 83, 60, 83], 3)
>>> print(result)
B
>>> result = grade_calc([76, 60, 70, 75], 2)
>>> print(result)
C
## description
# first we sort the list elements from higher to lower,
#then we sum the elements until the element before to-drop. 
# Finally, we use if else conditons test for finding the letter grade

## Question 4
def odd_even_filter(numbers):
  sublist1, sublist2, lst = [], [], []
  for element in numbers:
    if element %2 ==0:
      sublist1.append(element)
    else:
      sublist2.append(element)
  lst.append(sublist1)
  lst.append(sublist2)
  print (lst)
  
>>> odd_even_filter([1,2,3,4,5,6,7,8,9])
[[2, 4, 6, 8], [1, 3, 5, 7, 9]]
>>> odd_even_filter([11,17,89,43,56,67,72,8,9])
[[56, 72, 8], [11, 17, 89, 43, 67, 9]]
>>> odd_even_filter([11,17,89,43,555,490])
[[490], [11, 17, 89, 43, 555]]

##description:
# if element devided by 2 remainder is 0,it's even, so we append it to the sublist1 that included even number
# if it is not even, it is odd, so we append it to the sublist2 that includes odd numbers
# Finally, we append sublist1 and 2 to the lst, respectively
