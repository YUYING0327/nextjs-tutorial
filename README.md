# Routing with Pages

在 pages 檔案夾新增檔案，如 about.js 就會產生新的頁面 /about

# Nested Routes

在 pages 檔案夾新增一個 blog 的檔案夾，新增 index.js 會是一個新的頁面，而此頁面的路徑將會跟檔案夾名稱一樣(blog)。這樣就可以在這路徑下(/blog)新增其他頁面，例如 first.js 路徑將會是(/blog/first)

# Dynamic Routes

假設我們需要一個我們需要一個產品列的頁面(/product)，但使用者可以添加 id 路徑 (/product/id) 看到單一產品的詳細資料 例如 (/product/1)

1. 在 pages 檔案夾新增一個 product 的檔案夾，且新增 index.js (/product)
2. 新增一個有方括號的檔案 [productId].js，在 /product/ 後可以加任何字。
3. 為了讓頁面對應到 id 要使用 useRouter hook
   導入 hook => import { useRouter } from 'next/router'
   創建一個 router 來使用 useRouter => const router = useRouter();
   創建 productId => const productId = router.query.productId;

## 4. 到目前為止，/id 的部分是可以隨意打得，所以我們可以再新增隨意一個檔，例如 sweater.js 此時，在/product/ 後面打 sweater 將會導向 sweater.js 的內容，因為 nextjs 會優先找到 Routes wiht Pages

# Nested Dynamic Routes

1. 在 product 資料夾裡面新增 [productId] 的資料夾，並把 [productId].js 改放進 [productId] 裡面改名為 index.js 這邊不會影響原本的動作
2. 在 product 資料夾裡面新增 review 的資料夾，再新增 [review].js 檔
3. 使用 useRouter
   創建一個 router 來使用 useRouter => const router = useRouter();
   const { productId, reviewId } = router.query;
   return Review {reviewId} for product {productId}
4. 現在到 /product/1/review/1

# Catch All Routes

1. 在 pages 檔案夾新增一個 docs 的檔案夾，並新增 [...params].js 的檔案
   現在，在 /product/ 後可以一直加路徑 /product/1/2/3/4/5 都會看到 home page
2. 使用 useRouter
   const router = useRouter();
   const { params } = router.query;
   現在使用 console.log 來查看 params，會看到一組 array(5)，項目即是 1,2,3,4,5
   但是最初渲染出來的 params 是 undefined
   所以我們要讓 params 一開始為 array => const { params = [] } = router.query;來避免發生問題
3. if (params.length === 2) {
   return (
      <h1>
      Viewing docs for feature {params[0]} and concept {params[1]}
      </h1>
      );
   } else if (params.length === 1) {
      return <h1>Viewing docs for feature {params[0]}</h1>;
   }

   return <h1>Docs Home Page</h1>;

   試試 http://localhost:3000/docs/feature1
   http://localhost:3000/docs/feature1/concept1

4. 現在如果到 http://localhost:3000/docs 將會看到 404 找不到頁面的畫面
   可以在 [...params].js 多加括號 [[...params].js]

# Link Component Navigation

1. 在主頁面 index.js 導入 Link => import Link from 'next/link';
2. 這樣就可以使用 Link 標籤 <Link></Link>
   <Link href="/blog">
        <a>Blog</a>
   </Link>
   注意的是，nextjs 用 Link href要放在 Link 標籤裡面
