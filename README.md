# protoc-gen-prost-bug

Steps to reproduce:

```
cd protoc-gen-prost-crate
cargo build
cd ..

buf generate
```

Error output:
```
panic: runtime error: slice bounds out of range [:-1]

goroutine 1 [running]:
github.com/bufbuild/buf/private/pkg/app/appproto.writeInsertionPoint({0x103f55ac8?, 0x103f55ac8?}, 0x1400004ebe0, {0x12cf73090?, 0x140005c7e00?})
        github.com/bufbuild/buf/private/pkg/app/appproto/response_writer.go:145 +0x354
github.com/bufbuild/buf/private/pkg/app/appproto.applyInsertionPoint({0x103f55ac8, 0x140005c7980}, 0x1400004ebe0, {0x103f517f0?, 0x140006869a0?}, {0x12cd9a5f8, 0x140006869a0})
        github.com/bufbuild/buf/private/pkg/app/appproto/response_writer.go:83 +0xf0
github.com/bufbuild/buf/private/pkg/app/appproto.(*responseWriter).WriteResponse(0x1?, {0x103f55ac8, 0x140005c7980}, {0x12cd9a5f8, 0x140006869a0}, 0x1400004ec80, {0x14000010350, 0x1, 0x29?})
        github.com/bufbuild/buf/private/pkg/app/appproto/response_writer.go:56 +0x114
github.com/bufbuild/buf/private/pkg/app/appproto/appprotoos.(*responseWriter).writeDirectory(0x140005591f0, {0x103f55ac8?, 0x140005c7980}, 0x10375a4e4?, {0x140006a0720, 0x29}, 0x1)
        github.com/bufbuild/buf/private/pkg/app/appproto/appprotoos/response_writer.go:262 +0x2b8
github.com/bufbuild/buf/private/pkg/app/appproto/appprotoos.(*responseWriter).addResponse(0x140000fc7ab?, {0x103f55ac8?, 0x140005c7980?}, 0x10375a364?, {0x140006a0720?, 0x103d1b780?}, 0x1?)
        github.com/bufbuild/buf/private/pkg/app/appproto/appprotoos/response_writer.go:163 +0xcc
github.com/bufbuild/buf/private/pkg/app/appproto/appprotoos.(*responseWriter).AddResponse(0x140005591f0, {0x103f55ac8, 0x140005c7980}, 0x140004cb430?, {0x140000fc7ab?, 0x14000686020?})
        github.com/bufbuild/buf/private/pkg/app/appproto/appprotoos/response_writer.go:111 +0xcc
github.com/bufbuild/buf/private/buf/bufgen.(*generator).generate(0x140004b8040, {0x103f55ac8, 0x140005c7980}, {0x12cd98108, 0x140005b92c0}, 0x1400013da40, {0x103f514f0, 0x14000686020}, {0x1037ed9c3, 0x1}, ...)
        github.com/bufbuild/buf/private/buf/bufgen/generator.go:141 +0x21c
github.com/bufbuild/buf/private/buf/bufgen.(*generator).Generate(0x14000122d10?, {0x103f55ac8, 0x140005c7980}, {0x12cd98108, 0x140005b92c0}, 0x140005b92c0?, {0x103f514f0, 0x14000686020}, {0x140004cb6e0, 0x1, ...})
        github.com/bufbuild/buf/private/buf/bufgen/generator.go:91 +0xc0
github.com/bufbuild/buf/private/buf/cmd/buf/command/generate.run({0x103f55ac8, 0x140005c7980}, {0x103f69b50, 0x140005b92c0?}, 0x140000bd340)
        github.com/bufbuild/buf/private/buf/cmd/buf/command/generate/generate.go:355 +0x80c
github.com/bufbuild/buf/private/buf/cmd/buf/command/generate.NewCommand.func1({0x103f55ac8?, 0x140005c7980?}, {0x103f69b50?, 0x140005b92c0?})
        github.com/bufbuild/buf/private/buf/cmd/buf/command/generate/generate.go:176 +0x30
github.com/bufbuild/buf/private/buf/bufcli.NewErrorInterceptor.func1.1({0x103f55ac8?, 0x140005c7980?}, {0x103f69b50?, 0x140005b92c0?})
        github.com/bufbuild/buf/private/buf/bufcli/errors.go:92 +0x34
github.com/bufbuild/buf/private/pkg/app/appflag.(*builder).run(0x140004bb400, {0x103f55a20, 0x1400038db40}, {0x103f60cb0, 0x14000116280}, 0x14000610e20)
        github.com/bufbuild/buf/private/pkg/app/appflag/builder.go:145 +0x410
github.com/bufbuild/buf/private/pkg/app/appflag.(*builder).NewRunFunc.func1({0x103f55a20, 0x1400038db40}, {0x103f60cb0, 0x14000116280})
        github.com/bufbuild/buf/private/pkg/app/appflag/builder.go:97 +0x74
github.com/bufbuild/buf/private/pkg/app/appcmd.commandToCobra.func2(0x1400059b200?, {0x1048fb1b0?, 0x0, 0x0?})
        github.com/bufbuild/buf/private/pkg/app/appcmd/appcmd.go:288 +0x230
github.com/spf13/cobra.(*Command).execute(0x1400059b200, {0x1048fb1b0, 0x0, 0x0})
        github.com/spf13/cobra@v1.6.0/command.go:920 +0x5b0
github.com/spf13/cobra.(*Command).ExecuteC(0x1400059a000)
        github.com/spf13/cobra@v1.6.0/command.go:1040 +0x354
github.com/spf13/cobra.(*Command).Execute(...)
        github.com/spf13/cobra@v1.6.0/command.go:968
github.com/bufbuild/buf/private/pkg/app/appcmd.run({0x103f55a20, 0x1400038db40}, {0x103f60cb0?, 0x14000616d20?}, 0x140000a1500)
        github.com/bufbuild/buf/private/pkg/app/appcmd/appcmd.go:241 +0x6d0
github.com/bufbuild/buf/private/pkg/app/appcmd.Main.func1({0x103f55a20?, 0x1400038db40?}, {0x103f60cb0?, 0x14000616d20?})
        github.com/bufbuild/buf/private/pkg/app/appcmd/appcmd.go:110 +0x30
github.com/bufbuild/buf/private/pkg/app.Run({0x103f55a58?, 0x1400012a000?}, {0x103f60cb0?, 0x14000616d20}, 0x140006bff08)
        github.com/bufbuild/buf/private/pkg/app/app.go:299 +0x64
github.com/bufbuild/buf/private/pkg/app.Main({0x103f55a58, 0x1400012a000}, 0x103f44908?)
        github.com/bufbuild/buf/private/pkg/app/app.go:289 +0x8c
github.com/bufbuild/buf/private/pkg/app/appcmd.Main({0x103f55a58?, 0x1400012a000?}, 0x102c89594?)
        github.com/bufbuild/buf/private/pkg/app/appcmd/appcmd.go:91 +0x3c
github.com/bufbuild/buf/private/buf/cmd/buf.Main({0x1037ee09e?, 0x140000021a0?})
        github.com/bufbuild/buf/private/buf/cmd/buf/buf.go:86 +0x44
main.main()
        github.com/bufbuild/buf/cmd/buf/main.go:20 +0x28
```


protoc usage:
```
protoc --prost-crate_out=bufgen --prost-crate_opt=gen_crate=bufgen/Cargo.toml test.proto
```

Error output:

```
Cargo.toml: insertion point "features" not found.
```
