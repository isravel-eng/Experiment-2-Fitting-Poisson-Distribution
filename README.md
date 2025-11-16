# Experiment-2-Fitting-Poisson-Distribution
Aim: 
To fit Poisson distribution for the arrival of objects per minute from the feeder. 
# Software required: 

Python and Visual Component Tool
# Theory: 

1. The Poisson distribution gives the probability of a number of events occurring in a fixed interval of time or space when events occur independently and at a constant average rate (λ).
2. The probability mass function (PMF) is:  
<img width="1171" height="73" alt="image" src="https://github.com/user-attachments/assets/e28da9e9-3b3f-4969-baa9-2ff06c3358ba" />
3. Here, λ = mean number of occurrences, and e = 2.718 (base of natural logarithm).
4. The mean and variance of a Poisson distribution are both equal to λ.
5. Applicable when events occur independently, singly, and at a constant rate.
# Algorithm
<img width="1144" height="412" alt="image" src="https://github.com/user-attachments/assets/6bf357bd-7ba2-4908-8c93-ef74e4747a4f" />

# Program
**_Name : ISRAVEL Y <br>
 Reg No : 25018187 <br>
 Slot Name : 3P1-1<br>
 [colab link](https://colab.research.google.com/drive/1IlRZRK1bhjGjY7jzSMETlQam2r6l5uyR?usp=sharing)_**  

```py
import numpy as np
import math
import scipy.stats
import builtins

Data = [int(i) for i in input("Enter the data with space: ").split()]
length = len(Data)
M = builtins.max(Data)

x = list()
freq = list()

# frequency of each arrival
for i in range(M+1):
    freq.append(Data.count(i))
    x.append(i)

sum_freq = np.sum(freq)

# probabilities based on observed frequencies
p = [freq[i]/sum_freq for i in range(M+1)]

# mean of the distribution
mean = np.inner(x, p)

print("X    P(X=x)    Obser.freq   Expec.freq  xi")
print()

chi = 0
for i in x:
    p_i = (math.exp(-mean) * (mean**i)) / math.factorial(i)
    e = p_i * sum_freq
    xi = ((freq[i] - e)**2) / e
    chi += xi
    print(f"{i}   {p_i:.3f}       {freq[i]}        {e:.2f}        {xi:.3f}")

print()
print("Calculated chi square value:", f"{chi:.4f}")

# chi-square table value
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)
print(f"Table value of chi square at 1% level is {table_chi2:.4f}")

if chi < table_chi2:
    print("✔ The data can be fitted in Poisson Distribution at 1% LOS")
else:
    print("✘ The data cannot be fitted in Poisson Distribution at 1% LOS")
```



# Output

<img width="602" height="380" alt="image" src="https://github.com/user-attachments/assets/4a11d073-8ef5-42c7-973f-21069681b81d" />


# Result
The Poisson Distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 

