# Spring Petclinic - OpenShift on Z

## Objective

* Use OpenShift Java "source-to-image" builder
* Build a container image from a pre-compiled Java `jar` file
* Run the new image on OpenShift

## Build Instructions

1. Download `app.jar` to a directory of your choice on your computer.
2. Create a new Project: `oc new-project spring-petclinc`
3. Create the build: `oc new-build openjdk-11-rhel8:1.0 --name=spring-petclinic --binary=true`
4. Start the build: `oc start-build spring-petclinic --from-file=app.jar --follow`

Once the build completes, you will have a new image in the internal registry.

## Deploy Instructions

1. From the "Developer" perspective (Top Left)
2. Make sure you are in the "spring-petclinic" project.
3. From the left navigation, select `+Add`
4. Click on the "Container Image" tile.
5. Pick the **Image Stream tag from internal registry** radio button.
6. Select the `spring-petclinic` image stream from the `spring-petclinic` project and the `latest` tag.
7. You can keep all the defaults (or browse through them if you like).  It will also create a `route` by default.
8. Click `Create`

This will start the container.  It will probably show "ready" before the Java app is fully started, since we haven't added any liveness or readiness probes yet.

If you wait 10-20 seconds after the pod turns dark blue, you can click the little "box with arrow" link at the top-right of the pod to go the route URL.  You should see the Pet Clinic.

If you have Java installed locally, you can also run the app locally with:
```
java -jar app.jar
```
Then access the app at http://localhost:8080 once it has started.


