---
title: Master 및 model 데이터베이스와 일치 하도록 사용자 정의 데이터베이스의 데이터 정렬을 설정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c686446f-dae1-4b05-a3df-837b3422988d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b48696fb56c40062d62f04845715170887f84fda
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929167"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>master 및 model 데이터베이스와 일치하도록 사용자 정의 데이터베이스의 데이터 정렬 설정
  이 규칙은 사용자 정의 데이터베이스가 master 또는 model의 데이터 정렬과 동일한 데이터베이스 데이터 정렬을 사용하여 정의되었는지 확인합니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 사용자 정의 데이터베이스의 데이터 정렬을 master 또는 model의 데이터 정렬과 맞추는 것이 좋습니다. 그렇지 않으면 데이터 정렬 충돌이 발생하여 코드가 실행되지 않을 수 있습니다. 예를 들어 저장 프로시저가 한 테이블을 임시 테이블에 조인할 경우 사용자 정의 데이터베이스의 데이터 정렬과 model 데이터베이스의 데이터 정렬이 서로 다르면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 일괄 처리를 종료하고 데이터 정렬 충돌 오류를 반환할 수 있습니다. 이러한 오류가 발생하는 것은 model의 데이터 정렬을 기본으로 사용하는 tempdb에서 임시 테이블이 생성되기 때문입니다.  
  
 데이터 정렬 충돌 오류가 발생하면 다음 중 한 가지 해결 방법을 사용하십시오.  
  
-   사용자 데이터베이스의 데이터를 내보내고 master 및 model 데이터베이스와 데이터 정렬이 동일한 새로운 테이블로 가져옵니다.  
  
-   사용자 데이터베이스 데이터 정렬과 일치하는 데이터 정렬을 사용하도록 시스템 데이터베이스를 다시 작성합니다. 시스템 데이터베이스를 다시 작성 하는 방법에 대 한 자세한 내용은 [시스템 데이터베이스 다시 작성](../relational-databases/databases/system-databases.md)을 참조 하세요.  
  
-   사용자 테이블을 tempdb의 테이블에 조인하는 저장 프로시저는 사용자 데이터베이스의 데이터 정렬을 사용하여 tempdb에 테이블을 만들도록 수정합니다. 이렇게 하려면 다음 예에서와 같이 임시 테이블의 열 정의에 `COLLATE database_default` 절을 추가합니다.  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>참조 항목  
 [데이터베이스 데이터 정렬 설정 또는 변경](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [열 데이터 정렬 설정 또는 변경](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE&#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)  
  
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Microsoft 기술 자료 문서 325335](https://go.microsoft.com/fwlink/?linkid=117751)  
  
 [방법: 명령 프롬프트에서 SQL Server 2008 설치](https://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
