# Prompt

You are attempting to find the index of the first appearance of one string (the needle) inside of another (the haystack).

# Examples

``` javascript
indexOf('or', 'hello world'); // should return 7
indexOf('hello world', 'or'); // should return -1
indexOf('howdy', 'hello world'); // should return -1
indexOf('oox', 'ooboxoooxo'); // should return 6
```

## Common approaches:

***Built-in methods***

Most students' first instincts will be to use built-in string methods like ```indexOf()```, ```includes()``` or ```substring()```. ```indexOf()``` is, of course, explicitly forbidden; steer them away from methods like ```includes()``` and ```substring()```.

The reason to avoid this is that many whiteboard interviews will be language-agnostic and focus on the underlying concepts. You will want to show that you understand how these methods work, not that you happened to read the right documentation the night before.

Another reason is that by using these methods, you may actually be adding more (hidden) complexity. Look into how ```indexOf()```, ```includes()``` and ```substring()``` work under the hood. Many built-in methods actually add an operation that's O(n), or worse.

***split() and loop***

Most students also move to split the haystack into an array of characters, and then loop through.

This approach would work; but imagine the space complexity of generating a new array and then holding it in memory for a very, very large haystack. You would be introducing another O(n) dimension in time and space, where n is the length of the haystack.

If they're in a groove, have them finish out this approach and pseudocode it; then ask them how they would do this without generating a second copy of the haystack.

That should lead you to the given solution, which uses pointers.

# Solution(s)

```javascript
function indexOf (needle, haystack) {
  for (let hIdx = 0; hIdx <= haystack.length - needle.length; hIdx++) {
    for (let nIdx = 0; nIdx < needle.length; nIdx++) {
      if (haystack[hIdx + nIdx] !== needle[nIdx]) break;
      if (nIdx + 1 === needle.length) return hIdx;
    }
  }
  return -1;
}
```

*Note: where n is the haystack size and m the needle size, the solution above is O(n&#42;m). There are [other algorithms](https://en.wikipedia.org/wiki/String_searching_algorithm#Single_pattern_algorithms), such as [Boyer-Moore](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string_search_algorithm) (well, [modified slightly](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string_search_algorithm#The_Galil_Rule)), that can perform at O(n+m) time—or even faster.*
