#include <iostream>
using namespace std;
 
struct sinhvien{
	char ten[10];
	char gioitinh[5];
	float diemtb;
	int tuoi;
	int mssv;
};
 
struct SV{
	sinhvien s;
	SV *next;
};
 
typedef struct SV* sv;
 
//Cap phat dong mot node moi voi du lieu la so nguyen x
sv makeNode(){
	sinhvien s;
	cout<<"Nhap thong tin sinh vien: \n";
	cout<<"Nhap MSSV: ";
	cin>>s.mssv;
	cout<<"Nhap ten: ";
	cin>>s.ten;
	cout<<"Nhap gioi tinh: ";
	cin>>s.gioitinh;
	cout<<"Nhap tuoi: ";
	cin>>s.tuoi;
	cout<<"Nhap diem trung binh: ";
	cin>>s.diemtb;
	sv tmp = new SV();
	tmp->s = s;
	tmp->next = NULL;
	return tmp;
}
 
//Kiem tra rong
bool empty(sv a){
	return a == NULL;
}
 
int Size(sv a){
	int cnt = 0;
	while(a != NULL){
		++cnt;
		a = a->next; // gan dia chi cua not tiep theo cho node hien tai
		//cho node hien tai nhay sang not tiep theo
	}
	return cnt;
}
 
//them 1 phan tu vao dau danh sach lien ket
void insertFirst(sv &a){
	sv tmp = makeNode();
	if(a == NULL){
		a = tmp;
	}
	else{
		tmp->next = a;
		a = tmp;
	}
}
 
//Them 1 phan tu vao cuoi dslk
void insertLast(sv &a){
	sv tmp = makeNode();
	if(a == NULL){
		a = tmp;
	}
	else{
		sv p = a;
		while(p->next != NULL){
			p = p->next;
		}
		p->next = tmp;
	}
}
 
//Them 1 phan tu vao giua
void insertMiddle(sv &a,int pos){
	int n = Size(a);
	if(pos <= 0 || pos > n + 1){
		cout << "Vi tri chen khong hop le !\n"; return;
	}
	if(pos == 1){
		insertFirst(a); return;
	}
	else if(pos == n + 1 ){
		insertLast(a); return;
	}
	sv p = a;
	for(int i = 1; i < pos - 1; i++){
		p = p->next;
	}
	sv tmp = makeNode();
	tmp->next = p->next;
	p->next = tmp;
}
 
//xoa phan tu o dau
void deleteFirst(sv &a){
	if(a == NULL) return;
	a = a->next;
}
 
//xoa phan tu o cuoi
void deleteLast(sv &a){
	if(a == NULL) return;
	sv truoc = NULL, sau = a;
	while(sau->next != NULL){
		truoc = sau;
		sau = sau->next;
	}
	if(truoc == NULL){
		a = NULL;
	}
	else{
		truoc->next = NULL;
	}
}
 
//Xoa o giua
void deleteMiddle(sv &a, int pos){
	if(pos <=0 || pos > Size(a)) return;
	sv truoc = NULL, sau = a;
	for(int i = 1; i < pos; i++){
		truoc = sau;
		sau = sau->next;
	}
	if(truoc == NULL){
		a = a->next;
	}
	else{
		truoc->next = sau->next;
	}
}
 
void in(sinhvien s){
	cout << "--------------------------------\n";
	cout << "MSSV : " << s.mssv << endl;
	cout << "Ho ten :" << s.ten << endl;
	cout << "Gioi tinh :" << s.gioitinh << endl;
	cout << "Tuoi :" << s.tuoi << endl;
	cout << "Diem trung binh : " <<s.diemtb<<endl;
	cout << "--------------------------------\n";
}
 
void inds(sv a){
	cout << "Danh sach sinh vien :\n";
	while(a != NULL){
		in(a->s);
		a = a->next;
	}
	cout << endl;
}
 
void sapxep(sv &a){
	for(sv p = a; p->next != NULL; p = p->next){
		sv min = p;
		for(sv q = p->next; q != NULL; q = q->next){
			if(q->s.diemtb < min->s.diemtb){
				min = q;
			}
		}
		sinhvien tmp = min->s;
		min->s = p->s;
		p->s = tmp;
	}
}

void pressAnyKey(){
	cout<<"\n\nBam phim bat ky de tiep tuc...";
	getchar();
	system("cls");
}

int main(){
	sv head = NULL;
	int pos;
	int key;
	
	while(true){
		cout << "*************************MENU**************************\n";
        cout << "**  1. Chen sinh vien vao dau danh sach.             **\n";
        cout << "**  2. Chen sinh vien vao cuoi danh sach.            **\n";
        cout << "**  3. Chen sinh vien vao giua danh sach.            **\n";
        cout << "**  4. Xoa sinh vien o dau.                          **\n";
        cout << "**  5. Xoa sinh vien o cuoi.                         **\n";
        cout << "**  6. Xoa sinh vien o giua.                         **\n";
        cout << "**  7. Duyet danh sach lien ket.                     **\n";
        cout << "**  8. Sap xep cac sinh vien trong danh sach.        **\n";
        cout << "**  0. Thoat                                         **\n";
        cout << "*******************************************************\n";
        cout << "Nhap tuy chon cua ban : ";
        cin >> key;
        switch(key){
        	case 1:
        		cout<<"\n1. Chen sinh vien vao dau danh sach.\n";
        		insertFirst(head);
        		cout<<"\nChen sinh vien thanh cong!\n\n";
				break;
        	case 2:
        		cout<<"\n2. Chen sinh vien vao cuoi danh sach.\n";
        		insertLast(head);
        		break;
        	case 3:
        		cout<<"\n3. Chen sinh vien vao giua danh sach.\n";
        		cout<<"Nhap vi tri can chen: ";
				cin>>pos;
        		insertMiddle(head, pos);
        		cout<<"\nChen sinh vien thanh cong!\n\n";
        		break;
        	case 4:
        		deleteFirst(head);
        		break;
        	case 5:
        		deleteLast(head);
        		break;
        	case 6:
        		cout<<"Nhap vi tri can xoa: ";
        		cin>>pos;
        		deleteMiddle(head, pos);
        		break;
        	case 7:
        		inds(head);
        	case 8:
        		sapxep(head);
        	case 0:
        		cout << "\nBan da chon thoat chuong trinh!";
				getchar();
				return 0;
			default:
                cout << "\nKhong co chuc nang nay!";
                cout << "\nHay chon chuc nang trong hop menu.";
            	pressAnyKey();
            	break;
        }	
    }
    return 0;
}
