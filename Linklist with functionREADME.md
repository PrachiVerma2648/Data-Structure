# Data-Structure
#include <stdio.h>
#include <stdlib.h>
typedef struct lklist
{
	int info;
	struct lklist *next;
} node;
node *temp = NULL;
node *ptr=NULL;
void insertAtEnd(node **head, int data);              
void insertAtBeg(node **head, int data);              
void insertAfterSpecific(node **head, int data);      
void insertAtSpecificPosition(node **head, int data); 
void traversing(node *head);                          
void deleteSpecific(node **head, int data);           
void deleteSpecificPosition(node **head, int data);   
int main()
{

	int n = 0, data = 0;
	node *head = NULL;
	while (1)
	{
		printf("\nEnter your choice\n");
		printf("1 for insert at begning\n");
		printf("2 for insert at end\n");
		printf("3 for insert after specific element\n");
		printf("4 for insert at specific element\n");
		printf("5 for traversing\n");
		printf("6 for delete a element\n");
		printf("7 for delete a element at specific element\n");
		printf("13 for exit\n");
		scanf("%d", &n);
		if (n == 13)
		{
			exit(1);
		}
		switch (n)
		{
		case 1:
			printf("Enter the element you want to insert\n");
			scanf("%d", &data);
			insertAtBeg(&head, data); 
			break;
		case 2:
			printf("Enter the element you want to insert\n");
			scanf("%d", &data);
			insertAtEnd(&head, data); 
			break;
		case 3:
			printf("Enter element after which you want to insert the element\n");
			scanf("%d", &data);
			insertAfterSpecific(&head, data);
			break;
		case 4:
			printf("Enter the position where you want to insert the element");
			scanf("%d", &data);
			insertAtSpecificPosition(&head, data);
			break;
		case 5:
			traversing(head); 
			break;
		case 6:
			printf("Enter the element you want to delete\n");
			scanf("%d", &data);
			deleteSpecific(&head, data);
			break;
		case 7:
			printf("Enter the position of element which you want to delete\n");
			scanf("%d", &data);
			deleteSpecificPosition(&head, data);
			break;

		default:
			printf("Enter the valid choice\n");
			break;
		}
	}

}
void insertAtBeg(node **head, int data)
{
	temp = (node *)(malloc(sizeof(node)));
	temp->info = data;
	temp->next = *head;
	*head = temp;
	printf("node insert successfully\n");
}
void traversing(node *head)
{
	while (head != NULL)
	{
		printf("%d ", head->info);
		head = head->next;
	}
}
void insertAtEnd(node **head, int data)
{
	temp = (node *)(malloc(sizeof(node)));
	temp->info = data;
	temp->next = NULL;
	if (*head == NULL)
	{
		*head = temp;
		printf("node insert successfully\n");
		return;
	}
	ptr = *head;
	while (ptr->next != NULL)
	{
		ptr = ptr->next;
	}
	ptr->next = temp;
	printf("node insert successfully\n");
}
void insertAfterSpecific(node **head, int data)
{
	if (*head == NULL)
	{
		printf("No element found\n");
	}
	ptr = *head;
	while (ptr != NULL)
	{
		if (ptr->info == data)
			break;
		ptr = ptr->next;
    }
    if (ptr == NULL)
    {
        printf("no element found\n");
    }
    else
    {
        printf("Enter the element you want to insert\n");
        scanf("%d", &data);
        temp = (node *)(malloc(sizeof(node)));
        temp->info = data;
        temp->next = ptr->next;
        ptr->next = temp;
        printf("Node insert successfully\n");
    }
}
void insertAtSpecificPosition(node **head, int data)
{
    node *ptr = *head;
    data--;
    while (data > 1 && ptr != NULL)
    {
        ptr = ptr->next;
        data--;
    }
    if (ptr != NULL)
    {
        printf("Enter the element that you want to insert\n");
        scanf("%d", &data);
        temp = (node *)(malloc(sizeof(node)));
        temp->info = data;
        temp->next = ptr->next;
        ptr->next = temp;
        printf("node insert successfully\n");
    }
    else
    {
        printf("Enter the vaid position\n");
    }
}
void deleteSpecific(node **head, int data)
{
    if (*head == NULL)
    {
        printf("no element found\n");
    }
	ptr = *head;
    if (ptr->info == data)
    {
        ptr = *head;
        *head = ptr->next;
        free(ptr);
        printf("Node delete successfully\n");
    }
    else
    {
        while (ptr->next != NULL)
        {
            if (data == (ptr->next)->info)
            {
                temp = ptr->next;
                ptr->next = temp->next;
                free(temp);
                printf("Node insert successfully\n");
                break;
            }
            ptr = ptr->next;
        }
        if (ptr == NULL)
            printf("no element found\n");
    }
}
void deleteSpecificPosition(node **head, int data)
{
    node *ptr = *head;
    if (ptr == NULL)
    {
        printf("No data present\n");
        return;
    }
    if (data == 1)
    {
        temp = *head;
        *head = ptr->next;
        free(temp);
        printf("Node delete successfully\n");
        return;
    }
    data--;
    while (data > 1 && ptr != NULL)
    {
        ptr = ptr->next;
        data--;
    }
    if (ptr != NULL)
    {
        temp = (ptr->next);
        if (ptr->next != NULL)
            ptr->next = (ptr->next)->next;
        free(temp);
        printf("node delete successully\n");
    }
}
