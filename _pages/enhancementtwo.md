---
permalink: /enhancementtwo/
title: "Enhancement Two: Algorithm and Data Structures"
modified: 2024-02-27
---

## Bid ID Search Structure Enhancement

The artifact select for the enhancement in the algorithms and data structures category is the Hash Table C++ file for the Bid ID Search Structure assignment in the Data Structures and Algorithms course (CS260). The artifact was originally created in December 2020, consisting of data from CSV files, two C++ files, a C++ header file, and a selection of debug files. The purpose of the assignment was to explore hashing algorithms by implementing a hash with chaining of collisions for bids loaded from a CSV file. Once the C++ project was created and the appropriate compiler was chosen, the storage structure needed to be defined. The options were between an array or a vector for the storage.


### Weaknesses and Limitations

1. The hash table falls short when it comes to ordered data retrieval and operations
2. The hash table's performance generally degrades due to increased collisions.
3. The original code had an outdated declaration head that did not reflect the assignment submitted.


### Original Hash Table File - Highlight of Class Definition

```cpp
//============================================================================
// Hash Table class definition
//============================================================================

/**
 * Define a class containing data members and methods to
 * implement a hash table with chaining.
 */
class HashTable {

private:
    // FIXME (1): Define structures to hold bids
	struct Node {
		Bid bid;
		unsigned key;
		Node* next;

		//default constructor
		Node() {
			key = UINT_MAX;
			next = nullptr;
		}

		//initialize with a bid
		Node(Bid aBid) : Node() {
			bid = aBid;
		}

		//Initialize with a bid and a key
		Node(Bid aBid, unsigned aKey) : Node(aBid) {
			key = aKey;
		}
	};

	vector<Node> nodes;

	unsigned tableSize = DEFAULT_SIZE;

    unsigned int hash(int key);

public:
    HashTable();
    HashTable(unsigned size);
    virtual ~HashTable();
    void Insert(Bid bid);
    void PrintAll();
    void Remove(string bidId);
    Bid Search(string bidId);
};

/**
 * Default constructor
 */
HashTable::HashTable() {
    // FIXME (2): Initialize the structures used to hold bids
	nodes.resize(tableSize);
}

HashTable::HashTable(unsigned size) {
	this->tableSize = size;
	nodes.resize(tableSize);
}

/**
 * Destructor
 */
HashTable::~HashTable() {
    // FIXME (3): Implement logic to free storage when class is destroyed
	nodes.erase(nodes.begin());
}

/**
 * Calculate the hash value of a given key.
 * Note that key is specifically defined as
 * unsigned int to prevent undefined results
 * of a negative list index.
 *
 * @param key The key to hash
 * @return The calculated hash
 */
unsigned int HashTable::hash(int key) {
    // FIXME (4): Implement logic to calculate a hash value
	return key % tableSize;
}

/**
 * Insert a bid
 *
 * @param bid The bid to insert
 */
void HashTable::Insert(Bid bid) {
    // FIXME (5): Implement logic to insert a bid

	//calculate the key for this bid
	unsigned key = hash(atoi(bid.bidId.c_str()));

	//Try and retrieve node using the key
	Node* oldNode = &(nodes.at(key));

	//if no entry for this key
	if (oldNode == nullptr) {
		Node* newNode = new Node(bid, key);
		nodes.insert(nodes.begin() + key, (*newNode));
	} else {
		// node found
		if (oldNode->key == UINT_MAX) {
			oldNode->key = key;
			oldNode->bid = bid;
			oldNode->next = nullptr;
		} else {
			//find the next open node (last one)
			while (oldNode->next != nullptr) {
				oldNode = oldNode->next;

			}

			oldNode->next = new Node(bid, key);
		}
	}
}

/**
 * Print all bids
 */
void HashTable::PrintAll() {
    // FIXME (6): Implement logic to print all bids
	for (int i = 0; i < nodes.size(); ++i) {
		displayBid(nodes[i].bid);
	}
}

/**
 * Remove a bid
 *
 * @param bidId The bid id to search for
 */
void HashTable::Remove(string bidId) {
    // FIXME (7): Implement logic to remove a bid
	unsigned key = hash(atoi(bidId.c_str()));
	nodes.erase(nodes.begin() + key);
}

/**
 * Search for the specified bidId
 *
 * @param bidId The bid id to search for
 */
Bid HashTable::Search(string bidId) {
    Bid bid;

    // FIXME (8): Implement logic to search for and return a bid
    //calculate the key for this bid
	unsigned key = hash(atoi(bid.bidId.c_str()));

	//try and retrieve node using the key
	Node* node = &(nodes.at(key));

	//if not entry found
	if (node == nullptr || node->key == UINT_MAX) {
		return bid;

	}

	//if node found that matches key
	if (node != nullptr && node->key != UINT_MAX
			&& node->bid.bidId.compare(bidId) == 0) {
		return node->bid;

	}

	//walk the linked list to find the match
	while (node != nullptr) {
		if (node->key != UINT_MAX && node->bid.bidId.compare(bidId) == 0) {
			return node->bid;
		}
		node = node->next;
	}

    return bid;
}
```


### Enhancements Made

1.	Created the header declaration for the binary tree C++ file with the binary tree file name.
2.	Created a node structure and defined the class that includes the key, value, and pointers.
3.	Implemented the necessary operations for the balanced binary tree, including insertions, deletions, balancing logic, and range query.
4.	Created the main function section with a display, load, and strDouble function.
5.	Implemented static methods for testing.
6.	Created a header declaration for the CSVparser.cpp file.


The enhancements made to the Hash Table class file, and its associated files, were completely different than the enhancement originally proposed. The original plan consisted of converting the hash table to a distributed hash table (DHT) and integrating a graphical interface. Once the plan was put into motion, it was clear that there would still be limitations to the DHT. The DHT does not maintain an order for easy navigation and queries are generally more complex. Changing the plan to convert the hash table to a balanced binary search tree (BST) allowed for a simpler conversion and ongoing maintenance, and it is well-suited for data structures that consist of dynamic data, or data that changes over time. 


### Enhanced Balanced Binary Search Tree - Highlight of Class Definition

```cpp
//============================================================================
// Binary Search Tree class definition
//============================================================================

/**
 * Define a class containing data members and methods to
 * implement a binary search tree with balancing.
 */
class BSTree {

private:
    struct Node {
        Bid bid;
        Node* left;
        Node* right;

        Node(Bid aBid) : bid(aBid), left(nullptr), right(nullptr) {}
    };

    Node* root;

    void addNode(Node*& node, Bid bid);
    void inOrder(Node* node);
    Node* removeNode(Node* node, string bidId);
    Node* findMin(Node* node);
    Node* search(Node* node, string bidId);
    void rangeQuery(Node* node, string lower, string upper);

public:
    BSTree();
    virtual ~BSTree();
    void Insert(Bid bid);
    void PrintAll();
    void Remove(string bidId);
    Bid Search(string bidId);
    void RangeQuery(string lower, string upper);
};

BSTree::BSTree() : root(nullptr) {}

BSTree::~BSTree() {
    destroyTree(root);
}

// Implementation of destroyTree
void BSTree::destroyTree(Node* node) {
    if (node) {
        destroyTree(node->left);
        destroyTree(node->right);
        delete node;
    }
}

void BSTree::Insert(Bid bid) {
    addNode(root, bid);
}

void BSTree::PrintAll() {
    inOrder(root);
}

Bid BSTree::Search(string bidId) {
    Node* result = search(root, bidId);
    if (result == nullptr) {
        return Bid(); // Empty if not found
    } else {
        return result->bid;
    }
}

void BSTree::Remove(string bidId) {
    root = removeNode(root, bidId);
}

void BSTree::RangeQuery(string lower, string upper) {
    rangeQuery(root, lower, upper);
}

/**
 * Private method to add a node to the tree.
 * @param node Reference to the current node in the tree
 * @param bid The bid to insert
 */
void BSTree::addNode(Node*& node, Bid bid) {
    // If the current node is null, insert the new node here.
    if (node == nullptr) {
        node = new Node(bid);
    }
    // If the bidId of the new bid is less than the current node's bidId, go to the left subtree.
    else if (bid.bidId.compare(node->bid.bidId) < 0) {
        addNode(node->left, bid);
    }
    // If the bidId of the new bid is greater than the current node's bidId, go to the right subtree.
    else {
        addNode(node->right, bid);
    }
}

/**
 * Private method to perform an in-order traversal of the tree.
 * @param node The current node in the traversal
 */
void BSTree::inOrder(Node* node) {
    if (node == nullptr) {
        return;
    }

    // Traverse the left subtree
    inOrder(node->left);

    // Visit the current node (process the current node, e.g., display its bid information)
    displayBid(node->bid);

    // Traverse the right subtree
    inOrder(node->right);
}

/**
 * Private method to remove a node from the tree.
 * @param node The current node in the traversal
 * @param bidId The bid ID of the node to be removed
 * @return The new root of the subtree after removal
 */
BSTree::Node* BSTree::removeNode(Node* node, string bidId) {
    // Base case: The node is not found
    if (node == nullptr) {
        return node;
    }

    // Recur down the tree
    if (bidId < node->bid.bidId) {
        node->left = removeNode(node->left, bidId);
    } else if (bidId > node->bid.bidId) {
        node->right = removeNode(node->right, bidId);
    } else {
        // Node with only one child or no child
        if (node->left == nullptr) {
            Node* temp = node->right;
            delete node;
            return temp;
        } else if (node->right == nullptr) {
            Node* temp = node->left;
            delete node;
            return temp;
        }

        // Node with two children: Get the inorder successor (smallest in the right subtree)
        Node* temp = findMin(node->right);

        // Copy the inorder successor's content to this node
        node->bid = temp->bid;

        // Delete the inorder successor
        node->right = removeNode(node->right, temp->bid.bidId);
    }
    return node;
}

/**
 * Helper method to find the node with the minimum value in a given subtree.
 * @param node The root of the subtree
 * @return The node with the minimum value in the subtree
 */
BSTree::Node* BSTree::findMin(Node* node) {
    Node* current = node;

    // Loop down to find the leftmost leaf
    while (current && current->left != nullptr) {
        current = current->left;
    }

    return current;
}

/**
 * Private method to search for a bid by its bidId.
 * @param node The current node in the traversal (starts with the root).
 * @param bidId The bid ID to search for.
 * @return The node containing the bid with the specified bidId, or nullptr if not found.
 */
BSTree::Node* BSTree::search(Node* node, string bidId) {
    // Base case: root is null or bidId is present at root
    if (node == nullptr || node->bid.bidId == bidId) {
        return node;
    }

    // Value is greater than root's bidId, search in the right subtree
    if (node->bid.bidId < bidId) {
        return search(node->right, bidId);
    }

    // Value is less than root's bidId, search in the left subtree
    return search(node->left, bidId);
}

/**
 * Private method to perform a range query on the tree.
 * Processes nodes that fall within the specified range [lower, upper].
 * @param node The current node in the traversal.
 * @param lower The lower bound of the range.
 * @param upper The upper bound of the range.
 */
void BSTree::rangeQuery(Node* node, string lower, string upper) {
    if (node == nullptr) {
        return; // Base case: Reached the end of a branch
    }

    // Since the tree is a BST, nodes are in order, it can be determined which side(s) to explore.
    // If the current node's bidId is greater than the lower bound, explore the left subtree.
    if (node->bid.bidId > lower) {
        rangeQuery(node->left, lower, upper);
    }

    // If the current node is within the range, process it. Display the bid.
    if (node->bid.bidId >= lower && node->bid.bidId <= upper) {
        displayBid(node->bid);
    }

    // If the current node's bidId is less than the upper bound, explore the right subtree.
    if (node->bid.bidId < upper) {
        rangeQuery(node->right, lower, upper);
    }
}
```

### Lessons Learned

Converting the hash table to a balanced binary search tree (BST) was important to learning concepts in algorithms and data structures. For example, after considering what a scenario in a real-world application would entail, sales would be added and logged throughout the month, and the key would be needed to search for any new entries to search for them in a hash table, which is not necessary with a BST, since the range query can include a search for all entries in a month. The challenge in the hash table enhancement was weighing the pros and cons of different data structures or variations of a data structure to determine the best solution for the data set.


### Skills and Abilities Showcased

1.	Understanding of data structures by showing a deep understanding of different data structures and their respective advantages and disadvantages. This is critical in database design, where the choice of data structure can significantly affect performance and storage efficiency.
2.	Algorithmic complexity management in the ‘0(log n)’ complexity, used for insertion, deletion, and search operations. Understanding and managing this complexity is necessary to ensure the performance of database operations, especially when dealing with large datasets.
3.	Performance optimization through an optimized query performance. Balanced BSTs can enhance search performance over hash tables when it comes to range queries or ordered data retrieval, which are common in databases.


### Course Outcomes Demonstrated

### Design, develop, and deliver professional-quality oral, written, and visual communications that are coherent, technically sound, and appropriately adapted to specific audiences and contexts by:

1.	Implementing UX design and communication tailored to the audience.
2.	Developing code for collaboration, maintenance, and continuous improvement.
3.	Using the interface to encourage stakeholder engagement for expedited error handling.

### Design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, while managing the trade-offs involved in design choices (data structures and algorithms)by:

1.	Load balancing and complexity management of algorithms through a Distributed Hash Table.
2.	Data integrity and adherence to industry security standards by transitioning to a DHT.
3.	Computing a hash table to a DHT for evaluating latency vs decentralization.


Original and enhanced technical files can be found in the course repository [CS260 Algorithm and Data Structures]([[https://github.com/dpoloniajr/CS-320-Software-Testing-Automation-and-QA]).
