Se creo una integración utilizando Github action y las acciones del Marketplace.

Actions usadas: 
*Build and push Docker images by Docker: loguea a dockerhub, buildea la imagen y la sube.
*kubectl-simple by steebchen: descarga la imagen de dockerhub y la monta a un deployment my-app a través del kubeconfig en base64 que utiliza para conectarse al proveedor de servicios cloud (no pude probarlo por problemas con mi proveedor).