## Investigation for etcd

### Start etcd service

Download etcd from [etcd release](https://github.com/coreos/etcd/releases),
then start etcd. For simple test issue, just run `./etcd` to start.

### Run simple function test

```
$ go run main.go
TestSingle: ok
TestBulk: ok
TestTxn: ok
TestWatch: ok
TestLock: ok
TestLease: ok
```

### Run function test using go test
```
$ cd etcd
$ go test -v
=== RUN   Test_BulkPutDelete_1
--- PASS: Test_BulkPutDelete_1 (0.03s)
       	bulk_test.go:56: bulk put bulk query delete pass
=== RUN   Test_PutQueryDelete
--- PASS: Test_PutQueryDelete (0.03s)
PASS
ok     	github.com/chenglch/investigation/etcd/etcd    	0.069s
```

### Run benchmark test
```
$ cd etcd
$ go test -test.bench=".*"
goos: darwin
goarch: amd64
pkg: github.com/chenglch/investigation/etcd/etcd
Benchmark_BulkPut_Count100-4           	     100       	  10260749 ns/op
Benchmark_BulkQuery_Count100-4         	    1000       	   1293056 ns/op
Benchmark_BulkDelete_Count100-4        	     100       	  10679618 ns/op
Benchmark_Put_Count1-4                 	     100       	  10389580 ns/op
Benchmark_Get_Count1-4                 	    5000       	    365238 ns/op
Benchmark_Delete_Count1-4              	     100       	  10222882 ns/op
Benchmark_PutOneThread_Count100-4      	       1       	1009137089 ns/op
Benchmark_PutMultiThread_Count100-4    	     100       	  15422256 ns/op
Benchmark_PutOneThread_Count500-4      	       1       	5226328923 ns/op
Benchmark_PutMultiThread_Count500-4    	      30       	  47461453 ns/op
Benchmark_Watch_Count1-4               	     200       	   9454095 ns/op
Benchmark_Watch_Count100-4             	     200       	   9759887 ns/op
PASS
ok     	github.com/chenglch/investigation/etcd/etcd    	43.047s
```