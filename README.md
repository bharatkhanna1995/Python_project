class LinearSystemSolver:

    def matinA(self,m,n):
        from numpy import zeros,array
        A_=zeros((m,n),float)
        for i in range(m):
            for j in range(n):
                A_[i,j]=float(input('enter value at A['+str(i+1)+']['+str(j+1)+']  '))
        return A_


    def matinb(self,m):
        from numpy import zeros,array
        b_=zeros((m),int)
        for i in range(m):
            b_[i]=int(input('enter value at b['+str(i+1)+']  '))
        return b_


    def concat(self,m,n,A,b):
        from numpy import zeros,array
        C_=zeros((m,n+1),float)
        for i in range(m):
            for j in range(n):
                C_[i,j]=A[i,j]
        for i in range(m):
            C_[i,n]=b[i]
        return C_


    def bsubs(self,m,n,C):
        from numpy import zeros,array
        x_=zeros((m),float)
        for i in range(m-1,-1,-1):
            x_[i]=C[i,n]
            for j in range(i+1,n):
                x_[i]-=C[i,j]*x_[j]
            x_[i]=x_[i]/C[i,i]
        return x_

    def pivot(self,m,n,C):
        from numpy import zeros,array
        C_=zeros((m,n+1),float)
        C_=C
        for i in range(0,n):
            if C_[i,i]==0:
                for j in range(i+1,m):
                    if C_[j,i]!=0:
                        temp_rw=C_[i].copy()
                        C_[i],C_[j]=C_[j],temp_rw
        return(C_)


    def solve(self,method):

        if method=='gauss':

            m,n=int(input('row ')),int(input('column'))
            A=self.matinA(m,n)
            b=self.matinb(m)
            C=self.concat(m,n,A,b)
            C=self.pivot(m,n,C)
            for i in range(0,n):
                for k in range(i+1,m):
                    r=C[k,i]/C[i,i]
                    if r!=0:
                        for d  in range(0,n+1):
                            C[k,d]-=r*C[i,d]
            x=self.bsubs(m,n,C)
            return(x)

        if method=='gaussjordan':

            m,n=int(input('row ')),int(input('column'))
            A=self.matinA(m,n)
            b=self.matinb(m)
            C=self.concat(m,n,A,b)
            C=self.pivot(m,n,C)

            for i in range(0,n):
                for k in range(0,n):
                    if k!=i:
                        r=C[k,i]/C[i,i]
                        if r!=0:
                            for d  in range(0,n+1):
                                C[k,d]-=r*C[i,d]

            x=self.bsubs(m,n,C)
            return(x)


        elif method =='gauss-siedel':

            import numpy as np
            n=int(input('order'))
            A=self.matinA(n,n)
            b=self.matinb(n)
            eps,D,L,U=np.zeros(n),np.zeros(n),np.zeros(n),np.zeros(n)
            for i in range(n) :
                eps[i]=.0000001                  #value for epsilon
            lmt=20                                     #iteration limit

            for i in range(n):
                for j in range(n):
                    if i==j:
                        D[i,j]=A[i,j]
                    elif i>j:
                        L[i,j]=A[i,j]
            U=A-L-D

            for i in range(lmt):
                if np.greater(abs(np.dot(A,x)-b),eps).any():
                    q=- (np.dot(np.linalg.inv(L+D), b + np.dot(U, x)))
                    x=q
                else:
                    break
            return(x)

        else:
            return NULL

