---
title: MSSQLSERVER_4104 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4104 (Database Engine error)
ms.assetid: 52dc32d8-97ad-4ef0-834d-2e68f215d007
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55bbf20609dc364fdb79c0c785ccffb691da991e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63018672"
---
# <a name="mssqlserver4104"></a>MSSQLSERVER_4104
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|4104|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|ALG_MULTI_ID_BAD|  
|메시지 텍스트|여러 부분으로 구성된 식별자 "%.*ls"은(는) 바인딩할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 엔터티 이름을 해당 엔터티의 *식별자*라고 합니다. 예를 들어 쿼리에서 열 및 테이블 이름을 지정하여 엔터티를 참조할 경우 항상 식별자가 사용됩니다. 여러 부분으로 구성된 식별자에는 하나 이상의 한정자가 접두사로 포함되어 있습니다. 예를 들어 테이블 식별자는 해당 테이블이 들어 있는 데이터베이스 이름이나 스키마 이름 같은 한정자를 접두사로 사용하고 열 식별자는 테이블 이름이나 테이블 별칭 같은 한정자를 접두사로 사용할 수 있습니다.  
  
오류 4104는 지정된 여러 부분으로 구성된 식별자가 기존 엔터티로 매핑될 수 없음을 나타냅니다. 이 오류는 다음과 같은 경우에 반환될 수 있습니다.  
  
-   열 이름의 접두사로 제공된 한정자가 쿼리에 사용된 테이블 또는 별칭 이름과 일치하지 않습니다.  
  
    예를 들어 다음 문에서는 테이블 별칭(`Dept`)을 열 접두사로 사용하지만 테이블 별칭이 FROM 절에서 참조되지 않습니다.  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department;  
    ```  
  
    다음 문에서는 여러 부분으로 구성된 열 식별자 `TableB.KeyCol`이 WHERE 절에 두 테이블 간 JOIN 조건의 일부로 지정되어 있지만 `TableB`가 쿼리에서 명시적으로 참조되지 않습니다.  
  
    ```  
    DELETE FROM TableA WHERE TableA.KeyCol = TableB.KeyCol;  
    ```  
  
    ```  
    SELECT 'X' FROM TableA WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   테이블의 별칭 이름이 FROM 절에 제공되어 있지만 열에 대해 제공된 한정자가 테이블 이름입니다. 예를 들어 다음 문에서는 테이블 이름 `Department`를 열 접두사로 사용하지만 테이블에는 FROM 절에서 참조된 별칭(`Dept`)이 포함되어 있습니다.  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department AS Dept;  
    ```  
  
    별칭을 사용하는 경우 문의 다른 위치에서 테이블 이름을 사용할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 여러 부분으로 구성된 식별자가 테이블 이름을 접두사로 사용하는 열을 참조하는지 또는 열 이름을 접두사로 사용하는 CLR UDT(사용자 정의 데이터 형식)의 속성을 참조하는지 확인할 수 없습니다. 이는 열 이름의 접두사로 테이블 이름이 사용되는 것과 같은 방법으로 UDT 열의 속성이 열 이름과 속성 이름 사이에 마침표 구분 기호(.)를 사용하여 참조되기 때문입니다. 다음 예에서는 두 개의 테이블 `a` 및 `b`를 만듭니다. `b` 테이블에는 CLR UDT `dbo.myudt2`를 데이터 형식으로 사용하는 `a` 열이 포함되어 있습니다. SELECT 문에는 여러 부분으로 구성된 식별자 `a.c2`가 포함되어 있습니다.  
  
    ```  
    CREATE TABLE a (c2 int);   
    GO  
    ```  
  
    ```  
    CREATE TABLE b (a dbo.myudt2);   
    GO  
    ```  
  
    ```  
    SELECT a.c2 FROM a, b;   
    ```  
  
    UDT `myudt2`에 `c2`라는 속성이 없다고 가정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `a.c2` 식별자가 `a` 테이블의 `c2` 열을 참조하는지 또는 `b` 테이블의 `a` 열과 `c2` 속성을 참조하는지 확인할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
  
-   쿼리의 FROM 절에 지정된 테이블 이름 또는 별칭 이름과 열 접두사가 일치하도록 수정하십시오. FROM 절에 테이블 이름의 별칭이 정의되어 있는 경우 해당 테이블과 연결된 열의 한정자로 이 별칭만 사용할 수 있습니다.  
  
    `HumanResources.Department` 테이블을 참조하는 위의 문은 다음과 같이 수정할 수 있습니다.  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department AS Dept;  
    GO  
    ```  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department;  
    GO  
    ```  
  
-   쿼리에 모든 테이블이 지정되어 있고 테이블 간의 JOIN 조건이 올바로 지정되어 있는지 확인합니다. 위의 DELETE 문은 다음과 같이 수정할 수 있습니다.  
  
    ```  
    DELETE FROM dbo.TableA  
    WHERE TableA.KeyCol = (SELECT TableB.KeyCol   
                            FROM TableB   
                            WHERE TableA.KeyCol = TableB.KeyCol);  
    GO  
    ```  
  
    `TableA`에 대한 위의 SELECT 문은 다음과 같이 수정할 수 있습니다.  
  
    ```  
    SELECT 'X' FROM TableA, TableB WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
    로 구분하거나 여러  
  
    ```  
    SELECT 'X' FROM TableA INNER JOIN TableB ON TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   식별자에 대해 고유하고 명확하게 정의된 이름을 사용합니다. 이렇게 하면 코드를 보다 쉽게 읽고 유지 관리할 수 있으며 여러 엔터티를 모호하게 참조하는 위험을 최소화할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[MSSQLSERVER_107](~/relational-databases/errors-events/mssqlserver-107-database-engine-error.md)  
[데이터베이스 식별자](~/relational-databases/databases/database-identifiers.md)  
  
