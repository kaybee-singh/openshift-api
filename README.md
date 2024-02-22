
# How to run a job using API in Red Hat Openshift Container Platform 4?



## Installation

Fetch the authentication token to use with API command


```bash
$ export TOKEN=$(oc whoami -t)
$ echo $TOKEN
```
    

Prepare the Json for the job, following is the Json file example. Replace with job name, container name and container image as per the requirement.


```bash
$ cat job-api.json
{
  "apiVersion": "batch/v1",
  "kind": "Job",
  "metadata": {
    "name": "kay"
  },
  "spec": {
    "template": {
      "metadata": {
        "name": "kaybee"
      },
      "spec": {
        "containers": [
          {
            "name": "test-container",
            "image": "busybox:latest",
            "command": ["echo", "This is a Job for testing"]
          }
        ],
        "restartPolicy": "Never"
      }
    }
  }
}
```

Run the API command and provide the above Json file with the command. Following command will create the job in kay namespace, so replace the namespace as per environment.


```bash
$ curl -k -X POST -H "Authorization: Bearer ${TOKEN}" -H "Content-Type: application/json" --data @job-api.json $(oc whoami --show-server)/apis/batch/v1/namespaces/kay/jobs
```
## Authors

- [@kaybee-singh](https://www.github.com/kaybee-singh)

