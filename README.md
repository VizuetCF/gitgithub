## Cómo utilizar git y GitHub

Este repositorio sirve como resúmen del [curso de Git y github de Platzi](https://platzi.com/github), por [Freddy Vega](https://github.com/freddier/hyperblog).

**Git** es un sistema de control de versiones (**VCS version control system**), 

Registra los **cambios** realizados sobre un archivo o conjunto de archivos a lo largo del **tiempo**, por lo tanto no tendrás versiones como 

* tarea.txt
* tarea2.txt
* tarea2-final.txt 
* tarea2-final2.txt 
* tarea2-final2-esteeselbueno.txt 

Además de que envés de guardar los archivos completos se guardan **sólo los cambios**.

Git es algo así como el `Ctrl+Z` (deshacer) de los programadores, suponiendo que el `Ctrl Z` guardara todo el **historial de modificación** de los archivos, ya que con git puedes moverte en la historia (algo así como una máquina del tiempo).

## Flujo básico de git

El flujo normal de git es el siguiente:

`git init`: Empiezas un repositorio

`git add archivo.txt`: Agregas los cambios del archivo.txt al **staging area** para decirle a git que se prepare para guardar los cambios

`git commit -m 'Descripción del commit'`: Guarda los cambios en la base de datos del VCS (creando una nueva versión)

**Tipos de Control de versiones:**

* Local: Sólo funciona en una sóla máquina, es útil, pero no incorpora la colaboración.
* Centralizado (en un sólo servidor): Toda la información está depositada en un sólo repositorio, lo que hace que el trabajo se maneje directamente en el servidor. 
* Distribuído: La información se encuentra respaldada en diferentes peers, diferentes servidores y/o diferentes máquinas, lo que permite trabajar y compartir de manera sencilla.

## Archivos binarios y de texto plano

Git permite guardar tanto binarios como archivos de texto plano, pero está diseñado para modificar archivos de texto plano, ¿la razón? como git guarda los cambios entre versiones en el tiempo, son prácticamente no rastreables los cambios entre una versión y otra de un binario, mientras que son muy transparentes en los archivos de texto plano.

## Diferencias de git contra otros VCS

Git guarda referencia a los archivos no cambiados

Trabajo online efectivo

Git tiene Integridad: No puedes perder información durante su transmición

### Ventajas de git contra otros manejadores de versiones

* Veloz
* Diseño sencillo
* Fuerte apoyo del desarrollo no lineal
* Completamente distribuido
* Capaz de manejar grandes proyectos

## Operaciones principales de git

Es importante saber cuál es el estatus de tus cambios, ya que al modificar un archivo, éste no por defecto se va a git, sino que se modifica en el **working directory**, para que sea trackeado por git debe de pasar por el **staging area** y llegar al **repositorio**, opcionalmente podría llegar al **repositorio remoto**. A continuación más detalle.

* **Working directory (Local):** El working directory es el espacio de trabajo no rastreado por git, al modificar un archivo, este se modificará en el working directory andtes de que le des `git add` para agregarlo al staging area.

* **Staging Area:** Es un espacio en memoria ram dónde están guardados los cambios, pero todavía no están en el repositorio (no son trackeados por git). para agregar al staging area se utiliza el comando `git add`

  ```bash
  git add archivo.txt #Agrega el archivo.txt al staging area
  git add . #Agrega todos los cambios de los archivos en las subcarpetas del directorio en el que te encuentras al staging area
  git add -A #Agrega todos los cambios del repositorio en el que estás trabajando al staging area
  ```

* **Git repository:** Es el lugar dónde se trackean los cambios, cuando algo está en el repositorio, ya está en la historia de git y puedes acceder a ese historial mediante los commits. `git commit`

  ```bash
  git commit -m 'Commit 1' #Crea un commit (sube los cambios al repositorio local) con el nombre 'Commit 1'
  git commit #Se prepara para hacer commit y abre el editor por defecto de la terminal para ponerle nombre
  ```

  Es una buena práctica ser descriptivos con los cambios que se hicieron en cada commit.

* **Remote repository**: Acá entra github, el repositorio remoto es una copia de tu repositorio local, pero en Internet. Para mandar cambios al repositorio remoto es con el comando `git push`

  ```bash
  git push origin master #Empuja (envía) los cambios de la rama master al servidor remoto 'origin' 
  ```

## Commit

Un commit es un cambio rastreable (de 1 o varios archivos), es confirmar un conjunto de cambios provisionales de forma permanente y tenemos el superpoder de ponerle nombre a este cambio.

La historia de tu desarrollo se van guardando mediante commits, ya que cada cambio confirmado tiene modificaciones importantes hasta llegar al cambio actual.

Para hacer un commit, es muy sencillo, tenemos que tener agregado en el staging (`git add -A`) y usar el comando commit

```bash
Git commit -m 'commit'
```

Si trabajamos en algo experimental o que no queremos que sea parte del flujo principal, podemos hacer una nueva rama (**branch**), recordemos que la rama principal suela llamarse **master**, por lo tanto ésta branch nueva tendrá su propia historia (posterior al punto donde se creó).

Para crear una rama nueva con la información de la rama actual usamos el comando

```bash
git checkout -b nombre-del-branch
```

Si los cambios que realizaste en tu rama nueva son un avance en el código, puedes fusionarlo a la rama master (o a otra), para ésto tienes que cambiarte a master y hacer el comando es `merge`

```bash
git checkout master # nos cambiamos a la rama master
git merge rama-nueva # Fusionamos los cambios de la 'rama-nueva' en master
```

## Archivos trackeados

- **Archivos Tracked**: Son los archivos que viven dentro de Git, no tienen cambios pendientes y sus últimas actualizaciones han  sido guardadas en el repositorio gracias a los comandos `git add` y `git commit`.
- **Archivos Staged**: Son archivos en Staging. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando `git add`, aunque no sus últimos cambios. Git ya sabe de la existencia de estos  últimos cambios pero todavía no han sido guardados definitivamente en el repositorio porque falta ejecutar el comando `git commit`.
- **Archivos Unstaged**: Entiendelos como archivos *“Tracked pero Unstaged”*. Son archivos que viven dentro de Git pero no han sido afectados por el comando `git add` ni mucho menos por `git commit`. Git tiene un registro de estos archivos pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.
- **Archivos Untracked**: Son archivos que NO viven dentro de Git, solo en el disco duro. Nunca han sido afectados por `git add`, así que Git no tiene registros de su existencia.

## Configurar el entorno de git

Para configurar la información del usuario global de git de tu máquina deberás de utilizar el comando `git config` declarando que modificaras de manera `--global` la variable (`email` o `name`) de tú `user` lo que significa que estarás definiendo qué usuario está utilizando git en tu máquina (que firma su autenticidad)

```bash
git config --global user.email "tu@email.com" # Configura el correo del usuario de git 
git config --global user.name "Tu Nombre" # Configura el nombre del usuario de git 

```

Llaves SSH

```bash
ssh-keygen -t rsa -b 4096 -C "email@dominio.org"
```



**git init**

Con git init creas un entorno de trabajo para git, además de la carpeta oculta .git, dónde se guardará toda la información relevante al control de versiones, es muy sencillo, en un directorio que no esté trackeado por git usa el comando `git init`

```bash
git init #Empiezas un repositorio
```

**git add**

Git add agrega los archivos y carpetas que elijas al staging area, que es como el espacio en memoria ram donde están los cambios que se van a subir en el futuro.

```bash
git add <archivo.txt> # Agregas los cambios del archivo.txt al **staging area** para decirle a git que se prepare para guardar los cambios
git add -A # Agregas todos los cambios al staging area
git add . # Agregas los cambios de los subdirectorios de la carpeta en la que te encuentras
```

**git commit**

Graba los cambios que están en el `staging area` en el `repositorio`.

```bash
git commit #Se prepara para hacer commit y abre el editor por defecto de la terminal para ponerle nombre
git commit -m 'Descripción del commit': #Guarda los cambios en la base de datos del VCS (creando una nueva versión)
git commit --amend:
```

**Estado**

Muestra el estado del working directory, muestra si hay cambios en el working directory sin agregar, o si hay algo en el staging area sin que se haya hecho un commit.

```bash
git status
```

**git log** 

Te muestra el historial de los commits que has hecho

```bash
git log # Muestra todos los commits con la información default
git log -3 #ultimos tres commits
git log --oneline #Resumido
git log --oneline --graph #Te lo muestra Resumido y bonito
```

**Show**

Muestra el mensaje del último commit y la diferencia textual. Es como log, pero con la diferencia de que muestra los cambios precisos que se hicieron en el commit

```bash
git show
```

**git diff**

Nos compara y muestra los cambios sufridos entre los dos commits. Los id de los commit se pueden encontrar ejecutando git log.

```bash
git diff <referenci sha1> #
git diff <referencia2> <referencia1> <archivo>
```

**git reset**

```bash
git reset --soft #Agrega al staging
git reset --mixed #No lo agrega al staging
git reset --hard # 
```

**Cambiar el editor de código default de git**

```bash
git config --global core.editor “nano --wait”
```

**Branchs (Ramas)**

Versiones alternas de un proyecto

```bash
git branch nombre 
git branch -d nombre # Eliminar rama
git branch -D nombre # Forzar eliminado de rama
git branch -m nombre_viejo nombre_nuevo # Cambiar nombre de la rama
git checkout #cambiar de ramas
git checkout cambio_rama # Cambiar a la rama <cambio_rama>
git checkout -b nueva-imagen # Crear rama <nueva-imagen> y switchear a ésta
git merge <rama-arreglada> # mezclando la rama actual con la <rama-arreglada> 
# Tenemos que estar en la rama output para hacer un merge o un rebase
git merge --abort
git rebase # hace prácticamente lo mismo que merge, cambiamos la historia de nuestro proyecto sin crear bifurcaciones del proyecto. Es mejor usar merge, 
#Usar solo git rebase de manera local.

```

## Repositorio remoto (GitHub)

GitHub es el cliente de git más popular, tanto que, se podría decir que es la red social del código, ésto porque te permite tener tus repositorios en la nube, tener un perfil profesional (con los aportes, tus repositorios y demás información de tu vidad de programador) y todo con un núcleo de git por dentro.

.

Como git es un VMS distribuído, entonces el código funciona en diferentes servidores (máquinas), pero para que vinculemos un servidor remoto tenemos que configurar un origen que indique con qué repositorio remoto estaremos trabajando, básicamente es una sintaxis que nos indica que le vamos a poner un pseudónimo a la url de dónde vamos a trabajar.

.

El comando para agregar un orígen remoto es:

```bash
git remote add origin <url_repositorio>
```

Donde:

* **git remote** = El comando que indica que vamos a trabajar con un servidor remoto
* **add** = Agrega un alias para el servidor remoto
* **origin** = Es el alias del servidor remoto (ésto para no tener que poner la url completa cada que quieres hacer un cambio)
* **<url_repositorio>** = Es la url dónde está el repositorio en la nube, en este caso de github (https://github.com/<tu_usuario_de_github>/<nombre_de_tu_repositorio>)

Ya que agregaste tu servidor remoto `origin` puedes jalaro o empujar los cambios, osea sincronizar tu servidor remoto con el local, para eso tenemos 2 comandos

* git pull: Jala los cambios del servidor, pero cómo podemos tener configurados diferentes repositorios remotos, tenemos que definir de dónde lo vamos a bajar y qué rama vamos a bajar, para eso podemos utilizar el siguiente comando:

  ```bash
  git pull <remoto> <rama>
  ```

  En el caso de la rama master y el remoto origin:

  ```bash
  git pull origin master
  ```

  Ésto bajará todos los cambios a tu local, pero si de pura casualidad la historia es diferente (el repositorio remoto tiene commits diferentes, puede ser un Readme nuevo) tienes que forzar bajar los cambios con el flag `--allow-unrelated-histories`.

  ```bash
  git pull origin master --allow-unrelated-histories
  ```

* git push: Empuja los cambios desde el local al remoto.

  ```bash
  git push <remote> <rama>
  ```

  La sintaxis es la misma que para el pull:

  ```bash
  git push origin master
  ```



## Llaves públicas y privadas

Es un problema guardar el usuario y la contraseña de tu cuenta de github en tu máquina porque puede ser extraído si alguien accede a tu equipo, para eso podemos cifrar tu identidad con el algoritmo de Llaves públicas y privadas (o Cifrado asimétrico de un sólo camino )

Este algoritmo sirve para mandar mensajes privados entre varios nodos con la lógica de que firmas tu mensaje con una llave pública vinculada con una llave privada que puede leer el mensaje.

El flujo es:

1. Creas una llave pública y una llave privada (ambas están vinculadas)
2. Cifras el mensaje con la llave pública (puede ser llave de otra persona)
3. Envías el mensaje
4. El receptor, al tener la llave privada puede descifrar el mensaje.

Este algoritmo es completamente seguro, así es cómo se mandan las comunicaciones en bancos, la comunicación entre servidores o las firmas electrónicas.

### Git stash

git stash: es otro de los limbos, como el staging area. Para agregar los cambios estos deben estar en el staging area.
git stash list: nos muestra la lista de stash que tengamos.
git stash drop stash@{numero}: nos permite borrar un stash.
git stash apply: aplicamos el último cambio
Guardar en el limbo los cambios

git stash
git stash drop <numero_estado> #eliminar un stash
git stash apply #Agrega el estado ultimo
git stash apply <estado> #agregar stash exacto

### git cherry-pick 

Escoger commits
git cherry-pick [SHA1] nos permite cambiar un commit a otra rama para salvarnos la vida.
Vim
:wq #guardar y salir

MAC
pbcopy < “archivo”

## Forks o Bifurcaciones

Es una característica única de GitHub en la que se crea una copia exacta del estado actual de un repositorio directamente en GitHub, éste repositorio podrá servir como otro origen y se podrá clonar (como cualquier otro repositorio), en pocas palabras, lo podremos utilizar como un git cualquiera

Un fork es como una bifurcación del repositorio completo, tiene una historia en común, pero de repente se bifurca y pueden variar los cambios, ya que ambos proyectos podrán ser modificados en paralelo y para estar al día un colaborador tendrá que estar actualizando su fork con la información del original.

Al hacer un fork de un poryecto en GitHub, te conviertes en dueñ@ del repositorio fork, puedes trabajar en éste con todos los permisos, pero es un repositorio completamente diferente que el original, teniendo alguna historia en común.

Los forks son importantes porque es la manera en la que funciona el open source, ya que, una persona puede no ser colaborador de un proyecto, pero puede contribuír al mismo, haciendo mejor software que pueda ser utilizado por cualquiera.

Al hacer un fork, GitHub sabe que se hizo el fork del proyecto, por lo que se le permite al colaborador hacer pull request desde su repositorio propio.

## Trabajando con más de 1 repositorio remoto

Cuando trabajas en un proyecto que existe en **diferentes repositorios remotos** (normalmente a causa de un **fork**) es muy probable que desees poder **trabajar con ambos repositorios**, para ésto puedes crear un **remoto adicional** desde consola.

```bash
git remote add <nombre_del_remoto> <url_del_remoto> 
```

```bash
git remote upstream https://github.com/freddier/hyperblog
```

Al crear un **remoto adicional** podremos, hacer **pull** desde el nuevo **origen** (en caso de tener permisos podremos hacer fetch y push)

```bash
git pull <remoto> <rama>
```

```bash
git pull upstream master
```

Éste `pull` nos traerá los **cambios del remoto**, por lo que se estará al día en el proyecto, el flujo de trabajo cambia, en adelante se estará trabajando haciendo **pull desde el upstream** y **push al origin** para pasar a hacer **pull request**.

```bash
git pull upstream master
git push origin master
```

## Fetch

git fetch origin master
git push
git push origin master --tags
git push origin “branch”
git pull origin master
Llaves SSH
ssh-keygen -t rsa -b 4096 -C "davbelom@gmail.com"
Proyectos
Proyecto por feature grande

## Etiquetas, versiones

Comandos para trabajar con etiquetas:

- Crear un nuevo tag y asignarlo a un commit: 

  ```bash
  git tag -f -a <version-nueva> -m  <Comentario> <version>
  git tag -f -a nombre-del-tag id-del-commit
  ```

* Borrar un tag en el repositorio local: 

  ```bash
  git tag -d nombre-del-tag
  ```

- Listar los tags de nuestro repositorio local: 

  ```bash
  git tag
  git show-refs --tags
  ```

- Publicar un tag en el repositorio remoto

  ```bash
  git push origin --tags
  ```

- Borrar un tag del repositorio remoto: 

  ```bash
  git tag -d nombre-del-tag # Borrar los tags en local
  git push origin :refs/tags/nombre-del-tag # Borrar los tags en remoto
  ```

## Pull request: 

Es una funcionalidad de github (en gitlab llamada merge request y en bitbucket push request), en la que un colaborador pide que revisen sus cambios antes de hacer merge a una rama, normalmente master.

Al hacer un pull request se genera una conversación que pueden seguir los demás usuarios del repositorio, así como autorizar y rechazar los cambios.

El flujo del pull request es el siguiente

1. Se trabaja en una **rama paralela** los cambios que se desean (`git checkout -b <rama>`)
2. Se hace un **commit** a la rama (`git commit -am '<Comentario>'`)
3. Se **suben** al **remoto** los **cambios** (`git push origin <rama>`)
4. En GitHub se hace el `pull request` comparando la **rama master** con la rama del **fix**.
5. Uno, o varios colaboradores  revisan que el **código sea correcto** y dan **feedback** (en el chat del pull request)
6. El colaborador hace los cambios que desea en la **rama** y lo **vuelve a subir** al remoto (automáticamente jala la historia de los cambios que se hagan en la rama, en remoto)
7. Se **aceptan los cambios** en GitHub
8. Se hace **merge** a `master` desde GitHub

**Importante**: Cuando se modifica una `rama`, también se modifica el `pull request`

