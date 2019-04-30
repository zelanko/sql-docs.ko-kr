---
title: 혼합 형식 및 단순 내용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf0e4f54334d84aea5a33392655110374e893cc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241264"
---
# <a name="mixed-type-and-simple-content"></a>혼합 형식 및 단순 내용
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 혼합 형식을 단순 내용으로 제한할 수 없습니다.  
  
## <a name="example"></a>예제  
 아래의 XML 스키마 컬렉션에서 `myComplexTypeA` 는 혼합 형식으로 비워둘 수 있습니다. 즉 해당 요소의 `minOccurs` 가 모두 0으로 설정됩니다. `myComplexTypeB` 선언에서처럼 혼합 형식을 단순 내용으로 제한하려는 시도는 지원되지 않습니다. 따라서 다음과 같은 XML 스키마 컬렉션을 만들 수 없습니다.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns"  
xmlns:ns1="http://ns1">  
  
    <complexType name="myComplexTypeA" mixed="true">  
        <sequence>  
            <element name="a" type="string" minOccurs="0"/>  
            <element name="b" type="string" minOccurs="0" maxOccurs="23"/>  
        </sequence>  
    </complexType>  
  
    <complexType name="myComplexTypeB">  
        <simpleContent>  
            <restriction base="ns:myComplexTypeA">  
                <simpleType>  
                    <restriction base="int">  
                        <minExclusive value="25"/>  
                    </restriction>  
                </simpleType>  
            </restriction>  
        </simpleContent>  
    </complexType>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
