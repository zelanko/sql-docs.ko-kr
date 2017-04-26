---
title: "MSSQLSERVER_1505 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8383fd472e054f26db78ab8ec28b4a67e81e7f02
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver1505"></a>MSSQLSERVER_1505
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1505|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DUP_KEY|  
|메시지 텍스트|개체 이름 '%.*ls' 및 인덱스 이름 '%.\*ls'에 키가 중복되므로 CREATE UNIQUE INDEX 문이 종료되었습니다.  중복 키 값은 %ls입니다.|  
  
## <a name="explanation"></a>설명  
이 오류는 고유 인덱스를 만들려고 했지만 테이블에 지정된 중복 값을 가진 행이 두 개 이상 있는 경우에 발생합니다. 고유 인덱스는 인덱스를 만들고 UNIQUE 키워드를 지정하거나 UNIQUE 제약 조건을 만들 때 생성됩니다. 테이블은 인덱스 또는 제약 조건에 정의된 열에 중복 값이 있는 행을 포함할 수 없습니다.  
  
다음과 같은 **Employee** 테이블의 데이터를 고려합니다.  
  
|LastName|FirstName|JobTitle|HireDate|  
|------------|-------------|------------|------------|  
|Walters|Rob|Senior Tool Designer|2004-11-19|  
|Brown|Kevin|Marketing Assistant|NULL|  
|Brown|Jo|Design Engineer|NULL|  
|Walters|Rob|Tool Designer|2001-08-09|  
  
행에 중복 값이 있으므로 **LastName** 또는 **LastName**, **FirstName**의 열 조합에 고유 인덱스를 만들 수 없습니다.  
  
**HireDate** 열에서는 고유성 위반이 발생할 가능성이 있습니다. 인덱싱 작업에서 NULL 값은 동일한 값으로 간주됩니다. 따라서 둘 이상의 행에서 키 값이 NULL인 경우에는 고유 인덱스 또는 제약 조건을 만들 수 없습니다. 위와 같은 데이터의 경우 **HireDate** 또는 **LastName**, **HireDate** 열 조합에 고유 인덱스를 만들 수 없습니다.  
  
오류 메시지 1505는 고유성 제약 조건을 위반한 첫 번째 행을 반환하므로 테이블에 다른 중복 행이 있을 수 있습니다. 모든 중복 행을 찾으려면 지정된 테이블을 쿼리하고 GROUP BY 및 HAVING 절을 사용하여 중복 행을 반환하십시오. 예를 들어 다음 쿼리는 **Employee** 테이블에서 이름과 성이 중복되는 행을 반환합니다.  
  
SELECT LastName, FirstName, count(*) FROM dbo.Employee GROUP BY LastName, FirstName HAVING count(\*) > 1;  
  
## <a name="user-action"></a>사용자 동작  
다음과 같은 해결 방법을 고려해 보십시오.  
  
-   인덱스 또는 제약 조건 정의에서 열을 추가하거나 제거하여 고유 복합 인덱스를 만듭니다. 앞의 예에서는 인덱스 또는 제약 조건 정의에 **MiddleName** 열을 추가하여 중복 문제를 해결할 수 있습니다.  
  
-   고유 인덱스 또는 제약 조건을 만들 열을 선택할 때는 NOT NULL로 정의된 열을 선택합니다. 이렇게 하면 둘 이상의 행에서 키 값이 NULL인 경우 발생하는 고유성 위반의 가능성을 없앨 수 있습니다.  
  
-   중복 값이 데이터 입력 오류로 인한 것이면 데이터를 직접 수정한 다음 인덱스나 제약 조건을 만듭니다. 테이블에서 중복 행을 제거하는 방법에 대한 자세한 내용은 기술 자료 문서 139444 [SQL Server의 테이블에서 중복 행을 제거하는 방법](http://support.microsoft.com/kb/139444)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[CREATE INDEX&#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[고유 인덱스 만들기](~/relational-databases/indexes/create-unique-indexes.md)  
[UNIQUE 제약 조건 만들기](~/relational-databases/tables/create-unique-constraints.md)  
  

