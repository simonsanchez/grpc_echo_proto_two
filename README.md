# General Notes on Package Versioning

The companion repo that implements the gRPC server lives [here](https://github.com/simonsanchez/grpc_echo_server).

# v0 and v1

The following workflows apply to `v0` and `v1` releases. This assumes all development is happening on the `main` branch for `grpc_echo_proto_two`.

`v2+` are handled separately.

## Workflow

- Make changes
- `git tag` the commit
- Push up the code and the tag
- In the repo that contains the server implementation, update to the latest or to a specific version.

## Update to the latest

go get github.com/simonsanchez/grpc_echo_proto_two@latest

## Update to specific version

go get github.com/simonsanchez/grpc_echo_proto_two@v0.2.0

# v2 and Beyond

These packages are handled _very_ differently. I followed the exact steps recommended in [Google's blog](https://blog.golang.org/v2-go-modules) and it worked like a charm (although feels a bit janky).

tl;dr

- Create a subdirectly in the root folder `./v2`.
- Copy over all existing files into the subdirectory.
- Update `./v2/go.mod` to use the new suffix.
- In `./v2/echo.proto` update the import path used in `go_package` to also use the `/v2` suffix.
- Compile the new proto change
- Tag the release and push everything up.
- In the repo that contains the server implemention, update with

```
go get github.com/simonsanchez/grpc_echo_proto_two/v2
```

# Git Tagging

## List

```
# local tags
git tag -n
```

## Tag a commit

```
git tag -a <TAG> -m "Helpful message here plz"
```

## Pushing to remote

Tags are pushed separately.

```
# push up the code
git push origin main

# push up the tag
git push origin <TAG>
```

## Removing tags

Tags are removed from local and remotes separately.

```
# remove from local
git tag -d <TAG>

# remove from remote
git push --delete origin <TAG>
```
