# 擴充套件更多

但是如果我們想要擴充套件到六個節點以上應該怎麼辦？

主分片的數量在索引建立的時候就已經指定了，實際上，這個數字定義了能**儲存**到索引中的資料最大量（具體的數量取決於你的資料，硬體的使用情況）。例如，讀請求——搜尋或者文件恢復就可以由主分片或者從分片來執行，所以當你擁有更多份資料的時候，你就擁有了更大的吞吐量。

從分片的數量可以在執行的叢集中動態的調整，這樣我們就可以根據實際需求擴充套件或者縮小規模。接下來，我們來增加一下從分片組的數量：

```Js
PUT /blogs/_settings
{
   "number_of_replicas" : 2
}
```

增加`number_of_replicas`到2：
![三節點兩從叢集](../images/02-05_replicas.png)

從圖中可以看出，現在 `blogs` 的索引總共有9個分片：3個主分片和6個從分片。也就是說，現在我們就可以將總節點數擴充套件到9個，就又會變成一個節點一個分片的狀態了。最終我們得到了三倍搜尋效能的三節點叢集。

****
> ### 提示

當然，僅僅是在同樣數量的節點上增加從分片的數量是根本不能提高效能的，因為每個分片都有訪問系統資源的許可權。你需要升級硬體配置以提高吞吐量。

不過更多的從分片意味著我們有更多的冗餘：通過上文的配置，我們可以承受兩個節點的故障而不會丟失資料。

****
