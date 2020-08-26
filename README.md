# Practica
Puedes ver mis avances en el informe de practica en el siguiente [enlace](main.pdf)

Además el overleaf de trabajo se encuentra aquí [enlace](https://www.overleaf.com/9226984625zkchnzwjnkcr)

Otro papaer lo puedes encontrar [aquí](semana2/paper.pdf)
## Simulación en esferas

Con las siguientes lineas de código se genera una simulación en una esfera.

~~~
library("plot3D")

grid_size = 100;

eps = 0.01;
theta = seq(0+eps,pi-eps,l=grid_size);
phi = seq(0,2*pi-eps,l=grid_size);
coord = expand.grid(phi,theta);
x = sin(coord[,2])*cos(coord[,1]);
y = sin(coord[,2])*sin(coord[,1]);
z = cos(coord[,2]);
nsites = length(x);
val = 0.99999999999;
escala = 1;
mat = array(dim=c(nsites,nsites));

cova <- function(escala,geod){
  res = exp(-3*geod/escala);
  return(res)    
}

for(i in 1:nsites){
  for(j in 1:nsites){
    prod = x[i]*x[j]+y[i]*y[j]+z[i]*z[j];
    if(prod > val){dij = 0;}
    if(prod < -val){dij = pi;}
    if(prod <= val & prod >= -val){dij = acos(prod);}
    mat[i,j] = cova(escala,dij);          
  }
}

set.seed(0)
datos = t(chol(mat))%*%rnorm(nsites);

scatter3D(x,y,z,colvar=datos)
~~~

Generando la siguiente simulación.

![sim1](simulacion/sim1.pdf)

[Volver al inicio](https://fabimath.github.io/Fabimath/)
