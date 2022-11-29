---
title: data structure
date: 2022-11-28 +09:00
categories: [data structure]
tags: [data, structure]
---


# Data Structure

- Array
- Linked list
- stack
- queue



## Array
---
    : ArrayList, Vector

배열 생성

```java
int[] intArr;
int count;

public int ARRAY_SIZE;
public static final int ERROR_NUM = -99999999;

public MyArrayList() {
    // 기본생성자로 생성 시 배열 크기 10
    count = 0;
    ARRAY_SIZE = 10;
    intArr = new int[ARRAY_SIZE];
}

public MyArrayList(int size) {
    // 지정한 사이즈의 배열 생성
    count = 0;
    ARRAY_SIZE = size;
    intArr = new int[ARRAY_SIZE];
}
```

요소 추가

```java
public void addElement(int num) {
    // 배열이 가득 찬 경우 return
    if(count >= ARRAY_SIZE) {
        System.out.println("not enough memory");
        return;
    }
    // 값 저장 후 count 증가
    intArr[count++] = num;
}
```

위치 지정 요소 추가

```java
public void insertElement(int position, int num) {
    int i;
    if(count >= ARRAY_SIZE) {
        System.out.println("not enough memory");
        return;
    }else if  (position < 0 || position > count) {
        System.out.println("insert error");
        return;
    }

    for(i = count-1;i>=position;i--) {
        intArr[i+1] = intArr[i];
    }

    intArr[position] = num;
    count++;
}
```
*이미지 첨부

요소 삭제

```java
public int removeElement(int position) {
    int ret = ERROR_NUM;
    // 배열이 비어있을 경우 에러값 return
    if(isEmpty()) {
        System.out.println("empty array");
        return ret;
    }
    if(position < 0 || position >= count) {
        System.out.println("remove Error");
        return ret;
    }

    ret = intArr[position];

    for(int i=position;i<count-1;i++) {
        intArr[i] = intArr[i+1];
    }
    count--;

    return ret;
}
```
*이미지 첨부

지정요소 찾기

```java
public int getElement(int position) {
    int ret = ERROR_NUM;
    if(isEmpty()) {
        System.out.println("empty array");
        return ret;
    }
    if(position < 0 || position >= count) {
        System.out.println("get Error");
        return ret;
    }
    ret = intArr[position];
}
```

예외처리를 위한 null 체크
```java
public boolean isEmpty() {
    if(count == 0) {
        return true;
    }else {
        return false;
    }
}
```

전체 출력
```java
public void printAll() {
    if(count == 0) {
        System.out.println("empty array");
        return;
    }

    for(int i=0;i<count;i++) {
        System.out.println(intArr[i]);
    }
}
```

## Linked list
---

노드 객체

```java
public class MyListNode {

    private String data;        // 자료
    public MyListNode next;     // 링크

    public MyListNode() {
        data = null;
        next = null;
    }

    public MyListNode(String data) {
        this.data = data;
        next = null;            // head일 경우 null
    }

    public MyListNode(String data, MyListNode link) {
        this.data = data;
        this.next = link;
    }

    public String getData() {
        return data;
    }
}
```

연결리스트 생성, 노드 추가

```java
private MyListNode head;
int count;

public MyLinkedList() {
    head = null;
    count = 0;
}

public MyListNode addElement(String data) {
    MyListNode newNode;

    if(head == null) {
        // 맨 처음일 때 
        newNode = new MyListNode(data);
        head = newNode;
    }else {
        newNode = new MyListNode(data);
        MyListNode temp = head;

        while(temp.next != null) {
            temp = temp.next;
            temp.next = newNode;
        }
    }
    count++;

    return newNode;
}
```

지정 위치에 노드 추가하기

```java
public MyListNode insertElement(int position, String data) {
    int i;
    MyListNode tempNode = head;
    MyListNode newNode = new MyListNode(data);

    if(position < 0 || position > count) {
        System.out.println("add Error");
        return null;
    }

    if(position == 0) {
        newNode.next = head;
        head = newNode;
    }else {
        MyListNode preNode = null;
        for(i=0;i<position;i++) {
            preNode = tempNode;
            tempNode = tempNode.next;
        }
        newNode.next = preNode.next;
        preNode.next = newNode;
    }
    count++;

    return newNode;
}
```
지정 위치의 노드 삭제하기
```java
public MyListNode removeElement(int position) {
    int i;
    MyListNode tempNode = head;

    if(position < 0 || position > count) {
        System.out.println("add Error");
        return null;
    }

    if(position == 0) {
        // head 삭제 시
        head = tempNode.next;
    }else {
        MyListNode preNode = null;
        for(i=0;i<position;i++) {
            preNode = tempNode;
            tempNode = tempNode.next;
        }
        preNode.next = tempNode.next;
    }
    count--;
    System.out.println(position + "번 노드 삭제완료");

    return tempNode;

}
```

지정 위치의 노드값 가져오기

```java
public String getElemt(int position) {
    int i;
    MyListNode tempNode = head;

    if(position >= count) {
        System.out.println("get Error");
        return new String("error");
    }

    if(position == 0) {
        return head.getData();
    }

    for(i=0;i<position;i++) {
        tempNode = tempNode.next;
    }
    return tempNode.getData();
}
```

전체 출력, 전체 삭제, 크기 출력하기

```java
public void printAll() {
    if(count == 0) {
        System.out.println("empty array");
        return;
    }

    MyListNode temp = head;
    while(temp != null) {
        System.out.println(temp.getData());
        temp = temp.next;
        if(temp!=null) {
            System.out.println("->");
        }
    }
    System.out.println();
}

public void removeAll() {
    head = null;
    count = 0;
}

public int getSize() {
    return count;
}
```

## Stack
---   

스택 생성
```java
int top;
MyArrayList arrayList;

public MyArrayStack() {
    top = 0;
    arrayList = new MyArrayList();
}

public MyArrayStack(int size) {
    arrayList = new MyArrayList(size);
}
```

데이터 추가(push)
```java
public void push(int data) {
    if(isFull()) {
        System.out.println("stack is full!");
        return;
    }
    arrayList.addElement(data);
    top++;
}
```
데이터 삭제(pop)
```java
public int pop() {
    if(top == 0) {
        System.out.println("stack is empty");
        return MyArrayList.ERROR_NUM;
    }
    return arrayList.removeElement(--top);
}
```
크기 출력하기, 전체 출력
```java
public int getSize() {
    return top;
}

public boolean isFull() {
    if(top == arrayList.ARRAY_SIZE) {
        return true;
    }else {
        return false;
    }
}

public void printAll() {
    arrayList.printAll();
}
```


## queue
---
큐 인터페이스 사용, 연결리스트 클래스 상속하여 큐 생성하기

```java
import package.linkedlist.MyLinkedList;
import package.linkedlist.MyListNode;

interface IQueue {
    void enQueue(String data);
    void deQuere();
    void printAll();
    // input은 enQueue, output은 deQueue
}

public class MyListQueue extends MyLinkedList implements IQueue {
    MyListNode front;
    MyListNode tail;
    // 자료의 삭제는 front에서, 추가는 tail/rear에서 이루어진다.

    public MyListQueue() {
        front = null;
        tail = null;
    }
}
```

enQueue() 구현하기

```java
@Override
public void enQueue(String data) {
    MyListNode newNode;

    if(isEmpty()) {
        // 맨 처음일 때
        newNode = addElement(data);
        front = newNode;
        tail = newNode;
    }else {
        newNode = addElement(data);
        tail = newNode;
    }
    System.out.println(newNode.getData() + " added");
}
```

deQueue() 구현하기

```java
public void deQueue() {
    if(isEmpty()) {
        System.out.println("Queue is empty");
        return;
    }else {
        front = front.next
    }
}
```

전체 출력하기

```java
@Override
public void printAll() {
    if(isEmpty()) {
        System.out.println("Queue is empty");
        return;
    }
    MyListNode temp = front;

    while(temp != null) {
        System.out.println(temp.getData() + ", ");
        temp = temp.next;
    }
    System.out.println();
}
```