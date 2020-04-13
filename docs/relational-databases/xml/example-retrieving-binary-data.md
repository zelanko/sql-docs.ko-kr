---
title: '예제: 이진 데이터 검색 | Microsoft 문서'
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: RothJa
ms.author: jroth
ms.openlocfilehash: 8d66e1ec9c580030f1f65f030cdb0367d8f4f430
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664500"
---
# <a name="example-retrieving-binary-data"></a>예제: 이진 데이터 검색

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

다음 쿼리는 **varbinary(max)** 유형 열에 저장된 제품 사진을 반환합니다. 이진 데이터를 base64 인코딩 형식으로 반환하기 위해 쿼리에서 `BINARY BASE64` 옵션을 지정합니다.

## <a name="example"></a>예제

```sql
USE AdventureWorks2012;
GO
SELECT ProductPhotoID, ThumbNailPhoto
FROM Production.ProductPhoto
WHERE ProductPhotoID=1
FOR XML RAW, BINARY BASE64 ;
GO
```

다음의 결과가 예상됩니다.

```console
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>
```

## <a name="see-also"></a>참고 항목

[FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)
