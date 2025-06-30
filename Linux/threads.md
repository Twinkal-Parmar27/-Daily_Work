```c
//Write a C program to create a thread that prints "Hello, World!"?
#include<stdio.h>
#include<pthread.h>

pthread_mutex_t lock;

void* Print_Hello(void*arg);

int main()
{
	pthread_t thread;
	pthread_mutex_init(&lock,NULL);

	pthread_create(&thread,NULL,Print_Hello,NULL);
	pthread_join(thread,NULL);

	pthread_mutex_destroy(&lock);
}

void* Print_Hello(void*arg)
{	
	pthread_mutex_lock(&lock);
	printf("Helllo:\n");
	pthread_mutex_unlock(&lock);
}


//Modify the above program to create multiple threads, each printing its own message?
#include<stdio.h>
#include<pthread.h>

void* Print_Message(void* arg)
{
	char*msg=(char*)arg;
	printf("%s\n",msg);
}

int main()
{
	pthread_t threads[3];
	char*message[]={"Thread 1:Hello","Thread 2:Hello","Thread 3:Hello"};

	for(int i=0;i<3;++i)
		pthread_create(&threads[i],NULL,Print_Message,message[i]);

	for(inti=0;i<3;++i)
		pthread_join(threads[i],NULL);
}

//Develop a C program to create two threads that print numbers from 1 to 10 concurrently?
#include<stdio.h>
#include<pthread.h>

void* Print_Numbers(void*arg)
{
	char*name=(char*)arg;

	for(int i=1;i<=10;++i)
		printf("%s prints:%d\n",name,i);
}

int main()
{
	pthread_t thread1,thread2;

	pthread_create(&thread1,NULL,Print_Numbers,"Thread A");
	pthread_create(&thread2,NULL,Print_Numbers,"Thread B");

	pthread_join(thread1,NULL);
	pthread_join(thread2,NULL);
}

//Implement a C program to create a thread that calculates the factorial of a given number?
#include<stdio.h>
#include<pthread.h>

int number=5;
factorial=1;

void* Factorial(void* arg)
{
	int n=*((int*)arg);

	for(int i=1;i<=n;++i)
		factorial=factorial*i;
}

int main()
{
	pthread_t thread;

	pthread_create(&thread,NULL,Factorial,&number);
	pthread_join(thread,NULL);

	printf("Factorial of %d is %d\n",number,factorial);
}

//Write a C program to create two threads that print their thread IDs?
#include <stdio.h>
#include <pthread.h>

pthread_mutex_t lock;

void* print_id(void* arg) 
{   
    pthread_mutex_lock(&lock);
    printf("Thread ID: %lu\n", pthread_self());
    pthread_mutex_unlock(&lock);
    return NULL;
}

int main() 
{
    pthread_t t1, t2;
    pthread_mutex_init(&lock,NULL);

    pthread_create(&t1, NULL, print_id, NULL);
    pthread_create(&t2, NULL, print_id, NULL);

    pthread_join(t1, NULL);
    pthread_join(t2, NULL);

    pthread_mutex_destroy(&lock);

    return 0;
}

//Develop a C program to create a thread that prints the sum of two numbers?
#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>

pthread_mutex_t lock;
void* print_sum(void* arg)
{
	pthread_mutex_lock(&lock);
	int* numbers=(int*)arg;
	int a=numbers[0];
	int b=numbers[1];
	printf("sum=%d\n",a+b);
	free(numbers);
	pthread_mutex_unlock(&lock);
}
int main()
{
	pthread_t thread;
	pthread_mutex_init(&lock,NULL);
	int* numbers=(int*)malloc(2*sizeof(int));
	numbers[0]=4;
	numbers[1]=7;
	pthread_create(&thread,NULL,print_sum,numbers);
	pthread_join(thread,NULL);
	pthread_mutex_destroy(&lock);
}
//Implement a C program to create a thread that calculates the square of a number?
#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>

pthread_mutex_t lock;

void* Square(void* arg)
{	
	pthread_mutex_lock(&lock);
	int num=*((int*)arg);
	int result=num*num;
	
	printf("Square of %d is %d\n",num,result);
	pthread_mutex_unlock(&lock);

}

int main()
{
	pthread_t thread;
	pthread_mutex_init(&lock,NULL);
	int Number=6;

	pthread_create(&thread,NULL,Square,&Number);
	pthread_join(thread,NULL);
	pthread_mutex_destroy(&lock);
}

//Write a C program to create a thread that prints the current date and time?
#include<stdio.h>
#include<pthread.h>
#include<time.h>

pthread_mutex_t lock;

void* Date_Time(void* arg)
{	
	pthread_mutex_lock(&lock);
	time_t now=time(NULL);
	printf("Current Date and Time:%s",ctime(&now));
	pthread_mutex_unlock(&lock);

}

int main()
{
	pthread_t thread;
	pthread_mutex_init(&lock,NULL);

	pthread_create(&thread,NULL,Date_Time,NULL);
	pthread_join(thread,NULL);
	pthread_mutex_destroy(&lock);
}

//Develop a C program to create a thread that checks if a number is prime?
#include<stdio.h>
#include<pthread.h>
#include<stdbool.h>

pthread_mutex_t lock;

void* Prime(void* arg)
{	
	pthread_mutex_lock(&lock);
	int num=*((int*)arg);
	if(num<=1)
	{
		printf("%d isnot prime\n",num);
	}

bool prime=true;

for(int i=2;i<=num/2;i++)
	{
		if(num%i==0)
		{
			prime=false;
			break;
		}
	}
		printf("%d is %s\n",num,prime?"prime":"not prime");
		return NULL;
		pthread_mutex_unlock(&lock);
}

int main()
{
	pthread_t thread;
	pthread_mutex_init(&lock,NULL);
	int Number=29;

	pthread_create(&thread,NULL,Prime,&Number);
	pthread_join(thread,NULL);
	pthread_mutex_destroy(&lock);
}

//Implement a C program to create a thread that checks if a given string is a palindrome?
#include<stdio.h>
#include<string.h>
#include<pthread.h>
#include<stdbool.h>

pthread_mutex_t lock;

void* Palindrome(void* arg)
{
	pthread_mutex_lock(&lock);
	char*str=(char*)arg;
	int len=strlen(str);
	bool flag=true;

	for(int i=0;i<len/2;++i)
	{
		if(str[i]!=str[len-i-1])
		{
			flag=false;
			break;
		}
	}
	printf("%s is palindrome\n",str,flag?"a":"not a");
	return NULL;
	pthread_mutex_unlock(&lock);
}

int main()
{
	pthread_t thread;
	pthread_mutex_init(&lock,NULL);
	char word[]="madam";

	pthread_create(&thread,NULL,Palindrome,word);
	pthread_join(thread,NULL);
	pthread_mutex_destroy(&lock);
}

//Implement a C program to create a thread that generates random numbers and
synchronizes access to a shared buffer?
#include<stdio.h>
#include<pthread.h>
#include<semaphore.h>
#include<unistd.h>

#define BUFFER_SIZE 5

int buffer[BUFFER_SIZE];
int count=0;

pthread_mutex_t mutex;
sem_t full, empty;

void *producer(void*arg)
{
	for(int i=1;i<10; i++)
	{
		sem_wait(&empty);
		pthread_mutex_lock(&mutex);

		buffer[count++]=i;
		printf("Produced:%d\n",i);

		pthread_mutex_unlock(&mutex);
		sem_post(&full);
		sleep(1);
	}
}

void *consumer(void*arg)
{
	for(int i=1;i<10; i++)
	{
		sem_wait(&full);
		pthread_mutex_lock(&mutex);

		int item=buffer[--count];
		printf("Consumed:%d\n",item);

		pthread_mutex_unlock(&mutex);
		sem_post(&empty);
	}
	sleep(2);
}
int main()
{
	pthread_t prodthread,consthread;

	pthread_mutex_init(&mutex,NULL);
	sem_init(&full,0,0);
	sem_init(&empty,0,BUFFER_SIZE);

	pthread_create(&prodthread,NULL,producer,NULL);
	pthread_create(&consthread,NULL,consumer,NULL);

	pthread_join(prodthread,NULL);
	pthread_join(consthread,NULL);

	pthread_mutex_destroy(&mutex);
	sem_destroy(&full);
	sem_destroy(&empty);
}

//Implement a C program to create two threads that increment and decrement a shared
variable, respectively, using mutex locks?
#include<stdio.h>
#include<pthread.h>

pthread_mutex_t lock;
int shared_var=0;

void* increment(void*arg)
{
for(int i=0;i<5;i++)
{
	pthread_mutex_lock(&lock);
	shared_var++;
	printf("Increment thread:%d\n",shared_var);
	pthread_mutex_unlock(&lock);
}
}

void* decrement(void*arg)
{
for(int i=0;i<5;i++)
{
	pthread_mutex_lock(&lock);
	shared_var--;
	printf("Decrement thread;%d\n",shared_var);
	pthread_mutex_unlock(&lock);
}
}

int main()
{
	pthread_t thread1,thread2;
	pthread_mutex_init(&lock,NULL);

	pthread_create(&thread1,NULL,increment,NULL);
	pthread_create(&thread2,NULL,decrement,NULL);

	pthread_join(&thread1,NULL);
	pthread_join(&thread2,NULL);

	pthread_mutex_destroy(&lock);

	printf("Final output:%d\n",shared_var);
}

//Develop a C program to create a thread that reads input from the user and synchronizes
access to shared resources?

#include <stdio.h>
#include <pthread.h>
#include <string.h>

char shared_buffer[100];
pthread_mutex_t lock;

void* read_input(void* arg)
{
    pthread_mutex_lock(&lock);
    printf("Enter your name: ");
    fgets(shared_buffer, sizeof(shared_buffer), stdin);
    pthread_mutex_unlock(&lock);
    return NULL;
}

int main()
{
    pthread_t thread;
    pthread_mutex_init(&lock, NULL);

    pthread_create(&thread, NULL, read_input, NULL);
    pthread_join(thread, NULL);
    

    pthread_mutex_destroy(&lock);
}

