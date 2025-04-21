#include <iostream>
using namespace std;
// Định nghĩa cấu trúc hàng đợi ưu tiên
struct node {
    int data;          // Giá trị của phần tử 
   
   int priority;     // Độ ưu tiên của phần tử
   
   node* next;   // Con trỏ đến node tiếp theo của danh sách liên kết
   }; 
   
// Tạo node mới
   node* makeNode(int x, int p) {   
       node* newNode = new node(); // Cấp phát động
   
       newNode->data = x;                       // Gán giá trị của phần tử
   
       newNode->priority = p;                 // Gán độ ưu tiên của phần tử
   
       newNode->next = nullptr;          // Gán con trỏ NULL
   
       return newNode;                             // Trả về node mới là con trỏ kiểu node
   }

// Khởi tạo hàng đợi ưu tiên
   node* head = nullptr;      // con trỏ head kiểu node
   // Độ phức tạp O(1)

// Kiểm tra rỗng
bool isEmpty(node* &head) { 
    return head == nullptr; 
 }
 // Độ phức tạp O(1)
 
 // Thêm 1 phần tử vào danh sách
void enqueue( node* &head, int data, int priority ) {
    node* newNode = makeNode(data, priority); // Tạo một node mới với giá trị và độ ưu tiên cho trước 
  // Nếu hàng đợi rỗng / độ ưu tiên của node mới cao hơn node đầu tiên 
  if ( isEmpty( head ) || head->priority < priority) { 
     newNode->next = head; 
     head = newNode; 
  } else { 
     node* temp = head; // Tạo biến tạm temp duyệt qua các node để tìm vị trí chèn thích hợp
  // Tìm node có độ ưu tiên thấp hơn hoặc bằng để chèn trước nó  
     while (temp->next != nullptr && temp->next->priority > priority) { 
     temp = temp->next;  
  } 
  // Chèn node mới trước các node có cùng độ ưu tiên 
       newNode->next = temp->next; 
       temp->next = newNode;
    } 
  }
  //  Độ phức tạp: O(n)

  // Xóa phần tử có độ ưu tiên cao nhất
void dequeue(node* &head) { 

    if ( isEmpty(head) ) {          // Kiểm tra xem danh sách có rỗng không
    
    cout << " Danh sach rong " << endl; 
    
    return;               
    } 
    cout << " Gia tri: " << head->data << endl;
    
    node* temp = head;               // gán biến tạm temp là con trỏ đầu danh sách
    
    head = head->next;               // dịch con trỏ đầu danh sách về sau 
    
    delete temp;                            // xóa biến tạm
    }  
    // Độ phức tạp: O(1)

// Truy vấn phần tử có độ ưu tiên cao nhất
void peek(node* head) {    
    if ( isEmpty(head) ) { 
           cout << " Danh sach rong  " << endl;  
           return;
       } 
       cout << "Peek: " << head->data << " " << head->priority << endl; 
   } 
   // Độ phức tạp: O(1)

   // Cập nhật độ ưu tiên
void updatePriority(node* &head, int data, int newPriority) {   
    if ( isEmpty(head) ) { 
       cout << " danh sach rong " << endl;   
       return;
    } 
   // Tìm và xóa node có giá trị "data"   
    node* back = head;
    node* front = nullptr;
    while ( back != nullptr  &&  back->data != data) {        
               front = back;  
              back = back->next; 
     }
   if ( back == nullptr ){
         cout << " khong tim thay data " << endl;
      }
   if (front == nullptr){
          head=back->next;
       }else{
         front->next=back->next;
        delete back;
        enqueue(head, data, newPriority);
}
}
// Độ phức tạp: O(n)

// Thao tác hiển thị
void duyet(node* head){
   if ( isEmpty(head) ) {
      cout << "Hang doi rong " << endl;
      return;
  }
    while (head != nullptr) {
    cout << head->data << ", " << head-> priority << endl;
   head = head->next;
}
}
// Đếm số phần tử 
int size(node* head){
   int count = 0;
while (head != nullptr){
    count++;
    head=head->next;
   }
 return count;
}
// Cả 2 thao tác đều có độ phức tạp: O(n)

int main() {
   node* head = nullptr;  // Khởi tạo danh sách liên kết rỗng

   // Thêm các phần tử vào hàng đợi với độ ưu tiên khác nhau
   enqueue(head, 5, 1);  // Thêm phần tử 5 với độ ưu tiên 1
   enqueue(head, 3, 3);  // Thêm phần tử 3 với độ ưu tiên 3
   enqueue(head, 8, 2);  // Thêm phần tử 8 với độ ưu tiên 2
   // Hiển thị các phần tử trong hàng đợi
   cout << "Danh sach trong hang doi:" << endl;
   duyet(head);
   // Truy vấn phần tử ưu tiên cao nhất
   peek(head);
   // Cập nhật độ ưu tiên của phần tử có giá trị 5
   cout << "Cap nhat do uu tien cua phan tu 5 thanh 4" << endl;
   updatePriority(head, 5, 4);  // Cập nhật độ ưu tiên của phần tử 5 thành 4
   // Hiển thị các phần tử trong hàng đợi sau khi cập nhật
   cout << "Danh sach trong hang doi sau khi cap nhat:" << endl;
   duyet(head);
   // Loại bỏ phần tử ưu tiên cao nhất
   cout << "Xoa phan tu uu tien cao nhat:" << endl;
   dequeue(head);
   // Hiển thị các phần tử trong hàng đợi sau khi loại bỏ
   cout << "Danh sach trong hang doi sau khi xoa:" << endl;
   duyet(head);
   // Kiểm tra số lượng phần tử trong hàng đợi
   cout << "So luong phan tu trong hang doi: " << size(head) << endl;

   return 0;
}


      
