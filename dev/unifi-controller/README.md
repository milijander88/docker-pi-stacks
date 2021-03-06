# Unifi Controller

A few notes regarding the Unifi Controller.

- Set the network to "backend"

- You can keep all the ports commented out and tell Traefik to route to port 8443 in the label section.

    `- "traefik.port=8443"`

- The configuation must include this label:

    `- "traefik.protocol=https"` 
    
    This overrides the default http protocol. If you don't have that label you will be plagued with a "Bad Request" message, followed by "This combination of host and port requires TLS."

- Since the Unifi controller ships with its own self-signed certificate, you must include `"insecureSkipVerify = true"` at the global (top) level of the `traefik.toml` configuration file.

    `insecureSkipVerify`: If set to true invalid SSL certificates are accepted for backends. This disables detection of man-in-the-middle attacks so should only be used on secure backend networks.

- Once you launch the container, you should be able to go straight to `https://unifi.${FQDN}` to begin the initial setup. Once it's configured, go to `Settings --> Controller` and set `Controller Hostname/IP` to your fully qualified domain name (or the LAN IP address of the host system running the UniFi Controller).
