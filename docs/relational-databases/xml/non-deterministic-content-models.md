---
title: "비결정적 콘텐츠 모델 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "비결정적 콘텐츠 모델"
  - "콘텐츠 모델 [SQL Server의 XML]"
ms.assetid: 9d4513e7-dd19-4491-b7c7-28bc7c2f8589
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# 비결정적 콘텐츠 모델
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1(서비스 팩 1) 이전에, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 비결정적 콘텐츠 모델이 있는 XML 스키마를 거부했습니다.  
  
 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1부터 비결정적 콘텐츠 모델은 발생빈도 제약 조건이 0 또는 1이거나 해제된 경우 허용됩니다.  
  
## 예제: 비결정적 콘텐츠 모델이 거부됨  
 다음 예에서는 비결정적 콘텐츠 모델이 있는 XML 스키마를 만들려고 시도합니다. `<root>` 요소에 `<a>` 요소가 두 개 포함된 하나의 시퀀스가 있는지 또는 `<root>` 요소에 각각 `<a>` 요소가 하나씩 포함된 두 개의 시퀀스가 있는지가 명확하지 않기 때문에 이 코드는 실패합니다.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="1" maxOccurs="2">  
                <element name="a" type="string" minOccurs="1" maxOccurs="2"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
 발생빈도 제약 조건을 고유한 위치로 이동하여 스키마를 수정할 수 있습니다. 예를 들어 이 제약 조건을 포함하는 시퀀스 파티클로 이동할 수 있습니다.  
  
```  
<sequence minOccurs="1" maxOccurs="4">  
    <element name="a" type="string" minOccurs="1" maxOccurs="1"/>  
</sequence>  
```  
  
 또는 이 제약 조건을 포함된 요소로 이동할 수 있습니다.  
  
```  
<sequence minOccurs="1" maxOccurs="1">  
     <element name="a" type="string" minOccurs="1" maxOccurs="4"/>  
</sequence>  
```  
  
## 예제: 비결정적 콘텐츠 모델이 허용됨  
 다음 스키마는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 이전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 버전에서 거부됩니다.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="0" maxOccurs="unbounded">  
                <element name="a" type="string" minOccurs="0" maxOccurs="1"/>  
                <element name="b" type="string" minOccurs="1" maxOccurs="unbounded"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
## 참고 항목  
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  