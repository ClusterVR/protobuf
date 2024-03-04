TMPDIR := tmp
PKGDIR := $(TMPDIR)/nuget
OUTDIR := outs

.PHONY: build
build: $(OUTDIR)/Google.Protobuf.dll $(OUTDIR)/System.Runtime.CompilerServices.Unsafe.dll

.PHONY: clean
clean:
	rm -rf $(TMPDIR) && rm -rf $(OUTDIR)

$(TMPDIR):
	mkdir -p $(TMPDIR)

$(OUTDIR):
	mkdir -p $(OUTDIR)

$(OUTDIR)/Google.Protobuf.dll:
	dotnet build ../csharp/src/Google.Protobuf/Google.Protobuf.csproj -c Release -f netstandard2.0 --output $(OUTDIR)

$(OUTDIR)/System.Runtime.CompilerServices.Unsafe.dll: $(OUTDIR)
	dotnet restore ../csharp/src/Google.Protobuf/Google.Protobuf.csproj --packages $(PKGDIR)
	# NOTE: it can be resolved to multiple versions, so we specify the version explicitly.
	cp -p $(PKGDIR)/system.runtime.compilerservices.unsafe/6.0.0/lib/netstandard2.0/System.Runtime.CompilerServices.Unsafe.dll $(OUTDIR)
