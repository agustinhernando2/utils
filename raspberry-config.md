# acceder a la raspi y X11 forwarding
ping raspberrypi.local
ssh -X agustin@192.168.100.120

# instalar tailscale, correrlo como nodo de salida y compartir subred, ver documentacion
sudo tailscale up --advertise-routes=192.168.100.0/24 --advertise-exit-node

# pi-hole
http://192.168.100.120/admin
contr:xxx

w para ver dispositivos conectados y carga
nproc numero de procesadores





