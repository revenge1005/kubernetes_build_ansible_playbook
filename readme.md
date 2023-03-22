# [Ubuntu 22.04] Kubernetes Build (Ansible)

![3](https://user-images.githubusercontent.com/42735894/226969742-83f386ca-6c3f-4856-a348-dbce970f80a6.PNG)

<br>

## (a) 구성

![1](https://user-images.githubusercontent.com/42735894/226969757-b33dd321-82a6-4d0c-974a-53b976003e97.PNG)

<br>

## (b) Ansible Install - Ansible Node

```bash
{
	sudo apt update; 
	sudo apt install software-properties-common -y
	sudo add-apt-repository --yes --update ppa:ansible/ansible -y
	sudo apt install ansible -y
}
```

<br>

## (c) /etc/hosts 업데이트

```bash
cat <<EOF >>/etc/hosts

# Control Node.
192.168.219.100  k8s-master  k8s-master.test.com
# Ansible Managed Nodes.
192.168.219.101  k8s-node01  k8s-node01.test.com
192.168.219.102  k8s-node02  k8s-node02.test.com
EOF
```

<br>

## (d) SSH 키 생성

```bash
{
	ssh-keygen -t ed25519 -C "Ansible Test" -N ''
	for i in k8s-master k8s-node01 k8s-node02;
	do
	    ssh-copy-id -i ~/.ssh/id_ed25519.pub $i
	done
}
```

<br>

## Result

![2](https://user-images.githubusercontent.com/42735894/226969760-a82a72aa-b016-4a55-b932-e32237a43328.PNG)