# class06: r functions
erica yue hu (pid:a17787225)

## background

functions are at the heart of using R. Everything we do involves calling
and using functions (from data input)

all functions in R have at least 3 things:

1.  A **name** the thing we use to call the function.
2.  one or more input **arguments** that are comma separated
3.  the **body**, lines of code between curly brackets { } that does the
    work of the function

## A first function

lets write a silly wee function to add some numbers:

``` r
add<- function (x) {
  x+1
}
```

lets try it out

``` r
add(100)
```

    [1] 101

will ts work?

``` r
add(c(100,200,300))
```

    [1] 101 201 301

modify it to be more useful and add more than just 1

``` r
add <- function (x,y=1) {
  x+y 
}
```

^this means that if you don’t have y, it is gonna just be 1

``` r
add(100,10)
```

    [1] 110

``` r
add (100)
```

    [1] 101

``` r
plot(1:10, col="blue",typ="b")
```

![](class06_files/figure-commonmark/unnamed-chunk-7-1.png)

``` r
log(10, base = 10)
```

    [1] 1

> **N.B** Input arguments can be either **required** or **optional**.
> the later have a fall-back default that is specifed in the function
> code with an equals sign.

``` r
#add(x=100,y=200,z=300) ts does not work cuz we have notin for z. 
```

\##A second function all functions in R look like this

    name <- function (arg) {
      body
    }

the `sample(0)` function in R takes a sample of the specified size from
the elements of x using either with or without replacement.

``` r
sample(1:10, size = 4)
```

    [1]  4  7 10  9

> Q. Return 12 numbers picked randomly from the input 1:10

``` r
sample(1:10, size =12, replace = TRUE)
```

     [1]  9  7  5  1 10  6  7  5  8  3 10  7

`replace = true` allows you to get the same number for more than once

> Q. write the code to generate a random 12 nucleotide long DNA
> sequence?

``` r
sample( c("A","C","G","T"), size = 12, replace = TRUE)
```

     [1] "C" "T" "G" "G" "A" "C" "A" "C" "A" "C" "G" "G"

another way to write ts:

``` r
bases <-  c("A","C","G","T")
sample(bases, size=12, replace = TRUE)
```

     [1] "G" "C" "A" "A" "G" "C" "C" "A" "G" "G" "G" "T"

> Q. write a first version function called `generate_dna()` that
> genarates a user specified length `n` random DNA sequence?

    name <- function (arg) {
      body
    } 

``` r
generate_dna <- function(n=6) {
  bases <- c("A","C","G","T")
  sample(bases, size = n, replace = TRUE)
}
```

``` r
generate_dna(100)
```

      [1] "A" "A" "A" "A" "A" "G" "T" "C" "T" "C" "C" "A" "T" "T" "G" "A" "G" "C"
     [19] "T" "T" "T" "A" "T" "A" "T" "C" "C" "G" "A" "A" "T" "T" "G" "C" "A" "C"
     [37] "G" "G" "C" "C" "C" "C" "G" "C" "C" "G" "A" "G" "T" "G" "T" "G" "A" "G"
     [55] "T" "G" "A" "C" "C" "C" "T" "T" "C" "T" "T" "C" "C" "T" "A" "G" "T" "T"
     [73] "G" "A" "G" "A" "A" "C" "G" "C" "G" "T" "C" "T" "A" "A" "C" "A" "C" "G"
     [91] "G" "G" "A" "T" "C" "C" "T" "G" "C" "G"

``` r
#this calls the function 
```

n = 6, just means tht if you don’t put anything in, then it is gonna run
as 6

> Q.modify ur function to return a FASTA like seequence so rather than
> \[1\] “G” “C” “A” “A” “T” we want “GCAAT”.

``` r
generate_dna <- function(n=6) {
  bases <- c("A","C","G","T")
  seq=sample(bases, size = n, replace = TRUE)
  paste(seq, collapse = "")

}
```

``` r
generate_dna(10)
```

    [1] "ATGTGTAACC"

> Q. give the user an option to return FASTA format output sequence or
> strandard multi-element vector format

``` r
generate_dna <- function(n=6, fasta=TRUE) {
  bases <- c("A","C","G","T")
  seq<-sample(bases, size = n, replace = TRUE)
  
  if(fasta){
    seq<-paste(seq, collapse="")
    cat("Hello...")
  } else { 
    cat ("...is it me ur looking for...")
  }

  
    return(seq)

}
```

``` r
generate_dna(10,fasta=T)
```

    Hello...

    [1] "TAGTTTGAAG"

``` r
generate_dna(10,fasta=F)
```

    ...is it me ur looking for...

     [1] "A" "A" "G" "C" "A" "T" "T" "C" "T" "G"

if fasta condition is fulfilled, then it is going to do everything in
the sequence that is listed inside the if loop

\##A new cool function \>Q. write a funciton called `generate_protein()`
that generates a user specified length protein sequence in FASTA like
format?

> Q. use ur new `generate_protein()` function to generate sequences
> between length 6 and 12 amino acids in legnth and check any of these
> are unique in nature (i.e found in the NR database at NCBI)

``` r
generate_protein<- function(n=10){
  aa <- c("A","R","N","D","C","Q","E","G","H","I",
  "L","K","M","F","P","S","T","W","Y","V",
  "U")
  seq = sample(aa, size=n, replace=TRUE)

  return (paste(seq, collapse=""))
    
}
```

``` r
generate_protein(30)
```

    [1] "FHDMRIDSWMNECPTCMIKIIIIAWVGQVD"

> Question 2: using a for loop

``` r
generate_protein<- function(n){
  aa <- c("A","R","N","D","C","Q","E","G","H","I",
  "L","K","M","F","P","S","T","W","Y","V",
  "U")
  seq = sample(aa, size=n, replace=TRUE)
  
  return (paste(seq, collapse=""))
}
```

``` r
for (i in 6:12) {
  cat(">", i, "\n", sep = "")
  cat (generate_protein(i),"\n")
}
```

    >6
    FGLEDF 
    >7
    KGRRSMG 
    >8
    PPKHUGCV 
    >9
    STGWAQUAG 
    >10
    DCUFMUYGQS 
    >11
    SSNLWGLMQGM 
    >12
    ERKLGCMMRPKQ 
