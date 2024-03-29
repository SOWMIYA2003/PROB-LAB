# PROB-LAB
### Mean and variance of a discrete distribution
![Q1](https://github.com/SOWMIYA2003/PROB-LAB/assets/93427443/d9f21444-c2ee-4d84-a967-0fe362cdadbf)
```
import numpy as np
L=[int(i) for i in input().split()]

#Construction of frequency table
x=list();f=list()
N=len(L);M=max(L)
for i in range (M+1):
    c=0
    for j in range(N):
        if L[j]==i:
            c=c+1
    f.append(c) #adding elements to list f
    x.append(i) #adding elements to list x

sf=np.sum(f) #sum of frequency - sf
# calculating probability distribution
p=list()
for i in range(M+1):
    p.append(f[i]/sf) # calculating probability distribution
#calculate mean
mean=np.inner(x,p) # multiplying corresponding element - inner function
EX2=np.inner(np.square(x),p) #to find variance = ex^2 - (ex)^2
# variance
var=EX2-mean**2 
# standard deviation
SD=np.sqrt(var)

print("The Mean arrival rate is %.3f"%mean)

print("The Variance of arrival from feeder is %.3f"%var)

print("The Standard deviation of arrival from feeder is %.3f"%SD)

```
### Fitting Poisson distribution

![Q2](https://github.com/SOWMIYA2003/PROB-LAB/assets/93427443/ff3aa4ef-aef2-4ce1-94d6-607d45528db1)
```
import numpy as np
import math
import scipy.stats

##### Constructing frequency distribution
L=[int(i) for i in input(). split()]
N=len(L);M=max(L)
X=list();f=list()
for i in range (M+1):
    c=0
    for j in range(N):
        if L[j]==i:
            c=c+1
    f.append(c)
    X.append(i)
print(X)
print(f)

#### Finding Probability distribution and Mean
sf=np.sum(f)
p=list()
for i in range(M+1):
    p.append(f[i]/sf)
mean=np.inner(X,p)

#### Fitting Poissson distribution
P=list();E=list(); xi=list()
print(" X P(X=x) Obs.Fr Exp.Fr xi")
print("------------------------")
for x in range(M+1):
    P.append(math.exp(-mean)*mean**x/math.factorial(x))

    E.append(P[x]*sf)
    xi.append((f[x]-E[x])**2/E[x])
    print("%2.2f %2.3f %4.2f %3.2f %3.2f"%(x,P[x], f[x], E[x], xi[x]))
print("-----------------------")

####   Chi square test to test the Fit
cal_chi2_sq=np.sum(xi)
print("Calculated value of Chi square is %4.2f"%cal_chi2_sq)
table_chi2=scipy.stats.chi2.ppf(1-.01, df=M)
print("Table value of Chi square at 1  level is %4.2f"%table_chi2)
if cal_chi2_sq<table_chi2:
    print("The given data can be fitted in Poissson distribution at 1% LOS")
else:
    print("The given data cannot be fitted in Poisson distribution at 1% LOS")

```
### Correlation and regression for data analysis
![Q3](https://github.com/SOWMIYA2003/PROB-LAB/assets/93427443/c213d73f-a82c-4d24-a148-28bcb2d64546)
```
import numpy as np
import math
import matplotlib.pyplot as plt
x=[ int(i) for i in input().split()]
y=[ int(i) for i in input().split()]
N=len(x)
Sx=0
Sy=0
Sxy=0
Sx2=0
Sy2=0
for i in range(0,N):
    Sx=Sx+x[i]
    Sy=Sy+y[i]
    Sxy=Sxy+x[i]*y[i]
    Sx2=Sx2+x[i]**2
    Sy2=Sy2+y[i]**2
r=(N*Sxy-Sx*Sy)/(math.sqrt(N*Sx2-Sx**2)*math.sqrt(N*Sy2-Sy**2))
print("The Correlation coefficient is %0.3f"%r)
byx=(N*Sxy-Sx*Sy)/(N*Sx2-Sx**2)
xmean=Sx/N
ymean=Sy/N
print("The Regression line Y on X is ::: y = %0.3f + %0.3f (x-%0.3f)"%(ymean,byx,xmean))
plt.scatter(x,y)
def Reg(x):
  return ymean + byx*(x-xmean)
x=np.linspace(20,80,51)
y1=Reg(x)
plt.plot(x,y1,'r')
plt.xlabel('x-data')
plt.ylabel('y-data')
plt.legend(['Regression Line','Data points'])
```
### Single server with infinite capacity (M/M/1):(oo/FIFO)
![Q4](https://github.com/SOWMIYA2003/PROB-LAB/assets/93427443/602054b2-e7b5-4613-a65d-77339905f531)
```
arr_time=float(input("Enter the mean inter arrival time of objects from Feeder (in secs): "))
ser_time=float(input("Enter the mean  inter service time of Lathe Machine (in secs) :  "))
Robot_time=float(input("Enter the Additional time taken for the Robot (in secs) :  "))
lam=1/arr_time
mu=1/(ser_time+Robot_time)
print("--------------------------------------------------------------")
print("Single Server with Infinite Capacity - (M/M/1):(oo/FIFO)")
print("--------------------------------------------------------------")
print("The mean arrival rate per second : %0.2f "%lam)
print("The mean service rate per second : %0.2f "%mu)
if (lam <  mu):
    Ls=lam/(mu-lam)
    Lq=Ls-lam/mu
    Ws=Ls/lam
    Wq=Lq/lam
    print("Average number of objects in the system : %0.2f "%Ls)
    print("Average number of objects in the conveyor :  %0.2f "%Lq)
    print("Average waiting time of an object in the system : %0.2f secs"%Ws)
    print("Average waiting time of an object in the conveyor : %0.2f secs"%Wq)
    print("Probability that the system is busy : %0.2f "%(lam/mu) )
    print("Probability that the system is empty : %0.2f "%(1-lam/mu) )
else:
    print("Warning! Objects Over flow will happen in the conveyor")
print("---------------------------------------------------------------")

```
### Multiple server with infinite capacity - (M/M/c):(oo/FIFO)
![Q5](https://github.com/SOWMIYA2003/PROB-LAB/assets/93427443/b8a516ec-066a-4218-af83-e76bbbc199f3)
```
import math
arr_time=float(input("Enter the mean inter arrival time of objects from Feeder (in secs): "))
ser_time=float(input("Enter the mean  inter service time of Lathe Machine (in secs) :  "))
Robot_time=float(input("Enter the Additional time taken for the Robot (in secs) :  "))
c=int(input("Number of service centre :  "))
lam=1/arr_time
mu=1/(ser_time+Robot_time)
print("--------------------------------------------------------------")
print("Multiple Server with Infinite Capacity - (M/M/c):(oo/FIFO)")
print("--------------------------------------------------------------")
print("The mean arrival rate per second : %0.2f "%lam)
print("The mean service rate per second : %0.2f "%mu)
rho=lam/(c*mu)
sum=(lam/mu)**c*(1/(1-rho))/math.factorial(c)
for i in range(0,c):
    sum=sum+(lam/mu)**i/math.factorial(i)
P0=1/sum
if (rho<1):
    Lq=(P0/math.factorial(c))*(1/c)*(lam/mu)**(c+1)/(1-rho)**2
    Ls=Lq+lam/mu
    Ws=Ls/lam
    Wq=Lq/lam
    print("Average number of objects in the system : %0.2f "%Ls)
    print("Average number of objects in the conveyor :  %0.2f "%Lq)
    print("Average waiting time of an object in the system : %0.2f secs"%Ws)
    print("Average waiting time of an object in the conveyor : %0.2f secs"%Wq)
    print("Probability that the system is busy : %0.2f "%(rho))
    print("Probability that the system is empty : %0.2f "%(1-rho))
else:
    print("Warning! Objects Over flow will happen in the conveyor")
print("--------------------------------------------------------------")

```
### Series Queues with infinite capacity - Open Jackson Network
```

arr_time=float(input("Enter the mean inter arrival time of objects from Feeder (in secs): "))
ser_time1=float(input("Enter the mean  inter service time of Lathe Machine 1 (in secs) :  "))
ser_time2=float(input("Enter the mean  inter service time of Lathe Machine 2 (in secs) :  "))
ser_time3=float(input("Enter the mean  inter service time of Lathe Machine 3 (in secs) :  "))
Robot_time=float(input("Enter the Additional time taken for the Robot (in secs) :  "))
lam=1/arr_time
mu1=1/(ser_time1+Robot_time)
mu2=1/(ser_time2+Robot_time)
mu3=1/(ser_time3+Robot_time)
print("-----------------------------------------------------------------------")
print("Series Queues with infinite capacity- Open Jackson Network")
print("-----------------------------------------------------------------------")
if (lam <  mu1) and (lam <  mu2) and (lam <  mu3):
    Ls1=lam/(mu1-lam)
    Ls2=lam/(mu2-lam)
    Ls3=lam/(mu3-lam)
    Ls=Ls1+Ls2+Ls3
    Lq1=Ls1-lam/mu1
    Lq2=Ls2-lam/mu2
    Lq3=Ls3-lam/mu3
    Wq1=Lq1/lam
    Wq2=Lq2/lam
    Wq3=Lq3/lam
    Ws=Ls/(3*lam)
    print("Average number of objects in the system S1 : %0.2f "%Ls1)
    print("Average number of objects in the system S2 : %0.2f "%Ls2)
    print("Average number of objects in the system S3 : %0.2f "%Ls3)
    print("Average number of objects in the overall system    : %0.2f "%Ls)
    print("Average number of objects in the conveyor S1  :  %0.2f "%Lq1)
    print("Average number of objects in the conveyor S2  :  %0.2f "%Lq2)
    print("Average number of objects in the conveyor S3  :  %0.2f "%Lq3)
    print("Average waiting time of an object in the conveyor S1 : %0.2f secs"%Wq1)
    print("Average waiting time of an object in the conveyor S2 : %0.2f secs"%Wq2)
    print("Average waiting time of an object in the conveyor S3 : %0.2f secs"%Wq3)
else:
    print("Warning! Objects Over flow will happen in the conveyor")
print("----------------------------------------------------------------------")
```



![Q6](https://github.com/SOWMIYA2003/PROB-LAB/assets/93427443/6d29950f-3097-418a-a4ea-d493d044ceb4)

