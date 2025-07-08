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
<p>The worst case scenario of unordered_map occurs when there is a case of collision, and for understanding the collision we must umderstand the concept of <b>DIVISION METHOD</b>.</p>
<h1>Division Method in Hashing</h1>

<h2>Why We Use Division Method</h2>
<ul>
  <li>We use <code>unordered_map</code> by default for speed.</li>
  <li>If it gives a TLE (Time Limit Exceeded), then we fall back to <code>map</code>.</li>
</ul>

<h2>Hashing Techniques</h2>
<ul>
  <li>Hashing can be done using several methods:
    <ul>
      <li>Division method (most used)</li>
      <li>Folding method (mostly academic)</li>
      <li>Mid-square method (mostly academic)</li>
    </ul>
  </li>
</ul>

<h2>What is Division Method?</h2>
<ul>
  <li>Used when you can’t afford to create a large array for direct hashing.</li>
  <li>Example array: [2, 5, 16, 28, 139]</li>
  <li>To store this via array hashing, you'd need an array of size 140.</li>
  <li>But if you're given a constraint (e.g., size ≤ 10), use: <code>arr[i] % 10</code> to reduce size.</li>
</ul>

<h2>Steps in Division Method</h2>
<ul>
  <li><b>Pre-storing:</b> <code>hash[arr[i] % 10]++;</code></li>
  <li><b>Fetching:</b> <code>hash[num % 10];</code></li>
</ul>

<h2>Example Hash Table (After Division)</h2>
<pre>
Index : 0 1 2 3 4 5 6 7 8 9
Count : 0 0 1 0 0 1 1 0 1 1
</pre>
<p>→ We reduced the element range using modulo and stored frequency compactly.</p>

<h2>When This Logic Fails</h2>
<ul>
  <li>If 18 occurs twice, we can't distinguish it from other elements that give the same remainder.</li>
  <li>This breaks the assumption: <code>freq(18) == freq(hash[8])</code>.</li>
</ul>

<h2>Solution: Linear Chaining</h2>
<ul>
  <li>We create chains (using linked lists or vectors) for each hash index.</li>
  <li>Each element is inserted into <code>hash[key % size]</code> as a list.</li>
  <li>Sorted order is optional, but storing original values is necessary.</li>
</ul>

<h2>Example for Linear Chaining</h2>
<p>Array: [2, 5, 16, 28, 139, 38, 48, 28, 18]</p>
<ul>
  <li>All values with same unit digit (8) are stored in <code>hash[8]</code> chain.</li>
</ul>

<h2>Hash Table After Chaining</h2>
<pre>
Index : Value
0     : 
1     : 
2     : 
3     : 
4     : 
5     : 
6     : 
7     : 
8     : 18 → 28 → 28 → 38 → 48
9     : 
</pre>

<h2>Fetching Frequency with Chaining</h2>
<ul>
  <li>Go to <code>hash[num % 10]</code> → this gives the right chain.</li>
  <li>Traverse that chain and count occurrences of the target number.</li>
</ul>

<h1>Collision in Hashing</h1>

<h2>What is Collision?</h2>
<ul>
  <li>Occurs when two or more elements map to the same hash index.</li>
  <li>Even 2 keys colliding is a collision.</li>
  <li>Expected in hashing, but becomes a problem when many values collide into one index.</li>
</ul>

<h2>Worst Case</h2>
<ul>
  <li>If all N elements map to the same index → Time Complexity becomes O(N).</li>
  <li>This is the worst-case scenario for unordered_map.</li>
</ul>

<h2>When Does Collision Happen?</h2>
<ul>
  <li>Hash function is poor (e.g., <code>x % 10</code> for large patterns).</li>
  <li>Input data is patterned or adversarial (crafted to cause collisions).</li>
  <li>Even though <code>unordered_map</code> tries to rehash and resize, it can't always avoid this.</li>
</ul>

<h2>Note</h2>
<ul>
  <li>Only basic data types like int, double, string are allowed as keys in <code>unordered_map</code>.</li>
  <li>To use complex keys like <code>pair&lt;int, int&gt;</code>, you must use <code>map</code> or write a custom hash.</li>
</ul>

