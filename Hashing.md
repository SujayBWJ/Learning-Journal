<h1>Hashing</h1>
<h2>What is Hashing?</h2>
<ul>
  <li>Hashing is a technique to find the frequency of a given query (element or character) in a given array or string.</li>
  <li>The array can be numeric or character-based.</li>
</ul>

<h2>Why Brute Force Fails</h2>
<ul>
  <li>Iterates the entire array for every query using a counter.</li>
  <li>Efficient for few queries but becomes slow for large numbers of queries (e.g., 10<sup>10</sup> queries would take ~100 seconds).</li>
  <li>Hence, we shift to hashing.</li>
</ul>

<h2>How Hashing Works</h2>
<ul>
  <li><b>Input:</b> Accept an array of elements (numbers or characters).</li>
  <li><b>Main Process:</b> Create a hash array (or map) and iterate through the input to populate frequencies.</li>
  <li><b>Output:</b> Respond to queries in O(1) time using precomputed hash/map data.</li>
</ul>

<h1>Character Hashing</h1>
<ul>
  <li>Characters must be mapped to an index for hashing.</li>
  <li>This can be done using ASCII values.</li>
  <li>
    <b>Case 1 (lowercase only):</b> Index = ASCII(char) - ASCII('a')
  </li>
  <li>
    <b>Case 2 (uppercase only):</b> Index = ASCII(char) - ASCII('A')
  </li>
  <li>
    <b>Case 3 (mixed case or special chars):</b> Use ASCII(char) directly → Max 256 size array.
  </li>
  <li><b>Note:</b> Third case works for all → often preferred.</li>
</ul>

<h2>Limitations of Array Hashing</h2>
<ul>
  <li>If elements are large (e.g., 10<sup>9</sup>), array size becomes impractical.</li>
  <li>So we use <b>maps</b> (from STL in C++) to hash efficiently even with large keys.</li>
</ul>

<h1>Map vs Unordered Map in C++</h1>
<h2>Map</h2>
<ul>
  <li>Syntax: <code>map&lt;key, value&gt;</code></li>
  <li>Stores keys in <b>sorted order</b>.</li>
  <li>Time Complexity per operation (insert/retrieve/delete): <b>O(log N)</b></li>
  <li>Total for N operations: <b>O(N log N)</b></li>
</ul>

<h2>Unordered Map</h2>
<ul>
  <li>Syntax: <code>unordered_map&lt;key, value&gt;</code></li>
  <li>No specific order of keys.</li>
  <li>Average case time per operation: <b>O(1)</b></li>
  <li>Total time for N operations: <b>O(N)</b></li>
  <li><b>Worst case:</b> Due to collisions, each op may take O(N), leading to total <b>O(N<sup>2</sup>)</b>.</li>
  <li>Worst case is <b>very rare</b>, occurs only with poor hash functions or malicious input.</li>
</ul>

<h2>Choosing Between Map and Unordered Map</h2>
<ul>
  <li>Default to <b>unordered_map</b> for speed.</li>
  <li>If it gives TLE (Time Limit Exceeded), switch to <b>map</b> for guaranteed O(log N) stability.</li>
</ul>

<h2>Example</h2>
<p>For array: [1, 2, 3, 1, 3, 2, 12]</p>
<ul>
  <li><b>Map:</b> Requires only 4 units of space for 4 unique elements.</li>
  <li><b>Array hashing:</b> Requires array size of 13 (largest element + 1).</li>
</ul>

<pre><code>// C++ Example:
map<int, int> mp;
for (int i = 0; i < n; i++) {
    mp[arr[i]]++;
}

int q;
cin >> q;
while (q--) {
    int num;
    cin >> num;
    cout << mp[num] << endl;
}
</code></pre>

<p><b>Note:</b> Accessing a non-existing key in C++ map gives 0 by default.</p>
