#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int debug = 0;
int main(int argc, char **argv){
	
	u_int16_t evenFlip_e;
	u_int16_t oddFlip_f;
	u_int16_t allFlip_a;
	u_int16_t rt_s;
	u_int16_t value;
  extern int optind;
  extern char *optarg;
	char *ovalue;
  int c, i, err = 0;
  int eflag = 0, fflag = 0, aflag = 0, sflag = 0, oflag = 0;
  static char usage[] = "bitflip [-e] [-f] [-a] [-s] [-o outputfilename] intval\n";

  while ((c = getopt(argc, argv, "efaso:")) != -1)
    switch (c) {
		  case 'e':
			  eflag = 1;
			  break;
      case 'f':
        fflag = 1;
        break;
      case 'a':
        aflag = 1;
        break;
      case 's':
        sflag = 1;
        break;
		  case 'o':
			  oflag = 1;
        ovalue = optarg;
			  break;
		  case '?':
			  err = 1;
			  break;
  }

  if(argv[1] == NULL || (argv[optind]) == NULL){
    fprintf(stderr, usage, argv[0]);
  }

	//Assigning the argument to "value" and convert to int.
	value = atof(argv[optind]);
		
	//Displaying the value if none of the bitwise options are included..
	if (argv[2] == NULL){
		printf("Value: %d\n", value);
	}
		
	//Using the XOR operator with a for loop to flip even bits.
	if(eflag == 1){
	  evenFlip_e = value;
		for(i = 0; i < 16; i+=2){
			evenFlip_e = evenFlip_e ^ (1<<i);
		}
		printf("Even bits flipped: %d\n", evenFlip_e);
	}

	//Using the XOR operator with a for loop to flip odd bits.
	if(fflag == 1){
		oddFlip_f = value;
		for(i = 1; i < 16; i+=2){
			oddFlip_f = oddFlip_f ^ (1<<i);
		}
		printf("Odd bits flipped: %d\n", oddFlip_f);
	}

	//Using the NOT operator to flip all bits.
	if(aflag == 1){
		allFlip_a = ~value;
		printf("All bits flipped: %d\n", allFlip_a); 
	}

	/*Created two varaibales to stroe the left and right side. Then using the 
	OR operator to get ther ful 16-bit value.*/
	if(sflag == 1){
		rt_s = value;
		u_int16_t leftSide = 0;
		u_int16_t rightSide = 0;
		u_int16_t index = 15;
		for (i = 0; i < 8; i++){   
      leftSide |= ((rt_s & (1 << i)) << (index - i));
      index--;
    }   
    index = 0;
    for (i = 15; i > 7; i--){   
      rightSide |= ((rt_s & (1 << i)) >> (i - index));
      index++;
    }   
    rt_s = ((u_int16_t)leftSide | (u_int16_t)rightSide);
		printf("Switched all bits: %d\n", rt_s);
	}

  if(oflag == 1){ //Creating method to write to file.
    FILE *fptr = fopen(ovalue, "w");
    
    if(fptr == NULL){
      printf("Error. Could not open file.\n");
      exit(-1);
    }

    if(eflag == 1){
      fprintf(fptr, "Even bits flipped: %d\n", evenFlip_e);
    }

    if(fflag == 1){
      fprintf(fptr, "Odd bits flipped: %d\n", oddFlip_f);
    }

    if(aflag == 1){
      fprintf(fptr, "All bits flipped: %d\n", allFlip_a);
    }

    if(sflag == 1){
      fprintf(fptr, "Switched all bits: %d\n", rt_s);
    }
    
    fclose(fptr); //Closing FILE pointer.

  }

	if(err == 1){ //Checking if there is an error at getopt.
		printf("Error");
	}

  return 0;

}
