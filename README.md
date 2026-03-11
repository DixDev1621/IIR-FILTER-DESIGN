# IIR-FILTER-DESIGN
# EXP 3 A: DESIGN OF LOW PASS BUTTERWORTH FILTER USING BILINEAR TRANSFORMATION TECHNIQUE

# AIM: 

# To perform design of Butterworth Filter Using Impulse Invariant and Bilinear Transformation Techniques using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
clc ; 
close ; 
wp=input('Enter the pass band frequency (Radians )= ' ); 
ws=input('Enter the stop band frequency (Radians )= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time=');

//Pre warping- Bilinear Transformation 
omegap=(2/T)*tan(wp/2); 
disp(omegap,'omegap='); 
omegas=(2/T)*tan(ws/2); 
disp(omegas,'omegas=');

//Order of the filter 
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap)); 
disp(N,'N='); 
N=ceil(N); 
disp(N,'Round off value of N=');

//Cut off frequency 
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N))); 
disp(omegac,'omegac='); 
 
disp('Normalised Analog LPF Transfer function H(S)='); 
hs_Normalised = analpf(N,'butt',[0,0],1); 
disp(hs_Normalised); 
 
disp('Analog LPF Transfer function H(S)='); 
hs= analpf(N,'butt',[0,0],omegac); 
disp(hs); 
z=poly(0,'z');//Defining variable z 
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation 
disp('Digital LPF Transfer function H(Z)='); 
disp(Hz);
HW=frmag(Hz,512); // Frequency response 
w=0:%pi/511:%pi ; 
plot(w/%pi,abs(HW)); 
xlabel(' Normalized Digital Frequency w'); 
ylabel('Magnitude ');
title(' Frequency Response of Butterworth IIR LPF');
```
# CALCULATION:
<img width="1197" height="1600" alt="image" src="https://github.com/user-attachments/assets/0f154d5d-d489-409d-87c4-b4fb3dbe783e" />
<img width="1022" height="1600" alt="image" src="https://github.com/user-attachments/assets/f69185d4-8b1f-44b1-8a27-16befe0a15aa" />
<img width="1184" height="1600" alt="image" src="https://github.com/user-attachments/assets/8269a35e-a854-4a72-890b-95b4bb040f1e" />


# OUTPUT: 

<img width="756" height="430" alt="image" src="https://github.com/user-attachments/assets/3439f725-8f77-4ea8-ad7e-855e8a0affb2" />

# RESULT: 
Thus, design of Butterworth Low pass IIR filter waveforms were plotted and output was verified.

# EXP 3 B: DESIGN OF LOW PASS CHEBYSHEV IIR FILTER USING BILINEAR TRANSFORMATION

# AIM: 

# To a design of low pass Chebyshev IIR filter using Bilinear Transformation.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
clc ; 
close ; 
wp=input('Enter the pass band frequency (Radians )= ' ); 
ws=input('Enter the stop band frequency (Radians )= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time='); 
 
//Pre warping- Bilinear Transformation 
omegap=(2/T)*tan(wp/2); 
disp(omegap,'omegap='); 
omegas=(2/T)*tan(ws/2); 
disp(omegas,'omegas=');

//Order of the filter  
N=acosh(sqrt(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1)))/(acosh(omegas/omegap)); 
disp(N,'N='); 
N=ceil(N); 
disp(N,'Round off value of N=');
 
//Cut off frequency 
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N))); 
disp(omegac,'omegac=');
Epsilon = sqrt ((10^(0.1*alphap))-1); 
disp(Epsilon,'Epsilon='); 
[pols ,gn] = zpch1(N, Epsilon,omegap ); 
disp(gn,'Gain'); 
disp(pols,'Poles'); 
hs=poly(gn,'s','coeff')/real(poly(pols,'s')); 
disp(hs,'Analog Low pass Chebyshev Filter Transfer function');
z=poly(0,'z');//Defining variable z 
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation 
disp(Hz,'Digital LPF Transfer function H(Z)='); 
HW=frmag(Hz,512); // Frequency response 
w=0:%pi/511:%pi ; 
plot(w/%pi,abs(HW)); 
xlabel(' Normalized Digital Frequency w'); 
ylabel('Magnitude '); 
title(' Frequency Response of Chebyshev IIR LPF'); 
```
# CALCULATION:
<img width="1197" height="1600" alt="image" src="https://github.com/user-attachments/assets/e16b4dfa-bda6-4795-a474-b6f35f2c5e83" />
<img width="1132" height="1600" alt="image" src="https://github.com/user-attachments/assets/60b36c90-5269-455b-981b-72f0bdae6f39" />
<img width="912" height="1600" alt="image" src="https://github.com/user-attachments/assets/64ed5723-a2ff-4927-97e5-ad016198b82c" />



# OUTPUT: 

<img width="676" height="558" alt="image" src="https://github.com/user-attachments/assets/e05104df-db73-447a-946b-f1270549c1c0" />


# RESULT: 
Thus design of Chebyshev Low pass IIR filter waveforms were plotted and output was verified.
