allow_k8s_contexts(os.getenv("CURRENT_CONTEXT", default='kind-kind'))

NAMESPACE = os.getenv("NAMESPACE", default='default')

k8s_custom_deploy(
    'spring-petclinic',
    apply_cmd="kubectl apply -f config/workload.yaml --namespace " + NAMESPACE + " >/dev/null" +
              " && kubectl get workload spring-petclinic --namespace " + NAMESPACE + " -o yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    deps=['pom.xml', './target/classes'],
    container_selector='workload'
)

k8s_resource('spring-petclinic', extra_pod_selectors=[{'serving.knative.dev/service': 'spring-petclinic'}])
