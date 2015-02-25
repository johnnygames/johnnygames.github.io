---
layout: post
title: The Name is Lists, Linked-Lists
feature-img: "img/sample_feature_img.png"
excerpt: You're in it now, the real nitty gritty of data structures, that good good. Let's move beyond that stack and queue bullshit and get down to business with a REAL data structure.
---

###Overview

Linked-lists store collections of data much like an array would do. What differentiates linked-lists from general arrays is how the computer fetches the values located within the collection. This is primarily due to the way a linked-list is structured. Generally speaking, there is a head and a tail to a linked-list, and each 'node' in the linked-list points to another 'node', thus created a method of traversal. As an example, if I add three values (a, b, c) to the tail of the linked-list with 'a' going first, 'b' second, and 'c' third, the pointer attached to the 'b' node would point to 'a' and the pointer attached to 'c' node would point to 'b'.

###Why?

I know what you're thinking, who really cares about linked-lists? Don't arrays already store collections of elements or values, why would I need to implement something that's not already built in to my language of choice? Well, that's a pretty damn good point, there are probably not going to be a huge number of situations where you will need to use a linked-list. However, if you are in the mood to get a job then you might want to pick up a thing or two about linked-lists, their benefits and drawbacks, their time and space complexity, and maybe even how to implement one. This would really benefit anyone going into a software engineering interview, as the linked-list is a staple in many 'Data Structures and Algorithms' courses and interviews.

###Nodes

Each piece of a linked-list is made up of a node, this node will be implemented using a traditional Javascript object that holds both a value and a reference to the connection node (or nodes). Now, I say that a node may reference more than one other node because in a doubly linked-list each node has a reference to the node 'behind' it and the one in 'front' of it.

This is a perfect time to introduce one of the benefits of a linked-list. In a traditional array, the memory that is allocated for positions must be contiguous. Each place in memory must be right next to the other and if that general allocation grew too large (which is possible when arrays are dynamically sized) that whole array must be move to where it can be placed contiguously. In comparison, a linked-list can be 'disjointed' in the sense that each individual node can be placed separately from the other within memory because each node has a reference to the connecting nodes. 

###Implementation

You know the drill! Let's code this sucker all pseudoclassical like. First things first, this is our basic constructor that will be used to instantiate a new linked-list. A quick note on the convetion, the underscore is used to show that things should be left alone and not accessed by force.

{% highlight js %}

var LinkedList = function() {
  this._head = null;
  this._tail = null;
  this._length = 0;

};

{% endhighlight %}

The method that we are creating below is going to be used in adding nodes to our linked-list. Our node will have a value and references to two other nodes. Also note that the value is passed in as an argument.

{% highlight js %}

LinkedList.prototype._makeNode = function (value) {
    var node = {
      value: value,
      next: null,
      prev: null
    };
    return node;
  };

{% endhighlight %}

This next method utilizes the _makeNode method to add a method to the tail of the linked-list. If the list happens to be empty (checked in the first 'if' statement) then the node that is added is both the head and tail of the linked-list.

{% highlight js %}

LinkedList.prototype.addToTail = function (value) {
    var node = this._makeNode(value);
    if (this._length === 0) {
      this._head = node;
      this._tail = node;
    } else {
      this._tail.next = node;
      node.prev = this._tail;
      this._tail = node;
    }
    this._length++;
    return node;
  };

{% endhighlight %}

This method will add a node to the head of the linked-list. We are really focusing on DRY principles here and if the linked-list is empty we are essentially doing the same as addToTail so we utilize that.

{% highlight js %}

LinkedList.prototype.addToHead = function (value) {
  var node = this._makeNewNode(value);
  if (this._length === 0) {
    this.addToTail(value);
    return;
  } else {
    this._head.prev = node;
    node.next = this._head;
    this._head = node;
  }
  this._length++;
  return node;
};

{% endhighlight %}

This next method utilizes a 'while' loop to iterate through each node in the linked-list will return true if the value is held within one of the nodes. 

{% highlight js %}

LinkedList.prototype.search = function (value) {
  var currentNode = this._head;
  while (currentNode) {
    if (currentNode.value === value) {
      return true;
    }
    currentNode = currentNode.next;
  }
  return false;
};

{% endhighlight %}

###Time Complexity

The time complexity of using the addToTail or addToHead methods will O(1) or constant time. Comparatively, searching through a linked-list for a certain value is O(n) or linear time.