# Single-Linkedlist

******************** Node.h *********************

#include<iostream>
using namespace std;

class Node {
private:
		int Data;
		Node* Next;

public:
		Node();
	    Node(int);
		void setData(int);
		void setNext(Node*);
		int getData();
		Node* getNext();
	    
};



********************* Linkedlist.h ********************

#include<iostream>
#include"Node.h"

class Linkedlist {
private:
	Node* Head;
	Node* Tail;

public:

	Linkedlist();
	bool isEmpty();
	void insertatHead(int);
	void insertatTail(int);
	void display();
	void insertatTarget(int, int);
	Node* searchTarget(int);
	void removeNode(int);

};



************************ implimantation.cpp ***********************

#include<iostream>
#include"Linkedlist.h"
using namespace std;

// ------- Node Class Implementation -------
Node::Node()
{
    Data = 1;
    Next = NULL;
}

Node::Node(int Data)
{
    this->Data = Data;  // Corrected this line
    Next = NULL;
}

void Node::setData(int Data)
{
    this->Data = Data;
}

int Node::getData()
{
    return Data;
}

void Node::setNext(Node* Next)
{
    this->Next = Next;
}

Node* Node::getNext()
{
    return Next;
}

// ------- Linked List Class Implementation -------
Linkedlist::Linkedlist()
{
    Head = NULL;
    Tail = NULL;
}

bool Linkedlist::isEmpty()
{
    return Head == NULL;
}

void Linkedlist::insertatTail(int data)
{
    Node* temp = new Node(data);
    if (isEmpty())
    {
        Head = temp;
        Tail = temp;
    }
    else
    {
        Tail->setNext(temp);
        Tail = temp;
    }
}

void Linkedlist::insertatHead(int data)
{
    if (isEmpty())
    {
        insertatTail(data);
    }
    else
    {
        Node* temp = new Node(data);
        temp->setNext(Head);
        Head = temp;
    }
}

void Linkedlist::display()
{
    Node* temp = Head;
    while (temp != NULL)
    {
        cout << temp->getData() << endl;
        temp = temp->getNext();
    }
}

Node* Linkedlist::searchTarget(int toFind)
{
    Node* temp = Head;
    while (temp != NULL)
    {
        if (temp->getData() == toFind)
        {
            return temp;
        }
        temp = temp->getNext();
    }
    return NULL;
}

void Linkedlist::insertatTarget(int target, int value)
{
    if (isEmpty())
    {
        cout << "list is empty" << endl;
        return;
    }
    else
    {
        Node* targetNode = searchTarget(target);
        if (targetNode == NULL)
        {
            cout << "not found" << endl;
            return;
        }
        else
        {
            Node* temp = new Node(value);
            temp->setNext(targetNode->getNext());
            targetNode->setNext(temp);
        }
    }
}

void Linkedlist::removeNode(int toRemove)
{
    Node* targetNode = Head;
    Node* prev = NULL;
    while (targetNode != NULL)
    {
        if (targetNode->getData() == toRemove)
        {
            break;
        }
        else
        {
            prev = targetNode;
            targetNode = targetNode->getNext();
        }
    }

    if (targetNode == NULL)
    {
        cout << "not found" << endl;
        return;
    }
    else
    {
        if (targetNode == Head)
        {
            Head = Head->getNext();
            targetNode->setNext(NULL);
            delete targetNode;
        }
        else if (targetNode == Tail)
        {
            Tail = prev;
            Tail->setNext(NULL);
            delete targetNode;
        }
        else
        {
            prev->setNext(targetNode->getNext());
            targetNode->setNext(NULL);
            delete targetNode;
        }
    }
}


*********************** main.cpp *********************

#include <iostream>
#include "Linkedlist.h"
using namespace std;

void displayMenu() {
    cout << "\n\t\t---** Linked List Operations **---" << endl;
    cout << "\t1. Insert at Head" << endl;
    cout << "\t2. Insert at Tail" << endl;
    cout << "\t3. Display List" << endl;
    cout << "\t4. Search for a Node" << endl;
    cout << "\t5. Insert after a Target Node" << endl;
    cout << "\t6. Remove a Node" << endl;
    cout << "\t7. Exit" << endl;
    cout << "\n\tEnter your choice: ";
}

int main() {
    Linkedlist list1;
    int choice, data, target;

    do {
        displayMenu();
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter the value you want to insert at Head: ";
            cin >> data;
            list1.insertatHead(data);
            cout << "Inserted " << data << " at Head." << endl;
            break;

        case 2:
            cout << "Enter the value you want to insert at Tail: ";
            cin >> data;
            list1.insertatTail(data);
            cout << "Inserted " << data << " at the tail." << endl;
            break;

        case 3:
            cout << "List contents:" << endl;
            list1.display();
            break;

        case 4:
            cout << "Enter the value to search for: ";
            cin >> data;
            if (list1.searchTarget(data)) {
                cout << "Value " << data << " found in the list." << endl;
            }
            else {
                cout << "Value " << data << " not found in the list." << endl;
            }
            break;

        case 5:
            cout << "Enter the target value after which to insert: ";
            cin >> target;
            cout << "Enter the value to insert: ";
            cin >> data;
            list1.insertatTarget(target, data);
            cout << "Inserted " << data << " after " << target << " if target was found." << endl;
            break;

        case 6:
            cout << "Enter the value to remove: ";
            cin >> data;
            list1.removeNode(data);
            cout << "Removed " << data << " if it existed in the list." << endl;
            break;

        case 7:
            cout << "Exiting program. Goodbye!" << endl;
            break;

        default:
            cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 7);

    return 0;
}
