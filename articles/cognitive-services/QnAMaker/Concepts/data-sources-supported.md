---
title: 受支持的数据源 - QnA Maker
titleSuffix: Azure Cognitive Services
description: QnA Maker 从半结构化内容（例如常见问题解答、产品手册、指南、支持文档，以及以网页、PDF 文件或 MS Word 文档文件形式存储的策略）中自动提取问答对。 也可以将内容从结构化 QnA 内容文件添加到知识库中。
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 11/27/2018
ms.author: tulasim
ms.openlocfilehash: 71b0739bacd8df586267b61a9135f448aa76479d
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53082231"
---
# <a name="data-sources-for-qna-maker-content"></a>QnA Maker 内容的数据源

QnA Maker 从半结构化内容（例如常见问题解答、产品手册、指南、支持文档，以及以网页、PDF 文件或 MS Word 文档文件形式存储的策略）中自动提取问答对。 也可以将内容从结构化 QnA 内容文件添加到知识库中。 

下表汇总了 QnA Maker 支持的内容类型和文件格式。

|源类型|内容类型| 示例|
|--|--|--|
|代码|常见问题解答（平面，包含节或主题主页）|[普通的常见问题解答](https://docs.microsoft.com/azure/cognitive-services/qnamaker/faqs)、[带链接的常见问题解答](https://www.microsoft.com/software-download/faq)、[带主题主页的常见问题解答](https://support.microsoft.com/products/windows?os=windows-10)|
|PDF / DOC|常见问题解答、产品手册、小册子、论文、海报策略、支持指南、结构化 QnA，等等。|[Structured QnA.doc](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/semi-structured.docx)、[Sample Product Manual.pdf](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/product-manual.pdf)、[Sample semi-structured.doc](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/semi-structured.docx)、[Sample white paper.pdf](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/white-paper.pdf)|
|Excel|结构化 QnA 文件（包括 RTF、 HTML 支持）|[Sample QnA FAQ.xls](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/QnA%20Maker%20Sample%20FAQ.xlsx)|
|TXT/TSV|结构化 QnA 文件|[示例 chit-chat.tsv](https://github.com/Azure-Samples/cognitive-services-sample-data-files/blob/master/qna-maker/data-source-formats/Scenario_Responses_Friendly.tsv)|

## <a name="data-source-locations"></a>数据源位置

只有公共 URL 对所有数据源才有效。 请勿提交要求进行身份验证的数据源。 可从经过身份验证的站点下载该文件，然后使用文件上传选项来提取问题和答案。

## <a name="faq-urls"></a>常见问题解答 URL

QnA Maker 可以支持 3 种不同形式的常见问题解答网页：纯文本常见问题解答页、带有链接的常见问题解答页、具有主题主页的常见问题解答页。

### <a name="plain-faq-pages"></a>纯文本常见问题解答页

这是最常见的常见问题解答页类型，其中答案会紧跟在同一页中的问题后面。 

下面是普通常见问题解答页的示例：

![知识库的纯文本常见问题解答页示例](../media/qnamaker-concepts-datasources/plain-faq.png) 

 
### <a name="faq-pages-with-links"></a>带链接的常见问题解答页 

在这种类型的常见问题解答页中，问题聚合在一起，并链接到同一页的不同部分或不同页中的答案。

下面的示例是一个常见问题解答页，其中的链接位于同一页上的不同部分：

 ![知识库的部分链接常见问题解答页示例](../media/qnamaker-concepts-datasources/sectionlink-faq.png) 


### <a name="faq-pages-with-a-topics-homepage"></a>带主题主页的常见问题解答页

这种类型的常见问题解答有一个带主题的主页，其中的每个主题都是一个链接，链接到不同页中的相关 QnA。 在这里，QnA Maker 会抓取所有链接的页以提取相应的问题与解答。

下面的示例是一个常见问题解答页，其中的主题主页有一个链接，链接到不同页中的常见问题解答部分。 

 ![知识库的深层链接常见问题解答页示例](../media/qnamaker-concepts-datasources/topics-faq.png) 


## <a name="pdf-doc-files"></a>PDF/DOC 文件

QnA Maker 可以处理 PDF 或 DOC 文件中的半结构化内容，将其转换为 QnA。 若要让文件适合提取，应该将内容以结构化形式进行组织，并在定义好的节中进行呈现。 这些节可以进一步拆分成子节或子主题。 提取最适用于结构清晰且具有分层标题的文档。

QnA Maker 根据视觉线索（例如字体大小、字体样式、编号、颜色等）来确定文件中的节、子节和关系。半结构化 PDF 或 DOC 文件可以是手册、常见问题解答、指南、策略、小册子、传单以及许多其他类型的文件。 下面是这些文件的一些示例类型。

### <a name="product-manuals"></a>产品手册

手册通常是产品附带的指导材料。 它可以帮助用户设置、使用、维护产品和排除产品故障。 当 QnA Maker 处理手册时，它会将标题和副标题作为问题提取，将后续内容作为答案提取。 请参阅[此处](https://download.microsoft.com/download/2/9/B/29B20383-302C-4517-A006-B0186F04BE28/surface-pro-4-user-guide-EN.pdf)的示例。

下面是一个手册示例，其中包含索引页和分层内容。

 ![知识库的产品手册示例](../media/qnamaker-concepts-datasources/product-manual.png) 

> [!NOTE]
> 提取最适用于具有目录和/或索引页的手册，以及具有分层标题的清晰结构。

### <a name="brochures-guidelines-papers-and-other-files"></a>小册子、指南、论文和其他文件

许多其他类型的文档也可进行处理，以便生成 QA 对，前提是它们有清晰的结构和布局。 其中包括：小册子，指南、报告、白皮书、科学论文、策略、书籍等。请参阅[此处](https://qnamakerstore.blob.core.windows.net/qnamakerdata/docs/Manage%20Azure%20Blob%20Storage.docx)的示例。

下面是一个半结构化文档的示例，没有索引：

 ![Azure Blob 存储半结构化文档](../media/qnamaker-concepts-datasources/semi-structured-doc.png) 

### <a name="structured-qna-document"></a>结构化 QnA 文档

DOC 文件中结构化问答的格式采用每行都有交替的问题和回答的形式，一个问题占据一行，后面的一行是其回答，如下所示： 

```text
Question1

Answer1

Question2

Answer2
```

下面是结构化 QnA Word 文档的示例：

 ![知识库的结构化常见问题解答文档示例](../media/qnamaker-concepts-datasources/structured-qna-doc.png) 

## <a name="structured-txt-tsv-and-xls-files"></a>结构化 *TXT*、*TSV* 和 *XLS* 文件

采用结构化 *.txt*、*.tsv* 或 *.xls* 文件形式的 QnA 也可上传到 QnA Maker，以便创建或增强知识库。  它们的内容可以是纯文本，也可以是 RTF 或 HTML 格式。 

| 问题  | Answer  | 元数据                |
|-----------|---------|-------------------------|
| 问题 1 | 答案 1 | <code>Key1:Value1 &#124; Key2:Value2</code> |
| 问题 2 | 答案 2 |      `Key:Value`           |

将忽略源文件中的任何其他列。

下面是结构化 QnA *.xls* 文件的示例，包含 HTML 内容：

 ![知识库的结构化常见问题解答 Excel 示例](../media/qnamaker-concepts-datasources/structured-qna-xls.png)

## <a name="structured-data-format-through-import"></a>通过导入提供的结构化数据格式

导入知识库将替换现有知识库的内容。 导入需要包含数据源信息的结构化 .tsv 文件。 这些信息可帮助 QnA Maker 将问答对分组，并将它们归因于特定数据源。

| 问题  | Answer  | 源| 元数据                |
|-----------|---------|----|---------------------|
| 问题 1 | 答案 1 | Url1 | <code>Key1:Value1 &#124; Key2:Value2</code> |
| 问题 2 | 答案 2 | 编辑|    `Key:Value`       |

## <a name="editorially-add-to-knowledge-base"></a>以编辑身份添加到知识库

如果没有预先存在的内容来填充知识库，可以在 QnA Maker 知识库中以编辑方式添加 QnA。 在[此处](../How-To/edit-knowledge-base.md)了解如何更新知识库。

## <a name="formatting-considerations"></a>格式设置注意事项

导入文件或 URL 后，它将转换为 Markdown 并以该格式存储。 如果转换过程未正确转换文件中的链接和 URL，则应在“编辑”页上编辑问题和答案。 

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [设置 QnA Maker 服务](../How-To/set-up-qnamaker-service-azure.md)

## <a name="see-also"></a>另请参阅 

[QnA Maker 概述](../Overview/overview.md)
