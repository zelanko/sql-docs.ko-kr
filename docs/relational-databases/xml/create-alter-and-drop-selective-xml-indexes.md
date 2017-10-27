---
title: "선택적 XML 인덱스 만들기, 변경 및 삭제 | Microsoft 문서"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c398f396-f630-4a2d-a264-f243c5346de1
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cff16890d58c610a08e7bbe0d5958de2e821b0a5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/18/2017

---
# <a name="create-alter-and-drop-selective-xml-indexes"></a>선택적 XML 인덱스 만들기, 변경 및 삭제
  새 선택적 XML 인덱스를 만들거나 기존 선택적 XML 인덱스를 변경 또는 삭제하는 방법에 대해 설명합니다.  
  
 선택적 XML 인덱스에 대한 자세한 내용은 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)를 참조하세요.  
  
##  <a name="create"></a> 선택적 XML 인덱스 만들기  
  
### <a name="how-to-create-a-selective-xml-index"></a>방법: 선택적 XML 인덱스 만들기  
 **Transact-SQL을 사용하여 선택적 XML 인덱스 만들기**  
 CREATE SELECTIVE XML INDEX 문을 호출하여 선택적 XML 인덱스를 만듭니다. 자세한 내용은 [CREATE SELECTIVE XML INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)를 참조하세요.  
  
 **예제**  
  
 다음 예에서는 선택적 XML 인덱스를 만드는 구문을 보여 줍니다. 또한 이 예에서는 선택적 최적화 힌트를 사용하여 인덱싱할 경로를 설명하는 구문의 여러 변형도 보여 줍니다.  
  
```tsql  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()'  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
)  
```  
  
  
##  <a name="alter"></a> 선택적 XML 인덱스 변경  
  
### <a name="how-to-alter-a-selective-xml-index"></a>방법: 선택적 XML 인덱스 변경  
 **Transact-SQL을 사용하여 선택적 XML 인덱스 변경**  
 ALTER INDEX 문을 호출하여 기존 선택적 XML 인덱스를 변경합니다. 자세한 내용은 [ALTER INDEX&#40;선택적 XML 인덱스&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md)를 참조하세요.  
  
 **예제**  
  
 다음 예에서는 ALTER INDEX 문을 보여 줍니다. 이 문은 인덱스의 XQuery 부분에 `'/a/b/m'` 경로를 추가하고 [CREATE SELECTIVE XML INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md) 항목의 예에서 만든 인덱스의 SQL 부분에서 `'/a/b/e'` 경로를 삭제합니다. 삭제할 경로는 해당 경로를 만들 때 지정한 경로 이름으로 식별됩니다.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
)  
```  
  
  
##  <a name="drop"></a> 선택적 XML 인덱스 삭제  
  
### <a name="how-to-drop-a-selective-xml-index"></a>방법: 선택적 XML 인덱스 삭제  
 **Transact-SQL을 사용하여 선택적 XML 인덱스 삭제**  
 DROP INDEX 문을 호출하여 선택적 XML 인덱스를 삭제합니다. 자세한 내용은 [DROP INDEX&#40;선택적 XML 인덱스&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md)를 참조하세요.  
  
 **예제**  
  
 다음 예에서는 DROP INDEX 문을 보여 줍니다.  
  
```tsql  
DROP INDEX sxi_index ON tbl  
```  
  
  
  

