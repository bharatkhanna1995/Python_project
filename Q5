class Integrate:
	def solve(self,order,coeffs,method):
		def f(x):
			sum=0
			for i in range(order+1):
				sum+=(coeffs[i]*(x**(order-i)))
			return sum
		if method=='trapezoid':
			a=float(input('enter the lower limit of interval: '))
			b=float(input('enter the upper limit of interval: '))
			n=int((b-a)/0.0005)
			x_values=[a]
			for i in range(1,n):
				x_values.append(float(str(x_values[0]+(0.001*i))[:5]))
			x_values.append(b)
			def trapezoid_solution(f,x_values,n):
				sum=0
				for i in range(1,n):
					sum+=f(x_values[i])
				sum*=2
				sum+=(f(x_values[0])+f(x_values[n]))
				ans=((x_values[n]-x_values[0])*sum)/(2*n)
				return ans
			return trapezoid_solution(f,x_values,n)
		elif method=='simpson':
			a=float(input('enter the lower limit of interval: '))
			b=float(input('enter the upper limit of interval: '))
			n=int((b-a)/0.0005)
			x_values=[a]
			for i in range(1,n):
				x_values.append(float(str(x_values[0]+(0.0005*i)[:5]))
			x_values.append(b)
			def simpson_solution(f,x_values,n):
				sum1,sum2,sum=0,0,0
				for i in range(1,n,2):
					sum1+=f(x_values[i])
				sum1*=4
				for i in range(2,n,2):
					sum2+=f(x_values[i])
				sum2*=2
				sum+=(f(x_values[0])+f(x_values[n])+sum1+sum2)
				ans=((x_values[n]-x_values[0])*sum)/(3*n)
				return ans
			return simpson_solution(f,x_values,n)
