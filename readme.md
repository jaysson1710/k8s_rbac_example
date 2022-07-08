## documentacion

- [secrets-serviceaccount](https://tanzu.vmware.com/developer/guides/platform-security-secrets-sa-what-is/)
- https://www.ibm.com/docs/en/cloud-paks/cp-management/2.0.0?topic=kubectl-using-service-account-tokens-connect-api-server
- [acceso_multiples_clusters](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)
- https://faun.pub/kubernetes-rbac-use-one-role-in-multiple-namespaces-d1d08bb08286
- [resources *](https://stackoverflow.com/questions/63871311/kubernetes-role-should-grant-access-to-all-resources-but-it-ignores-some-resourc)
>
para asociar el secreto a un service account -> se establece desde la creacion del secreto en la opcion :
>
- kubernetes.io/service-account.name: pod-read-sa
se debe especificar el identificador del service account
- Comando: `k get sa/pod-read-sa -o yaml`
- kubernetes.io/service-account.uid: 0ee50706-e95d-4807-88a0-9d12de7950a6
>
Una vez ya se tiene configurado el secreto, role, serviceaccount y rolebinding
Se debe establecer el contexto para poder trabajar y la asignacion de la clave generada (token)
```cmd
kubectl config set-credentials pod-read-sa --token=$(kubectl get secret mysecret -o jsonpath={.data.token} | base64 -d)
kubectl config set-context sa-context --user=pod-read-sa
```

para validar a que se tiene acceso 
`kubectl auth can-i delete cronjobs`
>
>
>
Revision de temas del proyecto True 
por solicitud de analisis
----------------------------------------------------------
-- realmente el problema fue que otro equipo borro el pod?
>
son riesgos generales (sin saber la configuracion del AKS)
-- riesgos en la configuracion que no tomen encuenta cada una de las aplicaciones
	-- reglas de firewall
-- No se manejan roles especificadas por namespace? o se manejan accesos genericos?
-- No se tiene perfilado cada equipo de trabajo
-- las aplicaciones se ecnuentran organizadas a traves de namespaces?
>
>
Identificar
-- criticidad del negocio y carga transaccional de True
-- como esta distribuido el cluster


