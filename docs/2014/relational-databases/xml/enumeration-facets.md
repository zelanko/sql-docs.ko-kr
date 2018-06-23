---
title: 열거 패싯 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- enumeration facets
ms.assetid: dec23a79-ddd6-4701-9721-55a2c435a34d
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cee53758a323112476a6b3bb572a075ed02bd410
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184428"
---
# <a name="enumeration-facets"></a>열거 패싯
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 패턴 패싯 형식이나 이러한 패싯을 위반하는 열거형의 XML 스키마를 거부합니다.  
  
## <a name="example"></a>예제  
 다음 스키마는 주요 열거 값이 대/소문자 값을 포함하기 때문에 거부됩니다. 또한 이 값이 소문자로만 값을 제한하는 패턴 값을 위반하기 때문에 거부됩니다.  
  
```  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
    <simpleType name="MyST">  
       <restriction base="string">  
          <pattern value="[a-z]*"/>  
       </restriction>  
    </simpleType>  
  
    <simpleType name="MyST2">  
       <restriction base="ns:MyST">  
           <enumeration value="mYstring"/>  
       </restriction>  
    </simpleType>  
</schema>'  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  