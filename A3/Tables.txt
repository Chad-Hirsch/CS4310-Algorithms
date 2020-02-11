### How Many Tables
### Class: CS4310
### By: Chad Hirsch
### Using Python3

import sys

def getKey(tuple):
    if tuple[0] >= tuple[1]:
        return tuple[1]
    return tuple[0]

if __name__ == "__main__":
    if sys.version_info[0] >= 3:
        file = input('Enter file name: ')
    else:
        file = raw_input('Enter file name: ')

    with open(file) as f:
        input = [tuple(map(int, i.split(' '))) for i in f]

    #sorting takes O(nlogn)
    input = sorted(input[1:], key=getKey)
    print(input)
    tables = []

    i = 0
    # iterating through the input list takes O(n * g)
    # where g is the number of sets in tables list
    while i < len(input):
        (n1, n2) = input[i]
        
        added = False

        # checking if n1 or n2 is already in a set takes O(g)
        for s in tables:

            # checking if n1 or n2 are in a set takes O(1)
            if n2 in s:
                s.add(n1)
                added = True
                break
            elif n1 in s:
                s.add(n2)
                added = True
                break

        if added == False:
            tables.append(set([n1,n2]))

        i += 1

    if len(tables) == 1:
        print('At least 1 table is needed')
		
    else:
        print('At least ' + str(len(tables)) + ' tables are needed')
		
		
	
