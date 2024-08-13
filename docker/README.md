# Docker Notes

These notes cover important topics related to Docker that I have identified. I have included examples and explanations to help me better understand these concepts and fill any gaps in my knowledge. These notes will serve as a valuable resource for me to review.

## Section 3
1. **Useful Commands**
   - `docker run -p 38282:8080 -d kodekloud/simple-webapp:blue`
   - `docker run <Image>:<Tag/Version(Uses-latest-if-not-specified)>`
   - `docker attach <Running_container_id>`
   - `docker inspect <container_name>`

## Section 4
1. **Command CMD**
   - Add in Dockerfile like `CMD command param1` or CMD["Command","param1"]
   - CMD ["sleep","5"] is correct, CMD["sleep 5"] is incorrect

2. **Entrypoint**
   - The ENTRYPOINT in a Dockerfile specifies the default command that runs when a container starts. It sets the main process that the container will execute, and unlike CMD, it cannot be easily overridden by passing arguments at runtime.
   - ENTRYPOINT ["executable", "param1", "param2"] is correct, In this example, the container will always run executable param1 param2 on startup.