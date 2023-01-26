# rapportTPS-TS




%Réalisé par Adil El Idrissi

m_Fs=8192;
Ts=1/m_Fs;
t=[0:Ts:1];
F_A=440; 
F_dol=262;
F_re=294;
F_m=330;
F_fa=349;
F_sol=392;
F_si=494;
F_do2=523;
A=sin(2*pi*F_A*t);
Dol=sin(2*pi*F_dol*t);
re=sin(2*pi*F_re*t);
mi=sin(2*pi*F_m*t);
fa=sin(2*pi*F_fa*t);
so=sin(2*pi*F_sol*t);
la=sin(2*pi*F_A*t);
si=sin(2*pi*F_si*t);
do=sin(2*pi*F_do2*t);

doremifasol_solfamiredo= [Dol,re,mi,fa,so,la,si,do,do,si,la,so,fa,mi,re,Dol];
faded =[fa,fa,fa,si,mi,mi,re,si,si,si,si,fa,fa,fa,mi];
sound(doremifasol_solfamiredo,m_Fs);
