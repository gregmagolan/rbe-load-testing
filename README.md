# Prep for test

Install [bazelisk](https://github.com/bazelbuild/bazelisk) (puts `bazel` on the path).

Run,

```
bazel build //...
```

If authenticating using credential-helper run,

```
credential-helper login aw-remote-ext.aws.silo.aspect.build
```

# Run test against silo

Increase CACHE_BUST value each test run to avoid cache hits from previous tests.

## ALB

```
time bazel test //... --config=ext-rbe-silo-alb --test_env=CACHE_BUST=1
```

## NLB

```
time bazel test //... --config=ext-rbe-silo-nlb --test_env=CACHE_BUST=1
```

## Other cluster

Change `other.cluster.com` in `.bazelrc` to the GRPC URL of the test cluster.

```
time bazel test //... --config=ext-rbe-other --test_env=CACHE_BUST=1
```
