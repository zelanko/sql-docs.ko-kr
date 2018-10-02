---
title: BINARY BASE64 옵션 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4b86b7c3a7a6eaa1b0c6a3bdae75ad82784a7fca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661081"
---
# <a name="use-the-binary-base64-option"></a>BINARY BASE64 옵션 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  쿼리에서 BINARY BASE64 옵션을 지정하면 이진 데이터가 base64 인코딩 형식으로 반환됩니다. 기본적으로 BINARY BASE64 옵션이 지정되지 않은 경우 AUTO 모드는 이진 데이터의 URL 인코딩을 지원합니다. 즉, 이진 데이터 대신 쿼리가 실행된 데이터베이스의 가상 루트의 상대 URL에 대한 참조가 반환됩니다. 이 참조를 사용하면 후속 작업에서 SQLXML ISAPI dbobject 쿼리를 사용하여 실제 이진 데이터를 액세스할 수 있습니다. 쿼리는 이미지를 식별하기 위해 기본 키 열과 같은 정보를 충분히 제공해야 합니다.  
  
 쿼리를 지정할 때 뷰의 이진 열에 대해 별칭이 사용되는 경우 별칭은 이진 데이터의 URL 인코딩으로 반환됩니다. 후속 작업에서 별칭은 아무 의미도 없으며 URL 인코딩은 이미지를 검색하는 데 사용할 수 없습니다. 따라서 FOR XML AUTO 모드를 사용하여 뷰를 쿼리할 때는 별칭을 사용하지 않아야 합니다.  
  
 예를 들어 SELECT 쿼리에서 모든 열에 BLOB에 대한 캐스트를 지정하면 임시 엔터티가 되어 관련 테이블 이름과 열 이름이 손실됩니다. 이것은 XML 계층 구조에서 이 값을 둘 위치를 알 수 없으므로, 이로 인해 AUTO 모드 쿼리에서 오류가 발생하게 됩니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 다음 쿼리에서는 BLOB(Binary Large Object)으로 캐스팅하기 때문에 오류가 발생합니다.  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 이 솔루션은 FOR XML 절에 BINARY BASE64 옵션을 추가합니다. 캐스트 지정을 없애면 예상대로 쿼리 결과가 만들어집니다.  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 다음은 결과입니다.  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
