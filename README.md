## Routing with Pages

在 pages 檔案夾新增檔案，如 about.js 就會產生新的頁面 /about

## Nested Routes

在 pages 檔案夾新增一個 blog 的檔案夾，新增 index.js 會是一個新的頁面，而此頁面的路徑將會跟檔案夾名稱一樣(blog)。這樣就可以在這路徑下(/blog)新增其他頁面，例如 first.js 路徑將會是(/blog/first)

## Dynamic Routes

假設我們需要一個我們需要一個產品列的頁面(/product)，但使用者可以添加 id 路徑 (/product/id) 看到單一產品的詳細資料 例如 (/product/1)

1. 在 pages 檔案夾新增一個 product 的檔案夾，且新增 index.js (/product)
2. 新增一個有方括號的檔案 [productId].js，在 /product/ 後可以加任何字。
3. 為了讓頁面對應到 id 要使用 useRouter hook
   導入 hook => import { useRouter } from 'next/router'
   創建一個 router 來使用 useRouter => const router = useRouter();
   創建 productId => const productId = router.query.productId;

# 4. 到目前為止，/id 的部分是可以隨意打得，所以我們可以再新增隨意一個檔，例如 sweater.js 此時，在/product/ 後面打 sweater 將會導向 sweater.js 的內容，因為 nextjs 會優先找到 Routes wiht Pages
