## custom-fsharp application

### Init

```bash
$ s init custom-fsharp -p alibaba

Initializing......
Initialization successfully
```

### Deploy

```bash
$ cd custom-fsharp && s deploy

Start ...
It is detected that your project has the following project/projects < MyFunctionDemo > to be execute
Start executing project MyFunctionDemo
Start the pre-hook
[Hook / Plugin] make build
Executing ...
Execute:
docker run --rm -i -v $(pwd):/tmp mcr.microsoft.com/dotnet/core/sdk:3.1 bash -c "cd /tmp/FSharpDemo && dotnet publish -r linux-x64 -c Release --self-contained true && cd /tmp/FSharpDemo/bin/Release/netcoreapp3.1/linux-x64/publish && mv FSharpDemo bootstrap && chmod +x bootstrap"
Microsoft (R) Build Engine version 16.7.1+52cd83677 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Determining projects to restore...
  Restored /tmp/FSharpDemo/FSharpDemo.fsproj (in 6.1 sec).
  FSharpDemo -> /tmp/FSharpDemo/bin/Release/netcoreapp3.1/linux-x64/FSharpDemo.dll
  FSharpDemo -> /tmp/FSharpDemo/bin/Release/netcoreapp3.1/linux-x64/publish/

End the pre-hook
Waiting for service custom-runtime-demo to be deployed...
Service custom-runtime-demo deploy success

Waiting for function custom-fsharp to be deployed...
Packing ...
Package complete.
Function: custom-runtime-demo@custom-fsharp creating ...
Deploy function custom-fsharp successfully
function custom-fsharp deploy success

Trigger: custom-runtime-demo@custom-fsharphttp_t deploying ...
This domain name is a temporary domain name. It is only used as a learning test and cannot be used in production environment.
```

### Invoke

The temporary domain name is `37342198-1986114430573743.test.functioncompute.com` in the example above, which could be found on the page of custom domain on the [Function Computer Console](https://fc.console.aliyun.com/).

The route is `weatherforecast` in the example and you can curl `${custom_domain}/weatherforecast` as follows.

```bash
$ curl 37342198-1986114430573743.test.functioncompute.com/weatherforecast
[{"date":"2020-12-07T12:00:13.7163832+00:00","temperatureC":29,"summary":"Mild","temperatureF":84},{"date":"2020-12-08T12:00:13.7181098+00:00","temperatureC":17,"summary":"Warm","temperatureF":62},{"date":"2020-12-09T12:00:13.7181208+00:00","temperatureC":35,"summary":"Freezing","temperatureF":94},{"date":"2020-12-10T12:00:13.7181242+00:00","temperatureC":1,"summary":"Balmy","temperatureF":33},{"date":"2020-12-11T12:00:13.7181246+00:00","temperatureC":-10,"summary":"Freezing","temperatureF":15}]
```