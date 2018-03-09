---
title: "OPENXML에서 value() 및 nodes() 메서드 사용 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OpenXML method [XML in SQL Server]
- value method [XML in SQL Server]
- nodes method [XML in SQL Server]
ms.assetid: c73dbe55-d685-42eb-b0ee-9f3c5b9d97f3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 831efec8d02c212f5a037423c42148e0c93fd072
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="use-the-value-and-nodes-methods-with-openxml"></a>OPENXML에서 value() 및 nodes() 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
**SELECT** 절에서 **xml** 데이터 형식에 여러 **value()** 메서드를 사용하여 추출된 값의 행 집합을 생성할 수 있습니다. **nodes()** 메서드는 추가 쿼리에 사용할 수 있는 선택된 각 노드에 대해 내부 참조를 생성합니다. **nodes()** 메서드와 **value()** 메서드를 조합하면 일부 행이 있고 해당 생성 시 사용된 경로 식이 복잡한 경우 행 집합을 더욱 효율적으로 생성할 수 있습니다.  
  
 **nodes()** 메서드는 특수한 **xml** 데이터 형식의 인스턴스를 생성하며 각 인스턴스에는 서로 다른 선택 노드에 대한 컨텍스트 집합이 있습니다. 이러한 종류의 XML 인스턴스는 **query()**, **value()**, **nodes()** 및 **exist()** 메서드를 지원하며 **count(\*)** 집계에 사용될 수 있습니다. 다른 용도로 사용하면 오류가 발생합니다.  
  
## <a name="example-using-nodes"></a>예: nodes() 사용  
 저자의 성과 이름을 추출한다고 가정해 보십시오. 이때 이름은 "David"가 아닙니다. 또한 이 정보를 FirstName 및 LastName의 두 열이 포함된 행 집합으로 추출합니다. **nodes()** 및 **value()** 메서드를 사용하면 다음과 같이 이 작업을 수행할 수 있습니다.  
  
```  
SELECT nref.value('(first-name/text())[1]', 'nvarchar(50)') FirstName,  
       nref.value('(last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T CROSS APPLY xCol.nodes('//author') AS R(nref)  
WHERE  nref.exist('first-name[. != "David"]') = 1  
```  
  
 이 예에서 `nodes('//author')` 는 각 XML 인스턴스에 대한 `<author>` 요소의 참조 행 집합을 생성합니다. 작성자의 성과 이름은 이러한 참조에 대해 **value()** 메서드를 평가하여 얻습니다.  
  
 SQL Server 2000은 **OpenXml()**을 사용하여 XML 인스턴스로부터 행 집합을 생성하는 기능을 제공합니다. 행 집합에 대한 관계형 스키마를 지정하고 XML 인스턴스 내의 값이 행 집합의 열로 매핑되는 방식을 지정할 수 있습니다.  
  
## <a name="example-using-openxml-on-the-xml-data-type"></a>예: xml 데이터 형식에서 OpenXml() 사용  
 다음에 표시된 것과 같이 **OpenXml()** 을 사용하여 이전 예의 쿼리를 다시 작성할 수 있습니다. 이러한 작업은 각 XML 인스턴스를 XML 변수로 읽고 OpenXML을 여기에 적용하는 커서를 만들어서 수행합니다.  
  
```  
DECLARE name_cursor CURSOR  
FOR  
   SELECT xCol   
   FROM   T  
OPEN name_cursor  
DECLARE @xmlVal XML  
DECLARE @idoc int  
FETCH NEXT FROM name_cursor INTO @xmlVal  
  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
   EXEC sp_xml_preparedocument @idoc OUTPUT, @xmlVal  
   SELECT   *  
   FROM   OPENXML (@idoc, '//author')  
          WITH (FirstName  varchar(50) 'first-name',  
                LastName   varchar(50) 'last-name') R  
   WHERE  R.FirstName != 'David'  
  
   EXEC sp_xml_removedocument @idoc  
   FETCH NEXT FROM name_cursor INTO @xmlVal  
END  
CLOSE name_cursor  
DEALLOCATE name_cursor   
```  
  
 **OpenXml()** 은 메모리 내 표현을 만들고 쿼리 프로세서 대신 작업 테이블을 사용합니다. 이 함수는 XQuery 엔진 대신 MSXML 버전 3.0의 XPath 버전 1.0 프로세서를 사용합니다. 작업 테이블은 동일 XML 인스턴스에 있는 경우에도 **OpenXml()**에 대한 여러 호출 간에 공유되지 않습니다. 이 때문에 확장성이 제한됩니다. **OpenXml()** 을 사용하면 WITH 절이 지정되지 않은 경우 XML 데이터에 대한 Edge 테이블 형식에 액세스할 수 있습니다. 또한 별개의 "오버플로" 열에서 남아 있는 XML 값을 사용할 수 있습니다.  
  
 **nodes()** 및 **value()** 함수 조합은 XML 인덱스를 효율적으로 사용합니다. 그 결과 이러한 조합은 **OpenXml**보다 많은 확장성을 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [OPENXML&#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
