---
title: FOR XML AUTO 쿼리 호환성 모드 90 이상에서 파생된 테이블 참조를 반환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- FOR XML AUTO [SQL Server]
ms.assetid: 10c32f06-f7e1-40e0-8f79-6d921f2bef1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 068346ed0adb5c74d5e892d25c2cc7b93fc57871
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096763"
---
# <a name="for-xml-auto-queries-return-derived-table-references-in-90-or-later-compatibility-modes"></a>FOR XML AUTO 쿼리는 호환성 모드 90 이상에서 파생 테이블 참조를 반환합니다.
  데이터베이스 호환성 수준이 90 이상으로 설정되어 있으면 AUTO 모드에서 실행되는 FOR XML 쿼리는 파생 테이블 별칭에 대한 참조를 반환합니다. 호환성 수준이 80으로 설정되어 있으면 FOR XML AUTO 쿼리는 파생 테이블을 정의하는 기본 테이블에 대한 참조를 반환합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 예를 들어 다음 테이블을 살펴봅니다.  
  
```  
CREATE TABLE Test(id int);  
INSERT INTO Test VALUES(1);  
INSERT INTO Test VALUES(2);  
```  
  
 파생 테이블을 포함하는 다음 쿼리는 호환성 수준 80 또는 90 이상에서 서로 다른 결과를 생성합니다.  
  
```  
SELECT * FROM   
   (SELECT a.id AS a, b.id AS b   
    FROM Test a JOIN Test b ON a.id=b.id)  
AS DerivedTest   
FOR XML AUTO;  
```  
  
 호환성 수준 80에서 이 쿼리는 다음 결과를 반환합니다. 이 결과는 파생 테이블 별칭 대신 파생 테이블의 기본 테이블 별칭 `a` 와 `b` 를 참조합니다.  
  
```  
<a a="1"><b b="1"/></a><a a="2"><b b="2"/></a>  
```  
  
 호환성 수준 90 이상에서 이 쿼리는 파생 테이블의 기본 테이블 대신 파생 테이블 별칭 `DerivedTest` 에 대한 참조를 반환합니다.  
  
```  
<DerivedTest a="1" b="1"/><DerivedTest a="2" b="2"/>  
```  
  
## <a name="corrective-action"></a>수정 동작  
 필요에 따라 파생 테이블을 포함하고 있고 호환성 수준 90 이상에서 실행되는 FOR XML AUTO 쿼리 결과의 변경 내용을 반영하도록 애플리케이션을 수정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
