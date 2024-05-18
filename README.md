# Docker Security: Attacks and Mitigations

## Overview
This project, submitted for INSE 6130 Operating System Security at Concordia University, investigates various attack vectors and security measures in Docker environments. The report details the implementation of attacks on Docker containers and corresponding security applications to mitigate these threats.

## Part A - Implementation of Attacks on Docker
### 1. Attacking insecure volume mounts using 'docker socket'
Docker socket is used to communicate with the Docker daemon from within a container. By exploiting volume mounted docker.sock, attackers can gain privileges in the host system.
#### Execution:
1. Verify the presence of an RCE vulnerability in a Node.js application.
2. Exploit the RCE to insert a reverse shell payload.
3. Set up a listener using Netcat to intercept the reverse shell connection.
4. Use docker.sock to access host resources and control other containers.

### 2. Attacking container with 'sys_ptrace' capability
The `sys_ptrace` capability allows a container to monitor and control processes, posing security risks.
#### Execution:
1. Transfer the Metasploit reverse shell payload to the container.
2. Use netcat to connect back to the listener on the student VM.
3. Identify and target root processes on the host system.
4. Inject the payload to gain access to the host system.

### 3. Attacking host system security with 'dac_read_search' capability
The `dac_read_search` capability grants broad access to the filesystem, risking unauthorized access.
#### Execution:
1. Identify mounted files within the container.
2. Target SSH configuration files and keys.
3. Create a new user with root-level access.
4. Use the new credentials to SSH into the host system.

### 4. Corrupting Docker Source Image
By modifying a Docker image, attackers can inject a web shell to gain remote control.
#### Execution:
1. Use curl to interact with the Docker registry.
2. Modify the WordPress image to include a web shell.
3. Create and push the backdoored image to a private registry.
4. Interact with the web shell using curl.

### 5. Misconfigured Docker Socket
Exploiting Docker daemon misconfiguration to interact with the Docker API and compromise functions.
#### Execution:
1. Check for Docker daemon on port 2375.
2. Use curl to confirm connectivity.
3. Set Docker client to use TCP socket.
4. List Docker images and launch a container with host filesystem mount.
5. Gain root access using `chroot`.

## Part B - Implementation of Security Applications
### 1. Cgroups
Cgroups regulate resource consumption to ensure scalability and prevent denial-of-service attacks.
#### Implementation:
1. Set limits on the number of processes and CPU/memory usage within containers.

### 2. Capabilities
Capabilities provide fine-grained control over processes by granting only necessary privileges.
#### Implementation:
1. Drop unnecessary privileges such as `CHOWN` to enhance security.

### 3. Apparmor - Attack and Defence against Privilege Escalation using Disk Mount
Apparmor profiles restrict user access to programs and files, preventing privilege escalation.
#### Implementation:
1. Configure Apparmor profiles to prevent unauthorized disk mounts.

### 4. Seccomp Profile
Seccomp profiles restrict system calls to reduce the attack surface.
#### Implementation:
1. Define and apply seccomp profiles to Docker containers.
2. Monitor and adjust profiles to ensure necessary system calls are allowed.

## Challenges
While working on Docker security, we faced challenges such as replicating specific attacks, obtaining vulnerable Docker images, and troubleshooting. Despite these obstacles, we successfully implemented the project, maintaining robust security practices.

## Authors
- Avin Vincent (Attack Using ‘docker socket’)
- Likitha T Reddy (Attack Using ‘sys_ptrace’)
- Challa Likitha (Attack By injecting “Web Shell”)
- Chinnabathini Hima Bindu (Attack Using ‘dac_read_search’)
- Moksh Sood (Attack Using unprotected TCP socket)
- Divya Varshini Murathoti (Security Using Cgroups and Capabilities)
- Kunati Bala Krishna Yadav (Attack & Security Using Disk Mount)
- Yash Khosla (Security Using “Seccomp security”)



For more detailed information, please refer to the [full report](./INSE_6130_ProjectReport.docx.pdf)., the implementation of attacks and the working demo. 
