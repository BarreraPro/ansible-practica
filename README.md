
# 🐧 Práctica con Ansible y Docker

Este proyecto demuestra cómo automatizar tareas usando **Ansible** en un entorno simulado con **Docker**, creando 5 contenedores Ubuntu listos para recibir comandos remotos vía SSH.

## 🔧 Requisitos

- Docker Desktop
- Docker Compose
- VSCode (opcional)
- Git
- Cuenta en GitHub
- Ubuntu (como host o en WSL2)
- Ansible

## 📁 Estructura del proyecto

```bash
ansible-practica/
│
├── Dockerfile                # Imagen base con SSH y usuario ansible
├── docker-compose.yml        # Define 5 contenedores Ubuntu
├── ansible.cfg               # Configuración de Ansible
├── inventario.ini            # Hosts con IPs y puertos SSH
├── configurar-servidores.yml # Playbook para automatizar tareas
└── README.md                 # Este archivo
```

## 🐳 1. Levantar los contenedores

```bash
docker-compose up -d
```

Esto crea y ejecuta 5 contenedores Ubuntu (`ubuntu1` a `ubuntu5`) con puertos SSH expuestos del `2201` al `2205`.

## 🔐 2. Conexión SSH manual (opcional)

```bash
ssh ansible@127.0.0.1 -p 2201
# password: ansible
```

Todos los contenedores tienen el usuario:
- **Usuario:** `ansible`
- **Contraseña:** `ansible`

## ⚙️ 3. Inventario de Ansible

Archivo: `inventario.ini`

```ini
[servidores]
ubuntu1 ansible_host=127.0.0.1 ansible_port=2201 ansible_user=ansible ansible_password=ansible
ubuntu2 ansible_host=127.0.0.1 ansible_port=2202 ansible_user=ansible ansible_password=ansible
ubuntu3 ansible_host=127.0.0.1 ansible_port=2203 ansible_user=ansible ansible_password=ansible
ubuntu4 ansible_host=127.0.0.1 ansible_port=2204 ansible_user=ansible ansible_password=ansible
ubuntu5 ansible_host=127.0.0.1 ansible_port=2205 ansible_user=ansible ansible_password=ansible
```

## 📜 4. Ejecutar el playbook

Archivo: `configurar-servidores.yml`

Este playbook:

- Actualiza paquetes
- Crea el usuario `itla`
- Crea una carpeta `/home/itla/practica`
- Crea un archivo `hola.txt` dentro con el mensaje: “Hola mundo desde Ansible”
- Instala paquetes básicos

### Ejecutar el playbook:

```bash
ansible-playbook -i inventario.ini configurar-servidores.yml
```

## ✅ Verificación

Conéctate por SSH a un contenedor y verifica:

```bash
ssh ansible@127.0.0.1 -p 2201
ls /home/itla/practica
cat /home/itla/practica/hola.txt
```

Deberías ver:

```bash
hola.txt
Hola mundo desde Ansible
```

## 🧹 Apagar los contenedores

```bash
docker-compose down
```

---

## 📸 Autor

**BarreraPro**  
Estudiante de Electiva II  
[GitHub](https://github.com/BarreraPro)
