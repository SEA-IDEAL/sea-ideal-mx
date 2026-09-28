# MX 墨西哥选品站点

这是一个无需构建的静态 GitHub Pages 项目，页面从 `assets/products.csv` 读取墨西哥商品数据。它应部署到独立的 MX 仓库，不要覆盖现有的 SA 站点。

页面默认使用西班牙语，可切换 English 或中文。商品列表支持搜索、店铺浏览、佣金筛选、价格和佣金排序。类目筛选暂时隐藏，因为当前 MX 数据没有类目字段。

商品详情可将商品加入选品池。选品池按商品 ID 去重，显示并支持一键复制全部商品 ID。语言和选品池分别保存在浏览器的 `sea-ideal-mx-language` 与 `sea-ideal-mx-selection-pool` 中，不会与 SA 站点共用本地数据。

## 数据文件

站点读取 `assets/products.csv`，表头为：

```csv
row,product_name,price,shop,link,image_url,sheet_name,commission
```

当前文件由 `C:\Users\HI\Downloads\products_mx.csv` 转换而来：

- `商品 ID` → `row`
- `商品名称` → `product_name`
- `售价` → `price`，页面数据使用 `MX$` 明确表示墨西哥比索
- `店铺名称` → `shop` 和 `sheet_name`
- `商品链接` → `link`，使用左侧联盟链接
- `图片链接` → `image_url`
- `创作者佣金率` → `commission`

源文件是 GBK 编码，不是 UTF-8。浏览器端 CSV 已转换为 UTF-8，以正确显示西班牙语和中文；以后更新时也应先按同样映射转换，不能直接用原始导出文件覆盖 `assets/products.csv`。当前数据去除重复商品 ID 后有 293 条。

## 独立部署

1. 新建独立仓库，例如 `SEA-IDEAL/sea-ideal-mx`。
2. 将本目录中的 `index.html`、`app.jsx`、`csv.js`、`.nojekyll`、`assets/` 和 `README.md` 推送到新仓库的 `main` 分支。
3. 在新仓库打开 **Settings → Pages**，选择 **Deploy from a branch**，分支选 `main`，目录选 `/ (root)`。
4. 若仓库名为 `sea-ideal-mx`，默认项目站点地址是 `https://sea-ideal.github.io/sea-ideal-mx/`。只有仓库名为 `SEA-IDEAL.github.io` 时才是组织根站点，且同一组织只能有一个根站点。

本地预览必须通过 HTTP 服务访问，例如在项目根目录运行 `python -m http.server 8000`，再打开 `http://localhost:8000/`。直接双击 `index.html` 时，浏览器可能阻止读取 CSV。

CSV、图片和页面源文件在公开 GitHub Pages 仓库中均可下载，不要放入访问令牌或其他敏感数据。
