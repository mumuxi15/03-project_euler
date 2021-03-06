#### Euler's Project

##### Q1 - 20

1. If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23. Find the sum of all the multiples of 3 or 5 below 1000.

   233168

   ```python
   def Euler1(N):
     " failed at larger N due to large rounding error in python3"
       m3 = [i*3 for i in range(int((N-0.1)//3)+1)]
       m5 = [i*5 for i in range(int((N-0.1)//5)+1)]
       rs = set(m3+m5)
       print (sum(rs))
   
   def Euler1(N):
     " algorithmic approach - all pass"
   	m3 = int((N-0.1)//3)
   	m5 = int((N-0.1)//5)
   	m15 = int((N-0.1)//15)
   	m3_sum = 3*(1+m3)*m3//2
   	m5_sum = 5*(1+m5)*m5//2
   	m15_sum = 15*(1+m15)*m15//2
   	rs = m3_sum+m5_sum-m15_sum
   	print (rs)
   ```

2. Each new term in the Fibonacci sequence is generated by adding the previous two terms. By starting with 1 and 2, the first 10 terms will be:

   1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

   By considering the terms in the Fibonacci sequence whose values do not exceed N (<four million), find the sum of the even-valued terms.

   ```python
   def genFib(x):
     # F(1)=0, F(2)=1
   	# F(n) = F(n-1)+F(n-2) 
   	a, b = 0, 1
     even = 0
   	l = [a] # fib list
   	while b <= x:
   		a, b = b, a+b
   		if a%2 ==0:
   			even+=a
   	#l.append(a)
   	return even
   ```

   

3. The prime factors of 13195 are 5, 7, 13 and 29.

   What is the largest prime factor of the number 600851475143 ?

   ```python
   def LargestPrime(n):
   	'''start with largest prime number'''
   	maxPrime = 1
     # if remove multiples of 2
   	while n % 2 == 0:
   		maxPrime = 2
   		n = n // 2
   	# n must be odd here
   	for i in range(3,int(n**0.5)+1,1):
   		while n % i ==0: # remove all multiples of i
   			n = n // i
   			maxPrime = i
   						
   	if n > 2:        # normally i=1, except if residual is n
   		maxPrime  = n
   	return maxPrime
   ```

   

4. A palindromic number reads the same both ways. The largest palindrome made from the product of two 2-digit numbers is 9009 = 91 × 99.

   Find the largest palindrome made from the product of two 3-digit numbers which is less than N.

   ```python
   def panlidromic(x):
   	maxP = 1
   	for i in range(int(x**0.5),100,-1):
   		for j in range(min(x//i,999),100,-1): #3 digits
   			p = i*j
   			if p > maxP:
   				s = str(p)
   				if s == s[::-1]:
   					maxP = max(maxP, p)
   #					print (p,i,j)
   				
   	print ('max= ',maxP)
   	if maxP <=1:
   		return None
   	else:
   		return maxP
   ```

5. 2520 is the smallest number that can be divided by each of the numbers from 1 to 10 without any remainder.

   What is the smallest positive number that is evenly divisible by all of the numbers from 1 to 20?

   ```python
   --------------- #  without using GCD # -----------------------
   def smallest_divider(x):
   	'''find all primes <= x '''
   	prime = {}
   	product = 1
   	prime[2] = int(math.log(x,2))
   	x = x - 1 if x % 2 == 0 else x # start with odd number
   	for a in range(x,1,-2):
   		f = []
   		for i in range(int(a**0.5),2,-1):
   			while a % i == 0:
   				a = a//i
   				f.append(i)
   		if a > 2:
   			f.append(a)
   			
   		for i in set(f):
   			prime[i] = max(prime.get(i, 0), f.count(i))		
   		
   	for k, v in prime.items():
   		product = k**v*product
   	# e.g prime = {2:3,3:1,5:1,7:1}
   	print (product)
     
    --------------- #  with GCD # -----------------------
   def gcd(x,y):
   	while y!=0:
   		x,y=y,x%y
   	return x
   
   def smallest_divider(x):
   	'''p = A X B / gcd(A,B)'''
   	p = 2**int(math.log(x,2))
   	for a in range(3,x+1,1):
   		p = a*p//gcd(a,p)
   	print (p)
   ```

   

6. The sum of the squares of the first ten natural numbers is,

   $1^2+2^2+...+10^2=385$

   The square of the sum of the first ten natural numbers is,

   $(1+2+...+10)^2=55^2=3025$

   Hence the difference between the sum of the squares of the first ten natural numbers and the square of the sum is 3025−385=2640.

   Find the difference between the sum of the squares of the first one hundred natural numbers and the square of the sum.

   ```
   1 + 2 + ……….. + n = n(n+1) / 2
   1^2 + 2^2 + ……… + n^2 = n(n+1)(2n+1) / 6
   def calculation(N):
   	return (N*(N+1)//2)**2-N*(N+1)*(2*N+1)//6
   ```

7. By listing the first six prime numbers: 2, 3, 5, 7, 11, and 13, we can see that the 6th prime is 13.

   What is the 10 001st prime number?

   A: 10001 th prime is  104743

   ```python
   def isPrime(x):
   	# if isprime for x > 2
   	if x % 2 == 0: 
   		return False
   	for i in range(3,int(x**0.5)+1,1):
   		if x % i ==0: # remove all multiples of i
   			return False
   	return True
   	
   	
   def NthPrime(N):
   	'''start with largest prime number'''
   	if N == 1:
   		return 2
   	elif N == 2:
   		return 3
     
   	count, x = 2, 3
   	while count < N:
   		x += 2 # inc x by 2 at a time
   		if isPrime(x):
   			count += 1
   			print ('x = ',x, 'c=', count,N)
   			
   #	print (N,'th prime is ',x)
   	return x 
   ```

   

8. The four adjacent digits in the 1000-digit number that have the greatest product are 9 × 9 × 8 × 9 = 5832.

   73167176531330624919225119674426574742355349194934
   96983520312774506326239578318016984801869478851843
   85861560789112949495459501737958331952853208805511
   .......

   Find the thirteen adjacent digits in the 1000-digit number that have the greatest product. What is the value of this product?

   ```python
   def Ndigits(x,k):
   	s = [int(i) for i in str(x)]
   	maxp = -1
   	for i in range(len(s)-k+1):
   		p = 1
   		if 0 in s[i:i+k]:
   			p = 0
   		else:
   			for j in s[i:i+k]:
   				p = p*j
   		print (s[i:i+k], ' product = ',p)
   
   		maxp = max(p,maxp)
   	print (maxp)
   ```

9. A Pythagorean triplet is a set of three natural numbers, a < b < c, for which,

   a2 + b2 = c2

   For example, 3^2 + 4^2 = 9 + 16 = 25 = 5^2.

   There exists exactly one Pythagorean triplet for which a + b + c = 1000.
   Find the product abc.

   ```python
   def pythagorean(N):
       '''a < N/3
          b > a 
          a+b > c > N/3
          b > N/6
       
       '''
       for a in range(N//3,0,-1):
           for b in range(a+1,(N-a)//2+1,1):
               c = N-a-b
               if (c > b)&( b+a>c):
                   if a**2+b**2==c**2:
                       print ('triangle',a,b,c)
                       return a*b*c
                       
       return -1
   ```

   

10. The sum of the primes below 10 is 2 + 3 + 5 + 7 = 17.

   Find the sum of all the primes below two million.

   ```python
   -------    # the clever way    --------
   
   def sieve_of_Eratosthenes(N):
   	'''https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes'''
     N = N + 1
     A = [True]*N
     for i in range(2,int(N**0.5)+1):
     #		print ('i= ',i)
       if A[i]:
         j = i**2			
         while j<N:
           print (j)
           A[j] = False
           j += i
   
     prime = [i for i, x in enumerate(A) if x][2::]
     print (sum(prime))
   
   
   -------    # direct approach      --------
   
   def isPrime(x):
       # if isprime for x > 2
       if x % 2 == 0: 
           return False
       for i in range(3,int(x**0.5)+1,1):
           if x % i ==0: # remove all multiples of i
               return False
       return True
       
   def SumPrime(N):
       '''start with largest prime number'''
       S = {1:0,2:2}
       if N <= 2 :
           return S[N]
     
       T, x = 2, 3
       while x <= N:
           if isPrime(x):
               T += x
               # print ('x = ',x, 'sum=', T)
           x += 2 # inc x by 2 at a time
   
       return T
   ```

11. The product of these numbers is 26 × 63 × 78 × 14 = 1788696.

   What is the greatest product of four adjacent numbers in the same direction (up, down, left, right, or diagonally) in the 20×20 grid?

   ```python
   def Euler11(A):
   	N = len(A)
   	maxP = 0
   	for j in range(N):
   		for i in range(N):
   			
   			if i+4<=N:
   				H = [A[j][i],A[j][i+1],A[j][i+2],A[j][i+3]]
   				if 0 in H:
   					continue 
   				
   				maxP = max(maxP, A[j][i]*A[j][i+1]*A[j][i+2]*A[j][i+3])
   #					print (H, ' s= ',maxS, 'p = ',maxP//10000)
   					
   			if j+4<=N:
   				V = [A[j][i],A[j+1][i],A[j+2][i],A[j+3][i]]
   				if 0 in V:
   					continue 
   				maxP = max(maxP, A[j][i]*A[j+1][i]*A[j+2][i]*A[j+3][i])
   					
   			if (i+4<=N)&(j+4<=N):
   				D = [A[j][i],A[j+1][i+1],A[j+2][i+2],A[j+3][i+3]]
   				if 0 in D:
   					continue 
   				maxP = max(maxP, A[j][i]*A[j+1][i+1]*A[j+2][i+2]*A[j+3][i+3])
   					
   			if (j>=3)&(i+4<=N):
   				D= [A[j][i],A[j-1][i+1],A[j-2][i+2],A[j-3][i+3]]
   				if 0 in D:
   					continue 
   				maxP = max(maxP,A[j][i]*A[j-1][i+1]*A[j-2][i+2]*A[j-3][i+3])
   					
   	return maxP
   ```

12. The sequence of triangle numbers is generated by adding the natural numbers. So the 7th triangle number would be 1 + 2 + 3 + 4 + 5 + 6 + 7 = 28. The first ten terms would be:

   1, 3, 6, 10, 15, 21, 28, 36, 45, 55, ...

   Let us list the factors of the first seven triangle numbers:

    1: 1
    3: 1,3
    6: 1,2,3,6
   10: 1,2,5,10
   15: 1,3,5,15
   21: 1,3,7,21
   28: 1,2,4,7,14,28
   We can see that 28 is the first triangle number to have over five divisors.

   What is the value of the first triangle number to have over five hundred divisors?

   ```python
   def sieve(N):
   	'''https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes
   	   prime generator
   	'''
   	N = N + 1
   	A = [True]*N
   	for i in range(2,int(N**0.5)+1):
   		if A[i]:
   			for k in range(i**2,N,i):
   				A[k] = False
   	return A
   		
   
   def count_div(n):
   	'''counts with prime p
   	e.g n=360 [2,2,2,3,3,5] 4x3x2 (i+1)(j+1)(k+1)'''
   	c = 1
   	for p in range(2,n+1,1):
   		""""""
   		t = 0  #
   		if prime[p]: # if p is prime
   			if n % p == 0:  # p is a factor of n
   				while n % p ==0:
   					n = n//p
   					t += 1
   			c = c*(1+t)
   	return c
   
   def Euler12(N):
   	'''N: number of dividors
   	   n_th triangle = n x (n+1)/2
   	   since n , n+1 r co-prime
   	   find no of factors n has x no of factors n+1 has  -1  (1 counted twice)
   	'''
   	if N == 1:
   		return 3
   	elif N <= 3:
   		return 6
   	else:
   		n = 2
   		first = 2
   		second= 3
   		while n < N:
   
   			if first%2 == 0:
   				a = count_div(first//2)
   				b = count_div(first+1)
   			else:
   				a = count_div(second-1)
   				b = count_div(second//2)
   				
   			print (first,'x',second ,'/2=',first*second//2, '     ', a,b)
   			n = a*b-1
   			first += 1
   			second+= 1
   		print ('finanl ans:',(first-1)*(second-1)//2)
   		return (first-1)*(second-1)//2
   ```

13. Work out the first ten digits of the sum of the following one-hundred 50-digit numbers.

   ```python
   s = sum([int(input()) for l in range(int(input()))])
   print (str(s)[0:10])
   ```

14. The following iterative sequence is defined for the set of positive integers:

   n → n/2 (n is even)
   n → 3n + 1 (n is odd)

   Using the rule above and starting with 13, we generate the following sequence:

   13 → 40 → 20 → 10 → 5 → 16 → 8 → 4 → 2 → 1

   It can be seen that this sequence (starting at 13 and finishing at 1) contains 10 terms. Although it has not been proved yet (Collatz Problem), it is thought that all starting numbers finish at 1.

   Which starting number, under one million, produces the longest chain?
   
   ```python
   def collatz(n,c=0):
   	if n == 1:
   		return [1,c]
   	else:
   		n = n//2 if n%2==0 else 3*n+1
   		return collatz(n,c+1)
   ```
   
   
   
15. Starting in the top left corner of a 2×2 grid, and only being able to move to the right and down, there are exactly 6 routes to the bottom right corner.

   ![img](https://projecteuler.net/project/images/p015.png)

   How many such routes are there through a 20×20 grid?

   137846528820

   ```python
   def Euler15(N,M):
   	'''
   	https://www.mathblog.dk/project-euler-15/
   	
   	grid[i+1,j+1] = grid[i+1,j]+grid[i,j+1]
   	'''
   	MOD = 10**9+7
   	grid = [[1]*(M+1)]+[[1]+[0]*M for i in range(N)]
   	
   	for i in range(1,N+1):		
   		for j in range(1,M+1):
   			grid[i][j] = grid[i][j-1]+grid[i-1][j]		
   	return grid[N][M]
   ```
   
16. $2^{15} = 32768$ and the sum of its digits is 3 + 2 + 7 + 6 + 8 = 26.

   What is the sum of the digits of the number $2^{1000}$?

   ```python
   print (sum([int(a) for a in str(2**1000)])
   ```

17. If the numbers 1 to 5 are written out in words: one, two, three, four, five, then there are 3 + 3 + 5 + 4 + 4 = 19 letters used in total.

   If all the numbers from 1 to 1000 (one thousand) inclusive were written out in words, how many letters would be used?

   NOTE: Do not count spaces or hyphens. For example, 342 (three hundred and forty-two) contains 23 letters and 115 (one hundred and fifteen) contains 20 letters. The use of "and" when writing out numbers is in compliance with British usage.

18. By starting at the top of the triangle below and moving to adjacent numbers on the row below, the maximum total from top to bottom is 23.

   3
   7 4
   2 4 6
   8 5 9 3

   That is, 3 + 7 + 4 + 9 = 23.

   Find the maximum total from top to bottom of the triangle below:

   75
   95 64
   17 47 82
   18 35 87 10
   20 04 82 47 65
   19 01 23 75 03 34
   88 02 77 73 07 63 67
   99 65 04 28 06 16 70 92
   41 41 26 56 83 40 80 70 33
   41 48 72 33 47 32 37 16 94 29
   53 71 44 65 25 43 91 52 97 51 14
   70 11 33 28 77 73 17 78 39 68 17 57
   91 71 52 38 17 14 91 43 58 50 27 29 48
   63 66 04 68 89 53 67 30 73 16 69 87 40 31
   04 62 98 27 23 09 70 98 73 93 38 53 60 04 23

   NOTE: As there are only 16384 routes, it is possible to solve this problem by trying every route. However, Problem 67, is the same challenge with a triangle containing one-hundred rows; it cannot be solved by brute force, and requires a clever method! ;o)

   ```python
   def Euler18(A):
   #	bottom-up approach 
   	n = len(A) #no of lines
   	for i in range(n-2,-1,-1):
   		for j in range(len(A[i])):
   			A[i][j] = max(A[i][j]+A[i+1][j],A[i][j]+A[i+1][j+1])
   			
   	print (A[0][0])
   ```

19. You are given the following information, but you may prefer to do some research for yourself.

   - 1 Jan 1900 was a Monday.
   - Thirty days has September,
     April, June and November.
     All the rest have thirty-one,
     Saving February alone,
     Which has twenty-eight, rain or shine.
     And on leap years, twenty-nine.
   - A leap year occurs on any year evenly divisible by 4, but not on a century unless it is divisible by 400.

   How many Sundays fell on the first of the month during the twentieth century (1 Jan 1901 to 31 Dec 2000)?

20. *n*! means *n* × (*n* − 1) × ... × 3 × 2 × 1

   For example, 10! = 10 × 9 × ... × 3 × 2 × 1 = 3628800,
   and the sum of the digits in the number 10! is 3 + 6 + 2 + 8 + 8 + 0 + 0 = 27.

   Find the sum of the digits in the number 100!

   ```python
   def Euler20(x):
   #	sum of digits of x!
   	p = 1
   	for i in range(1,x+1):
   		p = p*i
   	print (sum([int(x) for x in str(p)]))
   ```

21. 

   

   

   

