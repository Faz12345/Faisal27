class Node:
    def __init__(self,vertex=0,weight=0,next=None):
        self.vertex = vertex
        self.weight = weight
        self.next = next
class List:
    def __init__(self,size):
        self.size = size
        self.graph = [None]*self.size
    def addEdge(self,u,v,w):
        node = Node(v,w,self.graph[u])
        node.next = self.graph[u]
        self.graph[u] = node

        node = Node(u,w,self.graph[v])
        node.next = self.graph[v]
        self.graph[v] = node
    def addVertex(self,u,v,w):
        self.addEdge(u,v,w)
    def delEdge(self,u,v,w):
        def remove(head,vertex,weight):
            dummy = Node(-1,-1,head)
            prev,curr = dummy,head
            while curr:
                if curr.vertex == vertex and curr.weight == weight:
                    prev.next = curr.next
                    break
                prev,curr = curr,curr.next
            return dummy.next
        self.graph[u] = remove(self.graph[u],v,w)
        self.graph[v] = remove(self.graph[v],u,w)
    def delVertex(self,k):
        for i in range(self.size):
            temp = self.graph[i]
            if temp and temp.vertex == k:
                self.graph[i] = temp.next
                continue
            prev = None
            while temp and temp.vertex != k:
                prev = temp
                temp = temp.next
            if prev and temp:
                prev.next = temp.next
    def display(self):
        for i in range(self.size):
            print(f'{i}:',end='')
            temp = self.graph[i]
            while temp:
                print(f'-->{{vertex : {temp.vertex} , weight : {temp.weight}}}',end='')
                temp = temp.next
            print()
        print()
