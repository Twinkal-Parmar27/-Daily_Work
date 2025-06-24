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
