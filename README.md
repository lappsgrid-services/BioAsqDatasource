# BioAsqDatasource

DataSource service to give access to BioASQ evaluation data.

To test and create a service do the following (this assumes you have Maven installed):

```
$ mvn generate-resources
$ mvn clean package
```

The first line generate the files `src/main/java/org/anc/lapps/datasource/generic/Version.java` and `VERSION` using the version number it found in the Maven POM file, and the second line compiles and creates the war archive `target/BioAsqDatasource#VERSION.war` that can be put on the LAPPS server.

You can test the service with Jetty:

```
mvn jetty:run
```

Connect to the site at [http://localhost:8080/bioasq-datasource/jsServices](http://localhost:8080/bioasq-datasource/jsServices). At that point you will see a simple page where the content includes the following.

<ul>
    <li>BioAsqDatasource</li>
    <ul>
        <li>interfaces</li>
        <ul>
            <li>DataSource</li>
            <ul>
                <li>String execute(String) [sample] +</li>
                <li>String getMetadata() [sample] +</li>
            </ul>
        </ul>
        </ul>
</ul>

Expand the plus next to `execute(String)`, paste some JSON text into the text area and press the invoke link. You cannot just put any JSON in there, it needs to be the JSON serialization of a data container with `discriminator` and `payload` attributes, for testing you can paste in the following text (note that it needs to be on one line).

```
{ "discriminator": "http://vocab.lappsgrid.org/ns/action/get", "payload": "589a246c78275d0c4a000032" }
```

The response should include *"Which 2 medications are included in the Qsymia pill?"*,
see [here](/src/site/payload.md) for the full response.
