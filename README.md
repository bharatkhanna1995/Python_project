#here it is withindentations
from numpy import *
n=int(input('order'))
A=zeros((n,n),float)
b=zeros((n),float)
D=zeros((n,n),float)
L=zeros((n,n),float)
U=zeros((n,n),float)
x=ones((n),float)
eps=zeros((n),float)

for i in range(n):
    eps[i]=.0000000001
lmt=20

for i in range(n):
    for j in range(n):
         A[i,j]=float(input('value at A['+str(i+1)+']['+str(j+1)+']  '))
        
for i in range(n):
    b[i]=float(input('value at b['+str(i+1) +']  '))
#getting values in D,U,L   
for i in range(n):
    for j in range(n):
        if i==j:
            D[i,j]=A[i,j]
        elif i>j:
            L[i,j]=A[i,j]
U=A-L-D

for i in range(lmt):
    if greater(abs(dot(A,x)-b),eps).any():
        q=- (dot(linalg.inv(L+D), b + dot(U, x)))
        x=q
        print (str(i),x)
    else:
        break
print(x)
