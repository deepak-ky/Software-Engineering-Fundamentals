
[java - Why Jackson needs a default constructor? - Stack Overflow](https://stackoverflow.com/questions/78247923/why-jackson-needs-a-default-constructor)

With a default constructor, Jackson first creates a default instance of the class and then injects the object's properties with each field read from the Json.

Likewise, with the `@JsonCreator` approach, Jackson first instantiates an object with only the properties specified as the parameters of the method annotated with `@JsonCreator`. Then, sets each remaining field from the Json into the object. The annotated method can be either a parameterized constructor or a static method.
		- The annotation doesn't need to include all the class' fields, but only a few of them, just so that Jackson is able to create an instance of  object and then set the remaining fields.


[How to parse JSON string with Jackson - Mkyong.com](https://mkyong.com/java/jackson-how-to-parse-json/#parse-json-string-with-jackson)

[Intro to the Jackson ObjectMapper | Baeldung](https://www.baeldung.com/jackson-object-mapper-tutorial)

[Jackson JSON Java Parser API Example Tutorial | DigitalOcean](https://www.digitalocean.com/community/tutorials/jackson-json-java-parser-api-example-tutorial)

