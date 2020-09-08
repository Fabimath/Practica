# Practica
Puedes ver mis avances en el informe de practica en el siguiente [enlace](main.pdf)

Además el overleaf de trabajo se encuentra aquí [enlace](https://www.overleaf.com/9226984625zkchnzwjnkcr)

Otro papaer lo puedes encontrar [aquí](semana2/paper.pdf)

Un paper mas sobre esferas [aquí](https://arxiv.org/pdf/1111.7077.pdf)

## Simulación en esferas

Con las siguientes lineas de código se genera una simulación en una esfera.

![wo](semana3/esferasimulada.ipynb)
~~~
library("plot3D")
library("gsl")

nlon = 600;    # number of longitude points
nlat = 600;    # number of latitude points

phi = seq(0,2*pi,length=nlon);
theta = seq(0,pi,length=nlat);

coord = expand.grid(phi,theta);  
x = sin(coord[,2])*cos(coord[,1]);
y = sin(coord[,2])*sin(coord[,1]);
z = cos(coord[,2]);
num = length(x);
print(num);  

Ntrunc = 50;     # Number of terms in the expansion
suma = array(dim=c(num,1),0);
for(n in 0:Ntrunc){
 
  bn = 1/(n^2+0.1);  #power spectrum
  print(n)
  fact = sqrt(bn) ; 

  suma  <-  suma  +  fact*rnorm(1,0,1)*legendre_sphPlm(n,0,cos(coord[,2]))  ;
  
     if(n>0){
        for(j in 1:n){
           ynm = legendre_sphPlm(n,j,cos(coord[,2])) * ( rnorm(1,0,sd=1) * cos(j*coord[,1]) +
                                                         rnorm(1,0,sd=1) * sin(j*coord[,1])  );
           suma <- suma +  fact*sqrt(2)* ynm;
        }
     }
}

svg("esfera.svg")
scatter3D(x,y,z,colvar=suma,theta=0,phi=0,box=F);  # realization plot
dev.off()
~~~

Generando la siguiente simulación.

![sim1](semana3/esfera.svd)

[Volver al inicio](https://fabimath.github.io/Fabimath/)
