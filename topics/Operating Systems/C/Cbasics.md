# C Programming Language

## How to read multiple lines in config file

We know that

```
 FILE * fp;
   if ( (fp = fopen("example.cfg", "r")) != NULL )
   {
      // get an operand from the configuration file
      fscanf(fp, "%d", &examp);
   }
```

Can read the first value from a config file and put it into our examp variable.

But how do we read multiple lines and set multiple config variables?

our fscanf function can take in multiple parameters (for each row)

Just make sure we specify the type of values we are reading in, in the second parameter (as shown)

```
   FILE * fp;
   if ( (fp = fopen("example.cfg", "r")) != NULL )
   {
      // get an operand from the configuration file
      fscanf(fp, "%d %d %d", &output1 ,&output2, &output3);
   }


   printf("%d\n", output1);
   printf("%d\n", output2);
   printf("%d\n", output3;
```

So output1 is the first row, output2 is the second row and so on.

They are all set to be ints, and at the end we just print them out.

That is how we read rows from a config file to set variables.

## Setting values for multiple environment variables

This one is simple, we just use getenv("name-of-our-environment-variable")

EXAMPLE:

```
 // Override the default values with an environment variable value.
   char * op1;
   if ( (op1 = getenv( "example1" )) != NULL )
   {
      // get an operand from the environment
      output1 = atoi(op1);
   }
    char * op2;
   if ( (op2 = getenv( "example2" )) != NULL )
   {
      // get an operand from the environment
      output2 = atoi(op2);
   }
    char * op3;
   if ( (op3 = getenv( "C\example3" )) != NULL )
   {
      // get an operand from the environment
      output3 = atoi(op3);
   }


   printf("Test env variables are working\n");
   printf("%d\n", output1);
   printf("%d\n", output2);
   printf("%d\n", output3);
```

## setting variables with command line arguments

This uses an array `char* argv[]` to parse through cmd line arguments

define the array

```
int main(int argc, char* argv[])
{}
```

Then you can parse through your cmd line argument,

```
   //filter -a -b -c
   // a = output1
   // b = output2
   // c = output3
   // Get a command line argument (if it exists).
   if (argc > 1)
   {  // get an operand from the command line
      output1 = atoi(argv[1]);
      output2 = atoi(argv[2]);
      output3 = atoi(argv[3]);
   }

   printf("Test Command line arguments are working\n");
   printf("%d\n", output1);
   printf("%d\n", output2);
   printf("%d\n", output3);
```
