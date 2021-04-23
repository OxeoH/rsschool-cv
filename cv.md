# Resume
Hello, my name is **Egor Timoshevich**.  

##Contacts:  
    Discord: #9890 SWATGFM  
    Email: egor33429@gmail.com  
    Phone number: +375333302983  
    
##Some facts about me:    
I think that money is not important. I have some goals like
to upgrade my brains in programming sphere and I wish that
this way will help me to see the world.  

##Skills:
    Programming languages: Python, C++
    I study some Python frameforks like BeautifulSoup, requests, lxml, SQlite

##Code examples:
###Course work(C++)
    #include <iostream>
    #include <stdio.h>
    #include <vector>
    #include <fstream>
    #include <string>
    
    using namespace std;
    
    struct STUD {
        int groupNum;
        string fullName[3];
        int educationType;
        int socialActivity;
        int passSubject[5];
        int markSubject[4];
        int averageMark;
        int grantcheck;
        int grantValue;
    };
    
    enum eduType{paid = 1, budgetary};
    enum socAct{active = 1, passive};
    enum passes{fail, pass};
    
    void add_info(vector <STUD> &mass);
    void save_info(vector <STUD> &mass);
    void show_info(vector <STUD> &mass);
    void calculate_grants(vector <STUD> &mass, int grant);
    void check_grant_requarements(vector <STUD> &mass);
    void calculate_ave_mark(vector <STUD> &mass);
    void del_info(vector<STUD> &mass);
    
    void main() {
        int cycle = 0;
        int choice_panel, choice_adm, choice_user;
        int grant;
    
        vector<STUD> mass;
    
        cout << "================Welcome!!!=================\n";
        cout << "\n===========================================";
        cout << "\nInput basic grant: ";
        cin >> grant;
        cout << "===========================================\n";
        cout << "\n===========================================\n";
        cout << "Admin panel [1] | User panel [2] | Exit [0]\n"
            << "Choice: ";
        cin >> choice_panel;
        cout << "===========================================\n";
        if (choice_panel == 1) {
            while (cycle != 1) {
                cout << "\n================Admin panel================\n";
                cout << "Add information about student [1]"
                << "\nSave information in base [2]\nShow database [3]\nDelete information [4]\nExit [0]\nChoice: ";
                cin >> choice_adm;
                cout << "===========================================\n";
                switch (choice_adm) {
                case 1:
                    add_info(mass);
                    calculate_ave_mark(mass);
                    check_grant_requarements(mass);
                    calculate_grants(mass, grant);
                    break;
                case 2:
                    save_info(mass);
                    break;
                case 3:
                    show_info(mass);
                    break;
                case 4:
                    del_info(mass);
                    break;
                case 0:
                    cycle = 1;
                    break;
                default:
                    cout << "\n===========================================";
                    cout << "\n===========Error: Invalid choice!==========\n";
                    cout << "===========================================\n";
                }
            }
        }
        else if (choice_panel == 2) {
            while (cycle != 1) {
                cout << "\n================User panel================\n" << "Show database [1]\nExit [0]\nChoice: ";
                cin >> choice_user;
    
                switch (choice_user) {
                case 1:
                    show_info(mass);
                    break;
                case 0:
                    cycle = 1;
                    break;
                default:
                    cout << "\n===========================================";
                    cout << "\n===========Error: Invalid choice!==========\n";
                    cout << "===========================================\n";
                }
            }
        }
    }//in process
    
    void add_info(vector <STUD> &mass){
        STUD students;
        cout << "\n==============Adding information===============";
        cout << "\nInput group number: ";
        cin >> students.groupNum;
        cout << "===============================================\n";
        cout << "Input student full name:\n";
        for (int i = 0; i < 3; i++) cin >> students.fullName[i];
        cout << "===============================================\n";
        cout << "Input type of education(paid - 1 or budgetary - 2): ";
        cin >> students.educationType;
        cout << "===============================================\n";
        cout << "Input social activity(active - 1 or passive - 2): ";
        cin >> students.socialActivity;
        cout << "===============================================\n";
        cout << "Input credits for 5 subjects(pass - 1 or fail - 0):\n";
        for (int i = 0; i < 5; i++) cin >> students.passSubject[i];
        cout << "===============================================\n";
        cout << "Input marks for 4 subjects(1 - 10):\n";
        for (int i = 0; i < 4; i++) cin >> students.markSubject[i];
        cout << "===============================================\n";
        mass.push_back(students);
    }//completed
    
    void check_grant_requarements(vector <STUD> &mass) {
        int counter_exams = 0, counter_passes = 0, counter_condition = 0;
    
        for (int i = 0; i < mass.size(); i++) {
            if (mass[i].educationType == 2) {
                counter_condition++;
            } //проверка на бюджет
    
            for (int j = 0; j < 5; j++)
            {
                if (mass[i].passSubject[j] == 1) {
                    counter_passes++;
                }
                if (counter_passes == 5) counter_condition++;
            }//проверка зачётов
    
            for (int k = 0; k < 4; k++)
            {
                if (mass[i].markSubject[k] >= 4) {
                    counter_exams++;
                }
                if (counter_exams == 4) counter_condition++;
            }//проверка экзаменов
            if (counter_condition == 3) mass[i].grantcheck = 1;
            else mass[i].grantcheck = 0;//проверка на соблюдение обязательных условий для получения стипендии
        }
    }//comleted
    
    void calculate_ave_mark(vector <STUD> &mass) {
        for (int i = 0; i < mass.size(); i++) {
            int avemark = 0;
            int avemark_ost = 0;
            for (int j = 0; j < 4; j++) avemark += mass[i].markSubject[j];
    
            avemark_ost = avemark % 4;
    
            if (avemark_ost >= 5) {
                avemark = (avemark / 4) + 1;
                mass[i].averageMark = avemark;
            }
            else {
                avemark /= 4;
                mass[i].averageMark = avemark;
            }
        }
    }//in process
    
    void calculate_grants(vector <STUD> &mass, int grant) {
        for (int i = 0; i < mass.size(); i++)
        {
            if (mass[i].grantcheck == 1) {
                if (mass[i].socialActivity == 1 && mass[i].averageMark >= 9) mass[i].grantValue = grant + (grant * 0.5);
                else if (mass[i].averageMark == 6 || mass[i].averageMark == 7) mass[i].grantValue = grant + (grant * 0.25);
                else if (mass[i].averageMark == 5) mass[i].grantValue = grant;
                else if (mass[i].averageMark <= 5) mass[i].grantValue = 0;
            }
            else mass[i].grantValue = 0;
        }
    }//comleted
    
    
    void show_info(vector <STUD> &mass) {
        for (int i = 0; i < mass.size(); i++)
        {
            cout << "\n=========Information about student number " << i+1 << "=========";
            cout << "\nGroup number: " << mass[i].groupNum;
            cout << "\n====================================================";
            cout << "\nFull name: " << mass[i].fullName[0] << " " << mass[i].fullName[1] << " " << mass[i].fullName[2];
            cout << "\n====================================================";
            cout << "\nType of education: ";
            switch (mass[i].educationType)
            {
            case paid:
                cout << "Paid";
                break;
            case budgetary:
                cout << "Budgetary";
                break;
            default:
                cout << "Error: No information!";
                break;
            }
            cout << "\n====================================================";
            cout << "\nSocial activity: ";
            switch (mass[i].socialActivity)
            {
            case active:
                cout << "Active";
                break;
            case passive:
                cout << "Passive";
                break;
            default:
                cout << "Error: No information!";
                break;
            }
            cout << "\n====================================================";
            cout << "\nCredits for 5 subjects(1 - Pass, 0 - Fail):";
            for (int j = 0; j < 5; j++)
            {
                cout << "\nSubject number " << j + 1 << ": ";
                switch (mass[i].passSubject[j])
                {
                case pass:
                    cout << "pass";
                    break;
                case fail:
                    cout << "fail";
                    break;
                default:
                    cout << "Error: No information!";
                    break;
                }
            }
            cout << "\n====================================================";
            cout << "\nMarks for 4 exam subjects: " << endl;
            for (int j = 0; j < 4; j++) cout << "Subject number " << j + 1 << ": " << mass[i].markSubject[j] << endl;
            cout << "====================================================";
            cout << "\nAverage mark: " << mass[i].averageMark;
            cout << "\n====================================================";
            cout << "\nValue of student grant: " << mass[i].grantValue;
            cout << "\n====================================================\n";
            cout << "\n--------------------------------------------------------------------\n";
        }
    }//completed
    
    void del_info(vector<STUD> &mass) {
        int del_number = 0;
        cout << "\n====================================================\n";
        cout << "Enter number of information block you want to delete: ";
        cin >> del_number;
        cout << "\n====================================================\n";
        if (mass.size() >= del_number) {
            auto iter = mass.cbegin();
            mass.erase(iter + del_number - 1);
            cout << "\n====================================================\n";
            cout << "======================Deleted!======================";
            cout << "\n====================================================\n";
        }
        else {
            cout << "\n====================================================\n";
            cout << "============There is no such information!============";
            cout << "\n====================================================\n";
        }
    }//completed
    
    void save_info(vector <STUD> &mass) {
        ofstream out("base.txt");
        cout << "==========Saving information...===========" << endl;
    
        for (int i = 0; i < mass.size(); i++)
        {
            out << mass[i].groupNum;
            out << mass[i].averageMark;
            out << mass[i].fullName[0] << mass[i].fullName[1] << mass[i].fullName[2];
            out << mass[i].educationType;
            out << mass[i].socialActivity;
            for (int j = 0; j < 5; j++) out << mass[i].passSubject[j];
            for (int j = 0; j < 4; j++) out << mass[i].markSubject[j];
            out << mass[i].averageMark;
            out << mass[i].grantValue;
        }
        out.close();
    
        cout << "\n===============Success!==============\n" << endl;
    }//comleted
##Experience
I took free online courses, tried to use the studied frameworks in practice.
##Education
BNTU, Yandex courses, self-development by interests, etc.
##English
Chatting with foreigners, watching videos of American bloggers and developers, reading frameworks documentations, etc.