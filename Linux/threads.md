```c
1.Write a C program to create a thread that prints "Hello, World!"?
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
