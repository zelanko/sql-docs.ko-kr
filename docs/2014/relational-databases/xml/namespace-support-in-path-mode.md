---
title: PATH 모드에서의 네임스페이스 지원 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad1a6af717dcfa8ea42d9171e5ab23d9c24c6225
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240792"
---
# <a name="namespace-support-in-path-mode"></a>PATH 모드에서의 네임스페이스 지원
  WITH NAMESPACES를 사용하여 PATH 모드에 네임스페이스 지원을 제공합니다. 예를 들어 다음 쿼리에서는 후속 SELECT 문에 사용할 수 있는 네임스페이스("a:")를 선언할 WITH NAMESPACES 구문을 보여 줍니다.  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>예  
 다음 예제에서는 SELECT 쿼리에서 XML을 생성할 때 PATH 모드를 사용하는 방법을 보여 줍니다. 이러한 쿼리는 대부분 ProductModel 테이블의 Instructions 열에 저장된 자전거 제조 지침 XML 문서에 대해 지정됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 PATH 모드 사용](use-path-mode-with-for-xml.md)  
  
  
