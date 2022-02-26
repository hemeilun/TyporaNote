# Java数据结构

<br/>

[TOC]



<br/>

1）线性结构作为最常用的数据结构，其特点是数据元素之间存在一一对应的线性关系

2）线性结构有两种不同的存储接哦古，即顺序存储结构和链式存储结构

3）顺序存储结构的线性表称为顺序表，顺序表中的存储元素是连续的；链式存储的线性表称为链表，链表中的存储元素不一定连续，元素节点中存放数据元素和它相邻元素的地址信息

4）线性结构常见的有：数组，队列，链表和栈。

<br/><br/>

## （一）稀疏矩阵

<br/>

应用实例：

1）使用稀疏矩阵，来保留二维数组（比如：棋盘，地图）

2）把稀疏矩阵保存，并且可以重新恢复原来的二维数组

<br/><br/>

思路：

（1）将二维数组转化为稀疏矩阵

1）遍历原始的二维数组，得到有效数据的个数sum

2）根据sum就可以创建稀疏数组

3）遍历原始的二维数组，将数据保存到稀疏数组中

<br/>

（2）将系数矩阵转化为二维数组

1）先读取稀疏数组的第一行，根据第一行的数据，创建原始的二维数组

2）一行行的读取稀疏数组中的数据并写入二维数组

<br/><br/>

代码实现（包括将稀疏矩阵写入和读取文件）：

```java
package SparseArray;

import java.io.*;

public class Sparse1 {
    public static void main(String[] args) {

        //创建棋盘
        int[][] chess = new int[11][11];
        chess[1][2]=1;
        chess[4][4]=2;

        //展示原始棋盘
        System.out.println("原始棋盘为：");
        for (int[] rows:chess) {
            for(int temp:rows){
                System.out.printf("%d\t",temp);
            }
            System.out.println();
        }
        System.out.println();


        //转化为稀疏矩阵
        //计算总共有多少个不为0的数据
        int sum=0;
        for (int i = 0; i <chess.length ; i++) {
            for (int j = 0; j <chess[i].length ; j++) {
                if(chess[i][j]!=0){
                    sum++;
                }
            }
        }

        //将具体的数据保存到稀疏矩阵中
        int[][] sparse = new int[sum+1][3];
        sparse[0][0]=11;
        sparse[0][1]=11;
        sparse[0][2]=sum;

        int count=0;          //计算现在是稀疏矩阵中的第几行
        for (int i = 0; i <chess.length ; i++) {
            for (int j = 0; j <chess[i].length ; j++) {
                if(chess[i][j]!=0){
                    count++;
                    sparse[count][0]=i;
                    sparse[count][1]=j;
                    sparse[count][2]=chess[i][j];
                }
            }
        }

        
        //将稀疏矩阵保存到文件中
        try {
            OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("sparse.txt"));
            StringBuilder sb = new StringBuilder("");
            for (int[] rows:sparse) {
                for(int temp:rows){
                    sb.append(temp+" ");
                }
                sb.append("\r\n");
            }
            osw.write(sb.toString(),0,sb.length());
            osw.close();

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }


        //将稀疏矩阵读出来
        try {
            BufferedReader br = new BufferedReader(new FileReader("sparse.txt"));

            String s =new String();
            s=br.readLine();
            int nownum=1;
            String[] strings = s.split(" ");

            int valnum=Integer.parseInt(strings[2]);     //总共有多少个数据
            int[][] sparce1 = new int[valnum+1][3]; //创建数组保存文件中的数据

            sparce1[0][0]=Integer.parseInt(strings[0]);
            sparce1[0][1]=Integer.parseInt(strings[1]);
            sparce1[0][2]=Integer.parseInt(strings[2]);


            while ((s=br.readLine())!=null){
                strings = s.split(" ");
                sparce1[nownum][0]=Integer.parseInt(strings[0]);
                sparce1[nownum][1]=Integer.parseInt(strings[1]);
                sparce1[nownum][2]=Integer.parseInt(strings[2]);
                nownum++;
            }

            br.close();

            System.out.println("从文件中读出的数据为：");
            for (int[] rows:sparce1) {
                for(int temp:rows){
                    System.out.printf("%d\t",temp);
                }
                System.out.println();
            }
            System.out.println();

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }




        //展示稀疏矩阵
        System.out.println("稀疏矩阵为：");
        for (int[] rows:sparse) {
            for(int temp:rows){
                System.out.printf("%d\t",temp);
            }
            System.out.println();
        }
        System.out.println();


        //将稀疏矩阵转化为棋盘
        //将稀疏矩阵中的值赋值给棋盘
        int[][] spatochess = new int[sparse[0][0]][sparse[0][1]];
        for (int i = 1; i <= sparse[0][2]; i++) {
            spatochess[sparse[i][0]][sparse[i][1]]=sparse[i][2];
        }

        System.out.println("稀疏矩阵转化为的棋盘为：");
        for (int[] rows:spatochess) {
            for(int temp:rows){
                System.out.printf("%d\t",temp);
            }
            System.out.println();
        }
        System.out.println();

        
        //运行结果：
        /*原始棋盘为：
        0	0	0	0	0	0	0	0	0	0	0
        0	0	1	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	2	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0

        从文件中读出的数据为：
        11	11	2
        1	2	1
        4	4	2

        稀疏矩阵为：
        11	11	2
        1	2	1
        4	4	2

        稀疏矩阵转化为的棋盘为：
        0	0	0	0	0	0	0	0	0	0	0
        0	0	1	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	2	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0
        0	0	0	0	0	0	0	0	0	0	0*/
    }
}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （二）链表

<br/>

### 1.链表介绍

<br/>

链表是有序的列表，如图：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStu1.png" alt="image-20220116203257800"  />

<br/>

具体说明：

1）链表在内存中是以结点的方式存储，是链式存储

2）每一个结点包括一个数据域和指针域，数据域用来保存数据，指针域用来指向下一个结点

3）各个结点之间并不是连续存储

4）链表分为：带头指针的链表 和 不带头指针的链表

<br/><br/><br/><br/>

### 2.单链表

<br/>

带头结点单链表的逻辑示意图：

<br/>

![image-20220116203819890](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru2.png)

<br/><br/>

单链表的多种操作：

<br/>

#### （1）添加

<br/>

单链表的添加有两种方式：

<br/>

1）尾插法

<br/>

步骤：

① 创建辅助结点并指向头结点

② 遍历链表，使辅助结点指向最后一个结点

③ 将辅助结点的next指向要添加的结点，添加完成

<br/>

```java
//添加结点（尾插法）
public void addNodeByTail(Node node){

    //让cur指向最后一个结点
    Node cur = headNode;
    while(cur.next!=null){
        cur = cur.next;
    }

    //将新结点加到链表后面
    cur.next = node;
}
```

<br/><br/>

2）头插法

<br/>

步骤：

① 将要添加结点的next指向头结点的next

② 将头结点的next指向要添加的结点，添加完成

<br/>

```java
//添加结点（头插法）
public void addNodeByHead(Node node){
    
    node.next = headNode.next;
    headNode.next = node;
    
}
```

<br/><br/><br/><br/>

#### （2）修改

<br/>

步骤：

① 创建辅助结点并指向头结点

② 遍历链表，找到指定结点

③ 将要修改的值赋值给指定结点，修改完成

<br/>

```java
//根据no修改结点
public void updateNodeByNo(Node node){

    Node cur = headNode;
    boolean ifExist = false;       //判断指定结点是否存在

    while(cur.next != null){
        cur = cur.next;
        if(node.no == cur.no){
            ifExist = true;
            break;
        }
    }

    if(ifExist == false)
    {
        System.out.println("结点不存在");
    }else{
        cur.name = node.name;
    }

}
```

<br/><br/><br/><br/>

#### （3）插入

<br/>

步骤：

① 创建辅助结点cur指向当前结点，创建辅助结点next指向cur的后一个结点

② 遍历链表找到指定位置

③ 将指定结点的next指向辅助结点next

④ 将cur的next指向指定结点，插入完成

<br/>

```java
//插入结点（使添加的结点按照序号从小到大排列）
public void sortByNo(Node node){

    Node cur = headNode; //记录当前结点
    Node next = null;    //记录当前结点的下一个结点
    boolean ifExist = false;  //判断指定结点是否已经存在

    //找到要插入的位置
    while (cur.next != null){

        next = cur.next;
        if(next.no < node.no){
            cur = cur.next;
        }else if(next.no == node.no){
            ifExist = true;
            break;
        }else if(next.no > node.no) {
            break;
        }

    }

    //保证cur.next为空时，next仍然指向cur的下一个
    if(cur.next == null)
        next = cur.next;

    //插入结点
    if(ifExist){
        System.out.println("结点已存在");
    }else {

        //找到位置后插入结点的两步
        node.next = next;
        cur.next = node;
    }

}
```

<br/><br/><br/><br/>

#### （4）删除

<br/>

步骤：

① 创建辅助结点指向头结点

② 遍历链表找到指定结点（通过指定结点的前一个结点的next来判断是否为指定结点，因为需要删除这个结点，所以要知道指定结点的前一个结点是什么）

③ 直接让，辅助结点的next指向辅助结点next的next，删除完成

<br/>

```java
//删除指定结点
public void deleteNodeByNo(Node node){

    Node cur = headNode;
    boolean ifExist = false;

    //找到指定的结点
    while(cur.next != null){

        if(cur.next.no == node.no){

            //找到指定结点直接删除
            cur.next = cur.next.next;
            ifExist = true;
            break;

        }else{
            cur = cur.next;
        }
    }

    if(ifExist == false){
        System.out.println("没有指定序号的结点");
    }

}
```

<br/><br/><br/><br/>

#### （5）遍历

<br/>

```java
//遍历链表
public void show()
{
    Node cur = headNode;
    while(cur.next != null){
        cur = cur.next;
        System.out.println(cur);
    }
}
```

<br/><br/><br/><br/>

#### （6）完整代码

<br/>

```java
package LinkedList;

public class SingleLinkedList {
    public static void main(String[] args) {


        //测试尾插法添加结点
        Node node1 = new Node(2,"张三");
        Node node2 = new Node(3,"李四");
        Node node3 = new Node(6,"王五");

        SingleList singleList = new SingleList();
        singleList.addNodeByTail(node1);
        singleList.addNodeByTail(node2);
        singleList.addNodeByTail(node3);

        System.out.println("尾插法添加结点：");
        singleList.show();

        System.out.println();


        //测试头插法添加结点
        Node node4 = new Node(1,"张三");
        Node node5 = new Node(2,"李四");
        Node node6 = new Node(3,"王五");

        SingleList singleList1 = new SingleList();
        singleList1.addNodeByHead(node4);
        singleList1.addNodeByHead(node5);
        singleList1.addNodeByHead(node6);

        System.out.println("头插法添加结点：");
        singleList1.show();

        System.out.println();


        //测试修改结点
        Node updateNode = new Node(2,"赵六");
        Node updateNode1 = new Node(5,"哈哈");

        System.out.println("修改后的链表：");
        singleList.updateNodeByNo(updateNode);
        singleList.show();

        singleList.updateNodeByNo(updateNode1);

        System.out.println();


        //测试有序插入
        Node node7 = new Node(4,"haha");
        singleList.sortByNo(node7);

        System.out.println("按序插入后：");
        singleList.show();

        System.out.println();


        //测试删除指定序号的结点
        singleList.deleteNodeByNo(node7);

        System.out.println("删除指定序号结点后：");
        singleList.show();

    }
}



//创建一个单链表
class SingleList{
    
    //规定头结点
    private Node headNode = new Node(0,"");
    

    //添加结点（尾插法）
    public void addNodeByTail(Node node){

        //让cur指向最后一个结点
        Node cur = headNode;
        while(cur.next!=null){
            cur = cur.next;
        }

        //将新结点加到链表后面
        cur.next = node;
    }
    
    
    //添加结点（头插法）
    public void addNodeByHead(Node node){
        
        node.next = headNode.next;
        headNode.next = node;
        
    }


    //根据no修改结点
    public void updateNodeByNo(Node node){

        Node cur = headNode;
        boolean ifExist = false;

        while(cur.next != null){
            cur = cur.next;
            if(node.no == cur.no){
                ifExist = true;
                break;
            }
        }

        if(ifExist == false)
        {
            System.out.println("结点不存在");
        }else{
            cur.name = node.name;
        }

    }



    //插入结点（使添加的结点按照序号从小到大排列）
    public void sortByNo(Node node){

        Node cur = headNode; //记录当前结点
        Node next = null;    //记录当前结点的下一个结点
        boolean ifExist = false;  //判断指定结点是否已经存在

        //找到要插入的位置
        while (cur.next != null){

            next = cur.next;
            if(next.no < node.no){
                cur = cur.next;
            }else if(next.no == node.no){
                ifExist = true;
                break;
            }else if(next.no > node.no) {
                break;
            }

        }

        //保证cur.next为空时，next仍然指向cur的下一个
        if(cur.next == null)
            next = cur.next;

        //插入结点
        if(ifExist){
            System.out.println("结点已存在");
        }else {

            //找到位置后插入结点的两步
            node.next = next;
            cur.next = node;
        }

    }



    //删除指定结点
    public void deleteNodeByNo(Node node){

        Node cur = headNode;
        boolean ifExist = false;

        //找到指定的结点
        while(cur.next != null){

            if(cur.next.no == node.no){

                //找到指定结点直接删除
                cur.next = cur.next.next;
                ifExist = true;
                break;

            }else{
                cur = cur.next;
            }
        }

        if(ifExist == false){
            System.out.println("没有指定序号的结点");
        }

    }



    //遍历链表
    public void show()
    {
        Node cur = headNode;
        while(cur.next != null){
            cur = cur.next;
            System.out.println(cur);
        }
    }

}




//规定结点的类型
class Node{
    public int no;              //编号
    public String name;         //姓名
    public Node next;           //指向下一个结点

    public Node(int no, String name) {
        this.no = no;
        this.name = name;
        this.next = null;
    }

    @Override
    public String toString() {
        return "Node{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }
}
```

<br/><br/><br/><br/>

### 3.双向链表

<br/>

双向链表与单链表大同小异，只是多了一个向前的指针

<br/>

![image-20220117212624762](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru3.png)

<br/>

在双向链表中，实现了添加，插入，修改，删除

这些步骤与单链表的步骤十分相同，我在下方的实现代码中将一些变化了的地方注释了

就像这样：

```java
        //
        doubleNode.pre = cur;   //新加的
```

<br/>

```java
package LinkedList;

public class DoubleLinkedList {

    public static void main(String[] args) {

        DoubleNode node1 = new DoubleNode(2,"张三");
        DoubleNode node2 = new DoubleNode(3,"李四");
        DoubleNode node3 = new DoubleNode(6,"王五");

        //测试添加结点
        DoubleList doubleList = new DoubleList();
        doubleList.addNodeByTail(node1);
        doubleList.addNodeByTail(node2);
        doubleList.addNodeByTail(node3);

        doubleList.show();

        System.out.println();

        //测试修改结点
        DoubleNode node4 = new DoubleNode(2,"haha");
        doubleList.updateNodeByNo(node4);

        doubleList.show();

        System.out.println();

        //测试按序插入结点
        DoubleNode node5 = new DoubleNode(7,"哈哈");
        doubleList.sortByNo(node5);

        doubleList.show();

        System.out.println();


        //测试删除结点
        doubleList.deleteNodeByNo(node4);
        doubleList.show();


    }
}


class DoubleList{

    public DoubleNode headNode = new DoubleNode(0,"");    //头结点

    //尾插法添加结点
    public void addNodeByTail(DoubleNode doubleNode){

        //让cur指向最后一个结点
        DoubleNode cur = headNode;
        while(cur.next!=null){
            cur = cur.next;
        }

        cur.next = doubleNode;
        
        //
        doubleNode.pre = cur;   //新加的

    }



    //插入结点（使添加的结点按照序号从小到大排列）
    public void sortByNo(DoubleNode node){

        DoubleNode cur = headNode; //记录当前结点
        DoubleNode next = null;    //记录当前结点的下一个结点
        boolean ifExist = false;  //判断指定结点是否已经存在

        //找到要插入的位置
        while (cur.next != null){

            next = cur.next;
            if(next.no < node.no){
                cur = cur.next;
            }else if(next.no == node.no){
                ifExist = true;
                break;
            }else if(next.no > node.no) {
                break;
            }

        }

        //保证cur.next为空时，next仍然指向cur的下一个
        if(cur.next == null) {
            next = cur.next;
        }

        //插入结点
        if(ifExist){
            System.out.println("结点已存在");
        }else {

            //
            node.next = next;                //这里变化了
            cur.next = node;
            node.pre = cur;

            if(next != null){
                next.pre = node;
            }

        }

    }



    //修改结点
    public void updateNodeByNo(DoubleNode node){

        DoubleNode cur = headNode;
        boolean ifExist = false;

        while(cur.next != null){
            cur = cur.next;
            if(node.no == cur.no){
                ifExist = true;
                break;
            }
        }

        if(ifExist == false)
        {
            System.out.println("结点不存在");
        }else{
            cur.name = node.name;
        }

    }



    //删除结点
    //这个地方，双向链表可以直接通过目标结点自身进行删除，不需要先找到它前面的结点
    public void deleteNodeByNo(DoubleNode node){

        DoubleNode cur = headNode;
        boolean ifExist = false;

        //找到指定的结点
        while(cur.next != null){

            cur = cur.next;
            if(cur.no == node.no){

                if(cur.next != null){

                    //
                    cur.pre.next = cur.next;   //这里变化了
                    cur.next.pre = cur.pre;

                }else{
                    
                    //
                    cur.pre.next = cur.next;   //这里变化了
                }

                ifExist = true;
                break;

            }
        }

        if(ifExist == false){
            System.out.println("没有指定序号的结点");
        }

    }


    //遍历链表
    public void show()
    {
        DoubleNode cur = headNode;
        while(cur.next != null){
            cur = cur.next;
            System.out.println(cur);
        }
    }


}


//双向链表的一个结点
class DoubleNode{
    public int no;
    public String name;
    
    //
    public DoubleNode pre;       //只是加了一个向前的指针
    public DoubleNode next;

    public DoubleNode(int no,String name) {
        this.no = no;
        this.name = name;
        pre = null;
        next = null;
    }

    @Override
    public String toString() {
        return "DoubleNode{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }
}
```

<br/><br/><br/><br/>

### 4.约瑟夫环

<br/>

单项循环链表实现

<br/>

约瑟夫（Josephu）问题：

设编号为1~n，共n个人围坐一圈，约定编号为k的人从1开始报数，数到m的人出列，下一个人再从1开始报数，依次类推，直到所有人出列，形成一个序列。

<br/>

步骤：

1）确定共有多少个人，从1~n开始编号，将n个人构成一个单向循环链表

2）从K号开始依次报数，每报到m，就从链表中删除这个结点

3）下一号再从1开始报数，最后只剩一个结点，并产生一个序列

<br/>

1）构建单向循环链表

步骤：

① 创建辅助结点lastNode指向循环链表的最后一个结点

② 根据人数进行循环，分为第一个结点和其他结点

-  当为第一个结点时，需要将first指向第一个结点，同时将lastNode指向第一个结点
-  当为其他结点时，需要将lastNode的next指向新结点，并将lastNode指向新结点，同时将新结点的next指向first

创建完成

<br/><br/>

2）解决出队序列

步骤：

① 创建辅助结点lastNode使其指向fist的前一个结点

② 因为要从序号k开始，所以first和lastNode同时向后移送k-1次

③ 每报到m个数就要出列，所以first和lastNode同时向后移送m-1次即可使first指向要出列的序号

④ 去除这个结点，让lastNode.next指向first.next，打印序号，再让first = first.next

⑤ 当 fitst和lastNode相同时，说明只剩下一个结点，直接打印出即可

<br/><br/>

代码实现：

<br/>

```java
package LinkedList;

public class JosephuLinkedList {
    public static void main(String[] args) {

        JosephuList josephuList = new JosephuList();

        //测试创建单向循环列表
        josephuList.creatList(25);
        josephuList.show();

        System.out.println();

        //测试约瑟夫环的输出序列
        josephuList.soveJosephu(1,2,25);

    }
}



class JosephuList{

    public JosephuNode first = new JosephuNode(-1);


    //根据数字创建环
    public void creatList(int num){

        JosephuNode lastNode = null;   //指向环中的最后一个结点

        if(num < 2){
            System.out.println("输入数字无意义");
            return;
        }

        for (int i = 1; i <= num; i++) {

            JosephuNode newNode = new JosephuNode(i);

            if(i == 1){
                first = newNode;
                newNode.next = first;
                lastNode = newNode;
            }else{
                lastNode.next = newNode;
                newNode.next = first;
                lastNode = newNode;
            }

        }
    }



    //约瑟夫问题的实现
    public void soveJosephu(int k, int m, int num){

        //判断给的数字是否合理
        if(m<1 || k <1 || k>num){
            System.out.println("输入数字无意义");
            return;
        }

        JosephuNode lastNode = first;  //指向first的前一个结点

        //首先，让last指到first的前面
        while(lastNode.next != first){
            lastNode = lastNode.next;
        }

        //让lastNode和first一同移动，使first移到编号为k的位置
        for (int i = 0; i < k-1; i++) {
            first = first.next;
            lastNode = lastNode.next;
        }

        //每报号从1到m,lastNode和first就移动m-1下
        while(true){

            for (int i = 0; i < m-1; i++) {
                first = first.next;
                lastNode = lastNode.next;
            }

            //去除报到号的结点
            lastNode.next = first.next;
            System.out.println(first.no);

            //让first指向报到号的下一个结点
            first = first.next;

            //当lastNode == first时，说明只有一个结点
            if(lastNode == first){
                System.out.println(first.no);
                break;
            }
        }

    }



    //遍历
    public void show(){

        JosephuNode cur = first;

        while(cur.next != first){
            System.out.println(cur.no);
            cur = cur.next;
        }
        System.out.println(cur.no);
    }

}





//创建约瑟夫环的每一个结点
class JosephuNode{
    public int no;
    public JosephuNode next;

    public JosephuNode(int no) {
        this.no = no;
        next = null;
    }
}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （三）栈

<br/>

### 1.基本概念及方法

<br/>

定义：

1）栈是一种先入后出的有序列表

2）栈是一种限制性列表，只允许在线性表的一端进行插入和删除；允许插入和删除的一端称为栈顶，另一端称为栈底

3）由定义可知，最先插入的数据在栈底，最后插入的元素在栈顶；最先删除的元素在栈顶，最后删除的元素在栈底

<br/>

在java中存在类类型Stack<E>用来表示栈

<br/>

![image-20220118190802236](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru4.png)

<br/><br/><br/><br/>

### 2.栈实现计算器

<br/>

问题：通过栈对 一个运算式 进行计算

<br/>

步骤：

1）创建一个index对运算式进行遍历，通过charAt(index)获取

2）如果发现是一个数字，就将数字压入数字栈

3）如果是运算符，分为如下情况：

- 如果为空，就直接将字符放入字符栈
- 如果不为空，创建循环（当字符栈不为空且当前符号优先级小于字符栈顶时进行循环），循环内将数字栈pop两个数，字符栈pop一个，进行计算，将计算结果push进数字串，循环结束后，将当前符号压入符号栈

4）表达式遍历结束后，就从数字栈和符号栈中顺序pop出数字和符号进行计算

5）最后数字栈中仅剩一个数，就是计算结果

<br/>

代码实现：

```java
package Stack;

import java.util.Stack;

public class ComputeStack {

    public static void main(String[] args) {

        //计算表达式
        String eva = "22-2-10+7*2-3*6+500";

        //创建一个字符栈和一个数字栈
        Stack<Integer> numStack = new Stack<>();
        Stack<Character> characterStack = new Stack<>();

        //遍历表达式的索引
        int index = 0;

        while(index < eva.length() ){

            Character numChar = eva.charAt(index++);
            int num = 0;     //用来保存运算的数字
            boolean ifNum = ifNum(numChar);  //判断是否是数字


            //如果时数字就直接压入数字栈
            if(ifNum == true){

                //将数字具体展示
                while(ifNum(numChar)){
                    num= num*10+(numChar-48);

                    //保证到达末尾时不会出错
                    if(index >= eva.length()){
                        break;
                    }
                    numChar = eva.charAt(index);
                    if(ifNum(numChar)){
                        index++;
                    }
                }

                numStack.push(num);
            }else{

                //如果是字符首先要判断字符栈是否为空
                //如果为空，就直接将字符放入字符栈，否则，应先比较优先级
                if(characterStack.empty()){
                    characterStack.push(numChar);
                }else{

                    //如果优先级比栈顶高就直接放入
                    if (returnOrder(numChar) > returnOrder(characterStack.peek())) {
                            characterStack.push(numChar);
                    } else {
                        while(!characterStack.empty() &&
                                returnOrder(numChar) <= returnOrder(characterStack.peek())) {
                            int num1 = numStack.pop();
                            int num2 = numStack.pop();
                            Character c1 = characterStack.pop();

                            numStack.push(operation(num1, num2, c1));
                        }
                        characterStack.push(numChar);
                    }
                }
            }

        }

        //当全部都放入栈之后，就直接计算
        while(!characterStack.empty()) {
            int num1 = numStack.pop();
            int num2 = numStack.pop();
            Character c1 = characterStack.pop();
            numStack.push(operation(num1, num2, c1));
        }

        System.out.println(numStack.pop());

    }

    //返回计算符的优先级
    //优先级越高，数字越大
    public static int returnOrder(char ope){
        if(ope == '+' || ope == '-'){
            return 1;
        }else if(ope == '*' || ope == '/'){
            return 2;
        }else{
            //其他运算符错误
            System.out.println("运算符超出程序运算范围");
            return -1;
        }
    }

    //判断字符是否为数字
    public static boolean ifNum(char c){
        if( c >= '0' && c <= '9'){
            return true;
        }else {
            return false;
        }
    }

    //对弹出的数字进行计算
    public static int operation(int num1,int num2,Character c1){
        switch (c1){
            case '+':return num1 + num2;
            case '-':return num2 - num1;
            case '*':return num1 * num2;
            case '/':return num1 / num2;
            default: System.out.println("计算符有误"); return 0;
        }
    }

}
```

<br/><br/><br/><br/>

### 3.逆波兰式计算器

<br/>

逆波兰式计算有两步：

1）将中缀表达式转化为后缀表达式（逆波兰式）

2）计算逆波兰式

<br/>

**将中缀表达式转为后缀表达式**

<br/>

步骤：

说明：括号中的内容是在具体操作时，可以用到的更为方便的方法

1）初始化两个栈，运算符栈和存储中间结果的栈s2（由于存储中间结果的栈只有在最后一步才会出栈，且出栈后还要逆序才是后缀表达式，所以存放时可以用List，这样就直接就是后缀表达式）

2）从左到右遍历中缀表达式(这里可以先遍历，将值和符号值放入一个List集合中，后面就直接遍历这个集合)

3）如果是数字，就直接放入s2

4）遇到括号时：

- 如果是" ( "，就直接放入运算符栈中
- 如果是" ) "，则依次弹出运算符栈顶的符号，并放入s2，直到栈顶为" ( "，就将" ( "弹出，且**不放入**s2

5）遇到运算符时：

- 如果符号栈为空或符号栈顶为" ( "，就直接放入栈中
- 否则，将运算符栈顶弹出并放入s2，再重新将运算符与栈顶进行比较，重复第5步，直到将符号放入栈中

6）遍历结束后，将符号栈中的符号依次放入s2

7）将s2中的元素依次弹出，经过逆序就是后缀表达式（如果用的时List，那List中存放的就是逆序表达式）

<br/><br/>

**计算后缀表达式**

<br/>

步骤：

1）初始化一个数字栈

2）遍历后缀表达式的List

3）当遇到数字时，直接将数字压入栈

4）当遇到符号时，弹出数字栈栈顶的两个数字，通过运算符计算，将计算结果放入数字栈

5）遍历结束后，数字栈的栈顶就是计算结果

<br/><br/>

代码实现：

```java
package Stack;

import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

public class ReversePolish {

    public static void main(String[] args) {

        String exp = "10+((20+3)*4)-50";

        List<String> infixExpressions = StringToList(exp);
        System.out.println("中缀表达式的List："+infixExpressions);

        System.out.println();

        List<String> postfixExpressions = infixToPostfix(infixExpressions);
        System.out.println("后缀表达式的List："+postfixExpressions);

        System.out.println();

        int num = calculatePostfixExpresssions(postfixExpressions);
        System.out.println("计算结果为："+ num );


    }


    //将字符串转化为List
    public static List<String> StringToList(String exp){

        List<String> list = new ArrayList<>();
        int index = 0;   //用来遍历字符串

        while(index < exp.length()){

            char c = exp.charAt(index);
            if(ifNum(c)){
                String s = "";

                while(index < exp.length() && ifNum(c)){
                    c= exp.charAt(index);
                    if(ifNum(c)){
                        index++;
                        s = s + c;
                    }
                }

                list.add(s);

            }else{
                list.add(""+c);
                index++;
            }
        }

        return list;
    }


    //将中缀表达式转化为后缀表达式
    public static List<String> infixToPostfix(List<String> infixExpressions){

        //用来保存后缀表达式的List
        List<String> list = new ArrayList<>();
        //存放运算符号
        Stack<String> charStack = new Stack<>();

        for(String item : infixExpressions){

            // "//d+"是数字的正则表达式
            if(item.matches("\\d+")){
                //如果是数字就直接放入list中
                list.add(item);
             }else if (item.equals("(")){
                //如果等于左括号，就直接放入栈中
                charStack.push(item);
            }else if (item.equals(")")){
                //如果等于右括号，将栈中符号依次放入list，直到栈顶符号为"("
                while(!charStack.peek().equals("(")){
                    list.add(charStack.pop());
                }
                charStack.pop();
            }else {
                //如果是运算符，首先看符号栈是否为空 或者 栈顶元素是否为"("，
                // 如果是，直接将运算符放入
                while(true) {
                    if (charStack.empty() || charStack.peek().equals("(")) {
                        charStack.push(item);
                        break;
                    } else {
                        //运算符不为空 或者 "(" 时，首先判断优先级
                        //如果item优先级比栈顶符号优先级高，就直接放入栈顶
                        //否则,将栈顶符号弹出放入list,继续比较高下一个栈顶符号
                        if(returnOrder(item)>returnOrder(charStack.peek())){
                            charStack.push(item);
                            break;
                        }else{
                            list.add(charStack.pop());
                        }

                    }
                }

            }

        }

        while(!charStack.empty()){
            list.add(charStack.pop());
        }

        return list;
    }


    //计算后缀表达式
    public static int calculatePostfixExpresssions(List<String> list){

        //创建符号栈和数字栈
        Stack<String> charStack = new Stack<>();
        Stack<Integer> numStack = new Stack<>();

        for(String item : list){

            //如果为数字就放入数字栈
            if(item.matches("\\d+")){
                numStack.push(Integer.parseInt(item));
            }else{
                int num1 = numStack.pop();
                int num2 = numStack.pop();
                numStack.push(operation(num1,num2,item));
            }
        }

        return numStack.pop();
    }



    //判断是否是数字
    public static boolean ifNum(char c){
        if( c >= '0' && c <= '9'){
            return true;
        }else {
            return false;
        }
    }


    //返回计算符的优先级
    //优先级越高，数字越大
    public static int returnOrder(String ope){
        if(ope.equals("+") || ope.equals("-")){
            return 1;
        }else if(ope.equals("*")|| ope.equals("/")){
            return 2;
        }else{
            //其他运算符错误
            System.out.println("运算符超出程序运算范围");
            return -1;
        }
    }


    //对弹出的数字进行计算
    public static int operation(int num1,int num2,String c1){
        switch (c1){
            case "+":return num1 + num2;
            case "-":return num2 - num1;
            case "*":return num1 * num2;
            case "/":return num1 / num2;
            default: System.out.println("计算符有误"); return 0;
        }
    }

}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （四）递归

<br/>

### 1.基本概念

<br/>

概念：简单来说，递归就是自己调用自己，每次调用时传入不同的变量。

<br/>

递归的调用机制：

1）当程序执行一个方法时，就会开辟一个独立的空间（栈）

2）每个独立空间的局部变量是独立的，他们之间也会共同使用一些公用数据

<br/><br/>

递归需要遵守的重要原则：

1）执行一个方法，就需要创建一个新的受保护的独立空间（栈空间）

2）方法的局部变量是独立的

3）如果方法参数列表中使用的是引用型变量，就会共享该引用类型的数据

4）**递归必须向退出递归的条件逼近**，否则就是无限递归

5）当一个方法执行完毕，或者遇到return，就会返回；遵守谁调用就将结果返回给谁，同时当方法执行完毕或者返回时，该方法也就执行完毕

<br/><br/>

递归能解决的问题：

1）各种数学问题，如：八皇后问题，汉诺塔，阶乘问题，迷宫问题，球和篮子问题

2）各种算法中也会用到递归，比如：快速排序，归并排序，二分查找，分治算法等

3）将用栈解决的问题 --> 用递归的话，代码比较简洁

<br/><br/><br/><br/>

### 2.迷宫问题

<br/>

问题：将一个小球放入迷宫，让其自己找到路径

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru5.png" alt="image-20220123200742968" style="zoom: 67%;" />



<br/>

实现简述：

小球每到达一个格子时首先判断这个格子是不是终点，如果是就结束，不是就走步骤1）

1）当小球到达一个格子后，先让其向下，如果可以走就进入下一个格子，重复步骤1），如果不能走（这个格子所有方向都不行）且下一个格子不为墙体时，就将下一个格子标为3，并返回先前的格子，如果是墙体，直接返回先前的格子

2）从此格再向右走，进入下一个格子，如果可以走就重复步骤1），不能走的步骤和1）相同

3）从此格再向左走，进入下一个格子，如果可以走就重复步骤1），不能走的步骤和1）相同

4）从此格再向上走，进入下一个格子，如果可以走就重复步骤1），不能走的步骤和1）相同

5）经过不断重复1，2，3，4，就可以找到出路

<br/>

代码实现：

```java
package Recursion;

public class Maze {

    public static void main(String[] args) {

        //初始化迷宫
        int[][] maze = new int[8][8];
        for (int i = 0; i < 8; i++) {
            maze[i][0] = 1;
            maze[i][7]=1;
        }
        for (int i = 1; i < 7 ; i++) {
            maze[0][i]=1;
            maze[7][i]=1;
        }
        maze[4][1]=1;
        maze[4][2]=1;
        maze[5][3]=1;
        maze[6][5]=1;

        //展示迷宫
        System.out.println("迷宫为：");
        for (int i = 0; i < 8 ; i++) {
            for (int j = 0; j < 8; j++) {
                System.out.print(maze[i][j]+" ");
            }
            System.out.println();
        }
        System.out.println();

        walkTheMaze(maze,1,1);

        //走完迷宫后形成的路
        System.out.println("走完后的迷宫：");
        for (int i = 0; i < 8 ; i++) {
            for (int j = 0; j < 8; j++) {
                System.out.print(maze[i][j]+" ");
            }
            System.out.println();
        }

    }



    // 1:表示墙体，2：表示走的路径，3：表示已走过但走不通的格子
    public static boolean walkTheMaze(int[][] maze,int m,int n){

        //如果已经到达终点，就直接返回true
        if(maze[6][6] == 2){
            return true;
        }

        //如果走的这一个没有走过，就先将此格标志为2
        if(maze[m][n] == 0){
            maze[m][n] = 2;

            //依次从此格：->下->右->左->上
            if(walkTheMaze(maze, m+1, n)){
                return true;
            }else if(walkTheMaze(maze, m, n+1)){
                return true;
            }else if(walkTheMaze(maze, m, n-1)){
                return true;
            }else if(walkTheMaze(maze, m-1, n)){
                return true;
            }else{
                //所有方向都走不通,就说明这个格子到不了终点
                maze[m][n] = 3;
                return false;
            }
        }else{
            return false;
        }
    }

}
```

<br/><br/><br/><br/>

### 3.八皇后问题

<br/>

问题：在一个8 x 8 的棋盘上，依次放置八个棋子，要求这8个棋子中任意两个，不能在同一行，同一列，同一斜线

<br/>

实现简述：

1）先放第一个棋子，依次放置在第一行的每一格，每放入一格，先检查是否可以放，

2）可以的话，就继续在第二行的每一格放第二个棋子，同样检查是否可以放

3）可以的话，就继续在第三行的每一格放第三个棋子，与上面两步同样的步骤，直到放完8个棋子。

4）由于放置的每一格都会向下延申而不会继续放这一行的下一格，所以只有当下一行的所有情况都放完才会继续放上面的另一格，这样就实现了将八皇后的每一种情况的展示出来

<br/>

代码实现：

```java
package Recursion;

public class QueueOfEight {

    static int count = 0;  //统计总共有多少种
    static int max = 8;    //总共有八个皇后

    //将满足的组合放入arr中，比如arr[1]=2,就知道第二个皇后放在第二行第三个位置
    static int[] arr = new int[8];

    public static void main(String[] args) {
        check(0);
        System.out.println("总共有"+count+"种方法");
    }

    public static void check(int n){

        //当n==max时，说明在放第9个皇后，因为只有8个皇后，所以就知道已经放完了
        if(n == max){
            show();
            return;
        }

        //在这一行的每个位置判断满不满足
        for (int i = 0; i < max; i++) {

            arr[n] = i;

            //满足就放下一个皇后
            if(judge(n)){
                check(n+1);
            }
        }

    }

    //判断放在皇后放在这个位置会不会冲突
    //直接通过一维数组就可以知道会不会冲突
    public static boolean judge(int n){

        for (int i = 0; i < n ; i++) {

          //当arr[n] == arr[i]表示二者处在同一列
          //当Math.abs(i-n) == Math.abs(arr[i]-arr[n])表示二者在一条斜线上
          //比如arr[1]=2,arr[2]=3,就知道第二个皇后放在第二行第三个位置，第三个皇后凡在第三行第四个位置，
          //这样一看，3-2=1，4-3=1，所以在一条斜线上，不行
          if(arr[n] == arr[i] ||
                  Math.abs(i-n) == Math.abs(arr[i]-arr[n]))
              return false;
          }
        return true;
    }

    //展示满足的情况
    public static void show(){
        count++;
        for (int i = 0; i < max; i++) {
            System.out.print(arr[i]+" ");
        }
        System.out.println();
    }

}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （五）排序

<br/>

### 1.时间复杂度

<br/>

**时间频度**

<br/>

定义：一个算法中语句执行的次数称为时间频度，记为：T(n)

注意：时间频度可以忽略常数，忽略低次项，忽略平方的系数

<br/>

**时间复杂度**

<br/>

作用：在事前，通过代码判断哪一种算法更优

定义：一般情况下，算法中的基本操作语句的重复执行次数是问题规模n的某个函数，用T(n)表示，若有某个辅助函数f(n)，使得当n趋近于无穷大时，T(n)/f(n)的极限值为一个不为0的常数，则称f(n)是T(n)的同数量级函数，记作T(n)=O(f(n)),称O(f(n))就是算法的渐进时间复杂度，简称时间复杂度

<br/>

计算时间复杂度的方法：

1）用常数1代替运行时间中的所有加法常数

2）修改后的运行次数函数中，只保留最高项

3）取出最高项的系数

<br/>

常见的时间复杂度：

O(1) < O(logn) < O(n) < O(n*logn) < O(n^2) < O(n^k) < O(2^n)

<br/><br/>

**空间复杂度**

<br/>

定义：该算法所消耗的存储空间

<br/><br/><br/><br/>

### 2.排序算法介绍

<br/>

定义：排序是将一组数据按照指定的顺序进行排列的过程

<br/>

分类：

1）内部排序：将排序的数据直接全部加载到内存中进行排序

2）外部排序：由于数据量过大，无法全部加载到内存中，需要借助外部存储

<br/>

1）稳定排序：存在同样元素时，排序后不改变原有顺序

2）不稳定排序：存在同样元素时，排序后可能改变原有顺序

<br/>

常见的内部排序：冒泡排序，选择排序，插入排序，希尔排序，快速排序，归并排序，堆排序，桶排序，基数排序

<br/>

![image-20220127164529962](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru13.png)

<br/><br/><br/><br/>

### 3.冒泡排序

<br/>

思想：

通过对排序序列从前到后，依次比较相邻元素的值，若发现逆序则交换，使值较大（或较小）的元素向后移，从而使得每一轮循环之后，最大或最小的元素排在最后

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru7.png" alt="image-20220127155721735" style="zoom:80%;" />

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class BubblingSort {

    public static void main(String[] args) {
        
        int[] arr = new int[]{1,2,3,5,4};
        boolean change0 = false;

        //冒泡排序
        //第一遍的循环表示轮数，排序n个数，就要排n-1轮
        //下一个循环是遍历每一轮，让最大的数排在最后，且每过一轮arr.length-1-i
        for (int i = 0; i < arr.length-1; i++) {
            for (int j = 0; j < arr.length-1-i; j++) {
                if(arr[j] > arr[j+1]){
                    change0 = true;
                    int tem = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = tem;
                }
            }

            //如果这一轮一次都没有改变,表示已经排好序，就直接退出
            if(change0){
                change0 = false;
            }else {
                break;
            }
        }

        System.out.println(Arrays.toString(arr));


    }
}
```

<br/><br/><br/><br/>

### 4.选择排序

<br/>

思想：

总共有n个元素，第一次从arr[0] ~ arr[n-1]选取最小（或最大）的值，与arr[0]交换；第二次从arr[1] ~ arr[n-1]选取最小（或最大）的值，与arr[1]交换；依次类推，最终排序完成

<br/>

![image-20220127160312838](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru8.png)

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class SelectSort {

    public static void main(String[] args) {

        int[] arr = new int[]{2,4,1,5,3};

        for (int i = 0; i < arr.length-1; i++) {

            int mixIndex = i;   //记录最小值对应的序号
            int tem = arr[i];   //记录最小值

            //因为这个最小值是要与最后一位数比较的，所以这个地方为arr.length
            for (int j = i+1; j < arr.length; j++) {
                  if(arr[j] < tem){

                      //如果这个j的比现在的最小数要小的话，就要将最小值和其对应的序号记录下来
                      mixIndex = j;
                      tem = arr[j];
                  }
            }

            //将第i个数与数组中i后面的最小值进行替换
            int x = arr[i];
            arr[i] = tem;
            arr[mixIndex] = x;
        }

        System.out.println(Arrays.toString(arr));
    }
}
```

<br/><br/><br/><br/>

### 5.插入排序

<br/>

思想：

把n个待排序的元素看成一个有序表和一个无序表，开始时有序表中只包含1个元素，无序表中包含有n-1个元素，排序过程中每次取无序表中最左边的元素，插入到有序表中对应得位置

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru9.png" alt="image-20220127160802698" style="zoom:80%;" />

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class InsertSort {

    public static void main(String[] args) {

        int[] arr = new int[]{2,4,1,5,3};

        //总共要进行arr.length轮，又是从1开始，所以后面用arr.length
        for (int i = 1; i < arr.length; i++) {

            int cur = i-1;  //记录前面值的序号
            int tem = arr[i];  //记录要被插入的值

            while(cur >= 0 && arr[cur] > tem){
                arr[cur+1] = arr[cur];
                cur--;
            }

            //将要插入的值插到对应的位置
            arr[cur+1] = tem;

        }

        System.out.println(Arrays.toString(arr));

    }

}
```

<br/><br/><br/><br/>

### 6.希尔排序

<br/>

思想：

把序列按下标得一定增量分组，对每组使用直接插入排序；随着增量得减少，每组包含得元素越来越多，当增量减少为1时，排序成功

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru10.png" alt="image-20220127161354193" style="zoom:67%;" />

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class ShellSort {

    public static void main(String[] args) {

        int[] arr = new int[]{2,4,1,5,3,10,9,2,4};

        //确定每一次分组的间隙是多大
        for(int pag = arr.length/2;pag>0;pag/=2){

            for(int i = pag;i<arr.length;i++){

                //这个地方实质是一个插入排序，所以需要将插入的数据先保存，然后进行移动
                //最后进行赋值
                int index = i;
                int tem = arr[i];

                //如果tem比此组最右边的值要小，才会进入if，否则说明这一次循环数组不需要改变
                if(tem < arr[index-pag]){
                    while(index-pag >= 0 && tem < arr[index-pag]){
                        arr[index] = arr[index-pag];
                        index -= pag;
                    }

                    arr[index] = tem;
                }
            }

        }

        System.out.println(Arrays.toString(arr));
    }
}
```

<br/><br/><br/><br/>

### 7.快速排序

<br/>

思想：

选择最左边的数据为分界线key，创建两个指针分别指向最左边和最右边，先让右边指针向左移动找到比key小的元素，再让左边指针向右移动找到比key大的元素，都找到后交换数据，左右指针重复相同操作，直到左右指针相遇，这时交换key与指针处的数据，使得在key左边的数据都比key小，右边的数据都比key大；再通过递归，分别对key左边和右边进行相同的操作，在只剩下一个数据时，返回；这样递归完成后就是有序的

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class QuickSort {

    public static void main(String[] args) {
        int[] arr = new int[]{2,11,1,5,3,10,9,2,4};
        quickSort(arr,0,arr.length-1);

        System.out.println(Arrays.toString(arr));

    }


    //快速排序
    public static void quickSort(int[] arr,int left,int right){

        if(left >= right){
            return;
        }

        int l = left;             //记录最左边的索引
        int r = right;            //记录最右边的索引
        int key = arr[left];      //以此值为分界线，让数组左边的值小于key,右边的值大于kay
        int tem;                  //临时变量

        //由于左右指针分别向右和向左进行遍历，所以二者最后一定会相遇，相遇说明整个数组已经遍历完了
        while(l != r){

            //这个一定要先让右边走，因为右边找的是比key小的元素，
            //这就可以让最后相遇的是比key小的元素，这样在与key交换后就保证比key小的都在左边

            //从右边找比key小的元素
            while(arr[r]>=key && l<r){
                r--;
            }

            //从左边找比key大的元素
            while (arr[l]<=key && l<r){
                l++;
            }

            //如果找到后发现l和r没有相遇，就说明找到了比key大和比key小的元素，进行交换
            if(l<r){
                tem = arr[l];
                arr[l] = arr[r];
                arr[r] = tem;
            }

        }

        //遍历完数组后，就将相遇的元素与key进行一个交换
        if(left != l) {
            tem = arr[left];
            arr[left] = arr[l];
            arr[l] = tem;
        }

        //从左边分组
        quickSort(arr,left,l-1);
        //从右边分组
        quickSort(arr,l+1,right);
    }
}
```

<br/><br/><br/><br/>

### 8.归并排序

<br/>

思想：

首先，将一个数组从中间分为两个数组，再将新的数组分别递归，继续不断分为两个数组，直到数组中只有一个元素；分完后，对数据进行合并，创建左右指针分别指向左边数组第一个元素和右边数组第一个元素，对数据进行比较，将更小（或更大）的元素放在临时数组内，同时将指针后移，继续比较，直到一方全部放入临时数组；再将另一方剩余的元素放入数组，最后将数组内的元素赋值给要排序的数组。全部递归完成后，数组有序

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru12.png" alt="image-20220127163527816" style="zoom:80%;" />

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class MergeSort {

    public static void main(String[] args) {

        int[] arr = new int[]{2,11,1,5,3,10,9,2,4};
        int[] temArr = new int[arr.length];

        grouping(arr,0,arr.length-1,temArr);

        System.out.println(Arrays.toString(arr));

    }


    //将数组分为一个个小元素
    public static void grouping(int[] arr,int left,int right,int[] temArr){

        if(left >= right){
            return;
        }
        int mid = (left+right)/2;

        //从左边开始分
        grouping(arr,left,mid,temArr);
        //从右边开始分
        grouping(arr,mid+1,right,temArr);

        //将左右两边合并
        merge(arr,left,mid,right,temArr);

    }

    //将左右两边合并为一个数组
    public static void merge(int[] arr,int left,int mid,int right,int[] temArr){

        int l = left;    //记录左边的第一个元素
        int r = mid+1;   //记录右边的第一个元素
        int temp = left; //记录临时数组的最左边序号

        //将左右两边数组合并为一个数组
        while(l<=mid && r<=right){

            //如果左边第一个元素小于右边第一个元素，就将左边第一个元素放入temArr
            //这个地方要有等于，否则有相等数的时候就会一直循环
            if(arr[l] <= arr[r]){
                temArr[temp++] = arr[l++];
            }

            //如果右边第一个元素小于左边第一个元素，就将右边第一个元素放入temArr
            if(arr[l] > arr[r]){
                temArr[temp++] = arr[r++];
            }

        }

        //当左边遍历完后,将右边剩余的放入临时数组
        while(r<=right){
            temArr[temp++] = arr[r++];
        }

        //当右边遍历完后,将左边剩余的放入临时数组
        while(l<=mid){
            temArr[temp++] = arr[l++];
        }

        //都放入临时数组后将临时数组中的值赋值给排序数组
        for (int i = left; i <= right ; i++) {
            arr[i] = temArr[i];
        }

    }
}
```

<br/><br/><br/><br/>

### 9.基数排序

<br/>

思想：

创建10个桶，首先看个位，比如个位为0，就放入第0个桶，遍历数组将数据放入后，从第0个桶开始拿数据放到数组中，全部放回数组后；再看十位，同样的操作；一直到最高位，最后在数组中的就是拍好序的数组

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class CardinalitySort {

    public static void main(String[] args) {


        int[] arr = new int[]{2345,112,356,9,87,56,4321};
        //首先要确定数组中的最大数有几位
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if(max<arr[i]){
                max=arr[i];
            }
        }
        int maxLength = (""+max).length();


        //创建桶来装数据
        int[][] bucket = new int[arr.length][10];
        //创建一个数组记录桶中有多少个数据
        int[] count = new int[10];

        for(int i=0,n=1;i<maxLength;i++,n*=10){

            //遍历数组将数据放入桶中
            for (int j = 0; j < arr.length; j++) {

                //记录余数
                int remainder= arr[j]/n%10;
                //将数据放入桶中
                //这个地方容易出错
                bucket[count[remainder]++][remainder] = arr[j];

            }


            //将桶中的元素取出放入数组中
            int num = 0;
            for (int j = 0; j < 10; j++) {
                for (int k = 0; k < count[j]; k++) {
                    //这个地方容易出错
                    arr[num++] = bucket[k][j];
                }

                //count需要清0
                count[j]=0;
            }

            System.out.println(Arrays.toString(arr));
        }

    }
}
```

<br/><br/><br/><br/>

### 10.堆排序

<br/>

在 树 -> 二叉树 处

<br/><br/><br/><br/><br/><br/><br/><br/>

## （六）查找

<br/>

### 1.基本概念

<br/>

定义：在指定数组中找到指定数据

<br/>

通常有三种类型：

1）顺序查找：从头开始，一一进行比较，相等就找到了

2）二分查找

3）插值查找

<br/><br/><br/><br/>

### 2.二分查找

<br/>

二分查找基本思想：将n个元素分成大致相等的两部分，取a[n/2]与x做比较，如果x=a[n/2],则找到x,算法中止；如果x<a[n/2],则只要在数组a的左半部分继续搜索x,如果x>a[n/2],则只要在数组a的右半部搜索x.

<br/>

要求：已经从小到大排序好

<br/>

比如：

[1,2,3,4,5,6,7,8,9]，要查找的数：2

首先找中间位置5，由于2<5，所以向左边找；再取中间3，由于2<3，继续向左找；取中间2，等于，表示已经找到

<br/>

代码实现：

```java
package Search;

public class BinarySearch {

    public static void main(String[] args) {

        int arr[] = new int[]{1,2,3,4,5,6,8,9};
        int i = binarySearch(arr, 0, arr.length - 1, 10);
        System.out.println(i);

    }

    public static int binarySearch(int[] arr, int left, int right, int val){

        //首先判断是否找到或者数组是否为空
        if(arr == null || arr.length<1 || left >right){
            return -1;
        }

        int mid = (left + right)/2;

        if(arr[mid] > val){
            return binarySearch(arr, left, mid-1, val);
        }else if(arr[mid] < val){
            return binarySearch(arr, mid+1, right, val);
        }else {
            return mid;
        }

    }
}
```

<br/><br/><br/><br/>

### 3.插值查找

<br/>

思想：与二分查找相同，只是分割比例不是固定的1/2，而是变动的

<br/>

代码可以看到只变动了一个地方：

```java
package Search;

public class InterpolateSearch {

    public static void main(String[] args) {
        int arr[] = new int[]{1,2,3,4,5,6,8,9};
        int i = interpolateSearch(arr, 0, arr.length - 1, 5);
        System.out.println(i);
    }

    public static int interpolateSearch(int[] arr,int left,int right,int val){

        if(arr.length<1 || arr[left]>val || arr[right] <val || left >right){
            return -1;
        }

        //变动
        int mid = left+(right-left)*(val-arr[left])/(arr[right]-arr[left]);

        if(arr[mid] > val){
            return interpolateSearch(arr, left, mid-1, val);
        }else if(arr[mid] < val){
            return interpolateSearch(arr, mid+1, right, val);
        }else {
            return mid;
        }
    }
}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

## （七）树

<br/>

### 1.基本用语

<br/>

结点：树的结点包含一个数据和若干指向其子树的分支。 

度：结点拥有的子树数。  

叶子（终端结点）：度数为0的结点。  

分支结点（非终端结点）：度数不为0的结点。 注意：除根节点外，分支结点也称为内部结点。 

树的度：分支结点中度数最大结点的度数。 

孩子：结点的子树的根称为结点的孩子。 相应的，该结点称为孩子的双亲。 

兄弟：同一个双亲的孩子之间称为兄弟。 

祖先：从根到该结点所经分支上的所有结点（包含根和双亲）。 反之，以该结点为根的所以结点称为该结点的子孙。 

有序树：树中结点的各子树看成从左到右都是有序的，称为有序树 反之，为无序树 。

<br/><br/><br/><br/>

### 2.二叉树

<br/>

#### （1）基本概念

<br/>

定义：每个结点最多只有两个子节点的一种树

结点分别称为：左结点和右结点，放在不同位置二叉树是不一样的

<br/>

一些概念：

满二叉树：如果该二叉树的所有叶子结点都在最后一层，并且结点总数为2^n-1（层数从1开始）

完全二叉树：如果该二叉树的所有叶子节点都在最后一层或倒数第二层，而且最后一层叶子结点左边连续，倒数第二层叶子结点右边连续

<br/>

顺序二叉树：

一个结点的数组下标为n，则左子树下标为：2\*n+1，右子树下标为：2\*n+2；

就是将一个数组以这种二叉树的形式进行输出

<br/><br/>

#### （2）基本操作

<br/>

**遍历**

<br/>

采用递归的方式进行遍历

这个地方直接上代码会比较好理解

<br/>

遍历的方式有三种：

根据二叉树父结点的输出位置来判断

父节点先输出就是先序遍历，中间输出就是中序遍历，后面输出就是后序遍历

三种输出方式代码是一致的，只是改变了代码的位置。

<br/><br/>

**查找**

<br/>

就是遍历二叉树，找到了就返回

<br/><br/>

**删除**

<br/>

就是首先找到这个结点的上一个结点，直接将上一个结点的一边置空就可以了

<br/><br/>

整体代码：

```java
package Tree.BInaryTree;

public class Traverse {
    public static void main(String[] args) {

        //简单建立二叉树
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(4);
        Node node5 = new Node(5);
        Node node6 = new Node(6);
        Node node7 = new Node(7);

        node1.left = node2;
        node1.right = node3;
        node3.right = node6;
        node2.right = node5;
        node2.left = node4;
        node5.left = node7;

        BinaryTree binaryTree = new BinaryTree();
        binaryTree.head = node1;

        //遍历结点
        binaryTree.preOrder();
        System.out.println();
        binaryTree.middleOrder();
        System.out.println();
        binaryTree.postOrder();
        System.out.println();

        //查找结点
        Node node8 = new Node(8);
        Node search = binaryTree.search(node1, node7);
        System.out.println(search);

        //删除结点
        binaryTree.delete(node2);
        binaryTree.preOrder();

    }
}


//二叉树
class BinaryTree{
    public Node head;

    //前序遍历
    //其实中序和后序代码是一样的，只不过是改变了输出的位置
    public void preOrder(){
       preOrder(head);
    }
    public void preOrder(Node node){

        if(head == null){
            return;
        }

        System.out.print(node.no+" ");

        //遍历左子树
        if(node.left != null){
            preOrder(node.left);
        }

        //遍历右子树
        if(node.right != null){
            preOrder(node.right);
        }

    }


    //中序遍历
    public void middleOrder(){
        middleOrder(head);
    }
    public void middleOrder(Node node){
        if(head == null){
            return;
        }

        if(node.left != null){
            middleOrder(node.left);
        }

        System.out.print(node.no+" ");

        if(node.right != null){
            middleOrder(node.right);
        }
    }


    //后序遍历
    public void postOrder(){
        postOrder(head);
    }
    public void postOrder(Node node){

        if(head == null){
            return;
        }

        if(node.left != null){
            postOrder(node.left);
        }

        if(node.right != null){
            postOrder(node.right);
        }

        System.out.print(node.no+" ");
    }


    //前序查找结点
    //查找结点实际上就是在遍历二叉树，如果满足就返回
    public Node search(Node node,Node target){

        if(head == null){
            return null;
        }

        //如果找到了就直接返回
        if(node.no == target.no){
            return node;
        }

        //先到左边找看有没有目标结点，有的话就返回当前结点
        if(node.left != null){
            Node l = search(node.left,target);
            if(l !=null){
                return l;
            }
        }

        //再向右边找
        if(node.right != null){
            Node r = search(node.right,target);
            if(r !=null){
                return r;
            }
        }

        //左边右边找完了，还是没有，直接返回null
        return null;

    }
    
    
    //删除结点
    //删除结点就是首先找到这个结点的上一个结点，直接将上一个结点的一边置空就可以了
    public void delete(Node target){
        if(head == null){
            return;
        }
        //假如要删除的结点是第一个结点，直接将二叉树置空
        if(head.no==target.no){
            head = null;
        }else{
            delete(head,target);
        }
        
    }
    public void delete(Node node,Node target){
        
        if(node.left != null){
            if(node.left.no != target.no) {
                delete(node.left, target);
            }else{
                node.left = null;
                return;
            }
        }

        if(node.right != null){
            if(node.right.no != target.no) {
                delete(node.right, target);
            }else{
                node.right = null;
                return;
            }
        }
        
    }

}


//树中的结点
class Node{
    public int no;
    public Node left;
    public Node right;

    public Node(int no) {
        this.no = no;
        this.left = null;
        this.right = null;
    }

    @Override
    public String toString() {
        return "Node{" +
                "no=" + no +
                '}';
    }
}
```

<br/><br/><br/><br/>

#### （3）线索二叉树

<br/>

基本介绍：

1）n个结点的二叉链表中含有n+1个空指针域，利用空指针域存放指向结点再某种遍历次序下的前驱和后继结点的指针，这种附加的指针称为线索

2）这种加上了线索的二叉链表称为线索链表，相应的二叉树称为线索二叉树。根据遍历次序的不同，可以分为前序线索二叉树，中序线索二叉树和后序线索二叉树

3）一个结点的前一个结点，称为前驱结点；一个结点的后一个结点，称为后继结点

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru14.png" alt="image-20220209224332685" style="zoom: 67%;" />

<br/>

代码实现：

```java
package Tree.BInaryTree;

public class ThreadBinaryTree {
    public static void main(String[] args) {
//简单建立二叉树
        ThreadNode threadNode1 = new ThreadNode(1);
        ThreadNode threadNode2 = new ThreadNode(2);
        ThreadNode threadNode3 = new ThreadNode(3);
        ThreadNode threadNode4 = new ThreadNode(4);
        ThreadNode threadNode5 = new ThreadNode(5);
        ThreadNode threadNode6 = new ThreadNode(6);
        ThreadNode threadNode7 = new ThreadNode(7);

        threadNode1.left = threadNode2;
        threadNode1.right = threadNode3;
        threadNode3.right = threadNode6;
        threadNode2.right = threadNode5;
        threadNode2.left = threadNode4;
        threadNode5.left = threadNode7;

        ThreadTree threadTree = new ThreadTree();
        threadTree.head = threadNode1;

        threadTree.toThreadTree(threadNode1);
        System.out.println(threadNode5.right);
        System.out.println(threadNode4.right);
        System.out.println(threadNode3.left);
        System.out.println(threadNode6.left);
        System.out.println(threadNode7.left);
        System.out.println(threadNode6.right);
        System.out.println(threadNode4.left);

        System.out.println();

        //前序遍历线索二叉树
        threadTree.preOrder();
    }
}


class ThreadTree{

    public ThreadNode head;
    public ThreadNode pre;  //指向当前节点的前驱结点

    //注释了的是中序线索二叉树，没注释的是前序，都是对的
    //将二叉树变为线索二叉树
    public void toThreadTree(ThreadNode threadNode){

        /*if(threadNode.left != null && threadNode.leftType == 0){
            toThreadTree(threadNode.left);
        }
        
        if(threadNode.left == null){
            threadNode.left = pre;
            threadNode.leftType = 1;
        }
        
        if(pre != null && pre.right == null){
            pre.right = threadNode;
            pre.rightType = 1;
        }
        
        pre = threadNode;
        
        
        if(threadNode.right != null && threadNode.rightType == 0){
            toThreadTree(threadNode.right);
        }*/

        //如果该结点左边为空，就直接将左指针指向pre，表示这个结点的前驱结点是pre
        if(threadNode.left == null){
            threadNode.left = pre;
            threadNode.leftType = 1;
        }

        //这个其实和上面是一样的，对于前一个结点的后继结点就是当前结点
        if(pre != null && pre.right == null){
            pre.right = threadNode;
            pre.rightType = 1;
        }

        pre = threadNode;

        if(threadNode.left != null && threadNode.leftType == 0){
            toThreadTree(threadNode.left);
        }

        if(threadNode.right != null && threadNode.rightType == 0){
            toThreadTree(threadNode.right);
        }
        
    }


    //遍历线索二叉树
    public void preOrder(){
        preOrder(head);
    }
    public void preOrder(ThreadNode threadNode){
        if(threadNode.left != null && threadNode.leftType == 0){
            preOrder(threadNode.left);
        }

        System.out.println(threadNode);

        if(threadNode.right != null && threadNode.rightType == 0){
            preOrder(threadNode.right);
        }
    }


}

//线索二叉树结点
class ThreadNode{
    public int no;
    public ThreadNode left;
    public int leftType;
    public ThreadNode right;
    public int rightType;

    public ThreadNode(int no) {
        this.no = no;
        this.left = null;
        this.leftType = 0;
        this.right = null;
        this.rightType = 0;
    }

    @Override
    public String toString() {
        return "ThreadNode{" +
                "no=" + no +
                '}';
    }
}
```

<br/><br/><br/><br/>

#### （4）堆排序

<br/>

基本介绍：堆排序是利用堆这种数据结构设计的一种排序算法，是一种选择排序，它的最坏，最好，平均时间复杂度均为O(nlogn)，他也是不稳定排序。

<br/>

大顶堆：每个结点的值都大于左右结点的值，通常用于从小到大排序

小顶堆：每个结点的值都小于左右结点的值，通常用于从大到小排序

<br/>

大顶堆举例：

<br/>

![image-20220213201356034](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru15.png)

<br/><br/>

思想说明：

1）堆排序是将数组首先建立为一个大顶堆，然后将根节点的值与最后一个结点的值进行对换；（这里就是将最大的值移到数组的最后，数组长度减一）

2）由于开始是一个大顶堆又只交换了根节点和最后一个结点，且数组长度已经减一，这时以它左右孩子为根节点的子树都是大顶堆，所以可以直接从根节点开始，继续形成大顶堆，再次将根节点的值与数组倒数第二个结点对换，数组长度再减一

3）后面一直重复第二步，直到数组长度为1，这时排序成功

<br/>

创建大顶堆的过程：

1）采用递归的方式进行

2）当是第一次创建大顶堆时，由于此时堆是没有规律的，所以要从最后一个非叶子节点开始不断进行第三步（将以该结点为根节点的子树转换为大顶堆），进行完后，以该结点为根节点的子树就是一个大顶堆，继续向上一个非叶子节点进行，当不断向上一个结点进行时，最后会到达根节点，这时整个堆就是一个大顶堆

3）首先定义一个值max记录当前结点的下标，比较当前结点和其左右子节点的值，将max指向最大值的下标，将当前结点与max对应的值进行交换，将max传入下一层（就是当前结点转化为了max下标的结点），当发现是叶子结点就返回

<br/>

代码实现：

```java
package Sort;

import java.util.Arrays;

public class HeapSort {

    public static void main(String[] args) {
        int[] arr = new int[]{2,4,1,5,3};
        heapSort(arr,arr.length);
        System.out.println(Arrays.toString(arr));
    }


    /**
     * 对指定结点进行大顶堆排序
     * 由于仍然是对数组进行排序，所以并不是传入结点，而是传入对应下标
     * @param arr   要排序的数组
     * @param length  数组的长度
     * @param m   当前结点下标
     */
    public static void sort(int[] arr,int length,int m){


        int max = m;       //记录最大值
        int left = 2*m+1;  //记录左子节点
        int right = 2*m+2; //记录右子节点


        //比较找到三个点中最大的
        if (left<length && arr[max] < arr[left]){
            max = left;
        }
        if (right<length && arr[max] < arr[right]){
            max = right;
        }

        //找到最大后，进行交换
        if(max != m){
            int tem = arr[m];
            arr[m] = arr[max];
            arr[max] = tem;

            //继续对下面进行递归，让下面也满足大顶堆
            sort(arr, length, max);

        }

    }


    /**
     * 对整个堆进行排序（上面的方法是对一个结点进行排序）
     * @param arr      要排序的数组
     * @param length   数组的长度
     */
    public static void heapSort(int[] arr,int length){

        //首先将数组进行堆的初始创建
        for(int i=length/2-1;i>=0;i--){
            sort(arr,length,i);
        }

        //完成第一轮后，这个堆就已经是一个大顶堆
        //对数组进行排序

         for (int i = length-1; i >= 0; i--) {

            //将堆顶与当前最后一个元素进行交换
            //每交换一次，数组长度-1
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            //经过初始化后，数组已经减1了，所以传入的是length-1
            sort(arr,i,0);

        }
    }

}
```



<br/><br/><br/><br/>

#### （5）哈夫曼树与哈夫曼编码

<br/>

##### ① 哈夫曼编码

<br/>

基本介绍：

1）给定n个权值作为n个叶子结点，构造一个二叉树，如果该二叉树的带权路径长度（wpl）达到最小，称这样的树为最优二叉树，也称为哈夫曼树（Huffman）

2）路径：假设根节点在第0层，那第n层的路径长度就是n

3）带权路径长度：所有叶子节点的路径长度乘以权的和

<br/>

![image-20220213204834964](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru16.png)

<br/><br/>

创建过程：

1）将每个数据都做成一个结点，根据权值从小到大进行排序，将每个结点视为一个树

2）取出权值最小的两个结点

3）组成一个新的树，左右结点就是最小的两个结点，权值就是两节点之和

4）将这个树放回数组并删除原先的两个结点，重复1，2，3，4，当数组中只剩下一个结点时，哈夫曼树就已经创建好了

<br/>

代码实现：

```java
package Tree.BInaryTree;

import java.util.ArrayList;
import java.util.Collections;

public class HuffmanTree {

    public static HuffmanNode head;

    public static void main(String[] args) {

        int[] arr = {13,7,8,3,29,6,1};

        // 对创建成功的哈夫曼树进行一个遍历
        head = createHuffmanTree(arr);
        preOrder(head);

    }



    //创建哈夫曼树
    public static HuffmanNode createHuffmanTree(int[] arr){

        ArrayList<HuffmanNode> arrayList = new ArrayList<>();

        //将数组放入到ArrayList中
        for (int m: arr) {
            arrayList.add(new HuffmanNode(m));
        }

        while(arrayList.size()>1) {

            //将数组进行排序
            Collections.sort(arrayList);

            HuffmanNode h0 = arrayList.get(0);  //arrayList中第一个结点
            HuffmanNode h1 = arrayList.get(1);  //arrayList中第二个结点

            //将最小的两个数进行合并形成一个新的树
            HuffmanNode newNode = new HuffmanNode(h0.weight+h1.weight);
            newNode.left = h0;
            newNode.right = h1;

            //将新结点加入到arrayList中
            arrayList.add(newNode);

            //将原先的两个结点删除
            arrayList.remove(h0);
            arrayList.remove(h1);

        }

        return arrayList.get(0);

    }


    //对树进行遍历
    public static void preOrder(HuffmanNode node) {

        if (head == null) {
            return;
        }

        System.out.print(node.weight + " ");

        //遍历左子树
        if (node.left != null) {
            preOrder(node.left);
        }

        //遍历右子树
        if (node.right != null) {
            preOrder(node.right);
        }

    }
}


//哈夫曼树的结点
class HuffmanNode implements Comparable<HuffmanNode>{
    public int weight;  //记录结点的权值
    public HuffmanNode left;
    public HuffmanNode right;

    public HuffmanNode(int weight) {
        this.weight = weight;
        this.left = null;
        this.right = null;
    }

    @Override
    public String toString() {
        return "HuffmanNode{" +
                "weight=" + weight +
                '}';
    }

    //表示从小到大排序
    @Override
    public int compareTo(HuffmanNode o) {
        return this.weight - o.weight;
    }
}
```

<br/><br/><br/><br/>

##### ② 哈夫曼编码

<br/>

定义：就是在哈夫曼树的基础上将每一条边都编上号，通向左结点的编上0，通向右节点的编上1，这样当达到叶子节点时，路径中所有数字组合起来就是该叶子结点的编号。

<br/>

经过哈夫曼编码后，任何一个叶子结点的编码都不会成为其他叶子结点编码的前缀，从而可以数据压缩。

<br/>

比如对于字符a，假设编号为001，而存储一个字符需要八位（1个byte），经过这种编码后就只有三位，所以数据量减少，实现压缩。

<br/><br/><br/><br/>

#### （6）二叉排序树

<br/>

定义：任何一个非叶子节点要求左子节点的值比当前结点的值小，右子节点的值比当前结点的值大；当存在相同的值时，可以放在左边或右边。

二叉排序树中序遍历时，即为从小到大排序

<br/>

![image-20220215193256641](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru17.png)

<br/><br/>

添加结点：

1）从根节点开始，当根节点为空时，直接赋值给根节点；

2）当根节点不空时，比较大小，若小于且左子树为空，将左子树指向当前节点，若小于但不为空，与左子树的结点进行比较，重复第2，3步相同动作，只是将根节点改为左子节点

3）若大于且右子树为空，将右子树指向当前结点，若大于且不为空，与右子树的结点进行比较，重复第2，3步相同动作，只是将根节点改为右子节点

<br/><br/>

删除结点：

1）找到要删除的结点node

- 从根节点开始，比较node与当前结点的大小，若node等于当前节点，直接返回当前节点；若小于当前节点且左子树不为空，向左子树继续查找，进入下一节点，进入左子树结点；若大于当前结点且右子树不为空，向右子树查找，进入下一节点
- 当比较下一个结点时，与上步动作相同，只是将根节点换为下一节点

2）找到要删除结点的父节点

- 从根节点，如果根节点为空或者根节点就是要删除的结点node，直接返回null
- 若不满足上面两种情况，当左子树不为空且node的值小于当前节点，再判读左子树的值是否等于要删除的结点，如果等于，直接返回当前节点，否则向左子树查找，当前节点改为左子树结点；当右子树不为空且node的值大于当前结点，再判读右子树的值是否等于要删除的结点，如果等于，直接返回当前节点，否则向右子树查找，当前结点改为右子树结点。
- 重复第二步，当达到叶子系欸但还是没有找到，直接返回null

3）判断node是否存在，如果不存在，直接返回

4）否则，首先判断要删除的结点是否有父节点，如果没有，代表node即为根节点，这时有三种情况：

- node没有子节点，直接将根节点置空
- node只有一个子结点，直接将根节点指向子节点
- node有两个子节点，创建一个临时结点，由于存储左子树的最大值或右子树的最小值（这里以右子树的最小值为例），首先让临时节点指向node的右子节点，再一直向左循环，找到最左边的结点，调用删除结点的函数，删除这个结点，删除完后，将node结点的值改为临时节点的值

5）如果有父节点，这时有三种相同的情况：

- node没有子节点，首先判断node是父节点的左节点还是右节点，是哪种结点就将那边置为空
- node有一个子节点，首先判断node是父节点的左节点还是右节点，直接将父节点的那边指向node的子节点
- node有两个子节点，处理方法与第四步第三种情况相同

<br/><br/>

代码实现：

```java
package Tree.BInaryTree;

public class BinarySortTree {

    public static void main(String[] args) {

        int[] arr = {7,3, 5, 2, 3, 10, 4, 15, 11, 9};

        ArrToBinarySortTree(arr);

        head.middleOrder();
        System.out.println();


        //查找结点测试
        BinarySortNode node1 = new BinarySortNode(9);

        BinarySortNode search = search(node1);
        System.out.println(search);

        BinarySortNode farher = searchFarther(node1);
        System.out.println(farher);

        //测试删除结点
        deleteBinartSortNode(new BinarySortNode(5));
        head.middleOrder();
        System.out.println();


    }

    static BinarySortNode head;

    /**
     * 添加节点
     *
     * @param node 将要添加的结点
     */
    public static void addNode(BinarySortNode node) {

        if (head == null) {
            head = node;
            return;
        } else {
            head.addNode(node);
        }
    }


    /**
     * 将数组转化为一个排序二叉树
     *
     * @param arr 数组
     */
    public static void ArrToBinarySortTree(int[] arr) {

        for (int i = 0; i < arr.length; i++) {
            addNode(new BinarySortNode(arr[i]));
        }

    }


    /**
     * 找到要删除的结点
     *删除3时，由于3右子树中最小的也是3，就会进入删除3的死循环
     * @param node 要删除的结点
     * @return 找到的结点
     */
    public static BinarySortNode search(BinarySortNode node) {

        if (head == null) {
            return null;
        } else {
            return head.search(node);
        }
    }


    /**
     * 查找要删除结点的父节点
     * @param node  要删除的结点
     * @return      返回查找到的父节点
     */
    public static BinarySortNode searchFarther(BinarySortNode node){

        if(head == null){
            return null;
        }else{
            if(head.no == node.no){
                return null;
            }else {
                return head.searchFather(node);
            }
        }

    }

    /**
     * 删除结点
     * 删除结点是对有唯一标识的结点进行删除
     * @param node  要删除的结点
     */
    public static void deleteBinartSortNode(BinarySortNode node){

        BinarySortNode search = search(node);
        BinarySortNode farther = searchFarther(node);

        //如果没有要找的结点，直接返回
        if(search == null){
            return;
        }

        //如果这个结点是根结点
        if(farther == null){

            //分别判断没有左右结点，只有一个左右节点，有两个左右结点
            if(search.left == null && search.right == null){
                head = null;
            }else if(search.left != null && search.right != null){
                //创建一个临时变量记录右子树的最小值
                BinarySortNode temp = search.right;

                while(temp.left!=null){
                    temp = temp.left;
                }

                //由于一直向左子树找，所以temp指向的一定是叶子节点或者只有右子树的结点
                //所以不会再进入这个地方
                deleteBinartSortNode(temp);

                search.no = temp.no;

            }else{
                head =  (search.left != null) ? search.left : search.right;
            }
        }else{

            if(search.left == null && search.right == null){

                if(farther.left == search){
                    farther.left = null;
                }else {
                    farther.right = null;
                }

            }else if(search.left != null && search.right != null){

                BinarySortNode temp = search.right;

                while(temp.left != null){
                    temp = temp.left;
                }

                deleteBinartSortNode(temp);

                search.no = temp.no;

            }else{

                if(farther.left == search){
                    farther.left = (search.left == null)?search.right:search.left;
                }else{
                    farther.right = (search.left == null)?search.right:search.left;
                }

            }
        }



    }


}



//二叉排序树的结点
class BinarySortNode{

    public int no;
    public BinarySortNode left;
    public BinarySortNode right;

    public BinarySortNode(int no) {
        this.no = no;
        this.left = null;
        this.right = null;
    }


    //中序遍历
    public void middleOrder(){
        if(this == null){
            return;
        }

        if(this.left != null){
            this.left.middleOrder();
        }

        System.out.print(this.no+" ");

        if(this.right != null){
            this.right.middleOrder();
        }
    }


    @Override
    public String toString() {
        return "BinarySortNode{" +
                "no=" + no +
                '}';
    }


    //添加结点
    public void addNode(BinarySortNode node) {

        //如果添加结点的值小于当前节点，就放在左边，否则，放在右边
        if(this.no > node.no){
            if(this.left == null){
                this.left = node;
            }else{
                this.left.addNode(node);
            }
        }else{
            if (this.right == null){
                this.right = node;
            }else {
                this.right.addNode(node);
            }
        }
    }


    //查找结点
    public BinarySortNode search(BinarySortNode node) {

       if(this.no == node.no){
           return this;
       }else if(this.no > node.no){
           if(this.left != null){
             return this.left.search(node);
           }
           return null;
       }else{
           if(this.right != null){
               return this.right.search(node);
           }
           return null;
       }

    }


    //查找要查找结点的父节点
    public BinarySortNode searchFather(BinarySortNode node){

        if(this.left != null && this.no > node.no){
            if(this.left.no == node.no){
                return this;
            }else{
                return this.left.searchFather(node);
            }

        }

        if(this.right != null && this.no <= node.no){
            if(this.right.no == node.no){
                return this;
            }else{
                return this.right.searchFather(node);
            }
        }

        return null;

    }

}
```

<br/><br/><br/><br/>

#### （7）平衡二叉树

<br/>

定义：又称平衡二叉搜素树，AVL树，可以保证查询效率较高

特点：它是一颗空树或者它的左右子树高度差不超过1，并且它的左右子树都是一颗平衡二叉树。平衡二叉树首先是一个排序二叉树

<br/>

平衡二叉树的生成：

1）查看树的高度，左右子树的高度

- 查看树的高度可以采用递归，将左右子树的较大值加1后返回
- 左右子树的高度，直接将左右子树的height返回

```java
//查看树的高度
public int height(){
    return Math.max(this.left==null?0:this.left.height(),this.right==null?0:this.right.height())+1;
}

//查看当前结点左子树的高度
public int leftHeight(){
    return this.left==null?0:this.left.height();
}

//查看当前结点右子树的高度
public int rightHeight(){
    return this.right==null?0:this.right.height();
}
```

<br/>

2）左旋转与右旋转

```java
//左边比右边高大于1，右旋转
public void rightRotate(){

    //创建一个新的结点
    AVLNode temp = new AVLNode(this.no);

    //将新结点的右子树指向原来结点的右子树
    temp.right = this.right;

    //将新结点的左子树指向原先左节点的右子树
    temp.left = this.left.right;

    //将当前结点的值改为原先左节点的值
    this.no = this.left.no;

    //将当前节点的左子树指向左节点的左子树
    this.left = this.left.left;

    //将当前结点的右子树指向新结点
    this.right = temp;
}


//右边比左边高大于1，左旋转
public void leftRotate(){

  AVLNode temp = new AVLNode(this.no);
  temp.left = this.left;
  temp.right = this.right.left;
  this.no = this.right.no;
  this.right = this.right.right;
  this.left = temp;

}
```

<br/>

3）左右旋转结合

- 由于可能出现左结点的右子树高于左节点的左子树，这样会在右旋转的过程中使原本左右子树的高低兑换，导致仍然不平衡，这时首先需要将左节点进行右旋转，在进行左旋转
- 或者右节点的左子树高于右节点右子树，这样会在左旋转的过程中使原本左右子树的高低兑换，导致仍然不平衡，这时首先需要将右节点进行左旋转，在进行左旋转

```java
//如果右子树比左子树高于1，进行左旋转
if(this.rightHeight() - this.leftHeight() > 1){
    //如果右子树的左子树比右子树的右子树高进行右旋转
    if(this.right != null && this.right.rightHeight() < this.right.leftHeight()){
        this.right.rightRotate();
        this.leftRotate();
    }else{
        this.leftRotate();
    }

    //进行完后直接返回
    return;
}

if(this.leftHeight() - this.rightHeight() > 1){
    if(this.left != null && this.left.leftHeight() < this.left.rightHeight()){
        this.left.leftRotate();
        this.rightRotate();
    }else{
        this.rightRotate();
    }
}
```

<br/>

4）由于每次旋转都是在添加结点的过程中，这样添加结点的经过的每一个结点都会判断以当前结点为根节点的树是否是AVL树，从添加的结点到根节点都会判断一遍，这样就可以保证左后整体是一个AVL树。

<br/><br/>

代码实现：

```java
package Tree.BInaryTree;

public class AVLTree {

    public static void main(String[] args) {

        //int[] arr = {7,3,10,2,5,3,4,9,15};
        int[] arr = {10,11,7,6,8,9};

        ArrToBinarySortTree(arr);

        head.middleOrder();
        System.out.println();

        System.out.println(head.height());
        System.out.println(head.leftHeight());
        System.out.println(head.rightHeight());

        //System.out.println(head.left.right);




    }

    static AVLNode head;

    /**
     * 添加节点
     *
     * @param node 将要添加的结点
     */
    public static void addNode(AVLNode node) {

        if (head == null) {
            head = node;
            return;
        } else {
            head.addNode(node);
        }
    }


    /**
     * 将数组转化为一个排序二叉树
     *
     * @param arr 数组
     */
    public static void ArrToBinarySortTree(int[] arr) {

        for (int i = 0; i < arr.length; i++) {
            addNode(new AVLNode(arr[i]));
        }

    }





}


//二叉排序树的结点
class AVLNode{

    public int no;
    public AVLNode left;
    public AVLNode right;

    public AVLNode(int no) {
        this.no = no;
        this.left = null;
        this.right = null;
    }


    //中序遍历
    public void middleOrder(){
        if(this == null){
            return;
        }

        if(this.left != null){
            this.left.middleOrder();
        }

        System.out.print(this.no+" ");

        if(this.right != null){
            this.right.middleOrder();
        }
    }


    @Override
    public String toString() {
        return "AVLNode{" +
                "no=" + no +
                '}';
    }


    //添加结点
    public void addNode(AVLNode node) {

        //如果添加结点的值小于当前节点，就放在左边，否则，放在右边
        if(this.no > node.no){
            if(this.left == null){
                this.left = node;
            }else{
                this.left.addNode(node);
            }
        }else{
            if (this.right == null){
                this.right = node;
            }else {
                this.right.addNode(node);
            }
        }


        //每添加一个结点,进行一次平衡二叉树的调整

        //如果右子树比左子树高于1，进行左旋转
        if(this.rightHeight() - this.leftHeight() > 1){
            //如果右子树的左子树比右子树的右子树高进行右旋转
            if(this.right != null && this.right.rightHeight() < this.right.leftHeight()){
                this.right.rightRotate();
                this.leftRotate();
            }else{
                this.leftRotate();
            }

            //进行完后直接返回
            return;
        }

        if(this.leftHeight() - this.rightHeight() > 1){
            if(this.left != null && this.left.leftHeight() < this.left.rightHeight()){
                this.left.leftRotate();
                this.rightRotate();
            }else{
                this.rightRotate();
            }
        }

    }



    //查看树的高度
    public int height(){
        return Math.max(this.left==null?0:this.left.height(),this.right==null?0:this.right.height())+1;
    }

    //查看当前结点左子树的高度
    public int leftHeight(){
        return this.left==null?0:this.left.height();
    }

    //查看当前结点右子树的高度
    public int rightHeight(){
        return this.right==null?0:this.right.height();
    }


    //左边比右边高大于1，右旋转
    public void rightRotate(){

        //创建一个新的结点
        AVLNode temp = new AVLNode(this.no);

        //将新结点的右子树指向原来结点的右子树
        temp.right = this.right;

        //将新结点的左子树指向原先左节点的右子树
        temp.left = this.left.right;

        //将当前结点的值改为原先左节点的值
        this.no = this.left.no;

        //将当前节点的左子树指向左节点的左子树
        this.left = this.left.left;

        //将当前结点的右子树指向新结点
        this.right = temp;
    }


    //右边比左边高大于1，左旋转
    public void leftRotate(){

      AVLNode temp = new AVLNode(this.no);
      temp.left = this.left;
      temp.right = this.right.left;
      this.no = this.right.no;
      this.right = this.right.right;
      this.left = temp;

    }

}
```

<br/><br/><br/><br/><br/><br/><br/><br/>

### 3.多叉树

<br/>

#### （1）B树

<br/>

定义：B树是一种平衡的多路查找树，B树中所有结点的子树的最大值为B树的阶，用m表示。一棵m阶的B树，如果不为空，就必须满足以下特性：

1）树中的每个结点至多有m-1个关键字，即m棵子树（叶节点也算B树的结点）

2）除根节点外，所有非叶子节点只有含有（m+1）/ 2 -1 个关键字，即（m+1）/ 2 棵子树。根节点的关键字可以小于这个值，可以没有子树，如果有子树，则至少含有两棵。

3）所有叶子节点在同一层上（各子树没有高度差，绝对平衡）。叶节点不带信息，实际不存在

4）<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru19.png" alt="image-20220223144038434" style="zoom: 80%;" />

<br/><br/>

B树示意图：

<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru18.png" alt="image-20220223143941470" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru20.png" alt="image-20220223144116772" style="zoom:67%;" />

<br/><br/>

**问题：**

一棵含有n个关键字的m阶B树：

1）有多少个叶节点？

2）最小高度是多少？

3）最大高度是多少？

注：最小高度和最大高度不包括叶子节点

<br/>

答：

1）n+1 个叶子节点

2）做小高度就是每一个结点都有m-1个关键字

![image-20220223144613612](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru21.png)

3）中间乘2是因为只计算了右子树，还有左子树

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru23.png" alt="image-20220223144719754" style="zoom:67%;" />

<br/><br/>

**B树的插入：**

<br/>

- 首先找到值的位置，将值放入，当当前结点的关键字数量超过最大限度时
- 从中间位置（m+1）/ 2 将原结点的关键字分为两部分，左边的关键字在原结点中，右边的关键字放在新结点中，中间位置的结点插入到原结点的父节点
- 如果上面的操作导致父节点的关键字个数也超出了上限，那对父节点也进行同样的操作。如果一直传递到根节点，则创建新的根节点，树的高度增加1层。

<br/><br/>

**B树的删除：**

<br/>

- 如果待删除关键字在终端结点中，并且该结点的关键字大于（m+1）/ 2 - 1，直接从该终端结点中删除
- 如果待删除的关键字在终端结点中，并且终端结点的关键字个数等于（m+1）/ 2 - 1，而与该结点相邻的兄弟结点（左或右）结点中关键字的个数大于（m+1）/ 2 - 1，则从兄弟结点中借一个关键字。
- 如果待删除结点的关键字在终端结点中，并且终端结点的关键字个数等于（m+1）/ 2 - 1，而与该结点相邻的兄弟结点（左或右）结点中关键字的个数等于（m+1）/ 2 - 1，把当前节点和相邻结点再加上父节点的关键字合并，如果这次合并导致父节点关键字小于（m+1）/ 2 - 1，则继续合并父节点，如果一直传递到根节点，就合并后结束
- 如果待删除的结点不在终端结点中，则用关键字的直接前驱或直接后继来代替被删除的关键字，把问题转化为删除终端节点的问题

<br/><br/><br/><br/>

#### （2）B+树

<br/>

定义：B+树是对B树的一种变形

<br/>

图示：

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru24.png" alt="image-20220223150818697" style="zoom:67%;" />

<br/>

说明：

1）树中的实际关键字是在叶子结点中，只能在叶子节点中找到对应的数据

2）索引只是对数据大致位置的一种说明，需要不断索引，找到数据的范围，再顺序查找

3）叶子中的数据是通过链表连接，并且数据之间是有序的，通过第一个数据可以直接遍历所有数据

4）一个m阶B+树，那叶子结点中最多有m个关键字

<br/><br/><br/><br/>

#### （3）B*树

<br/>

定义：B*树是对B+树的一个变形

<br/>

![image-20220223151655079](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru25.png)

<br/><br/><br/><br/><br/><br/><br/><br/>

## （八）图

<br/>

### 1.图的表示

<br/>

**图的代码在遍历中展示**

<br/>

#### （1）邻接矩阵

<br/>

可以采用矩阵的方式存储图：

当顶点x到顶点y有连接时，可以将点之间的权值写在arr/[x]/[y]中，表示这两个顶点相连

数组的长度和宽度都是顶点的数目

<br/>

![image-20220226195109640](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru28.png)

<br/><br/><br/><br/>

#### （2）邻接表

<br/>

顶点采用数组，与顶点相连的边用链表进行连接

<br/>

![image-20220226195704013](https://cdn.jsdelivr.net/gh/hemeilun/picture/javaDataStru29.png)



<br/><br/><br/><br/>

### 2.图的遍历

<br/>

（1）深度优先遍历（DFS）

<br/>

思路：

从图中一个未访问的顶点 V 开始，沿着一条路一直走到底，然后从这条路尽头的节点回退到上一个节点，再从上一个顶点的另一条路开始走到底...，不断递归重复此过程，直到所有的顶点都遍历完成，它的特点是不撞南墙不回头，先走完一条路，再换一条路继续走。

<br/><br/>

（2）广度优先遍历（BFS）

<br/>

思路：

从一个结点开始，先将所有与这个点相邻并且没有访问过的的点遍历完，并逐个放入队列，遍历完这个结点后，取出队列的第一个结点，继续遍历完它的相邻且没有访问过的结点，放入队列，.... ，不断重复，直到队列为空

<br/><br/>

代码实现：

<br/>

邻接矩阵：

```java
package Graph;

import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class Matrix {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入矩阵的顶点数：");
        int n = scanner.nextInt();
        Matrix map = new Matrix(n);

        map.createMatrix();
        map.showMatrix();

        System.out.println("深度优先遍历：");
        map.DFSStart();

        System.out.println("广度优先遍历：");
        map.BFSStart();



    }

    public int[] isVisited;                //判断是否被访问
    public int[][] matrix;                 //存储图的邻接矩阵
    //这个最好设置一个元素，记录顶点的数目


    //构造函数，用于初始化
    public Matrix(int n) {
        this.isVisited = new int[n];
        this.matrix = new int[n][n];
    }


    //构建邻接矩阵
    public void createMatrix(){

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入邻接矩阵的边数");
        int m = scanner.nextInt();

        System.out.println("请输入所有边的开始结点和结束结点");
        int x,y;

        for (int i = 0; i < m; i++) {
            x=scanner.nextInt();
            y=scanner.nextInt();
            matrix[x][y] = 1;
            matrix[y][x] = 1;
        }

    }


    //遍历邻接矩阵
    public void showMatrix(){
        for (int[] m: matrix) {
            for (int mm:m) {
                System.out.print(mm+" ");
            }
            System.out.println();
        }
        System.out.println();
    }


    
    //对图进行深度优先遍历，这是起始
    public void DFSStart(){

        //将isVisited数组初始化为0,代表没有访问过
        for (int i = 0; i < isVisited.length; i++) {
            isVisited[i] = 0;
        }

        //从第一个结点开始遍历
        for (int i = 0; i < isVisited.length; i++) {
            if(isVisited[i] == 0){
                DFS(i);
            }
        }
        System.out.println();

    }
    //深度优先遍历算法
    public void DFS(int n){

        isVisited[n] = 1;  //表示结点已经访问过了

        //输出此节点的序号
        System.out.print(n+" ");

        //对当前结点的相邻结点进行遍历
        //若发现相邻结点且没有被访问过，进入相邻结点的DFS
        for (int i = 0; i < isVisited.length; i++) {
            if(matrix[n][i] == 1 && isVisited[i] == 0){
                DFS(i);
            }
        }
    }



    //对图进行广度优先遍历，这是起始
    public void BFSStart(){
        //将isVisited数组初始化为0,代表没有访问过
        for (int i = 0; i < isVisited.length; i++) {
            isVisited[i] = 0;
        }

        //从第一个结点开始遍历
        for (int i = 0; i < isVisited.length; i++) {
            if(isVisited[i] == 0){
                BFS(i);
            }
        }
        System.out.println();
    }
    //广度优先遍历
    public void BFS(int n){

        //创建一个队列，用于保存广度遍历的顺序
        Queue<Integer> queue = new LinkedList<>();

        //将当前结点入队
        queue.offer(n);

        //
        //改变visit需要在入队的时候进行，不可以在出队的时候进行
        //因为在遍历时，可能出现虽然元素已经入队，但是并没有改visit，访问其他的元素时，
        //这个元素与其他元素之间联通，就会再次入队，导致输出错误
        isVisited[n] = 1;

        //只有当队列不为空时，才退出
        while(!queue.isEmpty()){

            int nn = queue.poll();
            System.out.print(nn + " ");

            //找到所有与当前节点相邻且没有访问过的的点，放入队列
            for (int i = 0; i < isVisited.length; i++) {
                if(matrix[nn][i] == 1 && isVisited[i] == 0){
                    queue.offer(i);
                    isVisited[i] = 1;
                }
            }
        }
    }


    /*
    7
    8
    0 1
    0 3
    1 2
    1 5
    1 6
    2 5
    3 4
    3 5
    */
}
```

<br/><br/>

邻接表：

```java
package Graph;

import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class Table {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入顶点数：");
        int n = scanner.nextInt();
        Table table = new Table(n);

        table.createTable();
        table.showTable();

        System.out.println("深度优先遍历：");
        table.DFSStart();

        System.out.println("广度优先遍历：");
        table.BFSStart();

    }


    public Vertex[] vertices;    //邻接表
    public int[] isVisited;      //判断是否访问
    public int num;              //记录顶点数

    //构造函数，根据顶点数构造邻接表
    public Table(int n) {
        this.vertices = new Vertex[n];

        //初始化不只是初始化数组，还要把数组内的非基本类初始化，否则就是空
        for (int i = 0; i < n; i++) {
            vertices[i] = new Vertex();
        }

        isVisited  = new int[n];

        this.num = n;
    }

    //初始化邻接表
    public void createTable(){

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入邻接矩阵的边数");
        int m = scanner.nextInt();

        System.out.println("请输入所有边的开始结点和结束结点");
        int x,y;

        for (int i = 0; i < m; i++) {

            x=scanner.nextInt();
            y=scanner.nextInt();

            Edge edge1 = new Edge();
            edge1.no = y;
            edge1.next = vertices[x].first;
            vertices[x].first = edge1;

            Edge edge2 = new Edge();
            edge2.no = x;
            edge2.next = vertices[y].first;
            vertices[y].first = edge2;

        }
    }


    //展示邻接表
    public void showTable(){

        System.out.println();
        System.out.println();
        for (int i = 0; i < num; i++) {

            System.out.print(i+" : ");
            Edge edge = vertices[i].first;
            while(edge!=null){
                System.out.print(edge.no+" ");
                edge = edge.next;
            }
            System.out.println();
        }
    }


    //深度优先遍历,从此开始
    public void DFSStart(){
        //将isVisited数组初始化为0,代表没有访问过
        for (int i = 0; i < num; i++) {
            isVisited[i] = 0;
        }

        //从第一个结点开始遍历
        for (int i = 0; i < num; i++) {
            if(isVisited[i] == 0){
                DFS(i);
            }
        }
        System.out.println();

    }
    //深度优先遍历
    public void DFS(int n){

        isVisited[n] = 1;
        System.out.print(n+" ");

        Edge edge = vertices[n].first;
        while(edge!=null){
            if(isVisited[edge.no] == 0){
                DFS(edge.no);
            }
            edge = edge.next;
        }
    }


    //广度优先遍历，从此开始
    public void BFSStart(){
        //将isVisited数组初始化为0,代表没有访问过
        for (int i = 0; i < num; i++) {
            isVisited[i] = 0;
        }

        //从第一个结点开始遍历
        for (int i = 0; i < num; i++) {
            if(isVisited[i] == 0){
                BFS(i);
            }
        }
        System.out.println();

    }

    private void BFS(int n) {

        Queue<Integer> queue = new LinkedList<>();

        queue.offer(n);
        System.out.print(n+" ");
        isVisited[n] = 1;

        while(!queue.isEmpty()){

            int nn = queue.poll();
            Edge edge = vertices[nn].first;

            while(edge != null){
                if(isVisited[edge.no] == 0){
                    queue.offer(edge.no);
                    System.out.print(edge.no+" ");
                    isVisited[edge.no] = 1;
                }
                edge = edge.next;
            }
        }

    }

}


//顶点
class Vertex{
    public int data;
    public Edge first;
}

//边
class Edge{
    public int no;
    public Edge next;
}

 /*
    7
    8
    0 1
    0 3
    1 2
    1 5
    1 6
    2 5
    3 4
    3 5
    */
```



<br/><br/><br/><br/>

### 3.图的最小生成树

<br/>

（1）Prim算法

<br/>

步骤：

1）将图中的顶点分为两个集合，一个是访问过的集合Y，一个是没访问过的集合N（两个集合就是一个isVisited数组，为1表示访问过，为0表示没访问过）

2）起始，访问过的只有一个点，所以从这个点开始

3）找到与 集合Y中的顶点 相连的最小边

4）将最小边中不在集合Y中的顶点放入集合Y

5）重复3），4）步骤，直到所有点都在集合Y中

<br/><br/>

（2）Kruskal算法

<br/>

步骤：

1）将所有边进行排序

2）将最小的边拿出，若不形成闭环，将边相连

3）由于最小生成树的边数为顶点数减1，所有重复2）顶点数减1次即可

<br/>

判断是否形成闭环：

标号法：

可以将每个顶点进行一个编号，如果编号相同，说明存在路径形成闭环，只有编号不同的顶点之间才可以相连，当相连后，将所有编号大的顶点编号改为顶点编号小的

<br/><br/>

```java
package Graph;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;

public class PrimAndKruskal {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入顶点数：");
        int n = scanner.nextInt();
        PrimAndKruskal pk = new PrimAndKruskal(n);

        pk.createTable();
        pk.showTable();

        pk.Kruskal();
        pk.Prim(6);

    }


    public VertexPK[] vertices;  //邻接表
    public int[] isVisited;      //判断是否访问
    public int num;              //记录顶点数
    public List<DetailedEdge> detailedEdges;    //存储边详细信息


    //构造函数，根据顶点数构造邻接表
    public PrimAndKruskal(int n) {
        this.vertices = new VertexPK[n];

        //初始化不只是初始化数组，还要把数组内的非基本类初始化，否则就是空
        for (int i = 0; i < n; i++) {
            vertices[i] = new VertexPK();
        }

        isVisited  = new int[n];

        this.num = n;
    }

    //初始化邻接表
    public void createTable(){

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入邻接矩阵的边数");
        int m = scanner.nextInt();

        //初始化边的数组
        detailedEdges = new ArrayList<>();

        System.out.println("请输入所有边的开始结点和结束结点");
        int x,y,z;

        for (int i = 0; i < m; i++) {

            x=scanner.nextInt();
            y=scanner.nextInt();
            z=scanner.nextInt();

            EdgePK edge1 = new EdgePK();
            edge1.no = y;
            edge1.weight = z;
            edge1.next = vertices[x].first;
            vertices[x].first = edge1;

            EdgePK edge2 = new EdgePK();
            edge2.no = x;
            edge2.weight = z;
            edge2.next = vertices[y].first;
            vertices[y].first = edge2;

            //将详细的边放入detailedEdges
            detailedEdges.add(new DetailedEdge(x,y,z));

        }
    }


    //展示邻接表
    public void showTable(){

        System.out.println();
        System.out.println();
        for (int i = 0; i < num; i++) {

            System.out.print(i+" : ");
            EdgePK edge = vertices[i].first;
            while(edge!=null){
                System.out.print(edge.no+" "+edge.weight+"   ");
                edge = edge.next;
            }
            System.out.println();
        }
        System.out.println();
    }




    //Prim算法
    public void Prim(int n){  //n：表示起始结点

        System.out.println("Prim算法连接过程：");

        //表示n已经放入连通集合，连通集合是已经连接的结点
        isVisited[n] = 1;

        //最小连通图边数一定为定点数减1，所以要循环num-1次
        for (int i = 0; i < num-1; i++) {

            int minValue = 100;   //用来记录最小的边的大小
            int minEdge = -1;     //用来记录最小边的边尾的值
            int start = -1;       //用来记录是那条边已经访问过

            //遍历连通集合，查找最短的边
            for (int j = 0; j < num; j++) {

              //从在集合中的点进行选边
              if(isVisited[j] == 1) {
                  EdgePK edgePK = vertices[j].first;

                  while (edgePK != null) {
                      if (edgePK.weight < minValue && isVisited[edgePK.no] == 0) {
                          minValue = edgePK.weight;
                          minEdge = edgePK.no;
                          start = j;
                      }
                      edgePK = edgePK.next;
                  }
              }

           }

           //找到最短边后，将最短边的边尾结点放入连通结合
           isVisited[minEdge] = 1;
           System.out.println(start+" 与 "+minEdge+" 相连,权值： "+minValue);

        }

        System.out.println();

    }




    //Kruskal算法
    public void Kruskal(){

        System.out.println("Kruskal算法连接过程：");
        //将边按从小到达排序，便于取出最小边
        Collections.sort(detailedEdges);

        //标号法判断是否形成闭环
        //将相连的两个点用较小的标号记录，只有不同标号之间才可以连下一条线
        //比如AB 标号为0 ，当边AC要连接时，只有C标号不为0，才可以连，否则形成闭环
        int[] biaohaofa = new int[num];
        for (int i = 0; i < num; i++) {
            biaohaofa[i] = i;
        }

        //选择相连的边
        for (int i = 0; i < num-1; i++) {

            DetailedEdge de = detailedEdges.get(0);  //获取最小的边
            detailedEdges.remove(de);                //移除最小边

            //如果标号一样，说明形成闭环
            //否则，没有形成闭环，可以相连
            if(biaohaofa[de.start] == biaohaofa[de.end]){
                i--;
                continue;
            }else{

                //获取大标号和小标号
                int mmin = Math.min(biaohaofa[de.start],biaohaofa[de.end]);
                int mmax = Math.max(biaohaofa[de.start],biaohaofa[de.end]);

                //将标号为mmax的全部变为mmin
                for (int j = 0; j < num; j++) {
                    if(biaohaofa[j] == mmax){
                        biaohaofa[j] = mmin;
                    }
                }

                System.out.println(de.start+" 与 "+de.end+" 相连,权值： "+de.weight);
            }

        }

        System.out.println();

    }

}


//顶点
class VertexPK{
    public int data;
    public EdgePK first;
}

//边
class EdgePK{
    public int no;
    public int weight;
    public EdgePK next;
}

//存储每一条边的具体信息 用于克鲁斯卡尔算法
class DetailedEdge implements Comparable<DetailedEdge> {
    public int start;
    public int end;
    public int weight;

    public DetailedEdge(int start, int end, int weight) {
        this.start = start;
        this.end = end;
        this.weight = weight;
    }

    @Override
    public int compareTo(DetailedEdge o) {
        return this.weight-o.weight;
    }
}


/*
    7
    11
    0 1 7
    0 3 4
    0 6 5
    1 2 3
    1 5 1
    1 6 6
    2 5 8
    2 6 2
    3 4 5
    3 5 3
    4 5 10
    */
```

<br/><br/><br/><br/>

### 4.Dijkstra和Floyd

<br/>

#### （1）Dijkstra算法

<br/>

作用：求一个顶点到其他所有顶点的最短路径

<br/>

步骤：

1）从一个顶点出发，找到与这个顶点相连且没有访问过另一顶点的最小边，将边相连，同时将前驱结点保存

2）将最小边对应的点当作顶点，重复步骤1），直到倒数第二个点放入，结束

<br/>

代码实现：

```java
package Graph;

import java.util.Scanner;

public class Dijkstra {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入顶点数：");
        int n = scanner.nextInt();
        Dijkstra djs = new Dijkstra(n);

        djs.createTable();
        djs.showTable();


        //测试dijkstra算法
        djs.dijkstra(3);
        djs.showPreAdnDistances();

    }

    public VertexD[] vertices;  //邻接表

    public int[] isVisited;      //判断是否访问
    public int[] distances;      //存储到达每个点的最短距离
    public int[] pre;            //存储先驱结点的序号

    public int num;              //记录顶点数


    //构造函数，根据顶点数构造邻接表
    public Dijkstra(int n) {
        this.vertices = new VertexD[n];

        //初始化不只是初始化数组，还要把数组内的非基本类初始化，否则就是空
        for (int i = 0; i < n; i++) {
            vertices[i] = new VertexD();
        }

        isVisited  = new int[n];
        distances = new int[n];
        pre = new int[n];

        this.num = n;
    }

    //初始化邻接表
    public void createTable(){

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入邻接矩阵的边数");
        int m = scanner.nextInt();

        //初始化距离,将初始距离设置为最大
        for (int i = 0; i < num; i++) {
            distances[i] = Integer.MAX_VALUE;

            //将先驱结点设置为-1
            pre[i] = -1;
        }

        System.out.println("请输入所有边的开始结点和结束结点");
        int x,y,z;

        for (int i = 0; i < m; i++) {

            x=scanner.nextInt();
            y=scanner.nextInt();
            z=scanner.nextInt();

            EdgeD edge1 = new EdgeD();
            edge1.no = y;
            edge1.weight = z;
            edge1.next = vertices[x].first;
            vertices[x].first = edge1;

            EdgeD edge2 = new EdgeD();
            edge2.no = x;
            edge2.weight = z;
            edge2.next = vertices[y].first;
            vertices[y].first = edge2;


        }
    }


    //展示邻接表
    public void showTable(){

        System.out.println();
        System.out.println();
        for (int i = 0; i < num; i++) {

            System.out.print(i+" : ");
            EdgeD edge = vertices[i].first;
            while(edge!=null){
                System.out.print(edge.no+" "+edge.weight+"   ");
                edge = edge.next;
            }
            System.out.println();
        }
        System.out.println();
    }




    //迪杰斯特拉算法
    //n：查找序号为n的结点到其他结点的最小值
    public void dijkstra(int n){

        isVisited[n] = 1;
        distances[n] = 0;

        //总共需要找num-1个点,但到最后一个点时，其他点都已经访问过了，所以不需要再走一遍
        for (int i = 0; i < num-1-1; i++) {

            EdgeD edge = vertices[n].first;

            //经过这一步就可以将目前到达相连点的最短距离记录在distances
            while(edge != null){

                if(isVisited[edge.no] == 0 && distances[edge.no] > distances[n]+edge.weight){
                    distances[edge.no] = distances[n]+edge.weight;
                    pre[edge.no] = n;
                }
                edge = edge.next;

            }


            int mmin = Integer.MAX_VALUE;    //选出最小的距离
            int mminNo = -1;                 //最小距离对应的编号
            for (int j = 0; j < pre.length; j++) {

                if(isVisited[j] == 0 && distances[j] < mmin){
                    mmin = distances[j];
                    mminNo = j;
                }
            }

            isVisited[mminNo] = 1;
            n = mminNo;

        }

    }


    //输出pre和distances两个数组
    public void showPreAdnDistances(){

        //pre数组为：
        System.out.println("pre数组为：");
        for (int i = 0; i < num; i++) {
            System.out.print(pre[i]+" ");
        }
        System.out.println();

        System.out.println("dis数组为：");
        for (int i = 0; i < num; i++) {
            System.out.print(distances[i]+" ");
        }
        System.out.println();
    }





}

//顶点
class VertexD{
    public int data;
    public EdgeD first;
}

//边
class EdgeD{
    public int no;
    public int weight;
    public EdgeD next;
}


/*
    7
    11
    0 1 7
    0 3 4
    0 6 5
    1 2 3
    1 5 1
    1 6 6
    2 5 8
    2 6 2
    3 4 5
    3 5 3
    4 5 10
    */
```

<br/><br/><br/><br/>

#### （2）Floyd算法

<br/>

思想：

使用邻接矩阵或邻接表G来表示图，初始化G，将不可直达的顶点初始化为无穷大，定义k结点，遍历N个顶点->k，使用k作为任意两顶点i,j之间的中介点， 如果G[i] [j]>G[i] [k]+G[k] [j]，则执行松弛操作，将每一个顶点当作中介点放入任意两顶点之间， 如果可以执行松弛操作，则进行松弛，这样在已知的路径上插入点使得路径更短。

（相通图是我编的，指的是图中任意两点之间的距离是知道的）

开始时，只能访问直接相连的点，所以不直接相连的点之间是不相通的（相通的意思是知道两点之间的距离），只有在加入点之后，经过这个点才可以相通。

当一个点已经在路径中时，说明这个点能够找到目前点所处相通图的其他点，就可以找到这个点与其他点的当前最短路径。

如果是两个相通图之间加了一个点，这个点又与两个相通图内的点相连，由于原先相通图是可以互相访问别的点的，所以加入这点后，相通图就成为了一个。

由于我们并不知道加入这点后到底是哪些点之间经过新加的点变短了，所以需要测试图中所有点。若两点之间经过这个点路径变短了，就可以改变这两个点之间的当前最短路径。

当加完所有的点之后，整个图才算完整，这时计算的值才是两点之间的最短路径。

<br/>

```java
package Graph;

import java.util.Scanner;

public class Floyd {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入矩阵的顶点数：");
        int n = scanner.nextInt();
        Floyd map = new Floyd(n);

        map.createMatrix();
        map.showMatrix();

        map.Floyd();
        map.showMatrix();

    }


    public int[] isVisited;                //判断是否被访问
    public int[][] matrix;                 //存储图的邻接矩阵
    public int[][] distances;              //存储点与点之间的距离

    //得到的结果，列表示起始结点，行代表结束结点，得到的值是路径中靠近结束结点的结点
    public int[][] pre;                    //记录先驱结点的序号
    public int num;                        //记录顶点数目
    //这个最好设置一个元素，记录顶点的数目


    //构造函数，用于初始化
    public Floyd(int n) {
        this.isVisited = new int[n];
        this.matrix = new int[n][n];
        this.distances = new int[n][n];
        this.pre = new int[n][n];
        this.num = n;
    }


    //构建邻接矩阵
    public void createMatrix(){

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入邻接矩阵的边数");
        int m = scanner.nextInt();

        System.out.println("请输入所有边的开始结点和结束结点");
        int x,y,z;

        for (int i = 0; i < m; i++) {
            x=scanner.nextInt();
            y=scanner.nextInt();
            z=scanner.nextInt();
            matrix[x][y] = z;
            matrix[y][x] = z;
        }


        //初始化距离矩阵
        for (int i = 0; i < num; i++) {
            for (int j = 0; j < num; j++) {

                if(i==j){
                    distances[i][j] = 0;
                }else{
                    distances[i][j] = matrix[i][j]==0?1000:matrix[i][j];
                }
            }
        }

        //初始化先驱矩阵
        for (int i = 0; i < num; i++) {
            for (int j = 0; j < num; j++) {
                pre[j][i] = i;
            }
        }

    }


    //遍历邻接矩阵
    public void showMatrix(){

        System.out.println("邻接矩阵为：");
        for (int[] m: matrix) {
            for (int mm:m) {
                System.out.print(mm+" ");
            }
            System.out.println();
        }
        System.out.println();

        System.out.println("距离矩阵为：");
        for (int[] m: distances) {
            for (int mm:m) {
                System.out.print(mm+" ");
            }
            System.out.println();
        }
        System.out.println();

        System.out.println("前驱矩阵为：");
        for (int[] m: pre) {
            for (int mm:m) {
                System.out.print(mm+" ");
            }
            System.out.println();
        }
        System.out.println();
    }




    //弗洛伊德算法
    public void Floyd(){

        //最外层表示需要进行的次数
        for (int k = 0; k < num; k++) {
            for (int i = 0; i < num; i++) {
                for (int j = 0; j < num; j++) {

                    if(distances[i][j] > distances[i][k]+distances[k][j]){
                        pre[i][j] = pre[i][k];
                    }

                    distances[i][j] = Math.min(distances[i][j],distances[i][k]+distances[k][j]);

                }
            }
        }
    }


}


/*
    7
    11
    0 1 7
    0 3 4
    0 6 5
    1 2 3
    1 5 1
    1 6 6
    2 5 8
    2 6 2
    3 4 5
    3 5 3
    4 5 10
    */
```

<br/><br/><br/><br/><br/><br/><br/><br/>



