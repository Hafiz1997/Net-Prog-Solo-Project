

#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <netdb.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>
#include <arpa/inet.h>
#include <time.h>

int main(void)
{
    int sockfd = 0;
    int bytesReceived = 0;
    char recvBuff[256];
    memset(recvBuff, '0', sizeof(recvBuff));
    struct sockaddr_in serv_addr;

    /* Create a socket first */
    if((sockfd = socket(AF_INET, SOCK_STREAM, 0))< 0)
    {
        printf("\n Error : Could not create socket \n");
        return 1;
    }

    /* Initialize sockaddr_in data structure */
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(5000); // port
    serv_addr.sin_addr.s_addr = inet_addr("127.0.0.1");

    /* Attempt a connection */
    if(connect(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr))<0)
    {
        printf("\n Error : Connect Failed \n");
        return 1;
    }

    /* Create file where data will be stored */
    FILE *fp;
    fp = fopen("sample_file.txt", "ab"); 
    char name[50];
    char pass[100];
    char contact[50];
    int num;
    printf("\nPlease Enter Your Name: ");
    scanf("%s", &name);
    printf("\nPlease Enter Your Matric Number: ");
    scanf("%i", &num);
    printf("\nPlease Enter Your Contact/Email: ");
    scanf("%s", &contact);
    printf("\nPlease Enter Your Password: ");
    scanf("%s", &pass);

   int i, x;

   printf("\n\nEncrypting the string.\n");

   //using switch case statements

      for(i = 0; (i < 100 && pass[i] != '\0'); i++)
        pass[i] = pass[i] + 3; //3 that is added to ASCII value as a key for encryption

	printf("\nEncryption Finished!!! \n");
	printf("\nThe Encrypted String: %s\n", pass);

 	time_t t= time(NULL);
	struct tm tm = *localtime(&t);
	fprintf(fp, "now: %d-%d-%d %d:%d:%d\n", tm.tm_year + 1900, tm.tm_mon + 1, tm.tm_mday,tm.tm_hour,tm.tm_min,tm.tm_sec);

    fprintf(fp, "Name: %s\nMatric: %d\nContact: %s\nPassword: %s\n\n", name, num, contact, pass);
    fclose(fp);
    if(NULL == fp)
    {
        printf("Error opening file");
        return 1;
    }

    /* Receive data in chunks of 256 bytes */
    while((bytesReceived = read(sockfd, recvBuff, 256)) > 0)
    {
        printf("Bytes received %d\n",bytesReceived);    
        // recvBuff[n] = 0;
        fwrite(recvBuff, 1,bytesReceived,fp);
        // printf("%s \n", recvBuff);
    }

    if(bytesReceived < 0)
    {
        printf("\n Read Error \n");
    }


    return 0;
}
