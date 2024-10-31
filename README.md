# ClusterAlmacenamiento-Hadoop

Este repositorio contiene un clúster de almacenamiento utilizando **Hadoop** y **HDFS** (Hadoop Distributed File System). En la rama `dev`, se han realizado pruebas sobre el funcionamiento del clúster en un contenedor de **Docker**, junto con ejemplos de operaciones básicas en HDFS. A continuación, se presenta un sencillo tutorial para llevar a cabo dichas pruebas:

## 🚀 Lanzar el clúster

Para iniciar el clúster de HDFS utilizando **Docker Compose**, sigue estos pasos:

1. **Inicia el clúster**:
```bash
docker-compose up -d
```

2. **Verifica que los contenedores estén en funcionamiento**:
```bash
docker ps
```

3. **Accede a la interfaz web del NameNode en: http://localhost:9870**

## 📁 Operaciones básicas en HDFS

### Listar directorios y archivos en HDFS

Para ver el contenido de un directorio en HDFS, utiliza el siguiente comando:
```bash
docker exec -it namenode hdfs dfs -ls /
```
### Subir archivos a HDFS

1. **Crea un directorio de prueba**:
```bash
echo "Hello, HDFS" > test.txt
```

2. **Copia el archivo al contenedor `namenode`**:
```bash
docker cp test.txt namenode:/tmp/
```

3. **Sube el archivo a HDFS**:
```bash
docker exec -it namenode hdfs dfs -put /tmp/test.txt /
```
Nota: Si no existe el directorio `hdfs://namenode:8020/user/root`, créalo con el siguiente comando:
```bash
docker exec -it namenode hdfs dfs -mkdir -p /user/root
```

4. **Ver el contenido de un archivo en HDFS**:
```bash
docker exec -it namenode hdfs dfs -cat /test.txt
```

5. **Eliminar un archivo o directorio en HDFS**:
- Para eliminar un archivo:
```bash
docker exec -it namenode hdfs dfs -rm /test.txt
```
- Para eliminar un directorio y su contenido:
```bash
docker exec -it namenode hdfs dfs -rm -r /ruta/en/hdfs/directorio
```

6. **Crear un directorio en HDFS**:
```bash
docker exec -it namenode hdfs dfs -mkdir /ruta/en/hdfs/nuevo_directorio
```

## 🔗 Fuentes
[Guía para configurar un clúster HDFS con Docker Compose](https://bytemedirk.medium.com/setting-up-an-hdfs-cluster-with-docker-compose-a-step-by-step-guide-4541cd15b168)
