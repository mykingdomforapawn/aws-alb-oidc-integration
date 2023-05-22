# aws-alb-oidc-integration

> This project is part two of my software architecture journey. See my [software-architecture-journey](https://github.com/mykingdomforapawn/software-architecture-journey) repository for more details.

This simple AWS solution setup enables the OpenID Connect (OIDC) integration of an Application Load Balancer (ALB) with an Identity Provider (IdP) of your choice, outsourcing the user authentication from your application to the ALB.

---

## Table of contents:

- [Get started](#get-started)
- [Infrastructure diagram](#infrastructure-diagram)
- [References](#references)

---

## Get started

### Configure an OIDC client in the IdP
- Create a client with a set of credentials
- Configure one of the following redirect URIs in the IdP client
    - https://[ALB domain name]/oauth2/idpresponse
    - https://[ALB alias]/oauth2/idpresponse

### Register a domain name with Route 53
- The OIDC integration needs to have an HTTPS listener on the ALB, which requires you to get a certificate for a domain that you own
- Whereas the certificate registration is automated in the Cloudformation template, the domain registration has to be done manually
- You can follow https://aws.amazon.com/de/getting-started/hands-on/get-a-domain/

### Populate the Cloudforation template
- The OIDC parameters can usually be found at https://[IdP domain name]/.well-known/openid-configuration
- The ALB HTTPS listener parameters can be found in Route 53 after you registered a domain

### Create the Cloudformation stack
- Create the stack and lie back
- You can access the ALB via the registered domain name
- Have a look at the diagram below to get a better understanding about what is going on behind the scenes

---

## Infrastructure diagram

![Diagram](diagram.drawio.png)

---

## References
- https://docs.aws.amazon.com/elasticloadbalancing/latest/application/listener-authenticate-users.html#configure-user-authentication
- https://aws.amazon.com/de/getting-started/hands-on/get-a-domain/
