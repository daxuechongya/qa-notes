# 📝 Flux Generate API 测试笔记

## 1. 接口信息

-   **URL**:\
    `POST https://hub.vidaxl.io/api/v1/images/generation/generate`

-   **用途**:\
    调用 Flux AI，根据 **WBG 图 + prompt** 生成场景图。

------------------------------------------------------------------------

## 2. 必填参数

请求体 JSON 格式：

``` json
{
  "promptName": "your_prompt_name",   // 必填，生成任务名
  "sku": "123456",                    // 必填，商品 SKU
  "prompt": "your generation prompt", // 必填，描述要生成的场景
  "aiServiceType": "flux",            // 必填，指定服务类型
  "imageUrl": "http://..."            // 必填，白底图(WBG)地址
}
```
