## Setup instruction

Install clang first.

### Method 1 - Clone this repo directly

1. Clone this repo:

	```bash
	rm -rf package/feeds
	git clone --depth=1 https://github.com/me-zjc/openwrt-feeds.git package/feeds
	```

2. Pull upstream commits:

	```bash
	git -C package/feeds pull
	```

- Remove

  ```bash
  rm -rf package/feeds
  ```

### Method 2 - Add this repo as a git submodule

1. Add new submodule:

	```bash
	rm -rf package/feeds
	git submodule add -f --name feeds https://github.com/me-zjc/openwrt-feeds.git package/feeds
	```

2. Pull upstream commits:

	```bash
	git submodule update --remote package/feeds
	```

- Remove

  ```bash
  git submodule deinit -f package/feeds
  git rm -f package/feeds
  git reset HEAD .gitmodules
  rm -rf .git/modules{/,/package/}feeds
  ```

### Method 3 - Add this repo as an OpenWrt feed

1. Add new feed:

	```bash
	sed -i "/feeds/d" "feeds.conf.default"
	echo "src-git feeds https://github.com/fw876/feeds.git" >> "feeds.conf.default"
	```

2. Pull upstream commits:

	```bash
	./scripts/feeds update feeds
	./scripts/feeds install -a -f -p feeds
	```

- Remove

  ```bash
  sed -i "/feeds/d" "feeds.conf.default"
  ./scripts/feeds clean
  ./scripts/feeds update -a
  ./scripts/feeds install -a
  ```

### Note

#### ⚠ For OpenWrt 21.02 or lower version
You have to manually upgrade Golang toolchain to [1.21](https://github.com/openwrt/packages/tree/openwrt-23.05/lang/golang) or higher to compile Xray-core.


