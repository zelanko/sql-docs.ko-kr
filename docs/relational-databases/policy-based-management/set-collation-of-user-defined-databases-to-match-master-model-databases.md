---
title: master 및 model 데이터베이스와 일치하도록 사용자 정의 데이터베이스의 데이터 정렬 설정
description: 정책을 사용하도록 설정하여 사용자 정의 데이터베이스와 시스템 데이터베이스의 데이터 정렬이 동일한지 확인하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 905accc62afdc12152110d44a18e61d4c8a9bcef
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89285131"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-master-and-model-databases"></a>master 및 model 데이터베이스와 일치하도록 사용자 정의 데이터베이스의 데이터 정렬 설정
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 규칙은 사용자 정의 데이터베이스가 master 또는 model의 데이터 정렬과 동일한 데이터베이스 데이터 정렬을 사용하여 정의되었는지 확인합니다.
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 사용자 정의 데이터베이스의 데이터 정렬을 master 또는 model의 데이터 정렬과 맞추는 것이 좋습니다. 그렇지 않으면 데이터 정렬 충돌이 발생하여 코드가 실행되지 않을 수 있습니다. 예를 들어 저장 프로시저가 한 테이블을 임시 테이블에 조인할 경우 사용자 정의 데이터베이스의 데이터 정렬과 model 데이터베이스의 데이터 정렬이 서로 다르면 SQL Server가 일괄 처리를 종료하고 데이터 정렬 충돌 오류를 반환할 수 있습니다. 이러한 오류가 발생하는 것은 model의 데이터 정렬을 기본으로 사용하는 tempdb에서 임시 테이블이 생성되기 때문입니다.

  데이터 정렬 충돌 오류가 발생하면 다음 중 한 가지 해결 방법을 사용하십시오.

  - 사용자 데이터베이스의 데이터를 내보내고 master 및 model 데이터베이스와 데이터 정렬이 동일한 새로운 테이블로 가져옵니다.

  - 사용자 데이터베이스 데이터 정렬과 일치하는 데이터 정렬을 사용하도록 시스템 데이터베이스를 다시 작성합니다. 시스템 데이터베이스를 다시 빌드하는 방법은 [시스템 데이터베이스 다시 빌드](../databases/rebuild-system-databases.md)를 참조하세요.

  - 사용자 테이블을 tempdb의 테이블에 조인하는 저장 프로시저는 사용자 데이터베이스의 데이터 정렬을 사용하여 tempdb에 테이블을 만들도록 수정합니다. 이렇게 하려면 다음 예제와 같이 임시 테이블의 열 정의에 COLLATE database_default 절을 추가합니다.
  
    ```
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )
    ```

## <a name="see-also"></a>참고 항목
  
 [서버 데이터 정렬 설정 또는 변경](../collations/set-or-change-the-server-collation.md)  

 [데이터베이스 데이터 정렬 설정 또는 변경](../collations/set-or-change-the-database-collation.md)

 [열 데이터 정렬 설정 또는 변경](../collations/set-or-change-the-column-collation.md)
 
 [데이터 정렬 정보 보기](../collations/view-collation-information.md)    
  
  
