# Bash solution for day 1 problem 1

## Summary of the problem

- 2 Teams are searching for the locations where the Chief Historian might be.
- Each location has a 'location ID'.
- 2 Groups trying to make a complete list of 'location ID'.
- The two lists are not similar.
- Pair the smallest 'location ID' from the left with the smallest 'location ID' from the right
- Measure the distance (difference) between each 'location ID' pair.
- Measure the total aggregate distance between all 'location ID' pairs.

# inputs

A text file with the 2 lists is presented in the following format

```text
18944   47230
94847   63037
93893   35622
```

## Steps to solution

1. Separate the numbers in the text file into two lists.
2. Order the numbers in each list from the smallest to the biggest.
3. Measure the distance between each 2 respective numbers.
4. Measure the total of distances.

## Solution

**save the numbers in a text file called input.txt"**

```bash
#!/bin/bash

# Generate an array from the input
list=(`cat input.txt`)

# Save the odd even elements into list.left.txt and the odd elements into list.right.txt
for el in "${!list[@]}"
do
  rem=$((${el} % 2))
  if [[ rem -eq 0 ]]
  then
    echo "${list[$el]}" >> list.left.txt
  else
    echo "${list[$el]}" >> list.right.txt
  fi
done

# Sorting the numbers
sort list.left.txt > list.left.sorted.txt
sort list.right.txt > list.right.sorted.txt

# create arrays from the two files
left=(`cat list.left.sorted.txt`)
right=(`cat list.right.sorted.txt`)

# calculate the difference and save it to a text file.
for ele in "${!left[@]}"
do
  diff=$(("${left[$ele]}"-"${right[$ele]}"))
  if [ $diff -ge 0 ]
  then
    echo "$diff" >> diffs.txt
  else
    diff=$(($diff * -1))
    echo "$diff" >> diffs.txt
  fi
done

# Import the differences as an array
di=(`cat diffs.txt`)

total=0

for elem in ${di[@]}
do
  total=$(($total + $elem))
done
echo "$total"
```
