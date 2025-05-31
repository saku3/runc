# runc

runcのbatsのintegration testをyoukiで実行する

```rust
just youki-release
# runcのルートディレクトリに配置する
mv ./youki ../runc/runc

```

```rust
.PHONY: localintegration
localintegration: runc test-binaries # make runcを実行すると、runcバイナリがルートディレクトリにできるので、削除(別にbats -t tests/integrationを実行すれば良いだけかもしれない)
	bats -t tests/integration$(TESTPATH)

NO_COLOR=1 make localintegration > youki-localintegration.txt
NO_COLOR=1 make localintegration | tee youki-integration.log
```

修正

- youkiはコマンドを渡すときに — をつける必要があるのでテストbatsを修正
- 一旦sh -c → -- sh -cの置換をしたが、個別で見つけないといけない例がある