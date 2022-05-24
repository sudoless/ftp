# goftp

A FTP client package for Go. Forked from [jlaffaye/ftp](https://github.com/jlaffaye/ftp).

## Install

```
go get -u github.com/jlaffaye/ftp
```

## Documentation

https://pkg.go.dev/github.com/jlaffaye/ftp

## Example

### Simple

```go
c, err := ftp.Dial("ftp.example.org:21", ftp.DialWithTimeout(5*time.Second))
if err != nil {
    log.Fatal(err)
}

err = c.Login("anonymous", "anonymous")
if err != nil {
    log.Fatal(err)
}

// Do something with the FTP conn

if err := c.Quit(); err != nil {
    log.Fatal(err)
}
```

### Store a file

```go
data := bytes.NewBufferString("Hello World")
err = c.Stor("test-file.txt", data)
if err != nil {
	panic(err)
}
```

### Read a file

```go
r, err := c.Retr("test-file.txt")
if err != nil {
	panic(err)
}
defer r.Close()

buf, err := ioutil.ReadAll(r)
println(string(buf))
```

## TODO

- [ ] Remove third party dependencies
- [ ] Increase test coverage
