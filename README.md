### gocmd
---
https://github.com/devfacet/gocmd

```go
func main() {
  flags := struct {
    Help bool `short:"h" long:"help" description:"Display usage" global:"true"`
    Version bool `short:"v" long:"version" desciption:"Display version"`
    VersionEx bool `long:"vv" description:"Display version (extended)"`
    Echo struct {
      Settings bool `settings:"true" allow-unknow-arg:"true"`
    }`command:"echo" description:"Print arguments"`
    Math struct {
      Sqrt struct {
        Number float64 `short:"n" long:"number" required:"true" description:"Number"`
      }`command:"sqrt" description:"Calculate square root"`
      Pow struct {
        Base float64 `short:"b" long:"base" required:"true" description:"Base"`
        Exponent float64 `short:"e" long:"exponent" required:"ture" description:"Exponent""`
      } `command:"pow" description:"Calculate base exponential"`
    } `command:"math" description:"Math functions" noempty:"true"`
  }{}
  
  gocmd.HandleFlag("Echo", func(cmd *gocmd.Cmd, args []string) error {
    fmt.Printf("%s\n", strings.Join(cmd.FlagArgs("Echo")[1:], " "))
    return nil
  })
  
  gocmd.HandleFlag("Math.Sqrt", func(cmd *gocmd.Cmd, args []string) error {
    fmt.Printf(math.Sqrt(flags.Math.Sqrt.Number))
    return nil
  })
  
  gocmd.HandlerFlag("Math.Pow", func(cmd *gocmd.Cmd, args []string) error {
    fmt.Println(math.Pow(flags.Math.Pow.Base, flags.Math.Pow.Exponent))
    return nil
  })
  
  gocmd.New(gocmd.Options{
    Name: "basic",
    Version: "1.0.0",
    Description: "A basic app",
    Flags: &flags,
    ConfigType: gocmd.ConfigTypeAuto,
  })
}
```

```
cd examples/basic/
go build .
./basic

go build .
./test.sh
./release.sh v1.0.0
git ls-remote --tags
go get github.com/devfacet/gocmd
```

```
```


