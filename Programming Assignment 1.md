# INF 502 - PA1 -  Implementing the Similarity algorithm 
## Descriptionof of  solution approach:
  * Read the assignment, start thinking about it and write everything I understand like inputs (user, file), outputs (shifted strings, maximum values), algorithm requirements. What function or modules? What are the main concepts or real things to be considered as class? 
  * Then I started thinking object oriented more deeply!What are the clear methods and attributes for the class of sequence? Length, Shift (I don’t remember the other things that I thought about)
  * What functions: Clearly two similarity functions for “number of matches” and “maximum contiguous chain” 
    * compare_score function (number of matches: calculate the maximum score):
 inputs: sequences	
 Output: score (matches #)
 How: using a loop to traverse the strings separately to calculate matches 
 
    * compare_contiguous function (calculate the size of the maximum contiguous chain that matches the sequences (score)):
Inputs: seqs
Output: contiguous
How: with the loop used for the first similarity function and using if: the last time that characters are matched, if previous index and current index differences is one, they are in chain and we add the contiguous number

    * make_sequence function 
        Which Generate a seq from file

    * Main:
      * took all the user defined inputs (which approach, name of files)
       * Calling make_sequence function
       * Outer loop: we consider both shifting the first and second sequence. Inner  loop for shifting from 0 to max_shift+1: ( sequences is shifted by one place and compared with the other one. then shifted two, and ...)
       * We use the shift method for generation the shifted sequences.We compute the score with compare_score. Using Compare_score to find the matches. We store each score (for each shift)  in the list scores. If we see the score is higher than previous scores, we update the sequences that should be printed to the sequences that resulted on that score. We use the same process to capture the max of contiguous and the related shifted sequences

  * At the final step, I test my code thoroughly for catching all exceptions
    * ValueError
    * using example sequences with different length
    * squences included wrong characters (whether all the characters are neucliotides or not)
## Source code
```python
# In[1]:

import os
import sys

# In[2]:

class Sequence:
    def __init__(self, seq):
        self.seq = seq
        for w in seq:
            if not w in ['A', 'T', 'G', 'C']:
                raise Exception(
                    'sequences included wrong characters (which are ATGC)')

    def shift(self, to: 'left' or 'right', length=1):
        if to == 'left':
            return self.seq + ''.join(['-' for i in range(length)])
        elif to == 'right':
            return ''.join(['-' for i in range(length)]) + self.seq
        else:
            raise Exception('action was not detected.')

# In[3]:

def make_sequence(path):
    try:
        with open(path, 'r') as f:
            return Sequence(f.readline().strip())
    except FileNotFoundError:
        print('Error: FileNotFoundError')
    except FileExistsError:
        print('Error: FileExistsError')

# In[4]:

def compare_score(seq1, seq2):
    assert len(seq1) == len(seq2), 'Sequences should have the same length.'

    score = 0
    for i in range(len(seq1)):
        if (seq1[i] == seq2[i]) and (not seq1[i] == '-') and (not seq2[i] == '-'):
            score += 1

    return score


# In[5]:


def compare_contiguous(seq1, seq2):
    assert len(seq1) == len(seq2), 'Sequences should have the same length.'

    count = 0
    index = -2
    contiguous = [0]
    for i in range(len(seq1)):
        if (seq1[i] == seq2[i]) and (not seq1[i] == '-') and (not seq2[i] == '-'):
            if index+1 == i:
                count += 1
            else:
                count = 1
            contiguous.append(count)
            index = i

    return max(contiguous)


# In[6]


try:
    print('Welcome to PA1')
    print('------------------------')

    while True:
        print('1. print scores only')
        print('2. print Max contiguous')
        print('3. Exit program')
        print()

        choose = input('Enter your choose: ')
        if choose == '3':
            break

        sequence1 = make_sequence(input('Enter first sequence file path: '))
        sequence2 = make_sequence(input('Enter second sequence file path: '))

        # may have ValueError exception (catches on line 134)
        max_shift = int(input('Enter maximum shift: '))

        assert max_shift < len(
            sequence1.seq) and max_shift < len(sequence2.seq)

        scores = []
        contigs = []
        sequences = []
        for action in [True, False]:
            for i in range(max_shift+1):
                shifted_seq1 = sequence1.shift(
                    'left' if action else 'right', i)
                shifted_seq2 = sequence2.shift(
                    'right' if action else 'left', i)

                # print('\nSEQUENCE 1 -> {}'.format(' '.join(shifted_seq1)))
                # print('SEQUENCE 2 -> {}'.format(' '.join(shifted_seq2)))
                if choose == '1':
                    score = compare_score(shifted_seq1, shifted_seq2)
                    # print('score is {}'.format(score))
                    scores.append(score)
                    if score >= max(scores):
                        sequences = [shifted_seq1, shifted_seq2]
                elif choose == '2':
                    contiguous = compare_contiguous(shifted_seq1, shifted_seq2)
                    # print('contiguous for this setting is: {}'.format(contiguous))
                    contigs.append(contiguous)
                    if contiguous >= max(contigs):
                        sequences = [shifted_seq1, shifted_seq2]

        if choose == '1':
            print('\nmax score is {}'.format(max(scores)))
            print('SEQUENCE 1 -> {}'.format(' '.join(sequences[0])))
            print('SEQUENCE 2 -> {}'.format(' '.join(sequences[1])))
        elif choose == '2':
            print('\nmax contiguous is {}'.format(max(contigs)))
            print('SEQUENCE 1 -> {}'.format(' '.join(sequences[0])))
            print('SEQUENCE 2 -> {}'.format(' '.join(sequences[1])))

except Exception as Error:
    print(Error)
except ValueError:
    print('Error: ValueError occurred')
```
## results
###   Approach-1

```sh
    * Result 1
Enter your choose: 1
Enter first sequence file path: s1.txt
Enter second sequence file path: s2.txt
Enter maximum shift: 6

max score is 3
SEQUENCE 1 -> - - - - A C T G A C T T T T
SEQUENCE 2 -> T T T A G C C G A T - - - -

    * Result 2 (wrong file)
Enter your choose: 1
Enter first sequence file path: s1
Error: FileNotFoundError
Enter second sequence file path: s3
Error: FileNotFoundError

    * Result 3 (exception: not equal length)
Enter your choose: 1
Enter first sequence file path: s1.txt
Enter second sequence file path: s4.txt
Enter maximum shift: 5
Sequences should have the same length.

    * Result 3 (exception: not ATGC)
Enter your choose: 1
Enter first sequence file path: s1.txt
Enter second sequence file path: s6.txt

sequences included wrong characters (which are ATGC)
------------------------------------------------------------------------------------------------
```
### Approach-2
```sh
    * Result 
1. print scores only
2. print Max contiguous
3. Exit program
Enter your choose: 2
Enter first sequence file path: s1.txt
Enter second sequence file path: s2.txt
Enter maximum shift: 5

max contiguous is 2
SEQUENCE 1 -> - - - - A C T G A C T T T T
SEQUENCE 2 -> T T T A G C C G A T - - - -
```
## Used Sequences
[I used the example you provided](https://github.com/igorsteinmacher/INF502-Fall2020/tree/master/assignments/examplesPA1/ex02). I just changed the names in this way: Seq1.txt >> S1.txt, Seq2.txt >> S2.txt, Seq4.txt >> S4.txt, Seq6.txt >> S6.tx
## benefits, hurdles, handling
The hardest part in coding was OO programming and defining the method shift for the class
  * Number of Matches Approach:
    * hurdles:
The hurdle I faced was how to shift both sequences and also faced problems in printing the output. 
     * How handeled:
Drinking more coffee helped or was a prerequisite to use OO programming and handling hurdles. Speaking loud to myself about what I was doing also helped!
Searching internet, talking with classmates
Visual examples helped to understand the problem and requirements better.
    * Benefits:
developing first approach made much more clear what should I do in the second approach (throughout the process of developing approach 1)
Developing the algorithm and designing the process help me to improve my programming skills. 

  * Maximum Chain:
    * hurdle:
updating of the contiguous match and design this contiguous match algorithm
    * How handeled: 
 Visual examples helped to understand the problem and requirements better.
 discussing with my  gropupmates and other professional
    * Benefit
This approach  enriches my python skills, and also algorithm skills
