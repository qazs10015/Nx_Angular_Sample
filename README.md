## 透過 NX 建立 angular 專案並設定 i18n 心得

### 建立 Angular

使用 NX 建立 Angular 的專案不難，透過以下指令即可輕鬆建立(記得把 `{project name}`  改掉)

> npx create-nx-workspace@latest {project name} --preset=angular-monorepo

### 加入多語系套件

Angular 新增多語系的文章有很多，[官網網站有說明如何安裝套件](https://angular.io/guide/i18n-common-add-package)，也可以參考 [The Will Will Web](https://blog.miniasp.com/post/2024/01/27/Angular-Internationalization-i18n)，這篇很詳細的介紹流程，但是都只有針對 `Angular CLI` 建立的專案

以下是使用 NX 語法 `npx nx add @angular/localize --project=angular-monorepo-i18n` 建立多語系專案時出現的錯誤訊息，目前沒有找到解法(2024/03/01)

![image](https://gist.github.com/assets/30744341/b098d377-2dd5-4ef5-8f8a-8c0d9ee22356)

內容是指套件安裝成功了，但是使用 `ng add` 的方式還伴隨著初始化的動作，而且就是這一動失敗了!!

但是**已經比對過初始化的程式碼**新增了甚麼地方，整體上不影響多語系的流程與功能

### 設定多語系

[官方網站](https://angular.io/guide/i18n-common-prepare)有說明要如何放置 `i18n`，剛剛提到的 [The Will Will Web](https://blog.miniasp.com/post/2024/01/27/Angular-Internationalization-i18n#:~:text=%E7%9A%84%E8%AE%8A%E6%9B%B4%E8%A8%98%E9%8C%84%E3%80%82-,%E9%96%8B%E5%A7%8B%E5%B0%8D%E5%B0%88%E6%A1%88%E9%80%B2%E8%A1%8C%E6%9C%AC%E5%9C%B0%E5%8C%96%E7%BF%BB%E8%AD%AF,-%E5%9C%A8%20Template%20%E5%A5%97%E7%94%A8) 有提到怎麼寫，就不多做贅述

要補充的只有在 `*.ts` 內要使用 `$localize` 這語法的話，有兩種做法：

1. 需要額外 `import '@angular/localize/init'`，比較不推薦

    ![image](https://gist.github.com/assets/30744341/564bd8ba-9145-4141-8d85-242815cbf940)

2. `tsconfig.base.json`，避免整個專案不認識 `$localize` 這個關鍵字，也是相較之下比較推薦的做法

    ![image](https://gist.github.com/assets/30744341/ab82500c-4838-4b6e-8ad2-f9f8df57db81)

### 提取所有的多語系資料

在上一個步驟應該就已經準備好要翻譯的資訊了，接下來只要透過指令存取成一個檔案就好

在 Angular CLI 中可以很簡單的透過 `ng extract-i18n` 執行，但是在 NX 中這樣的指令無法正常執行

需要透過 NX 自己的指令，推薦安裝 VSCode 套件 - [Nx Console](https://marketplace.visualstudio.com/items?itemName=nrwl.angular-console)

透過 GUI 介面就可以快速知道指令的內容

![image](https://gist.github.com/assets/30744341/d49f966d-2c84-421d-ad59-d42ef697a268)

接下來步驟就跟一般的 Angular 專案流程沒有區別了！