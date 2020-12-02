# URL base error data

* **Type**: Design proposal
* **Author**: Iraguha Jean-Paul
* **Status**: Draft

Goal: managing application errors using UTF-8 encoded string only

## Motivation


ERROR Frame (0x0B) is used for errors on individual requests/streams as well as connection errors and in response to SETUP frames. 

Frame Contents

```
     0                   1                   2                   3
     0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |                           Stream ID                           |
    +-----------+-+-+---------------+-------------------------------+
    |Frame Type |0|0|      Flags    |
    +-----------+-+-+---------------+-------------------------------+
    |                          Error Code                           |
    +---------------------------------------------------------------+
                               Error Data
```

* __Frame Type__: (6 bits) 0x0B
* __Error Code__: (32 bits = max value 2^31-1 = 2,147,483,647) Type of Error. [See list of valid Error Codes](https://github.com/rsocket/rsocket/blob/master/Protocol.md#error-frame-0x0b).
* __Error Data__: includes Payload describing error information. Error Data SHOULD be a UTF-8 encoded string. The string MUST NOT be null terminated.

Application layer logic generating a Reactive Streams _onError_ event will produce a __Frame Type__ equal to __APPLICATION_ERROR__.

## Problematic
- __Error Data__ UTF-8 only is the only room we have to managing application errors.
- __Error Data__ should be easily parsable
- An application can issue more that one error
- We need room for errors contextualization like resources identifiers, tracers,...

## Convention/Spec Proposal
### Using HTTP URL
- It is well-structured - so it is easy to parse
- HTTP URLs are transporting successfully information for many years.
- We have great knowledge of it - many lib exist
### Several errors management
URL could be separated by ';'
### Convention
- __Error Data__ : `ERROR_URL_1;ERROR_URL_2`
- __ERROR_URL__  : `ERROR_ORIGINATION_HOST/unique_error_code/tracer_1/tracer_2?context=context_value`
- __ERROR_ORIGINATION_HOST__: `http://port_name.protocol.route.service.namespace.env_type.env` 

__ERROR_ORIGINATION_HOST__ is inspired by Kubernetes DNS. Values on the left are more specifics.


### Java example

```java
import com.squareup.okhttp.HttpUrl;

class Main {
  public static void main(String[] args) {
    String erroData = "http://port_name1.protocol1.service1.namespace1.svc1.cluster1.local/unique_error_code1/trace_id1?context11=cute%20%23puppies1&context12=images1;http://port_name2.protocol2.service2.namespace2.svc2.cluster2.local/unique_error_code2/trace_id2?context12=cute%20%23puppies2&context2=images2";
    String[] splittedErrors = erroData.split(";");
    for (int i = 0, size = 2; i < size; i++) {
      System.out.println ("====================================");
      System.out.println("Parsing: " + splittedErrors[i]);
      System.out.println ("----------------Start-----------------");
       parse(splittedErrors[i]);
       System.out.println("================End====================");
    }
  }

  public static void parse(String urlLike) {
    HttpUrl url = HttpUrl.parse(urlLike);
    System.out.println("origin: "+ url.host());
    System.out.println("code: "+ url.pathSegments().get(0));
    System.out.println("tracer: "+ url.pathSegments().get(1));
    for (int i = 0, size = url.querySize(); i < size; i++) {
      System.out.println(url.queryParameterName(i) + ": " + url.queryParameterValue(i));
    }
  }
}

```
