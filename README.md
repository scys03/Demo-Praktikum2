# Demo-Praktikum2
1. AHHA

 Pertama, Kita perlu menyimpan bilangan tertinggi dalam range K berurut ke dalam suatu stack. Misalnya k adalah 3 dan bilangannya 5, maka kita harus memasukkan bilangan tertinggi dari hari ke 1-3,2-4 dan 3-5 ke sebuah stack. berikut source codenya :
  ```java
void push1(int bil){
	stack[++top]=bil;
}
void push3(link* deque,int angka){
	que* deck=(que*)malloc(sizeof(que));
	deck->bil=angka;
	if(deque->head==NULL){
		deque->head=deque->tail=deck;
	}
	else{
		deque->tail->next=deck;
		deck->prev=deque->tail;
		deque->tail=deck;
	}
	deque->head->prev=NULL;
	deque->tail->next=NULL;
}
void popfront(link* deque){
	if(deque->head!=NULL){
	if(deque->head==deque->tail){
			free(deque->head);
			deque->head=NULL;
			deque->tail=NULL;
		}
		else{
			que* temp=deque->head;
			deque->head=deque->head->next;
			free(temp);
			deque->head->prev=NULL;
		}
	}
}
void popback(link* deque){
	que* temp;
	if(deque->head!=NULL){
		if(deque->head==deque->tail){
			free(deque->head);
			deque->head=NULL;
			deque->tail=NULL;
		}
		else{
			temp=deque->tail->prev;
			free(deque->tail);
			deque->tail=temp;
			deque->tail->next=NULL;	
		}
	}
}
void cekbesar(int t,int k,link* deque){
	int i;
	for(i=0;i<k;i++){
		while((deque->head!=NULL)&&(stok[i]>=stok[deque->tail->bil])){
			popback(deque);
		}
		push3(deque,i);
	}
	for(i=k;i<t;i++){
		push1(stok[deque->head->bil]);
		while((deque->head!=NULL)&&(deque->head->bil<=i-k))
			popfront(deque);
		while((deque->head!=NULL)&&(stok[i]>=stok[deque->tail->bil]))
			popback(deque);
		push3(deque,i);
	}
	push1(stok[deque->head->bil]);
}
```
pada fungsi cekbesar(),kita melakukan iterasi terhadap array bernama stok[](berisi bilangan yang kita input) dari indeks ke 0, sampe indeks k-1.
Selagi mengiterasi,kita mengecek apakah deque kosong. Jika ya, kita melakukan fungsi push3, yaitu memasukkan bilangan (indeks) dari belakang.
Disini, yang kita masukkan  ke deque hanyalah i yaitu indeks bilangan tersebut, bukan bilangannya/isi dari stok berindeks i.
Jika tidak, kita memeriksa apakah isi stok berindeks i lebih besar sama dengan isi dari stok berindeks bilangan yang ada di deque tail.
Jika ya kita melakukan fungsi popback, yaitu menghapus bilangan(indeks) dari belakang, hingga isi dari stok indeks i lebih kecil dari isi berindeks bilangan deque tail. lalu melakukan fungsi push3 lagi.
Jika tidak kita langsung melakukan fungsi push3. 

Setelah iterasi ini habis, kita melakukan iterasi dari k hingga t(total bilangan yang kita input)-1. Iterasi ini berguna menambah isi dari stok berindeks deque head ke stack yang bernama stack.
Pada akhirnya di stack akan terisi semua bilangan maksimum per range K. Setelah itu kita akan memasukkan semua/ beberapa isi dari stack kedalam suatu stack baru bernama stok.
Stok ini akan diisi bilangan dari stack sebelumnya bergantung hari yang kita masukkan. Misalnya kita memenginput hari ke 3.
Maka kita akan memasukkan stack dengan posisi ke 1,2,3 ke stok. Perlu diingat bahwa hari yang diinput harus maju, jadi setelah kita menginput hari 3,
kita tidak tidak boleh menginput hari sebelum 3, yaitu 2 dan 1. jadi misalnya kita ingin menginput hari 5, maka kita memasukkan stack dari posisi 4 sampe 5 ke stok.
Pada saat kita memasukkan stack ke stok. kita juga mengecek mana bilangan maksimum dari rentang H lalu dimasukkan ke stack bernama maxval.
Berikut source codenya:
```java
while(iter<=H-1){
		if(stack[iter]==0) break;
		push(stack[iter]);
		if(top2==-1) push2(stack[iter]);
  	else{
			if(stack[iter]>=maxval[top2]) push2(stack[iter]);
		}
		iter++;
}
```
Cara memasukkan stack ke maxval dengan cara membandingkan apakah stack berindeks tersebut lebih besar dari top maxval.
Jika lebih besar kita memasukkan stack berindeks ke dalam maxval.
Maka nanti, kita akan mendapat 2 stack yang bernama stok yang berisi bilangan - bilangan yang berada dari stack dengan rentang H dan juga maxval yang berisi bilangan- bilangan maksimum dari stack dengan rentang H.
Setelah itu tergantung perintah inputan aksi. jika yang diinput adalah 1, Bobby akan memakan mie yang berada pada top of stok.
Jika stok kosong, Bobby akan mengeluarkan tulisan "Stok kosong". Jika tidak kosong, Bobby akan memakan yang berada pada top stok.
Jika yang dimakan pada top stok sama dengan yang berada pada top maxval, maka stack maxval akan melakukan fungsi pop, yaitu mengeluarkan bilangan yang berada pada tp maxval.
Jika perintahnya 2, Bobby akan menulis bilangan tertinggi yang ada pada stack tersebut yaitu bilangan yang berada pada top maxval.
berikut source codenya :
```java
for(i=0;i<Q;i++){
  scanf("%d",&x);
	if(x==1){
		if(top3!=-1){
			printf("Nyam\n");
			if(maxval[top2]==stok[top3]) pop();
			pop2();
		}
		else printf("Stok abis\n");
	}
	if(x==2){
		if(top3!=-1){
			printf("%d\n",maxval[top2]);
		}
		else printf("Stok abis\n");
	}
}
```
Jika stok kosong maka akan ditulis "Stok kosong". Program akan berhenti ketika menginput hari dan aksi dengan -1.

2.EZTR

Kita perlu mengecek apakah jumlah buka kurung dan tutup kurung sesuai dengan pasangannya. string bernama str akan dicek.
Jika string berindeks i adalah buka kurung ("(","[","{"),maka akan dimasukkan ke stack dengan fungsi push. 
berikut source codenya :
```java
if(str[i]=='('||str[i]=='['||str[i]=='{'){
	push(str[i]);
	continue;
}
```
Jika saat kita selesai memeriksa string berindeks 0, namun stack masih kosong, maka program akan berhenti dengan memprint "v:".
berikut source codenya :
```java
if(top==-1){
	printf("v:\n");
	count=1;
	return 0;
}
```
Jika string berindeks i adalah tutup kurung, maka kita akan mengecek apakah buka kurung yang ada di top stack sesuai,contohnya 
jika string berindeks i ="}", maka top stack harus berisi "{". Jika tidak sesuai, maka akan terprint "v:". Berlaku juga untuk "]" dan ")".
Jika setelah memeriksa string berindeks terakhir, stack masih berisi, maka print ":v", jika stack kosong print ":v". Berikut source codenya :
```java
if(str[i]==')'){
	x=stack[top];
	pop();
	if(x=='{'||x=='['){
		printf("v:\n");
		return 0;
	}
}
else if(str[i]=='}'){
	x=stack[top];
	pop();
	if(x=='('||x=='['){
		printf("v:\n");
		return 0;
	}
}
else if(str[i]==']'){
	x=stack[top];
	pop();
	if(x=='('||x=='{'){
		printf("v:\n");
		return 0;
	}
}
if(top==-1) printf(":v\n");
else printf("v:\n");
```

3. SDM

Pada kasus ini, kita meminta untuk menentukan apakh struktur data itu queue, stack,queue stack atau tidak tahu. opsi lainnya yaitu eror. Eror nih terjadi ketika kita ngepop suatu bilangan namun isi struktur data itu kosong. Berikut source codenya :
```java
if(a==2){
	keluar++;
	if(list->head==NULL){
		count=0;
	continue;
}
if(count==0) printf("error nih :(\n");
```
Tidak tahu terjadi ketika kita ingin mengepop suatu bilangan, namun bilangan itu tidak ada di head atau tail dan juga ketika kita belum ngepop sama sekali ditandai dengan s=0,dan q=0.Berikut source codenya :
```java
else if(b!=list->head->bil&&b!=list->tail->bil){
	s=0;
	q=0;
	hitung=1;
	continue;
}
if((s==0&&q==0)||hitung==1) printf("tidak tahu\n");
```
stack terjadi kita semua bilangan yang kita pop, adalah bilangan yang baru saja kita masukkan,ditandai dengan s=1,q=0. berikut source codenya :
 ```java
else if(b==list->tail->bil){
	command='s';
	s=1;
}
if(s==1&&command=='s'){
	pop(list);
}
else if(s==1&&q==0) printf("stack\n");
```
Queue terjadi ketika semua bilangan kita pop adalah bilangan yang kita masukkan pertama kali ditandai dengan q=1,s=0. berikut source codenya :
```java
else if(b==list->head->bil){
	command='q';
	q=1;
}
else if(q==1&&command=='q'){
	dequeue(list);
}
else if (s==0&&q==1) printf("queue\n");
else if(s==1&&q==1) printf("queue stack\n");
```
Queue sama stack terjadi ketika kita mengepush suatu bilangan sekali, dan kita mengpop bilangan itu juga sekali. Atau ketika kita ada bilangan yang sama di head sama tail, sehingga kita bisa beranggapan bahwa struktur data itu adalah struktur data queue atau stack. Namun ketika ada bilangan yang sama di head sama tail, cara kita memilih bilangan mana yang mau dipop dengan melihat perintah selanjutnya. berikut source codenya :
```java
if(masuk>1&&keluar>=1&&masuk>keluar){
	if(list->head->bil==b&&list->tail->bil==b&&count1==0){
	  s=1;
		q=1;
		count1=1;
	}
	else{
		count2=0;
	}
}
if(count1==1){
	bil=b;
	count1=2;
	continue;
}
if(count1==2){
	if(b==bil){			
		dequeue(list);
		pop(list);
	}
	else if(b==list->head->next->bil){
		dequeue(list);
		dequeue(list);
	}
	else if(b==list->tail->prev->bil){
		pop(list);
		pop(list);
	}
	else{
		s=0;
		q=0;
		hitung=1;
	}
	if(list->head==NULL||list->tail==NULL)
	  list->head=list->tail=NULL;
	count1=0;
	continue;
}
if(list->head->bil==b&&list->tail->bil==b&&count1==0){
	if(masuk==1&&keluar==1){
	count2=1;
	keluar=0;
	masuk=0;
}
list->head=list->tail=NULL;
}
if(count2 ==1){
  s=1;
	q=1;
}
else if(s==1&&q==1) printf("queue stack\n");
``` 
4. TDL

Pada kasus ini kita diminta untuk menentukan apakah kita bisa sampai ke ujung kanan atas dari ujung kiri bawah dengan hanya menggunakan aksi keatas, kebawah, kekiri kekanan. Pertama, jika isi dari array berindeks ujung kiri bawah adalah nol, maka program akan berhenti. Jika tidak maka kita akan mengecek apakah di kiri, kanan atas bawah terdapat array dengan nilai 1. Berikut source codenya :
```java
if(posisi[x][y+1]==1&&y+1<N){//kanan
	push1(x);
	push2(y);
	posisi[x][y]=0;
	y++;
}
else if(posisi[x+1][y]==1&&x+1<N){//bawah
	push1(x);
	push2(y);
	posisi[x][y]=0;
	x++;
}
else if(posisi[x][y-1]==1&&y-1>=0){//kiri
	push1(x);
	push2(y);
	posisi[x][y]=0;
	y--;
}
else if(posisi[x-1][y]==1&&x-1>=0){//atas
	push1(x);
	push2(y);
	posisi[x][y]=0;
	x--;
}
```
saat kita memeriksa kekanan, kiri,atas, bawah, kita akan memasukkan koordinat sekarang(bukan koordinat yang kita cek ke kanan,atas,kiri,atau bawah) kita masukkan ke 2 stack yang menampung koordinat x sama y. lalu array berndeks koordinat yang sekarang kita beri nilai nol, lalu kita pindah ke koordinat yang kita cek.Namun jika koordinat yang kita cek ke kiri,atas,bawah, kanan tidak menemui array bernilai 1, maka kita akan melakukan bactracking, dengan cara membuat nilai dari array berindeks koordinat sekarang menjadi nol, membuat koordinat x dan y menjadi koordinat dari stack x dan stack y dan mengpop koordinat x dan y yang berada distack. berikut source codenya :
```java
else{
  if(top==-1) break;
  if(top!=-1){
		posisi[x][y]=0;
		posisi[stack1[top]][stack2[top2]]=0;
		x=stack1[top];
		y=stack2[top2];
		pop1();
		pop2();
	}
}
```
ketika kita sudah menemui koordinat ujung kanan atas, kita langsung keluar dari while dan mencetak "Ada jalan ada Thamus",
jika kita tidak menemui koordinat ujung kanan atas,kita akan keluar jika stack x dan y sudah kosong dan mencetak "Buntu yaa Thanus"
