
# UNIVERSITY PROJECT (credit:LUMINAR) 

- student grade tracker program in c++

> [!warning]
> do not copy the program some update are left for specific purpose. use this as refference for your project to understand the working & basic concept of the program. 

- [x] work completed
- [ ] code clean
- [ ] flaw 420 not resolved 

## 📄 Documentation
## main 
in the main function `int main()` a loop variable `bool loop = true ;` is assigne to make loop `true` from `student_database class_Btcs;` object is created. `system("cls");` clear the screen, then the loop start and from object class_btcs a function is called `class_Btcs.display_menue();` in `class student_database`.

```
int main(){
	bool loop = true ;
	int x;
	student_database class_Btcs;
	system("cls");
	while(loop){
			class_Btcs.display_menue();
			loop=class_Btcs.input_cases(class_Btcs.take_input());
		
	}

}

```
## function

- `display_menue()` function display the menue from the vector menue

```
#include<iostream>

#include<fstream>
#include<sstream>

#include<vector>

using namespace std;

//class data 
class student_database{
private:
	vector<string> menu={"1.Add Student",
						 "2.Display All Student",
						 "3.Calculate Average Grade",
						 "4.Find Top Scorer",
						 "5.Search Student",
						 "6.View Subject-Wise Performance",
						 "7.Display Student With Passing Grade",
						 "8.Update Student Information",
						 "9.Delete a Student",
						 "10.Save Student Details to File",
						 "11.Exit"
						};
	string subject[5]={"math","english","science","social studies","computer"};

	vector<string> student_name;
	vector<double> student_sub_math;
	vector<double> student_sub_english;
	vector<double> student_sub_science;
	vector<double> student_sub_sst;
	vector<double> student_sub_com;
	vector<char>   student_pass;

public:
	

	void display_menue(){

		for(string i:menu){
			cout << i << endl;
		}
		cout<<endl;
	}
```
##

- after that from the class_Btcs object `take.input()` is called

```
while(loop){
			class_Btcs.display_menue();
			loop=class_Btcs.input_cases(class_Btcs.take_input());
		
	}
```
## take user input
- take input function take input from user for the menue choice range(1-11) in case of invalid input throw throws error use resserection in function to again take input when the input case gets true it return the input to object which calls a function `class_btcs.input_case()`.
> Here `stoi(){refference documentation}`function convert string into integer for comparison. 


```

	int take_input(){

		string i;
		try{
			cout << "Enter your Choice>>";
			cin >> i;

			if (stoi(i)>0 && stoi(i)<=11){
				return stoi(i);
			}else{
				throw i;
			}
		}catch(...){
			cout<<"invalid input"<<endl;
			return take_input();
		}

	}

```
## user input pass to function
- the input result is then pass to input case which pass the int and as per case run different function in `case 11:` return false so that [`loop=class_Btcs.input_cases(class_Btcs.take_input());`](https://github.com/Snp-Rj-Ind-code-error-420/record#main)  loop value become `false` and loop end.


```
	bool input_cases(int x){

		switch (x){
		case 1:
			add_student_menue();
			break;
		case 2:
			display_record();
			break;		
		case 3:
			average_grade();
			break;
		case 4:
			topper();
			break;
		case 5:
			search_student();
			break;
		case 6:
			display_sub_performance();
			break;
		case 7:
			display_pass();
			break;
		case 8:
			update_record();
			break;
		case 9:
			delete_record();
			break;
		case 10:
			save_data_to_file();
			break;
		case 11:
			return false; 
			break;
		default:
			cout << "how you reached here i left no bug"<<endl;
			return true;
			break;
		}

		return true;

	}
```
## first function add student
- `void add_student_menue()` function take name student name and there marks and in a array and calls function`void push_to_stack(double math,double eng,double sci,double sst,double com,string name)` marks range(1-100)
> `if (stod(inp)>-1 && stod(inp)<=100)` if not in range or not double type error is thrown and nothing is added to array.


```

	void add_student_menue(){
		string student_name_input;
		string inp;
		double marks[5];
		bool ignore=false;

		cout <<endl<< "enter student name>>";
		cin >> student_name_input;
		try{
		for(int i=0;i <5;i++){
			cout <<endl<< "enter marks of " <<subject[i]<<" >>";
			cin >> inp;
			if (stod(inp)>-1 && stod(inp)<=100){
				marks[i]=stod(inp);
			}else{
				throw inp;
			}	
			
		}

		if(!ignore){
			//cout << student_name_input<<marks[0]<<marks[1]<<marks[2]<<marks[3]<<marks[4]<<endl;
			push_to_stack(marks[0],marks[1],marks[2],marks[3],marks[4],student_name_input);
			system("cls");
			cout<<"record was added"<<endl;
		}
		}catch (...){
			system("cls");
			cout << "***invalid input***"<<endl<<endl;
		}
	}
```
##
- `void push_to_stack(double math,double eng,double sci,double sst,double com,string name)` push data to the [vector list in private class](https://github.com/Snp-Rj-Ind-code-error-420/record#function). 

```
	void push_to_stack(double math,double eng,double sci,double sst,double com,string name){
		student_name.push_back(name);
		student_sub_math.push_back(math);
		student_sub_english.push_back(eng);
		student_sub_science.push_back(sci);
		student_sub_sst.push_back(sst);
		student_sub_com.push_back(com);
		student_pass.push_back(pass_elegible( math, eng, sci, sst, com));
	}
```
##
- `char pass_elegible(double math,double eng,double sci,double sst,double com)` is a function give output in `char` if a student is `pass or fail (P/F)` and this get push to the vector.
```

	char pass_elegible(double math,double eng,double sci,double sst,double com){
		double arr[5]={math,eng,sci,sst,com};
		int cnt=0;
		for(int i=0;i<5;i++){
			if (arr[i] < 30){
				cnt++;
			}
		}

		if (cnt>=2){
			return 'F';
		}else{
			return 'P';
		}

	}
```
## second function to display record
- `case 2:` option 2 called function `void display_record()` itrate through threw the vector and display the student in the vector,`void display_record_cout_fun(int i)` is a function called many time for printing so seperated to call by other function.
> in case of no data is present in vector outputs `cout<<"no data"<<endl;`

```
	void display_record_cout_fun(int i){
			cout<<student_name[i]<<"\t\t\t\t||\t  "
				<<student_sub_math[i]<<"\t\t"
				<<student_sub_english[i]<<"\t\t"
				<<student_sub_science[i]<<"\t\t"
				<<student_sub_sst[i]<<"\t\t\t"
				<<student_sub_com[i]<<"\t"<<student_pass[i]<<endl;
	}

	void display_record(){
		system("cls");
		if(!(student_name.size()==0)){
			cout<<endl<<"student_name"<<"\t\t\t||\t"<<"mathematics\t"<<"english\t\t"<<"science\t\t"<<"social studies\t\t"<<"computer"<<endl;
			for (int i=0;i<student_name.size();i++){
				display_record_cout_fun(i);
			}
		}else{
			cout<<"no data"<<endl;
		}
	}
```
## third function to calculate the average of whole class
- `void average_grade()` function calculate avg by taking sum from all the subject vector and divide it by the total number of student by getting size of vector`avg_cal/student_name.size()`
```
	void average_grade(){
		double avg_cal=0;
		for (double i : student_sub_math){
			avg_cal+=i;
		}
		for (double i : student_sub_english){
			avg_cal+=i;
		}
		for (double i : student_sub_science){
			avg_cal+=i;
		}
		for (double i : student_sub_sst){
			avg_cal+=i;
		}
		for (double i : student_sub_com){
			avg_cal+=i;
		}
		system("cls");
		cout << "average of whole class is all subject = " <<avg_cal/student_name.size()<< endl;
	}
``` 
## fourth function to find top scorer
-  `void topper()` function calculate the topper by eleminating the fail student and calculate the sum total from every subject and finding the max and [displaying](https://github.com/Snp-Rj-Ind-code-error-420/record#second-function-to-display-record) who got the max score.

```
	void topper(){
		double total=-1,subject_sum;
		int indent=0;
		for(int i=0;i<student_name.size();i++){
			if (student_pass[i]=='P'){
				subject_sum=student_sub_math[i]+student_sub_english[i]+student_sub_science[i]+student_sub_sst[i]+student_sub_com[i];
				if (subject_sum>total){
					total=subject_sum;
					indent=i;
				}
			}
		}
		system("cls");
		if (student_pass[indent]=='P'){
			cout 	<< "The top scorer is "<<endl;
			display_record_cout_fun(indent);
		}
	}
```
## fifth function to find a student
- `void search_student()` function take the name of student and find it throught the vector and then display the student details in case of invalid input it throw `not found` 
> [!note]
> //flaw id 420 not resolve
```
	void search_student(){
		string inp;
		int indent=0;
		cout << "enter name of the student >>";
		cin >> inp;
		try{
			for (string i:student_name){
				if (i==inp){
					display_record_cout_fun(indent);
							break;
				}
				
				indent++;
			}
			
			if(indent==student_pass.size()){
					throw indent;
				}
		}catch(...){
		cout<<"not found"<<endl;
		}
	}
```
## sixth function to find subject wise performance
- `void display_sub_performance()` is a function that take input of subject indentation(1-5) then calculate the max in subject wise and then print the top scorer[`display_record_cout_fun(indent)`](https://github.com/Snp-Rj-Ind-code-error-420/record#second-function-to-display-record)
> [!note]
> //flaw id 420 not resolve
```

	void display_sub_performance(){
		string inp;
		try{
			cout << "Enter the subject indent>>";
			cin >> inp;

			if (stoi(inp)>0 && stoi(inp)<=5){
				double max=-1,subject_max=0;
				int indent=0;
				for(int i=0;i<student_name.size();i++){
					if (student_pass[i]=='P'){
						switch(stoi(inp)){
						case 1:
							subject_max=student_sub_math[i];
							break;
						case 2:
							subject_max=student_sub_english[i];
							break;
						case 3:
							subject_max=student_sub_science[i];
							break;
						case 4:
							subject_max=student_sub_sst[i];
							break;
						case 5:
							subject_max=student_sub_com[i];
							break;
						}
						if (subject_max>max){
							max=subject_max;
							indent=i;
						}
					}
				}
				system("cls");
				if (student_pass[indent]=='P'){
					//cout <<max<<'-'<<indent<< 
					cout <<"The top scorer of subject "<<subject[stoi(inp)-1]<<endl;
					display_record_cout_fun(indent);
				}
			}else{
				throw inp;
			}
		}catch(...){
			cout<<"***invalid input***"<<endl;
		}
	}
```
## seventh function to display student with passing grade
- `void display_pass()` function display the student with passing marks which is min 30 marks in all subject and if student has below 30 in two subject then student is in fail category.
```

	void display_pass(){
		system("cls");
		for(int i=0; i<student_name.size();i++){
			if (student_pass[i]=='P'){
				display_record_cout_fun(i);
			}
		}
	}
```
## eight function to update student data
- `void update_record()` function take the student name and use [`void search_student()`](https://github.com/Snp-Rj-Ind-code-error-420/record#fifth-function-to-find-a-student) similar algorithm to find the student and ask subject marks then call function `void update_to_stack(double math,double eng,double sci,double sst,double com,int indent)` which update the value in the vector.
```

	void update_to_stack(double math,double eng,double sci,double sst,double com,int indent){
		student_sub_math[indent]=math;
		student_sub_english[indent]=eng;
		student_sub_science[indent]=sci;
		student_sub_sst[indent]=sst;
		student_sub_com[indent]=com;
		student_pass[indent]=pass_elegible( math, eng, sci, sst, com);

	}

	void update_record(){
		string inp,inp2;
		int indent=0;
		double marks[5];
		bool ignore=false;
		cout << "enter name of the student >>";
		cin >> inp2;
		try{
			for (string i:student_name){
				if (i==inp2){

					try{
					for(int i=0;i <5;i++){
						cout <<endl<< "enter marks of " <<subject[i]<<" >>";
						cin >> inp;
						if (stod(inp)>-1 && stod(inp)<=100){
							marks[i]=stod(inp);
						}else{
							throw inp;
						}	
						
					}

					if(!ignore){
						update_to_stack(marks[0],marks[1],marks[2],marks[3],marks[4],indent);
						system("cls");
						cout<<"record was updated"<<endl;
					}
					}catch (...){
						system("cls");
						cout << "***invalid input***"<<endl<<endl;
					}
						break;
				}
				
				indent++;
			}
			
			if(indent==student_pass.size()){
					throw indent;
				}
		}catch(...){
		cout<<"not found"<<endl;
		}
	}
```
## nineth function to delete record
- `void delete_record()` function takes the student name and use the [`void search_student()`](https://github.com/Snp-Rj-Ind-code-error-420/record#fifth-function-to-find-a-student) same algorithm to find the vector indent and call the function `void delete_record_from_stack(int indent)` which use`vector.erase(begin(vector)+indentation)` function to remove data from the vector.
```

	void delete_record_from_stack(int indent){

		student_name.erase(begin(student_name)+indent);
		student_sub_math.erase(begin(student_sub_math)+indent);
		student_sub_english.erase(begin(student_sub_english)+indent);
		student_sub_science.erase(begin(student_sub_science)+indent);
		student_sub_sst.erase(begin(student_sub_sst)+indent);
		student_sub_com.erase(begin(student_sub_com)+indent);
		student_pass.erase(begin(student_pass)+indent);

	}

	void delete_record(){
		string inp;
		bool ignore=false;
		int indent=0;
		cout << "enter name of the student >>";
		cin >> inp;
		try{
			for (string i:student_name){
				if (i==inp){
					delete_record_from_stack(indent);
					ignore=true;
					system("cls");
					cout << "record was deleted" << endl;
					break;
				}
				
				indent++;
			}
			
			if(indent==student_pass.size() && !ignore){
					throw indent;
			}
		}catch(...){
		cout<<"not found"<<endl;
		}
	}

```
## tenth function to save file 
- `save_data_to_file()` function take the record from the vector and save it to the text file in specific order.
```

	void save_data_to_file(){
		ofstream out;
		out.open("record.txt");
		if(out.is_open()){
			out<<endl<<"student_name"<<"\t\t\t||\t"<<"mathematics\t"<<"english\t\t"<<"science\t\t"<<"social studies\t\t"<<"computer"<<endl;
			for (int i=0;i<student_name.size();i++){
				out <<student_name[i]<<"\t\t\t\t||\t  "
				<<student_sub_math[i]<<"\t\t"
				<<student_sub_english[i]<<"\t\t"
				<<student_sub_science[i]<<"\t\t"
				<<student_sub_sst[i]<<"\t\t\t"
				<<student_sub_com[i]<<"\t"<<student_pass[i]<<endl;
			}
			system("cls");
			cout<<"file was saved"<<endl;
			
		}
	}

	


};

```
# THANKS FOR READING
- love the work so plz appreciate  

