---
title: 对象检测 - 计算机视觉
titleSuffix: Azure Cognitive Services
description: 与使用计算机视觉 API 检测对象相关的概念。
services: cognitive-services
author: PatrickFarley
manager: cgronlun
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: conceptual
ms.date: 12/03/2018
ms.author: pafarley
ms.custom: seodec18
ms.openlocfilehash: 89323e584b4020613fe3ff8411df50f2ab96f156
ms.sourcegitcommit: 7cd706612a2712e4dd11e8ca8d172e81d561e1db
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53582722"
---
# <a name="object-detection"></a>对象检测

对象检测类似于[标记](concept-tagging-images.md)，但是 API 返回找到的每个对象的边框坐标（以像素为单位）。 例如，如果图像包含狗、猫和人，检测操作将列出这些对象及其在图像中的坐标。 可以使用此功能处理图像中对象之间的关系。 还可以确定图像中是否有多个相同标记的实例。

检测 API 根据图像中识别到的对象或生物应用标记。 请注意，用于标记的分类与用于对象检测的分类之间现在没有正式关系。 从概念上讲，检测 API 仅查找对象和生物，而标记 API 还可以包含诸如“室内”等上下文术语，这些术语不能使用边界框进行本地化。

## <a name="object-detection-example"></a>对象检测示例

以下 JSON 响应表明计算机视觉在示例图像中检测对象时所返回的内容。

![一位正在厨房中使用 Microsoft Surface 设备的女士](./Images/windows-kitchen.jpg)

```json
{
   "objects":[
      {
         "rectangle":{
            "x":730,
            "y":66,
            "w":135,
            "h":85
         },
         "object":"kitchen appliance",
         "confidence":0.501
      },
      {
         "rectangle":{
            "x":523,
            "y":377,
            "w":185,
            "h":46
         },
         "object":"computer keyboard",
         "confidence":0.51
      },
      {
         "rectangle":{
            "x":471,
            "y":218,
            "w":289,
            "h":226
         },
         "object":"Laptop",
         "confidence":0.85,
         "parent":{
            "object":"computer",
            "confidence":0.851
         }
      },
      {
         "rectangle":{
            "x":654,
            "y":0,
            "w":584,
            "h":473
         },
         "object":"person",
         "confidence":0.855
      }
   ],
   "requestId":"a7fde8fd-cc18-4f5f-99d3-897dcd07b308",
   "metadata":{
      "width":1260,
      "height":473,
      "format":"Jpeg"
   }
}
```

## <a name="next-steps"></a>后续步骤

了解[对图像进行分类](concept-categorizing-images.md)和[描述图像](concept-describing-images.md)的概念。