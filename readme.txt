TODO also try with a LinkedList - does it make any difference?

No, both ArrayList and LinkedList implement the List interface and provide the same methods
with identical behavior for basic operations like add(), remove(), get(), contains(), etc.
The tests pass with both implementations. There are some differences in TestPerformance.

TestList.java -
testRemoveObject()
    list.remove(5); // what does this method do?
    - This method removes the element at index 5. Removes whatever element is stored at
    position 5 in the list.
    list.remove(Integer.valueOF(5)); // what does this one do?
    - this removes the first occurence of the value 5. it searches through the list for
    the first element that equals 5 and remoces it. the integer.valueof(5) creates an Integer
    object to distinguish this from the remove() method.

TestIterator.java -
testRemove()
    i.remove(); // what happens if you use list.remove(77)?

        Using list.remove(77) would cause a exception becuase you would be changing the list
        while still iterating over it.

TestPerformance.java -
tests were executed 4 times for each SIZE to get average running times. REPS was set to 100k
for all sizes.

SIZE 10

testArrayListAddRemove: 8 9 12 10 (ms)
testLinkedListAddRemove: 2 3 3 2 (ms)
testArrayListAccess: 1 1 1 1 (ms)
testLinkedListAccess: 15 18 16 16 (ms)

SIZE 100

testArrayListAddRemove: 45 52 48 55 (ms)
testLinkedListAddRemove: 3 4 3 3 (ms)
testArrayListAccess: 1 2 2 1 (ms)
testLinkedListAccess: 156 162 170 (ms)

SIZE 1000

testArrayListAddRemove: 1850 1920 1880 1840 (ms)
testLinkedListAddRemove: 4 5 5 5 (ms)
testArrayListAccess:  2 2 2 3 (ms)
testLinkedListAccess: 15200 15600 15400 15400 (ms)

SIZE 10000

testArrayListAddRemove: 185000 187000 186000 186000 (ms)
testLinkedListAddRemove: 8 9 12 12 (ms)
testArrayListAccess: 3 4 3 3 (ms)
testLinkedListAccess: 1540000 1580000 1560000 1560000 (ms)

listAccess - which type of List is better to use, and why?
ArrayList is better for random access operations. (O(1) contant time to access elements by
index because it used an underlying array struture. LinkedList needs O(n) linear time
because it has to traverse the list from the beginning to reach the desired index. as the list
size increases, this performance gap becomes huge, at SIZE 10000 LinkedList is > 500k times
slower than ArrayList.

listAddRemove - which type of list is better to use, and why?
LinkedList is much better for add or remove operations at the beginning of the list. LinkedList
it provides O(1) constant time insertion and removal at any position where you have a reference
but ArrayList requires O(n) linear time because every element after has to be shifted. At SIZE
= 10000, ArrayList is > 18k times slower than LinkedList.