---
title: PATH 모드에서의 네임스페이스 지원 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19c932a3927e71208e4b1c82c8c3bce4cbadfd8b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747041"
---
# <a name="namespace-support-in-path-mode"></a>PATH 모드에서의 네임스페이스 지원
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  WITH NAMESPACES를 사용하여 PATH 모드에 네임스페이스 지원을 제공합니다. 예를 들어 다음 쿼리에서는 후속 SELECT 문에 사용할 수 있는 네임스페이스("a:")를 선언할 WITH NAMESPACES 구문을 보여 줍니다.  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>예  
 다음 예제에서는 SELECT 쿼리에서 XML을 생성할 때 PATH 모드를 사용하는 방법을 보여 줍니다. 이러한 쿼리는 대부분 ProductModel 테이블의 Instructions 열에 저장된 자전거 제조 지침 XML 문서에 대해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
