---
title: timestamp 데이터 형식에 대한 FOR XML 지원 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type
ms.assetid: 4e1920e1-e7a4-4069-965e-3f6039a6099e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ecfbc108ef35928d08a36bc7a22c415cabece27e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67943303"
---
# <a name="for-xml-support-for-the-timestamp-data-type"></a>timestamp 데이터 형식에 대한 FOR XML 지원
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML 변환에서 **timestamp** 유형 값은 **varbinary(8)** 데이터로 취급되며 항상 base 64로 인코드됩니다. 요청된 경우 XSD 또는 XDR 스키마는 이 유형을 반영합니다.  
  
```  
drop table t  
go  
create table t  
(c1 int,  
 c2 timestamp)  
go  
  
insert t values(1, null)  
go  
select * from t  
for xml auto, xmldata  
go  
```  
  
 다음은 결과입니다.  
  
```  
<Schema name="Schema1"   
        xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="t" content="empty" model="closed">  
    <AttributeType name="c1" dt:type="i4" />  
    <AttributeType name="c2" dt:type="bin.base64" />  
    <attribute type="c1" />  
    <attribute type="c2" />  
  </ElementType>  
</Schema>  
<t xmlns="x-schema:#Schema1" c1="1" c2="AAAAAAAAH04=" />  
```  
  
## <a name="see-also"></a>참고 항목  
 [다양한 SQL Server 데이터 형식에 대한 FOR XML 지원](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
