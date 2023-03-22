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

## (c) /etc/hosts 업데이트 - Ansible Node

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

## (d) SSH 키 생성 - Ansible Node

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

## 참고

- https://github.com/revenge1005/Ansible_study/tree/master/02.%20Ansible%20Tutorial%20-%202/Ansible%20Tutorial%202%20-%2009.%20Roles

- https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html#modules

- https://github.com/ansible/ansible/issues/39137

- https://techexpert.tips/ko/%EC%96%B4%EC%8A%AC%EC%97%90-%EC%9D%B4%EC%8A%AC%EC%9D%B4-%EC%9E%88%EB%8A%94/ansible-%EC%9A%B0%EB%B6%84%ED%88%AC-%EB%A6%AC%EB%88%85%EC%8A%A4%EC%97%90-%EB%8C%80%ED%95%9C-%ED%94%8C%EB%A0%88%EC%9D%B4-%EB%B6%81-%EC%98%88%EC%A0%9C/

- https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-docker-on-ubuntu-20-04

- https://www.arubacloud.com/tutorial/how-to-create-kubernetes-cluster-with-kubeadm-and-ansible-ubuntu-20-04.aspx

- https://stackoverflow.com/questions/41567196/ansible-how-to-add-variables-to-command-or-shell

- https://wikidocs.net/130351

- https://cumulus.tistory.com/42