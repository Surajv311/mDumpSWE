
# JSON vs Protobuf

- Protocol Buffers are language-neutral, platform-neutral extensible mechanisms for serializing structured data. Serialization is the process of converting the state of an object, that is, the values of its properties, into a form that can be stored or transmitted.
- JSON is a format that encodes objects in a string. In this context: Serialization means to convert an object into that string, and deserialization is its inverse operation (convert string -> object). When transmitting data or storing them in a file, the data are required to be byte strings, but complex objects are seldom in this format. Serialization can convert these complex objects into byte strings for such use. After the byte strings are transmitted, the receiver will have to recover the original object from the byte string. This is known as deserialization. Say, you have an object: {foo: [1, 4, 7, 10], bar: "baz"} serializing into JSON will convert it into a string: '{"foo":[1,4,7,10],"bar":"baz"}' which can be stored or sent through wire to anywhere. The receiver can then deserialize this string to get back the original object. {foo: [1, 4, 7, 10], bar: "baz"}. [Serialize, Deserialize in json _al](https://stackoverflow.com/questions/3316762/what-is-deserialize-and-serialize-in-json)
- When to use JSON and Protobuf:
  - JSON when: you need or want data to be human readable, data from the service is directly consumed by a web browser, your server side application is written in JavaScript, you aren’t prepared to tie the data model to a schema, the operational burden of running a different kind of network service is too great. 
  - Protobuf for relatively smaller size, guarantees type-safety, prevents schema-violations, gives you simple accessors, fast serialization/deserialization, backward compatibility.

[JSON vs protobuf _al](https://stackoverflow.com/questions/52409579/protocol-buffer-vs-json-when-to-choose-one-over-another)


----------------------------------------------------------------------





















