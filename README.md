# CECS 378 Reading Assignment: Buffer Overflow

### Assignment Description
Answer the following questions from the Chapter 10 reading from your textbook. Be through and complete with your answers. You may work on these questions with a partner (no more than two working together), but **both** students must submit the document individually along with both of your names on each submission in their own repositories.

1. Define *buffer overflow*.

2. What types of programming languages are vulnerable to buffer overflows?

3. What are the two broad categories of defenses against buffer overflows?

4. Describe how a return-to-system-call attack is implemented and why it is used.

5. Describe how a heap buffer overflow attack is implemented.

6. Describe how a global data area overflow attack is implemented.

7. Rewrite the program shown below so that it is no longer vulnerable to a buffer overflow. Don’t use any ‘safe’ libraries in your solution.

``` C
int main ( int argc , char * argv []) {
    int valid = FALSE ;
    char str1 [8];
    char str2 [8];
    next_tag ( str1 );
    gets ( str2 );
    if ( strncmp ( str1 , str2 , 8) == 0)
        valid = TRUE ;
    printf (" buffer1 : str1 (% s) , str2 (% s) , valid (% d)\n" , str1 , str2 , valid );
}

```

8. Rewrite the function shown below so that it is no longer vulnerable to a stack buffer overflow. Don’t use any ‘safe’ libraries in your solution.
``` C
void gctinp ( char * inp , int siz )
{
    puts (" Input value : ");
    fgets ( inp , siz , stdin );
    printf (" buffer3 getinp read %s\n" , inp );
}

void display ( char * val )
{
    char tmp [16];
    sprintf ( tmp , " read val : %s\n" , val );
    puts ( tmp );8
}

int main ( int argc , char * argv [])
{
    char buf [16];
    getinp ( buf , sizeof ( buf ));
    display ( buf );
    printf (" buffer3 done \n");
}
```

9. Rewrite the two functions shown below so they are no longer vulnerable to a buffer overflow attack. Don’t use any ‘safe’ libraries in your solution.
``` C
int copy_buf ( char *to , int pos , char * from , int len )
{
    int i; for (i =0; i < len ; i ++) {
        to [ pos ] = from [i ];
        pos ++;
    }
    return pos ;
}

short read_chunk ( FILE fil , char * to )
{
    short len ;
    fread (& len , 2, 1, fil );
    fread (to , 1, len , fil );
    return len ;
}
```

10. Rewrite the program shown below so that it is no longer vulnerable to a heap buffer overflow. Don’t use any ‘safe’ libraries in your solution.
``` C
/* record type to allocate on heap */
typedef struct chunk {
    char inp [64];  /* vulnerable input buffer */
    void (* process )( char *) ; /* pointer to function to process inp */
} chunk_t ;

void showlen ( char * buf )
{
    int len ;
    len = strlen ( buf );
    printf (" buffer5 read %d chars \n" , len );
}

int main ( int argc , char * argv [])
{
    chunk_t * next ;
    setbuf ( stdin , NULL );
    next = malloc ( sizeof ( chunk_t ));
    next -> process = showlen () ;
    printf (" Enter value : ");
    gets ( next -> inp );
    next -> process ( next -> inp );
    printf (" buffer5 done \n");
}
```

## Deliverables

Commit the answers to the questions in a readable file to your git repository by the due date and time indicated with your repository on GitHub Classroom. The only approved file submission format is Markdown. Other formats will only be accepted with explicit approval.

### Please note:

* Your writeup file *must* be done in [Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) format and must be included in the repository as a separate file. View the file [`README.md`](README.md?plain=1) for an example of Markdown.
* Any included images or screenshots should be done in `*.jpg`, `*.png`, or `*.gif` formats, and be included individually as files in your repository (i.e. no binary ‘document’ with the images pasted inside).
* Screenshots or images *may* be linked in your Markdown file writeup if you wish to do so.
