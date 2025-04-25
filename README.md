# 10101 (_Ten-Ten-One_) - Decentralised finance. For real.

<img href="https://matrix.to/#/#tentenone:matrix.org" alt="10101 dev chat" src="https://img.shields.io/matrix/tentenone%3Amatrix.org">

<p align="center">
  <img height="300" src="./logos/1500x1500.png" alt="10101 Logo">
</p>

10101 combines the power of a self-custodial on-chain and off-chain wallet with the vast world of trading. 10101 - a numeral palindrome and the binary representation of 21 - as in 21 million possible bitcoin. The vision of 10101 embodies what Bitcoin stands for: Decentralized and censorship resistant money.

## Getting Started

To begin, ensure that you have a working installation of the following items:

- [Docker](https://docs.docker.com/) and docker-compose
- [Rust language](https://rustup.rs/)
- Appropriate [Rust targets](https://rust-lang.github.io/rustup/cross-compilation.html) for cross-compiling to your device
- For Android targets:
  - Install [cargo-ndk](https://github.com/bbqsrc/cargo-ndk#installing)
  - Install Android NDK 22, then put its path in one of the `gradle.properties`, e.g.:

```
echo "ANDROID_NDK=.." >> ~/.gradle/gradle.properties
```

- For iOS targets:
  - XCode
  - Cocoapods

## Contributing

We encourage community contributions whether it be a bug fix or an improvement to the documentation.
Please have a look at the [contributing guidelines](./CONTRIBUTING.md).

## Dependencies

A lot of complexity for building the app has been encapsulated in a [just](justfile)-file.
You can install `just` with `cargo install just`.

To see the available commands with explanations, simply run `just --list`.

To install necessary project dependencies for all targets, run the following:

```sh
just deps
```

### Diesel database dependencies

Some crates, e.g. the coordinator use [`diesel`](https://diesel.rs/guides/getting-started) for the database connection.
This may require installing dependencies, such as e.g. `libpql` for the postgres database for the coordinator.

#### MacOS

On macOS, one can install `libpq` with the following command:

```sh
brew install libpq
```

Bear in mind that `libpq` is keg-only (not installed globally). This means that you have to add the library path the linker manually.
The are a number ways to do that (e.g. by setting rustflags), however the easiest one is to add the following lines to your `.zshrc`/`.bashrc`

```sh
export LDFLAGS="-L/usr/local/opt/libpq/lib"
export CPPFLAGS="-I/usr/local/opt/libpq/include"
```

This will ensure that `libpq` is available during building the project

## Running 10101

### Run the app natively (on your Linux/MacOS/other OS)

The following command will build and start all the necessary services, including the native desktop 10101 app.

```bash
just all
```

### Run the mobile-app on the iOS simulator

Note: Ensure that the iOS simulator is running on your machine so it can be selected as target.

The following command will build and start all the necessary services, including the native desktop 10101 app.

```bash
just all-ios
```

### Run the mobile-app on the Android simulator

Note: Ensure that the Android simulator is running on your machine so it can be selected as target.
Also ensure that you have run `just deps-android` to install the right targets for build.

The following command will build and start all the necessary services, including the android app.

```bash
just all-android
```

### How to faucet your wallet.

You can test the app on `regtest`, which means that the wallet needs to be fauceted with the provided steps before you can start trading.

#### Setup

1. If you have run the app before, we recommend to clear the dev environment by running `just wipe`

2. Start the complete project stack with `just all`.

#### Adding funds to 10101 wallet

1. Navigate to the receive screen.

2. Double-click on the generated QR code and click the "Pay with 10101 faucet" button. Note, if you do not specify an amount by
   default 1 BTC will sent to your regtest wallet.

#### Useful information for local regtest debugging

1. Follow coordinator's logs - `tail -f data/coordinator/regtest.log`
2. Block explorer - http://localhost:8080/
3. Bitcoin faucet - http://localhost:8080/faucet/

## Deploy for android beta

1. Create a `./mobile/android/key.properties` with the content from the key generation step from here https://docs.flutter.dev/deployment/android#signing-the-app
2. `just clean` never hurts but might not be necessary ;)
3. `just gen`
4. `just android-release`
5. `NETWORK=regtest just build-android-app-bundle`
6. `NETWORK=regtest just upload-app-bundle`

TL;DR;
a shortcut for this is available but it is recommended to execute each step separately:

```bash
just release-app-bundle-signet
```


------
# 10101（_Ten-Ten-One_）- 去中心化金融。真正的。

<img href="https://matrix.to/#/#tentenone:matrix.org" alt="10101 開發者聊天" src="https://img.shields.io/matrix/tentenone%3Amatrix.org">

<p align="center">
<img height="300" src="./logos/1500x1500.png" alt="10101 標誌">
</p>

10101 將自託管鏈上和鏈下錢包的功能與廣闊的交易世界結合在一起。 10101——數字回文和 21 的二進位表示——例如可能有 2100 萬個比特幣。 10101 的願景體現了比特幣的宗旨：去中心化、抗審查的貨幣。

＃＃ 入門

首先，請確保您已安裝以下項目：

- [Docker](https://docs.docker.com/) 與 docker-compose
- [Rust 語言](https://rustup.rs/)
- 適當的 [Rust 目標](https://rust-lang.github.io/rustup/cross-compilation.html) 用於交叉編譯到你的設備
- 對於 Android 目標：
- 安裝 [cargo-ndk](https://github.com/bbqsrc/cargo-ndk#installing)
- 安裝 Android NDK 22，然後將其路徑放入 `gradle.properties` 之一中，例如：

```
回顯“ANDROID_NDK = ..”>>〜/ .gradle / gradle.properties
```

- 對於 iOS 目標：
-XCode
- Cocoapods

## 貢獻

我們鼓勵社區做出貢獻，無論是修復錯誤還是改進文件。
請查看[貢獻指南](./CONTRIBUTING.md)。

依賴項

建置應用程式的許多複雜性已被封裝在 [just](justfile) 檔案中。
您可以使用“cargo install just”來安裝“just”。

要查看帶有解釋的可用命令，只需執行“just --list”。

若要為所有目標安裝必要的專案依賴項，請執行以下命令：

```sh
只是 deps
```

### Diesel 資料庫依賴項

有些板條箱，例如協調器使用 [`diesel`](https://diesel.rs/guides/getting-started) 進行資料庫連線。
這可能需要安裝依賴項，例如協調器的 postgres 資料庫的 `libpql`。

MacOS

在 macOS 上，可以使用以下命令安裝「libpq」：

```sh
brew 安裝 libpq
```

請記住，「libpq」僅適用於 keg（未全域安裝）。這意味著您必須手動新增連結器的庫路徑。
有多種方法可以做到這一點（例如透過設定 rustflags），但最簡單的方法是將以下幾行新增到你的 `.zshrc`/`.bashrc`

```sh
導出 LDFLAGS="-L /usr/local/opt/libpq/lib"
導出 CPPFLAGS="-I /usr/local/opt/libpq/include"
```

這將確保在建置專案期間可以使用“libpq”

## 運行 10101

### 本機運行應用程式（在您的 Linux/MacOS/其他作業系統上）

以下命令將建置並啟動所有必要的服務，包括原生桌面 10101 應用程式。

『`bash
只是全部
```

### 在 iOS 模擬器上執行行動應用程式

注意：確保 iOS 模擬器在您的機器上運行，以便可以將其選為目標。

以下命令將建置並啟動所有必要的服務，包括原生桌面 10101 應用程式。

『`bash
僅限所有 iOS
```

### 在 Android 模擬器上運行行動應用程式

注意：確保 Android 模擬器正在您的機器上運行，以便可以將其選為目標。
還要確保您已經運行“just deps-android”來安裝正確的建置目標。

以下命令將建置並啟動所有必要的服務，包括 android 應用程式。

『`bash
全部都是安卓系統
```

### 如何挖掘你的錢包。

您可以在“regtest”上測試該應用程序，這意味著您需要按照提供的步驟對錢包進行操作，然後才能開始交易。

#### 設定

1. 如果您之前曾執行過該應用程序，我們建議透過執行「just wipe」來清除開發環境

2. 使用「just all」啟動完整的專案堆疊。

#### 在 10101 年錢包中添加資金

1. 導航至接收螢幕。

2. 雙擊產生的二維碼，點選「使用10101水龍頭支付」按鈕。請注意，如果您沒有指定金額
預設 1 BTC 將發送到您的 regtest 錢包。

#### 本地 regtest 調試的有用信息

1. 追蹤協調器的日誌 - `tail -f data/coordinator/regtest.log`
2. 區塊瀏覽器 - http://localhost:8080/
3.比特幣水龍頭 - http://localhost:8080/faucet/

## 部署 Android Beta 版

1. 使用金鑰產生步驟中的內容建立 `./mobile/android/key.properties`，網址：https://docs.flutter.dev/deployment/android#signing-the-app
2.「只是清潔」永遠不會有害，但可能沒有必要;)
3. `just gen`
4. `僅 android-release`
5. `NETWORK=regtest just build-android-app-bundle`
6. `NETWORK=regtest 只是上傳應用程式包`

TL;DR;
可以使用快捷方式，但建議分別執行每個步驟：

『`bash
只需發布應用程式包簽名
```
