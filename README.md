# Provisioning

Este repositorio está diseñado para proporcionar clústeres como servicio, facilitando la creación, despliegue y eliminación de clústeres en diferentes zonas (edge, region, wavelength).

## Procedimiento

### **Creación de un clúster Gemelo Digital (DT - Siglas en ingles)**

1. **Preparación en el repositorio de `provisioning`**:
   - Navega al repositorio de `provisioning` y crea el espacio de trabajo para el DT en las carpetas correspondientes a las zonas (`edge`, `region`, `wavelength`).
   - Crea el archivo `NAME_CLUSTER.yaml` en la zona seleccionada.
     - Modifica el archivo `NAME_CLUSTER.yaml` con los parámetros necesarios para el clúster.
     - Asegúrate de que el valor de `clusters["name"]` coincide con el nombre del archivo `NAME_CLUSTER.yaml`.

2. **Preparación en el repositorio de `auto-ztp`**:
   - Crea el espacio de trabajo correspondiente al DT, organizando las carpetas por zonas (`edge`, `region`, `wavelength`).
   - Copia el contenido de la carpeta `digital-twins-example` como base.
   - Realiza un push con los cambios.

3. **Configuración en el repositorio de `iac-terragrunt`**:
   - Crea el espacio de trabajo para el DT.
   - Configura el módulo `subnets` en Terraform dentro del archivo `terragrunt.hcl` para cada clúster.
   - Realiza un push con los cambios.

4. **Regreso al repositorio de `provisioning`**:
   - Realiza un push de los cambios en la rama `dt/NAME_DT`.

5. **Despliegue del clúster**:
   - Una vez que los cambios han sido subidos, espera a que las acciones de GitHub (GitHub Actions) finalicen.
   - Accede a la interfaz de ArgoCD, filtra por el proyecto `clusters` y verifica que el clúster se sincronice automáticamente y se esté desplegando.

6. **Creación de un clúster en `edge` (adicional)**:
   - Ve al espacio de trabajo del DT en el repositorio de `iac-terragrunt`.
   - Llama al módulo `eni-lni` en Terraform desde el archivo `terragrunt.hcl`.
   - Verifica los IDs de las instancias EC2 del clúster en la consola de AWS.
   - Realiza un pull de los cambios en la rama principal.

7. **Finalización**:
   - Regresa al repositorio de `provisioning` y aprueba/mergea los cambios a la rama principal.
   - El clúster estará listo para ser utilizado.

### **Eliminación de un clúster DT**

1. **Preparación en el repositorio de `provisioning`**:
   - Elimina el archivo correspondiente al nombre del clúster (por ejemplo, `telefonica/edge/telefonica.yaml`).
   - Realiza un push de los cambios en la rama `dt/NAME_DT`.
   - Espera a que todas las acciones de GitHub (GitHub Actions) finalicen correctamente.

2. **Eliminación de parámetros en `iac-terragrunt`**:
   - Si el clúster está en `edge`, elimina los parámetros relacionados en el archivo `eni-lni/terragrunt.hcl`.
   - Para otros clústeres, elimina los parámetros correspondientes en `subnets/terragrunt.hcl`.
   - Realiza un push de los cambios en la rama principal.

3. **Finalización**:
   - Regresa al repositorio de `provisioning` y mergea los cambios a la rama principal.
   - El clúster será eliminado automáticamente.

---

## Descripción de carpetas principales

- **`demo`**: Ejemplos básicos para `edge`, `region` y `wavelength`.
- **`examples`**: Casos de uso específicos, como `digital-twins`, con ejemplos para las zonas `edge`, `region` y `wavelength`.
- **`opentwins`**: Configuraciones específicas para proyectos de OpenTwins, organizadas por zona.
- **`telefonica`**: Configuraciones específicas para proyectos internos de Telefónica, organizadas por zona.

## Licencia

Este projecto es licenciado bajo [Apache](LICENSE)