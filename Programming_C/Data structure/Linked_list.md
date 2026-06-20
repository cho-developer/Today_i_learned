0. Linked list의 종류
  Singly linked List
  Circular Linked List 
  Double Linked List





 <Singly Linked List>
 1. 특징   
    1-1: 일방향 으로 노드 연결됨.
    1-2: 첫번쨰 노드: Head. 
         끝 : NULL
    1-3: 노드 새로 추가하면 Header 파일의 포인터가 추가된 노드를 가르키게됨.    
 e.g.,)

 typedef struct ListNode{
    int data;
    struct ListNode* next;


 }ListNode;
 
 ListNode*insert_first(ListNode*head,int val)
 {
    ListNode*p=(ListNode*)malloc(sizeof(ListNode));

    p->data=val;
    p->next=head;
    head=p;



    return head;
 }


int main(int argc, const char* argv[]){

    ListNode *head=NULL;
    head=insert_first(head,1);//이렇게 반환값을 저장해줘야함. 

    
}


LinkedNode* delete_first(Linked Node* head){
if(head==NULL){return NULL;}

LinkedNode*removed=head;


head=removed->next;


free(removed);  

return head;
}

void printf_list(ListNode*head){


    for(ListNode*p=head; p!=NULL; p=p->next){

        printf("%d\n",p->data);


    }
    
}