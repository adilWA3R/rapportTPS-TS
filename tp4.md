# rapportTPS-TS

clear all
close all
clc


fe = 1/Te;
N = length(t);

fshift = (-N/2:N/2-1)*(fe/N);
f = (0:N-1)*(fe/N);
f1 = 500;
f2 = 400;
f3 = 50;
t = 0:Te:5-Te;
Te = 5*1e-4;
x = sin(2*pi*f1*t)+sin(2*f2*pi*t)+sin(2*pi*f3*t);
y = fft(x);
figure(1);
subplot(3,3,1)
plot(t,x)
legend(" Signal x avec T = 0.001");
xlabel("t");
 ylabel("x(t)");

subplot(3,3,2)
plot(fshift, fftshift(abs(y)));
legend(" Spectre du signal x avec T = 0.001");
xlabel("f");
ylabel("A");
subplot(3,3,3)
Tee = 0.0005 ;
fe2 = 1/Tee;
t2 = 0:Tee:5-Tee;
N2 = length(t2);

fshift2 = (-N2/2:(N2/2-1))*(fe2/N2);
x2 = sin(2*pi*f1*t2)+sin(2*f2*pi*t2)+sin(2*pi*f3*t2);
y2 = fft(x2);

plot(t2,x2);
legend(" Signal x avec T =0.0005");
xlabel("t");
ylabel("x(t)");

subplot(3,3,4)
plot(fshift2,fftshift(abs(y2)));
legend(" Spectre du signal x avec T =0.0005");
xlabel("f");
ylabel("A");

%% Partie de la transmittance complexe
%  tracé du module de H(f)
k = 1;
wc = 50;

h = (k*1j*((2*pi*f)/wc))./(1+1j*((2*pi*f)/wc));

figure(2);
semilogx(abs(h))
plot(abs(h))
legend("Module de h(f)")

wc2 = 500;
wc3 = 1000;

h1 = (k*1j*((2*pi*f)/wc2))./(1+1j*((2*pi*f)/wc2));
h2 = (k*1j*((2*pi*f)/wc3))./(1+1j*((2*pi*f)/wc3));

G = 20*log(abs(h));
G1 = 20*log(abs(h1));
G2 = 20*log(abs(h2));

P = angle(h);
P1 = angle(h1);
P2 = angle(h2);

figure(3);
subplot(3,1,1)
semilogx(f,G,f,G1,f,G2);
title("Diagramme de Bode")
xlabel("rad/s")
ylabel("decibel")
legend("G : wc=50","G1 : wc=500","G2 : wc=1000")

subplot(3,1,2)
semilogx(f,P,f,P1,f,P2)
legend("G : wc=50","G1 : wc=500","G2 : wc=1000")







%% Transmitance Complexe
   
    H = (K*1i*w/wc)./(1+1i*w/wc);
    G = 20*log(abs(H));
    Ang = angle(H);
    
   
    wc1=2*pi*500;
    H1 = (K*1i*w/wc1)./(1+1i*w/wc1);
    G1 = 20*log(abs(H1));
    Ang1 = angle(H1);
    
    wc2=2*pi*1000;
    H2 = (K*1i*w/wc2)./(1+1i*w/wc2);
    G2 = 20*log(abs(H2));
    Ang2 = angle(H2);
    
    wc3=2*pi*150;
    H3 = (K*1i*w/wc3)./(1+1i*w/wc3);
    G3 = 20*log(abs(H3));
    Ang3 = angle(H3);
    
    %representation des spectres leur Gain et le dephasage et spectre filtrer
   
       figure(4);
      semilogx(f,abs(H),f,abs(H1),f,abs(H2),f,abs(H3));
     legend("spectre du signal avec wc=50","spectre du signal avec wc1=2*pi*500"," spectre du signal avec wc2=2*pi*1000","spectre du signal avec wc3=2*pi*50");  
      grid on
     figure(5);
      semilogx(f,G,f,G1,f,G2,f,G3);
     legend("Courbe de Gain  wc=50","Courbe de Gain wc1=2*pi*500","Courbe de Gain wc2=2*pi*1000","Courbe de Gain wc3=2*pi*50");  
      grid on
    figure(6);
    subplot(3,3,3);
    semilogx(f,Ang,f,Ang1,f,Ang2,f,Ang3);
        grid on
        legend("Courbe de dephasage wc=50","Courbe de dephasage wc1=2*pi*500","Courbe de dephasage wc2=2*pi*1000","Courbe de dephasage wc3=2*pi*50"); 
    
     subplot(3,3,4);
        Hpass=[H1(1:floor(N/2)),flip(H1(1:floor(N/2)))];
        filter_freq = y .* Hpass;
        filter_temp = ifft(filter_freq,"symmetric");
    
       plot(fshift,fftshift(2*abs(fft(filter_temp)/N)));
       legend("spectre de phase apres filtrage avec H1 fc=500");
legend("Signal non filtré","Signal filtré")
