# [8-puzzle](https://tsotnezarandia.github.io/8-puzzle)

![puzzle](https://tsotnezarandia.github.io/8-puzzle/8-puzzle.png)

**რვიანი**-_ს ამონახსნის პოვნა ძებნის ალგორითმის საშუალებით_

## A ალგორითმის რეალიზაცია

```javascript
function A(state) {
  var closed = []; // განხილული კვანძების სია
  var opened = [ // შესაძლო კვანძთა გზები
    [state] // საწყისი მდგომარეობა
  ];

  // ------------------------------------------------------------

  function g(n) {
    return n.length; // გავლილი გზის წონა საწყისი კვანძიდან
  }

  function h(n, m = goal) {
    var d = 0; // ევრისტიკა - გზის ფასი მოცემული კვანძიდან
    for (var i = 0; i < n.length; i++) // მიზნის კვანძამდე
      if (n[i] != m[i])
        d++; // სხვის ადგილზე მყოფი უჯრედების რაოდენობა
    return d;
  }

  function f(n) {
    var node = n[n.length - 1];
    return g(n) + h(node); // ოპტიმალური ამონახსნი
  }

  function enqueue() {
    opened.sort(function(a, b) {
      return f(a) - f(b); // კვანძების მოწესრიგება
    });
  }

  // ------------------------------------------------------------

  while (opened.length > 0) {
    var node_list = opened.shift(); // შესაძლო "საუკეთესო" გზის
    var node = node_list[node_list.length - 1]; // ბოლო კვანძი
    if (includes(node))
      continue; // კვანძი აქამდე განხილულია
    if (h(node) == 0)
      return node_list; // ამონახსნი - "საუკეთესო" გზა
    closed.push(node); // კვანძი განხილულია
    var nodes = successors(node); // შესაძლო გადასვლები
    for (var i = 0; i < nodes.length; i++) {
      var n = node_list.slice();
      n.push(nodes[i]); // გზაში გადასვლის დამატება
      opened.push(n); // სიაში გზის დამატება
    }
    enqueue(); // გზების მოწესრიგება - "საუკეთესო" გზა თავშია
  }

  // ------------------------------------------------------------

  return null; // ამონახსნი ვერ მოიძებნა
}
```

### ლიცენზია

**© 2021 [Tsotne Zarandia](https://github.com/tsotnezarandia)**

[//]: # "LINKS"
