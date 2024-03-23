# Flask-with-Protocol-Buffer-Serializer
Flask sample project to demonstrate working with protocol buffers in request and response.

Runs currently on python 2. To run it on Python 3, just change add parentheses of print statements in each file.

Study more about Protocol buffer [here](https://auth0.com/blog/beating-json-performance-with-protobuf/).

##  Requirements to get this example running

The major requirements are mentioned [here](/requirements.txt).
You must have a protoc compiler and protobuf library in python

## To get this example running, do these steps.

1. First create a **.proto** file with the schema of your request/response classes. An example is given in the file **addressbook.proto**
2. Now, when you have created the **.proto** file, you have to generate python classes/descriptors for each and everything in your **.proto** file. To help automate this, Google provides **protoc** compiler and can be downloaded with help of this [blog](https://medium.com/@erika_dike/installing-the-protobuf-compiler-on-a-mac-a0d397af46b8) as the documentation is not quite good.
3. After installing the compiler, run the command ```protoc -I=. --python_out=. ./addressbook.proto```. A file addressbook_pb2.py will be created.
4. Now, you can use this file to serialise/deserialise your protobuf files. You can learn more about these files [here](https://developers.google.com/protocol-buffers/docs/pythontutorial).
5. I have provided 2 files **make_proto_file.py** to generate a sample protobuf file (saved as a binary file) and **read_display_proto_file.py** to display the contents of the binary protobuf file on _stdout_.
6. To run any of these files, provide a system argument as the name of binary file to be created. As example - ```python make_proto_file.py protofile1.pb```.
7. Now, you can run the Flask app by ```python flask_test.py```.
8. Use curl with the following command to test -
```curl -X POST -H "Accept: application/x-protobuf" -H "Content-type: application/x-protobuf" http://127.0.0.1:5000/load --data-binary @protofile1.pb > outputfile.pb```. The contents of the file will be printed as a json object after deserialisation of the protobuf file.
9. At last, you can check the output of **outputfile.pb**. In this case, it will be the same as we are uploading the same file, and returning the same.


Issues, contributions and additional examples are welcome.
