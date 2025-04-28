A Homelab Guide
==
This guide serves to offer many different tutorials for many different services

[[Docker]]
==
Docker is a service that allows you to easily run other services.  It offers an easy way to install the service and throw it away when it is no longer needed.

[[Dashy]]
==
Dashy is a self hosted webpage that can be used to link to other services' webpages.  It also offers a built-in way to add icons to easily identify the services.

[[HomeAssistant]]
==
Home Assistant is a home automation and management service.

[[NTFY]]
==
NTFY is a notification service that can be accessed through the command line.  This enables it to be called from automation scripts.

[[NUT]]
==
NUT (Network UPS Tool) is a monitoring software that monitors a UPS to dectect power outages.  It is also able to start shutdown scripts on other servers if the battery in the UPS gets below a certain level in order to prevent data loss.

[[PiHole]]
==
PiHole is a DNS server that blackholes known ad domains so that they are unable to load on any device on the network without having to install another application on each device.  Additionally, you can add known malicious domains so that if a device on the network is compromised, it might not be able to find it's control server.

[[Portainer]]
==
Portainer is a manager for Docker that allows you to monitor containers, easily view logs, and easily access a command line into each container.

[[Traefik]]
==
Traefik is a reverse proxy.  This allows it to offer a specific webpage to your other services so that you don't need to specify a port in the url for each service.  It also is able to generate SSL certificates for each webpage so that you don't get the annoying web-browser warning about 'a self signed certificate in chain'

[[Uptime Kuma]]
==
Uptime Kuma is a network monitoring tool.  It is able to monitor DNS, HTTP, PING, as well as many other service specific monitors.  It can also be integrated with NTFY to notify you if a service is down.

[[VMWare ESXi]]
==
ESXi is an operating system from VMWare that offers the ability to run other operating systems on one server.  This allows you to essentially have multiple computers on one computer and those other computers don't even realize that they aren't real.