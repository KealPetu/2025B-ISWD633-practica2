# COMPLETAR  
Comparando sus conocimientos antes de hacer la práctica con sus conocimientos después de hacer la tarea, explicar los principales aprendizajes logrados para beneficio de su formación profesional.  
Si solucionó un problema presentado al realizar la práctica también se debe documentar.

Hemos revisado temas com varaibles de entorno y redes de docker, temas fundamentales que nos ayudan mantener la seguridad e integridad de nuestros contenedores sin la necesidad de generar maquinas virtuales y manteniendo el bajo uso de recursos.

Docker contiene una gran variedad de herramientas que nos ayudan a moldear el contenedor a nuestras necesidades, ya sea de forma academica o en la vida profesional, como proyectos personales y organizacionales.

Consultar: Cómo se gestionan datos confidenciales con los secretos de Docker (Docker Secrets).

Resultados de la consulta: 

La **gestión de datos confidenciales con Docker Secrets** es una funcionalidad diseñada para proteger información sensible (como contraseñas, claves API, certificados, tokens, etc.) dentro de **entornos Docker Swarm** o **contenedores orquestados**.

Aquí te explico cómo funciona y cómo se usa 👇

---

### 🧩 **¿Qué son los Docker Secrets?**

Los **Docker Secrets** son objetos cifrados que permiten almacenar y distribuir información sensible de forma **segura y controlada** dentro de un clúster Docker Swarm.
Solo los **servicios autorizados** pueden acceder a esos secretos, y **Docker los gestiona en memoria**, evitando que se escriban en disco.

---

### 🔐 **Cómo Docker gestiona los secretos**

1. **Cifrado y almacenamiento interno:**

   * Los secretos se almacenan **cifrados en el administrador del Swarm**.
   * Solo se descifran **en el nodo donde se ejecuta el contenedor** que los necesita.
   * Nunca viajan sin cifrar por la red interna del clúster.

2. **Distribución controlada:**

   * Cada servicio debe **declarar explícitamente qué secretos necesita**.
   * Los secretos solo son montados en los contenedores de ese servicio (en `/run/secrets/`).
   * Cuando el contenedor termina, el secreto se elimina automáticamente de la memoria.

3. **Acceso dentro del contenedor:**

   * Una vez montado, el secreto aparece como un **archivo de texto plano** dentro del contenedor.
   * No se expone como variable de entorno (por seguridad).

---

### ⚙️ **Ejemplo de uso**

#### 1. Crear un secreto

```bash
echo "MiPasswordSeguro123" | docker secret create db_password -
```

#### 2. Ver los secretos existentes

```bash
docker secret ls
```

#### 3. Usar el secreto en un servicio

```bash
docker service create \
  --name mi_app \
  --secret db_password \
  nginx
```

Dentro del contenedor de `mi_app`, el secreto estará disponible en:

```
/run/secrets/db_password
```

#### 4. Leer el secreto dentro del contenedor

```bash
cat /run/secrets/db_password
```

---

### 🧠 **Buenas prácticas**

* **Nunca almacenar secretos en imágenes Docker** ni en variables de entorno.
* **Usar Docker Swarm o Kubernetes** para orquestar y distribuir secretos de forma segura.
* **Limitar el acceso**: solo los servicios que realmente lo necesitan deben tener el secreto.
* **Rotar los secretos regularmente** (crear nuevos y eliminar los antiguos).

---

### 🚫 **Limitación importante**

Docker Secrets **solo funciona nativamente en modo Swarm**.
Si usas contenedores “simples” (sin Swarm), deberías usar otras soluciones como:

* **Docker Compose + Docker Secrets externos** (desde versión 3.1 en adelante con Swarm activado)
* **Vault** (HashiCorp)
* **AWS Secrets Manager**, **Azure Key Vault**, **GCP Secret Manager**, etc.
