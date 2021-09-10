# -class MyLinked_list {
    private Node head;
    private Node last;
    private int size;

    MyLinked_list() {
    }

    public Node get(int index) throws Exception {
        if (index >= 0 && index <= this.size) {
            Node temp = this.head;

            for(int i = 0; i < index; ++i) {
                temp = temp.next;
            }

            return temp;
        } else {
            throw new IndexOutOfBoundsException("超出链表节点范围");
        }
    }

    public void insert(int data, int index) throws Exception {
        if (index >= 0 && index <= this.size) {
            Node insertedNode = new Node(data);
            if (this.size == 0) {
                this.head = insertedNode;
                this.last = insertedNode;
            } else if (index == 0) {
                insertedNode.next = this.head;
                this.head = insertedNode;
            } else if (index == this.size) {
                this.last.next = insertedNode;
                this.last = insertedNode;
            } else {
                Node prevNode = this.get(index - 1);
                insertedNode.next = prevNode.next;
                prevNode.next = insertedNode;
            }

            ++this.size;
        } else {
            throw new IndexOutOfBoundsException("超出链表节点范围");
        }
    }

    public Node remove(int index) throws Exception {
        if (index >= 0 && index < this.size) {
            Node removedNode = null;
            if (this.size == 0) {
                return null;
            } else {
                if (index == 0) {
                    removedNode = this.head;
                    this.head = this.head.next;
                } else {
                    Node prevNode;
                    if (index == this.size - 1) {
                        prevNode = this.get(index - 1);
                        removedNode = prevNode.next;
                        prevNode.next = null;
                        this.last = prevNode;
                    } else {
                        prevNode = this.get(index - 1);
                        Node nextNode = prevNode.next.next;
                        removedNode = prevNode.next;
                        prevNode.next = nextNode;
                    }
                }

                --this.size;
                return removedNode;
            }
        } else {
            throw new IndexOutOfBoundsException("超出链表节点范围");
        }
    }

    public void output() {
        for(Node temp = this.head; temp != null; temp = temp.next) {
            System.out.print(temp.data + " ");
        }

    }
}
