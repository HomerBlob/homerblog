---
layout: post
title: "List reverse"
date: 2018-01-29 01:00:00
categories: algorithms
---

# Problem

There is list with elements sequence \\(\mathbf{x}\_{1},\mathbf{x}\_{2},...,\mathbf{x}\_{n-1},\mathbf{x}\_{n}\\) and you want to change list elements order to \\(\mathbf{x}\_{n},\mathbf{x}\_{n-1},...,\mathbf{x}\_{2},\mathbf{x}\_{1}\\). So, you have to use current algorithm.

<!--description-->

# Discussion

Let's start with algorithm implementations.

#### With recursion

{% highlight C++ linenos %}
node* reverse_impl(node* prev, node* next) {
  node* res = NULL;

  if (next != NULL) {
    res = reverse_impl(next, next->next);
    next->next = prev;
  }
  else {
    res = prev;
  }

  return res;
}

node* reverse(node* list) {
  node* res = NULL;

  if (list != NULL) {
    res = reverse_impl(list, list->next);
    list->next = NULL;
  }

  return res;
}
{% endhighlight %}

Memory cost \\(\theta(n)\\)<br/>
Complexity \\(\theta(n)\\)

#### Without recursion

{% highlight C++ linenos %}
node* reverse(node* list) {
    node* prev = NULL;
    node* tmp = NULL;
    node* cur = list;

    if (cur != NULL && cur->next != NULL) {
        prev = cur;
        cur = cur->next;

        while (cur->next != NULL) {
            tmp = cur->next;
            cur->next = prev;
            prev = cur;
            cur = tmp;
        }

        cur->next = prev;
        list->next = NULL;
    }

    return cur;
}
{% endhighlight %}

Memory cost \\(\theta(1)\\)<br/>
Complexity \\(\theta(n)\\)

# Conclusion

Just use algorithm implementation without recursion.<br/>
See full code example [here](https://github.com/kofev/algorithms).
