Marvin Valerio- SETechAssessment- Senior Customer Solutions Engineer

Who am I?
I am passionate about cybersecurity and the world of technology. I am constantly eager to learn and stay prepared for what the world needs and demands, which I believe is crucial in this ever-changing technological landscape. With over 7 years of experience working for IBM in IBM Security Services, I have been instrumental in establishing successful relationships with important clients for the organization. Above all, I am a professional filled with passion to help and work as a team towards our clients' goals.
I started in a junior position as a Security Analyst and was promoted to a more senior role with customer-facing responsibilities. I then transitioned to become a Security Consultant and currently hold one of the most senior positions in Costa Rica, serving as the local leader of the Security Solutions Architects team. I am dedicated to my clients and teams, always willing to dig deep. As evidence of this, I successfully patented an invention with IBM last year for a security product (https://www.credly.com/badges/d5a69ade-f1f1-4023-9b96-8c0c00ddf6b0/public_url).
Why am I considering Sysdig as an opportunity despite being content in my current company? Firstly, I genuinely love Sysdig's products. I have practical knowledge in Falco, and much of my work as a Security Consultant involved deploying and integrating security products such as AWS GuardDuty, which is a threat detection system similar to Falco, GuardDuty  monitored AWS services like EKS and ECS I worked in SIEMs like QRadar and Splunk, like Resilient, IPS/IDS, and security suites to provide clients with the ROI they expect. Adapting and fine-tuning these tools to meet each client's environment and needs was crucial in demonstrating the value of the product.
Falco is very similar, and I have extensive knowledge ranging from its architecture to fine-tuning the rules, which I handle perfectly. I read the book "Practical Cloud Native Security" (https://learning.oreilly.com/library/view/practical-cloud-native/9781098118563/), which I found incredibly valuable and it helped me get started with Falco some time ago.
In general, I am passionate about all things related to security, and I am particularly excited about Kubernetes, Cloud Native environments, and how to secure them. Please note that I was on vacation this week, as it is the only vacation time I have with my son this year, so I had limited time. However, I hope that my responses and solutions demonstrate my passion for Sysdig's products, my overall knowledge in this field, and at the end, you will find an additional task I specifically worked on in Falco, where I have significant experience.
Thank you for taking the time to read this. I know that Sysdig employs highly intelligent individuals with a team-oriented culture, where everyone's skills complement each other. I believe I can contribute positively to the team with my skills. If you have any further questions, please let me know.
I hold several certifications, including some of the most senior ones in the security field, such as CISSP, CEH, IBM Cloud Security Engineer, AWS Security Specialist, Cloud Security Knowledge (CCSK), IBM Security Architect, IBM DevSecOps Specialty, among others. I understand that certifications alone do not determine whether someone is a good professional or not. However, they demonstrate my commitment to continuous growth and learning every day. Along with being an ethical professional and a team player, this mindset has helped me in my career.
https://www.linkedin.com/in/marvin-valerio-209690153/

Note:I set up this environment from scratch solely for evaluation purposes, so I didn't follow the principles of least privilege or implement standard security best practices as I would normally do. However, I did this to assess the value of the products and how they detect these behaviors. For example doinf this in the way I did, we can observe that we are not in compliance with SOC 2 and how alerts are generated for unauthorized root access without MFA, etc. This allows us to evaluate the value of Sysdig Secure, Monitor, and Falco. All information, credentials, etc., have already been purged to ensure that they are not exposed in this public repository.

TASKS:
1.Create Kubernetes cluster - Do this however you want (EKS, GKE, AKS, IKS, OKE, KOPS, OCP, Rancher, whatever! Lots of free 'credit' options out there.) 
Cluster Creation with eksctl

In this project, I opted to create a cluster using eksctl, a user-friendly and efficient tool. eksctl simplifies the cluster creation process by leveraging IaC (Infrastructure as Code) CloudFormation. With just a single command, I was able to create a fully functioning cluster, complete with two active nodes specifically for this assessment.
Requirements

Before proceeding with the cluster creation, ensure that the following prerequisites are met:

    IAM User
    AWS CLI
    AWS Access Key and Secret Key
    eksctl Installation.
    kubectl 
    I used homebrew, yes I know it is not a requirement bu Homebrew is indeed a helpful package manager, and it can greatly simplify the process of installing and managing software on macOS. Using Homebrew for installing eksctl and creating your EKS cluster is a convenient approach. It allows you to easily install eksctl with a single command and ensures that you have the necessary dependencies and versions required for your cluster.
AWS CLI configuration:
Config file
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/f2d15307-7a7d-498e-9bb0-180aa94bdcbf)
Credentials file: keys are not completed here just for security considerations?
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/09d48164-e065-4d89-a009-4fbc0a73bd48)
Command used after installed and met all requirements:
eksctl create cluster \
--name test-cluster-sysdig \
--region us-east-1 \
--nodegroup-name linux-nodes \
--node-type t2.micro \
--nodes 2
Results:
arvin@marvin-virtual-machine:~$ eksctl create cluster \
> --name test-cluster-sysdig \
> --region us-east-1 \
> --nodegroup-name linux-nodes \
> --node-type t2.micro \
> --nodes 2
2023-07-11 23:13:00 [ℹ]  eksctl version 0.148.0
2023-07-11 23:13:00 [ℹ]  using region us-east-1
2023-07-11 23:13:01 [ℹ]  setting availability zones to [us-east-1d us-east-1b]
2023-07-11 23:13:01 [ℹ]  subnets for us-east-1d - public:192.168.0.0/19 private:192.168.64.0/19
2023-07-11 23:13:01 [ℹ]  subnets for us-east-1b - public:192.168.32.0/19 private:192.168.96.0/19
2023-07-11 23:13:01 [ℹ]  nodegroup "linux-nodes" will use "" [AmazonLinux2/1.25]
2023-07-11 23:13:01 [ℹ]  using Kubernetes version 1.25
2023-07-11 23:13:01 [ℹ]  creating EKS cluster "test-cluster-sysdig" in "us-east-1" region with managed nodes
2023-07-11 23:13:01 [ℹ]  will create 2 separate CloudFormation stacks for cluster itself and the initial managed nodegroup
2023-07-11 23:13:01 [ℹ]  if you encounter any issues, check CloudFormation console or try 'eksctl utils describe-stacks --region=us-east-1 --cluster=test-cluster-sysdig'
2023-07-11 23:13:01 [ℹ]  Kubernetes API endpoint access will use default of {publicAccess=true, privateAccess=false} for cluster "test-cluster-sysdig" in "us-east-1"
2023-07-11 23:13:01 [ℹ]  CloudWatch logging will not be enabled for cluster "test-cluster-sysdig" in "us-east-1"
2023-07-11 23:13:01 [ℹ]  you can enable it with 'eksctl utils update-cluster-logging --enable-types={SPECIFY-YOUR-LOG-TYPES-HERE (e.g. all)} --region=us-east-1 --cluster=test-cluster-sysdig'
2023-07-11 23:13:01 [ℹ]  
2 sequential tasks: { create cluster control plane "test-cluster-sysdig", 
    2 sequential sub-tasks: { 
        wait for control plane to become ready,
        create managed nodegroup "linux-nodes",
    } 
}
2023-07-11 23:13:01 [ℹ]  building cluster stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:13:03 [ℹ]  deploying stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:13:33 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:14:03 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:15:04 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:16:05 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:19:27 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:20:28 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:21:28 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:22:29 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:23:29 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-cluster"
2023-07-11 23:25:35 [ℹ]  building managed nodegroup stack "eksctl-test-cluster-sysdig-nodegroup-linux-nodes"
2023-07-11 23:25:36 [ℹ]  deploying stack "eksctl-test-cluster-sysdig-nodegroup-linux-nodes"
2023-07-11 23:25:36 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-nodegroup-linux-nodes"
2023-07-11 23:26:07 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-nodegroup-linux-nodes"
2023-07-11 23:26:46 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-nodegroup-linux-nodes"
2023-07-11 23:28:36 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-nodegroup-linux-nodes"
2023-07-11 23:29:34 [ℹ]  waiting for CloudFormation stack "eksctl-test-cluster-sysdig-nodegroup-linux-nodes"
2023-07-11 23:29:34 [ℹ]  waiting for the control plane to become ready
2023-07-11 23:29:40 [✔]  saved kubeconfig as "/home/marvin/.kube/config"
2023-07-11 23:29:40 [ℹ]  no tasks
2023-07-11 23:29:40 [✔]  all EKS cluster resources for "test-cluster-sysdig" have been created
2023-07-11 23:29:40 [ℹ]  nodegroup "linux-nodes" has 2 node(s)
2023-07-11 23:29:40 [ℹ]  node "ip-192-168-20-182.ec2.internal" is ready
2023-07-11 23:29:40 [ℹ]  node "ip-192-168-59-191.ec2.internal" is ready
2023-07-11 23:29:40 [ℹ]  waiting for at least 2 node(s) to become ready in "linux-nodes"
2023-07-11 23:29:40 [ℹ]  nodegroup "linux-nodes" has 2 node(s)
2023-07-11 23:29:40 [ℹ]  node "ip-192-168-20-182.ec2.internal" is ready
2023-07-11 23:29:40 [ℹ]  node "ip-192-168-59-191.ec2.internal" is ready
2023-07-11 23:29:40 [✖]  kubectl not found, v1.10.0 or newer is required
2023-07-11 23:29:40 [ℹ]  cluster should be functional despite missing (or misconfigured) client binaries
2023-07-11 23:29:40 [✔]  EKS cluster "test-cluster-sysdig" in "us-east-1" region is ready
marvin@marvin-virtual-machine:~$ kubectl version
Command 'kubectl' not found, but can be installed with:
sudo snap install kubectl
marvin@marvin-virtual-machine:~$ curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   138  100   138    0     0    307      0 --:--:-- --:--:-- --:--:--   308
100 46.9M  100 46.9M    0     0  2637k      0  0:00:18  0:00:18 --:--:-- 3247k
marvin@marvin-virtual-machine:~$ sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
[sudo] password for marvin: 
marvin@marvin-virtual-machine:~$ kubectl version --client
WARNING: This version information is deprecated and will be replaced with the output from kubectl version --short.  Use --output=yaml|json to get the full version.
Client Version: version.Info{Major:"1", Minor:"27", GitVersion:"v1.27.3", GitCommit:"25b4e43193bcda6c7328a6d147b1fb73a33f1598", GitTreeState:"clean", BuildDate:"2023-06-14T09:53:42Z", GoVersion:"go1.20.5", Compiler:"gc", Platform:"linux/amd64"}
Kustomize Version: v5.0.1
marvin@marvin-virtual-machine:~$ kubectl version --short --client
Flag --short has been deprecated, and will be removed in the future. The --short output will become the default.
Client Version: v1.27.3
Kustomize Version: v5.0.1
marvin@marvin-virtual-machine:~$ kubectl version --short --client
Flag --short has been deprecated, and will be removed in the future. The --short output will become the default.
Client Version: v1.27.3
Kustomize Version: v5.0.1
marvin@marvin-virtual-machine:~$ kubectl get nodes
NAME                             STATUS   ROLES    AGE   VERSION
ip-192-168-20-182.ec2.internal   Ready    <none>   11m   v1.25.9-eks-0a21954
ip-192-168-59-191.ec2.internal   Ready    <none>   11m   v1.25.9-eks-0a21954
marvin@marvin-virtual-machine:~$ kubectl get ns
NAME              STATUS   AGE
default           Active   20m
kube-node-lease   Active   20m
kube-public       Active   20m
kube-system       Active   20m



2. Signup for a Sysdig Trial, make sure you Select All features when signing up (https://sysdig.com/start-free/)

I have signed up, and this is my customer ID just to confirm that I have subscribed.
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/3c9dae5a-601a-427e-bf34-dc8e3504394d)


3. Install the Sysdig Agent(s) to your Kubernetes cluster. 
The Kubernetes Sysdig Agent is installed and deployed on one of the nodes (ip-192-168-20-182.ec2.internal) in my EKS cluster. I installed it using the Wizard and Helm charts.


marvin@marvin-virtual-machine:~$ helm repo add sysdig https://charts.sysdig.com
helm repo update
helm install sysdig-agent --namespace sysdig-agent --create-namespace \
    --set global.sysdig.accessKey=342fb2e5-d51f-4635-931c-a155cb8c6b9c \
    --set global.sysdig.region=us4 \
    --set nodeAnalyzer.secure.vulnerabilityManagement.newEngineOnly=true \
    --set global.kspm.deploy=true \
    --set nodeAnalyzer.nodeAnalyzer.benchmarkRunner.deploy=false \
    --set global.clusterConfig.name=test-cluster-sysdig \
    sysdig/sysdig-deploy
"sysdig" already exists with the same configuration, skipping
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "sysdig" chart repository
Update Complete. ⎈Happy Helming!⎈
NAME: sysdig-agent
LAST DEPLOYED: Wed Jul 12 13:25:25 2023
NAMESPACE: sysdig-agent
STATUS: deployed
REVISION: 1
NOTES:
The agent for Sysdig Secure DevOps Platform is spinning up on each node in your
cluster. After a few seconds, you should see your hosts appearing in the
Sysdig Agent Health & Status Dashboard.

Links for your deployment:
  * Sysdig Monitor: https://app.us4.sysdig.com/#/dashboard-template/view.sysdig.agents?last=10
  * Sysdig Secure: https://app.us4.sysdig.com/secure/#/data-sources/agents
    

Pod Security Admission now replaces Pod Security Policies.
Be aware that if you enforce "baseline" or "restricted" policies in your cluster, you need to enforce "privileged" policy to this namespace:
    kubectl label --overwrite ns <sysdig-namespace> pod-security.kubernetes.io/enforce=privileged
Otherwise you're ok to go.
marvin@marvin-virtual-machine:~$ kubectl get deployments --all-namespaces
NAMESPACE      NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
kube-system    coredns                      2/2     2            2           14h
sysdig-agent   sysdig-agent-kspmcollector   1/1     1            1           2m7s
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/5c7c4c85-66e7-40ef-b541-0a963fe5a725)
As an extra point, I associated my AWS account with sysdig secure and monitor, where I had all my configuration. Additionally, I performed a Git integration with the provided application in the Voting-Appproject. Finally, I installed an agent on my Linux host.
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/40b5f82d-6b64-4bd6-aa62-968d25a0bf8a)
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/73abbbcf-4109-4f33-a374-007298f5dddd)
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/0d5f6466-1875-4834-bdcf-cdf597b1d2af)



4. Install the classic voting app into your K8s cluster (https://github.com/dockersamples/example-voting-app)

   Clone the repo to your github:
In this repository, https://github.com/mavaleri18/SYSDIG-TECH-ASSESMENT-APPS2, you can find where I cloned the app.

          marvin@marvin-virtual-machine:~/$ git pull origin main
       marvin@marvin-virtual-machine:~/$ git branch -r
marvin@marvin-virtual-machine:~$ git clone https://github.com/dockersamples/example-voting-app.git
Cloning into 'example-voting-app'...
remote: Enumerating objects: 1088, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 1088 (delta 0), reused 1 (delta 0), pack-reused 1084
Receiving objects: 100% (1088/1088), 1.16 MiB | 1.94 MiB/s, done.
Resolving deltas: 100% (409/409), done.
marvin@marvin-virtual-machine:~$ cd example-voting-app
marvin@marvin-virtual-machine:~/example-voting-app$ git remote add my-repo https://github.com/mavaleri18/SYSDIG-TECH-ASSESMENT-APPS2
marvin@marvin-virtual-machine:~/example-voting-app$ git push my-repo main
Enumerating objects: 1084, done.
Counting objects: 100% (1084/1084), done.
Delta compression using up to 4 threads
Compressing objects: 100% (616/616), done.
Writing objects: 100% (1084/1084), 1.14 MiB | 1.64 MiB/s, done.
Total 1084 (delta 409), reused 1084 (delta 409), pack-reused 0
remote: Resolving deltas: 100% (409/409), done.
To https://github.com/mavaleri18/SYSDIG-TECH-ASSESMENT-APPS2
 * [new branch]      main -> main

   Expose the app so you can browse to the UI and see it working:
   ![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/45660a64-39ae-47b9-8f36-31ac7fc8e0c6)

    ![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/9337555b-3b04-4697-98bd-aa0a742cdf51)

   ![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/187d1ce1-afbe-4008-8da5-a46d918fc2ea)


marvin@marvin-virtual-machine:~$ git clone https://github.com/mavaleri18/SYSDIG-TECH-ASSESMENT-APPS2
Cloning into 'SYSDIG-TECH-ASSESMENT-APPS2'...
remote: Enumerating objects: 1084, done.
remote: Counting objects: 100% (1084/1084), done.
remote: Compressing objects: 100% (616/616), done.
remote: Total 1084 (delta 409), reused 1084 (delta 409), pack-reused 0
Receiving objects: 100% (1084/1084), 1.14 MiB | 2.72 MiB/s, done.
Resolving deltas: 100% (409/409), done.
arvin@marvin-virtual-machine:~$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:6443
CoreDNS is running at https://127.0.0.1:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://127.0.0.1:6443/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
marvin@marvin-virtual-machine:~$ kubectl get nodes
NAME                   STATUS   ROLES                  AGE     VERSION
lima-rancher-desktop   Ready    control-plane,master   4h32m   v1.27.3+k3s1
marvin@marvin-virtual-machine:~$ cd SYSDIG-TECH-ASSESMENT-APPS2/
marvin@marvin-virtual-machine:~/SYSDIG-TECH-ASSESMENT-APPS2$ kubectl create -f k8s-specifications/
deployment.apps/db created
service/db created
deployment.apps/redis created
service/redis created
deployment.apps/result created
service/result created
deployment.apps/vote created
service/vote created
deployment.apps/worker created
marvin@marvin-virtual-machine:~/SYSDIG-TECH-ASSESMENT-APPS2$ kubectl get nodes
NAME                   STATUS   ROLES                  AGE     VERSION
lima-rancher-desktop   Ready    control-plane,master   4h34m   v1.27.3+k3s1
marvin@marvin-virtual-machine:~/SYSDIG-TECH-ASSESMENT-APPS2$ cd ~
marvin@marvin-virtual-machine:~$ kubectl get namespaces
NAME              STATUS   AGE
kube-system       Active   4h35m
default           Active   4h35m
kube-public       Active   4h35m
kube-node-lease   Active   4h35m
marvin@marvin-virtual-machine:~$ kubectl get pods -n default
NAME                      READY   STATUS    RESTARTS   AGE
redis-66949686f7-dgl5q    1/1     Running   0          4m9s
db-7fc468458-vncsm        1/1     Running   0          4m9s
worker-6fc5d5b668-fk7sv   1/1     Running   0          4m8s
result-6b9bc65689-7fp2z   1/1     Running   0          4m9s
vote-69dc45b49c-tv9qd     1/1     Running   0          4m8s



SYSDIG SECURE:
I want to emphasize that I created this deployment from scratch, and much of what I configured was intentionally done to create an insecure environment that does not follow security principles such as least privilege, etc. Additionally, I generated suspicious behaviors through commands to trigger alerts based on Falco rules. 

For example, you can see that 4 rules were triggered, matching 5 different tactics from the MITRE ATT&CK Framework. As I mentioned, based on the poor security configuration of the environment, one of the events that triggered an alert was "Console Root Login Without MFA." This goes against best practices in strong authentication, violates SOC2 requirements, and is, of course, a misconfiguration that should be addressed if receiving a real alert of this nature.
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/7c591892-f274-4043-be99-35f4fbf71ac6)
SYSDIG MONITOR:
In Sysdig Monitor, I would like to show you for now 2 things. First, by associating my AWS account, I can view metrics from my different services. Second, by running PromQL queries, I can perform granular queries and see exactly what I need.
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/a457b2f9-badc-41eb-8822-fefce678b409)
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/bb741318-1c56-474d-8c19-a0a596c287dd)

FALCO:
BONUS POINTS: I worked on a special task to demonstrate my knowledge in Falco. Essentially, I installed Falco on my machine and set up the connection with Falcosidekick UI. After that, I generated malicious activity using the event-generator. Finally, I performed a basic tuning by disabling a Falco rule.

In the Falco UI, I performed a search for alerts generated by the "Write below root" rule, which is associated with the use of the persistence tactic. When a rule like "Write below root" is triggered, it suggests that there is an attempt to modify or tamper with system rules in order to establish persistence. This behavior can involve altering the functionality of existing rules or introducing new rules that enable unauthorized access or control over the compromised system. Attackers often employ these techniques to maintain their presence within the targeted environment and ensure long-term persistence. By monitoring and investigating alerts related to this rule, it becomes possible to detect and respond to potential threats, helping to protect the integrity and security of the system.
It is important to emphasize that tuning these rules is key to providing the real value of Falco. Editing macros, managing lists, and adding exceptions will be crucial to prevent rules from triggering false positives. As in the example above, if such activity is performed by an admin that is expected to performe that task, adding that user to an exception list would be the best approach to avoid unnecessary noise.
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/0962dab4-1f62-48ce-84fb-3fc26714e03c)

Editing rule:
Enable:
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/70a879df-3187-43c7-8edc-23627644fd86)
Disabled:


![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/99e0ec05-0520-4753-b55b-f456b058eed7)

CLI Probe it was configured by me:
root@marvin-virtual-machine:/home/marvin# sudo systemctl status  falco
● falco-kmod.service - Falco: Container Native Runtime Security with kmod
     Loaded: loaded (/lib/systemd/system/falco-kmod.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2023-07-14 11:39:10 CST; 42min ago
       Docs: https://falco.org/docs/
   Main PID: 9112 (falco)
      Tasks: 9 (limit: 4600)
     Memory: 22.3M
        CPU: 30.386s
     CGroup: /system.slice/falco-kmod.service
             └─9112 /usr/bin/falco --pidfile=/var/run/falco.pid

jul 14 12:19:54 marvin-virtual-machine falco[9112]: {"hostname":"marvin-virtual-machine","output":"12:19:54.119785470: Error File below known binary directory renamed/removed (user=root user_loginuid=-1>
jul 14 12:19:54 marvin-virtual-machine falco[9112]: {"hostname":"marvin-virtual-machine","output":"12:19:54.120038674: Error File below known binary directory renamed/removed (user=root user_loginuid=-1>
jul 14 12:19:54 marvin-virtual-machine falco[9112]: {"hostname":"marvin-virtual-machine","output":"12:19:54.222125929: Error File below a known binary directory opened for writing (user=root user_loginu>
lines 1-21/21 (END)
root@marvin-virtual-machine:/home/marvin# sudo docker run -it --rm falcosecurity/event-generator run syscall --loop
WARN action not enabled                            action=syscall.ScheduleCronJobs
INFO sleep for 100ms                               action=syscall.SystemUserInteractive
INFO run command as another user                   action=syscall.SystemUserInteractive cmdArgs="[]" cmdName=/bin/login user=daemon
INFO sleep for 100ms                               action=syscall.ReadSensitiveFileUntrusted
INFO action executed                               action=syscall.ReadSensitiveFileUntrusted
INFO sleep for 100ms                               action=syscall.SystemProcsNetworkActiv



Feedback?
I really enjoyed the experience of working on this project. I know that I could have added a little more to it in general, but unfortunately, I received the evaluation this week, which coincided with my son's week and our planned vacation week when we were supposed to be away from home. Despite the time constraints and the fact that I would have liked a little more time or not being on vacation, I truly enjoyed the experience.

As technical feedback, I would add an exercise similar to the one I did for Falco since I consider Falco to be and will be crucial for anyone working with sysdig secure and wanting to secure Kubernetes and Cloud environments.



I worked on this lab in an Elastic environment:
![image](https://github.com/mavaleri18/SETechAssessment_mavaleri/assets/139200227/35578413-59ec-403b-b9a5-6db6a1fde7d3)









