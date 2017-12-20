# Cloud CLI Application

Application that provides a CLI to the KNoT Cloud.

## How to install and run meshblu cloud on local machine

1. Fill the knot-cloud-source/config.js file with gateway uuid and token in 68 and 69 lines. Also, setup parent connection on the same file in the 124 line, according format shown below:

```
parentConnection: {
  uuid: 'gateway_uuid',
  token: 'gateway_token',
  server: 'knot-test.cesar.org.br',
  port: 3000
  knotCloudUuid: 'gateway_uuid'
}
```

2. Install all dependencies, running:

> `npm install`

3. Then, run the cloud:

> `node server.js --http`

## How to use CLI Application

Let's take the following uuid and token as owner credentials:

- uuid: a585b687-1166-4dab-a4e8-5654274f0000
- token: 9d9e193c7bb3f8c1c45e28524f2d5cc353bcbe4b

The examples below will show how to use all CLI commands

To show a list of available commands:
> `node cli.js -h`

To create a thing in your gateway use:

> `node cli.js -s 127.0.0.1 -u a585b687-1166-4dab-a4e8-5654274f0000 register thing1`

To get the things from your gateways use:
> `node cli.js -u a585b687-1166-4dab-a4e8-5654274f0000 -t 9d9e193c7bb3f8c1c45e28524f2d5cc353bcbe4b devices`

With the return of command above use `getdata` and `data` to see the data stored on cloud:
> `node cli.js -s 172.24.15.213  -u a585b687-1166-4dab-a4e8-5654274f0000 -t 9d9e193c7bb3f8c1c45e28524f2d5cc353bcbe4b getdata 3a14a87f-45ac-4c1c-8620-0e6c31520007 1`

The command above are requesting data to sensor with ID 1 from thing `3a14a87f-45ac-4c1c-8620-0e6c31520007`

> `node cli.js -s 172.24.15.213  -u a585b687-1166-4dab-a4e8-5654274f0000 -t 9d9e193c7bb3f8c1c45e28524f2d5cc353bcbe4b data 3a14a87f-45ac-4c1c-8620-0e6c31520007 1`

And the command above return the list of data from sensor 1

You can set the data too:
> `node cli.js -s 172.24.15.213  -u a585b687-1166-4dab-a4e8-5654274f0000 -t 9d9e193c7bb3f8c1c45e28524f2d5cc353bcbe4b setdata 3a14a87f-45ac-4c1c-8620-0e6c31520007 1 true`

You can even update the thing's config:
> `node cli.js -s 172.24.15.213  -u a585b687-1166-4dab-a4e8-5654274f0000 -t 9d9e193c7bb3f8c1c45e28524f2d5cc353bcbe4b setconfig 3a14a87f-45ac-4c1c-8620-0e6c31520007 1 true`

The default config being sent is:
```json
"config":[{
    "event_flags": 8,
    "time_sec": 0,
    "lower_limit": 0,
    "upper_limit": 0
}]
```
but you can change it by using the options:
```
--event-flag or -f
--time or -T
--lower-limit or -l
--upper-limit or -L
```
 available in application

 as an example you can change the config to send sensor data each 10 seconds

> `node cli.js -s 172.24.15.213  -u a585b687-1166-4dab-a4e8-5654274f0000 -t 9d9e193c7bb3f8c1c45e28524f2d5cc353bcbe4b setconfig 3a14a87f-45ac-4c1c-8620-0e6c31520007 1 true -f 1 -T 10`
