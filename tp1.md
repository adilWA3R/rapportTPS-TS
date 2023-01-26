# rapportTP1-TS

clear all
close all
clc

%realiser par Adil El Idrissi


%declaration des variables 
    fe = 1e4;
    te = 1/fe;
    N  = 10000;
    t  = (0:N-1)*te; 
    x  = 1.2*cos(2*pi*440*t+1.2)+3*cos(2*pi*550*t)+0.6*cos(2*pi*2500*t);
    f = (0:N-1)*(fe/N);
    y = fft(x);

%spectre du signal x Transformé de Fourier
    plot (f, abs(y)
    legend("y=fft(x)");
    xlabel("f");
    ylabel("A");
    
    fshift = (-N/2:N/2-1)*(fe/N);
   % le fftshift permet de faire la transformé de fourier et de  centré à la fréquence zéro. 
    z = fftshift(x);
   %spectre d'amplitude  centré à la fréquence  zéro.
    plot(fshift,fftshift(2*abs(y)/N));
    legend("Spectre d'Amplitude centré en 0");
    xlabel("f");
    ylabel("A");
    
%bruit blanc gaussien au signal x
    bruit = 2*randn(size(x));
    xbruit = x+bruit;
    %transformé de fourier du signal bruité 
    ybruit = fft(xbruit);
    %spectre d'amplitude du signal bruité avec un bruit blanc gaussien de faible intensité
    plot(fshift,fftshift(2*abs(ybruit)/N))
    xlabel("f");
    ylabel("A");
    
% On ajoute un bruit avec une amplitude de 2 au signal originel 

    superbruit = 50*randn(size(x));
    xsuperbruit = x+superbruit;
    %transformé de fourier du signal bruité 
    ysuperbruit = fft(xsuperbruit);
     %spectre d'amplitude du signal bruité avec un bruit blanc gaussien de forte intensité
    plot(fshift,fftshift(2*abs(ysuperbruit)/N))

hold on

subplot(3,2,1) 
    plot(t,x,'.')
    legend("Signal x(t)")
    xlabel("t");
    ylabel("x(t)");
subplot(3,2,2) 
    plot(fshift,fftshift(2*abs(y)/N))
    legend("Spectre d'amplitude de x(t)")
    xlabel("f");
    ylabel("A");
subplot(3,2,3) 
    plot(t,xbruit,'.')
    legend("Signal x(t) bruité avec un bruit faible")
    xlabel("t");
    ylabel("x(t)");
subplot(3,2,4) 
    plot(fshift,fftshift(2*abs(ybruit)/N))
    legend("Spectre de x(t) bruité avec un bruit faible")
    xlabel("f");
    ylabel("A");
subplot(3,2,5) 
    plot(t,xsuperbruit,'.')
    legend("Signal x(t) bruité avec un bruit fort")
    xlabel("t");
    ylabel("x(t)");
subplot(3,2,6) 
     plot(fshift,fftshift(2*abs(ysuperbruit)/N))
      legend("Spectre de x(t) bruité avec un bruit fort")
      xlabel("f");
      ylabel("A");

      
  sound(x,fe)
  sound(xbruit,fe)
sound(xsuperbruit,fe)

![temp_freq](https://user-images.githubusercontent.com/105556070/214936045-7701fb7a-3ec0-4fad-beb2-cf2e0391e505.png)







clear all 
close all
clc
%réalisé par Adil El Idrissi

[x,fs] = audioread("bluewhale.au");

chant = x(2.45e4:3.10e4);
taille = length(chant);
ts = 1/fs;
t = (0:taille-1)*(10*ts);
fshift = (-taille/2:taille/2-1)*(fs/taille);

Chant2 = x(2e2:4.0229e4);
Taille = length(Chant2);
T = (0:Taille-1)*(10*ts);
fshift2 = (-Taille/2:Taille/2-1)*(fs/Taille);


%tansformation de fourier rapide sur le chant 
Schant = fft(chant);
%Densité spectrale du Chant
Densite_spectrale_chant = abs(Schant).^2/taille;


%transformation de fourier rapide sur le chant 
Schant2 = fft(Chant2);
%Densité spectrale du Chant lorsqu on a augementé la taille de l echantillon
Densite_spectrale_chant2 = abs(Schant2).^2/taille;





subplot(2,3,1)
sound(chant,fs);
plot(t,chant);
legend("representation du signal Chant");
xlabel("t");
ylabel("chant");

subplot(2,3,2)
plot(fshift,fftshift(2*abs(Schant)/taille));
legend("representation du spectre u signal Chant");
xlabel("Fréquence (Hz)");
ylabel("A");



subplot(2,3,3)
f = (0:floor(taille/2))*(fs/taille)/10;
plot(f,Densite_spectrale_chant(1:floor(taille/2)+1));
legend("Densité spectrale du chant");
xlabel("Fréquence (Hz)");
ylabel("Densité spectrale en puissance");


subplot(2,3,4)
sound(Chant2,fs);
plot(T,Chant2);
legend("representation du signal Chant 2");
xlabel("t");
ylabel("chant 2");

subplot(2,3,5)
plot(fshift2,fftshift(2*abs(Schant2)/Taille));
legend("representation du spectre en Amplitude du signal Chant 2");
xlabel("Fréquence (Hz)");
ylabel("A");


subplot(2,3,6)
f = (0:floor(Taille/2))*(fs/Taille)/10;
plot(f,Densite_spectrale_chant2(1:floor(Taille/2)+1));
legend("Densité spectrale du chant 2");
xlabel("Fréquence (Hz)");
ylabel("Densité spectrale en puissance");![blue whale](https://user-images.githubusercontent.com/105556070/214935622-6eac7a82-8cba-4b16-a224-54bfc7cf1cce.png)


