<h1>Hashing</h1>
<h2>What is hashing</h2>
<ul>
  <li>
    Hashing is basically a technique used to find out frequency of a given query
    from a given array.
  </li>
  <li>
    The given array can be either an array of numbers or a string of characters.
  </li>
</ul>

<!-- Number Hashing -->
<h1>Number Hashing</h1>
<h2>Brute-Force Approach</h2>
<ul>
  <li>
    In Brute-Force approach we just create a function containing a 'counter'
    variable and a for-loop which iterates over the given array and updates the
    counter variable when it locates the query everytime.
  </li>
  <li>
    The iteration stops at the terminating condition -> if index exceeds number
    of elements, and returns the final counter value.
  </li>
  <li>
    This approach works well, but its time complexity increases with the number
    of queries. For example, 10<sup>8</sup> queries take ~1 second, but 10<sup
      >10</sup
    >
    would take ~100 seconds, making it inefficient and time-taking, which is why
    we have to move towards an optimized approach i.e, <b>Hashing</b>.
  </li>
</ul>

<h2>How Hashing works?</h2>
<p>Hashing takes place in three main steps:</p>
<li>Input - Here we take the main array as input</li>
<li>Main Process - Here the actual logic of hashing is used</li>
<li>Output - Here we give out queries and get the output</li>

<ul>
  <li>
    The input is taken in the form of an array, which can be a string or a list
    of numbers.
  </li>
  <li>
    In the main process, we create a hash array and initialize it to 0, meaning all the values initially in the array would be 0. 
    Then we iterate through the input array and increment the value of the hash array at the index of the current element by 1.
    This will create a frequency table of the elements in the input array, meaning at the index of each element in the hash array, we will have the count of that element in the input array.
  </li>
    <li>
        Finally, we can query the hash array to get the frequency of any element in
        O(1) time complexity, which is very efficient compared to the brute-force
        approach.
</ul>

<!-- Character Hashing -->
<h1>Character Hashing</h1>
<ul>
  <li>Character Hashing is similar to Number Hashing, in number hashing, we were mapping the elements of input array to the indices of the hash array. So in the case of character hashing, we have to somehow associate the characters of the input string to an integer which can later be mapped to the indices of hash array.</li>
  <li>
    We can do this by using the ASCII values of the characters, which are unique
    for each character. For example, the ASCII value of 'a' is 97, 'b' is 98,
    and so on.
  </li>
  <li>There are three main cases that we must look into.</li>
    <ul>
      <li><b>Case 1: All characters of input string are in lowercase</b></li>
      <ul>
        <li>
          In this case, we can just subtract the ASCII value of the character from the ASCII value of 'a' (97) to get the index of the hash array.
          For example, for 'h', the index would be 104 - 97 = 7, so we would increment the value at index 7 of the hash array by 1 and so on for all characters.
        </li>
      </ul>
      <li><b>Case 2: All characters of input string are in uppercase</b></li>
       <ul>
        <li>
        When all the characters of the input string are in uppercase, we can subtract the ASCII value of the character from the ASCII value of 'A' (65) to get the index of the hash array.
        </li>
      </ul>
      <li><b>Case 3: Mixed case characters in input string</b></li>
      <ul>
        <li>
          In this case, we have a total of 256 characters, hence we can use the ASCII value of the character directly to get the index of the hash array. 
          For example, for 'h', the index would be 104, so we would increment the value at index 104 of the hash array by 1 and so on for all characters.
        </li>
    </ul>
</ul>
</ul>
<strong>
  The third approach can be applied to the other two as well, making it generally the most optimal choice.
</strong> 
