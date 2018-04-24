---
title: XML 데이터에 비즈니스 논리 추가 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- business logic [XML]
ms.assetid: 0877fb38-f1a2-43d8-86cf-4754be224dc1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8bd981fa60077792357c2d02d7e8675b79e57423
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="add-business-logic-to-xml-data"></a>XML 데이터에 비즈니스 논리 추가
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  비즈니스 논리를 여러 가지 방식으로 XML 데이터에 추가할 수 있습니다.  
  
-   XML 데이터의 삽입 및 수정 중에 도메인 특정 제약 조건을 강화하도록 행 또는 열 제약 조건을 작성할 수 있습니다.  
  
-   열에서 값을 삽입 또는 업데이트할 때 발생되는 트리거를 XML 열에 작성할 수 있습니다. 이 트리거는 도메인 특정 유효성 검사 규칙을 포함하거나 속성 테이블을 채울 수 있습니다.  
  
-   데이터베이스 엔진에 관리 코드를 실행하는 기능이 포함됩니다. 이 CLR(공용 언어 런타임) 통합을 사용하여 XML 값을 전달하는 관리 코드에 함수를 작성하고 System.Xml 네임스페이스에서 제공되는 XML 처리 기능을 사용할 수 있습니다. 한 예는 XSL 변환을 XML 데이터에 적용하는 것입니다. 또는 XML을 하나 이상의 관리 클래스로 역직렬화하고 관리 코드를 사용하여 작업할 수 있습니다.  
  
-   비즈니스 요구에 맞게 XML 열에서 처리를 시작하는 Transact-SQL 저장 프로시저와 함수를 작성할 수 있습니다.  
  
## <a name="example-applying-xsl-transformation"></a>예제: XSL 변환 적용  
 파일에 저장된 **xml** 데이터 형식 인스턴스와 XSL 변환을 수락하고, XML 데이터에 XSL 변환을 적용하고, 변환된 XML을 결과로 반환하는 CLR 함수 **TransformXml()** 를 고려해 보세요. 다음은 C#으로 작성된 기초 함수입니다.  
  
```  
public static SqlXml TransformXml (SqlXml XmlData, string xslPath) {  
   // Load XSL transformation  
   XslCompiledTransform xform = new XslCompiledTransform();  
   XPathDocument xslDoc = new XPathDocument (xslPath);  
   xform.Load(xslDoc);  
  
   // Load XML data   
   XPathDocument xDoc = new XPathDocument (XmlData.CreateReader());  
  
   // Return the transformed value  
   MemoryStream xsltResult = new MemoryStream();  
   xform.Transform(xDoc, null, xsltResult);  
   SqlXml retSqlXml = new SqlXml(xsltResult);  
   return (retSqlXml);  
}   
```  
  
 어셈블리를 등록하고 사용자 정의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 만든 후 다음 쿼리에서와 같이 **TransformXml()** 에 해당하는 **SqlXslTransform()** 함수를 Transact-SQL로부터 호출할 수 있습니다.  
  
```  
SELECT SqlXslTransform (xCol, 'C:\MyFile\xsltransform.xsl')  
FROM    T  
WHERE  xCol.exist('/book/title/text()[contains(.,"custom")]') =1;  
```  
  
 쿼리 결과에는 변환된 XML의 행 집합이 포함됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 CLR 통합은 XML 데이터를 테이블 또는 속성 승격으로 분해하고 System.Xml 네임스페이스에 있는 관리 클래스를 사용하여 XML 데이터를 쿼리할 수 있는 가능성을 확장합니다. 자세한 내용은 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)를 참조하세요.  
  
  
