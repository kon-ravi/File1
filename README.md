# File1
#include<stdio.h>
#include<stdbool.h>
struct process{
    int index;
    int arr_time,bt_time,wt_time;
    float priority;
    bool flag;
};
void sort(struct process arr[],int n){
    for(int i=1;i<n;i++){
        struct process obj=arr[i];
        int j=i-1;
        while(j>=0&&arr[j].priority>=obj.priority){
            if(arr[j].priority==obj.priority){
                if(arr[j].arr_time>obj.arr_time){
                   int p,q,r;
                   float d;
                   int e;
                   p=arr[j].arr_time;
                   q=arr[j].bt_time;
                   r=arr[j].wt_time;
                   d=arr[j].priority;
                   e=arr[j].index;
                   arr[j].arr_time=arr[j+1].arr_time;
                   arr[j].bt_time=arr[j+1].bt_time;
                   arr[j].wt_time=arr[j+1].wt_time;
                   arr[j].priority=arr[j+1].priority;
                   arr[j].index=arr[j+1].index;
                   arr[j+1].arr_time=p;
                   arr[j+1].bt_time=q;
                   arr[j+1].wt_time=r;
                   arr[j+1].priority=d;
                   arr[j+1].index=e;
                }
            }else{
                swapprocess(&arr[j],&arr[j+1]);
                   int p,q,r;
                   float d;
                   int e;
                   p=arr[j].arr_time;
                   q=arr[j].bt_time;
                   r=arr[j].wt_time;
                   d=arr[j].priority;
                   e=arr[j].index;
                   arr[j].arr_time=arr[j+1].arr_time;
                   arr[j].bt_time=arr[j+1].bt_time;
                   arr[j].wt_time=arr[j+1].wt_time;
                   arr[j].priority=arr[j+1].priority;
                   arr[j].index=arr[j+1].index;
                   arr[j+1].arr_time=p;
                   arr[j+1].bt_time=q;
                   arr[j+1].wt_time=r;
                   arr[j+1].priority=d;
                   arr[j+1].index=e;
            }
            j--;
        }
       arr[j+1].arr_time=obj.arr_time;
       arr[j+1].bt_time=obj.bt_time;
       arr[j+1].wt_time=obj.wt_time;
       arr[j+1].priority=obj.priority;
       arr[j+1].index=obj.index;
    }
};
void change_wt_priority(struct process arr[],int n,int wt,int start){
    for(int i=start;i<n;i++){
        if(arr[i].flag){
                arr[i].wt_time+=(wt-arr[i].arr_time);
                arr[i].flag=false;
        }else{
                arr[i].wt_time+=(wt);
        }

        arr[i].priority=(1+((float)arr[i].wt_time/arr[i].bt_time));
    }
}
void display(struct process a){
    printf("Procees id = %d\n",a.index);
    printf("Arr time = %d \n",a.arr_time );
    printf("Bt time = %d \n",a.bt_time);
    printf("Wt time = %d\n",a.wt_time);
    printf("priority = %f\n",a.priority);
}
void result(struct process arr[],int n){
    for(int i=0;i<n;i++){
        printf("Student no = %d, Wt time = %d \n",arr[i].index,arr[i].wt_time);
    }
}
int main(int argc, char const *argv[]) {
    printf("Enter number of students\n");
    int p_no;
    scanf("%d",&p_no);
    struct process arr[p_no];
    for(int i=0;i<p_no;i++){
            arr[i].priority=1;
            arr[i].wt_time=0;
            arr[i].index=i+1;
            arr[i].flag=true;
    }
    int at,bt;
    for(int i=0;i<p_no;i++){
        printf("For student %d:\n",i+1);
        printf("Enter arrival time and burst time:\n");
        scanf("%d %d",&at,&bt);
        if(at<10||at>12){
         printf("Teacher is not available\n");
         i--;
         p_no--;
         continue;
        }
        arr[i].arr_time=at;
        arr[i].bt_time=bt;
    }
    sort(arr,p_no);
    int curr=arr[0].index;
    for(int i=0;i<p_no;i++){
        printf("Current student: %d\n",curr);
        change_wt_priority(arr,p_no,arr[i].bt_time,i+1);
        sort(arr,p_no);
        curr=arr[i+1].index;
    }
    result(arr,p_no);
    return 0;
}
