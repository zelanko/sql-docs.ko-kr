---
title: "완료 하는 테스트 사례 준비 (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92bb189027afd6c5e91428017c5aa356676d575c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="finishing-test-case-preparation-oracletosql"></a>테스트 사례 준비 (OracleToSQL)를 완료합니다.
마법사의 마지막 페이지에는 테스트 사례 설명 및 테스트에 관련 된 개체에 대 한 정보가 표시 됩니다. 또한이 페이지에서 설정할 수 있습니다는 테스트 실행 옵션.  
  
**테스트 사례 정보** 섹션에는 테스트 사례 이름 및 설명을 표시 합니다.  
  
**개체 선택에 테스트할** 섹션에는 명명 된 개체 유형별로 그룹화 된 테스트 거친된 개체 목록이 포함 되어 있습니다.  
  
**개체 영향을 받는 하 여 테스트 하는 분석할** 섹션에는 명명 된 데이터 변경 내용을 테스트 거친된 개체 실행 후 비교 해야 하는 개체 목록이 표시 됩니다.  
  
## <a name="test-case-settings"></a>테스트 사례 설정  
에 **테스트 사례 설정** 섹션 다음 실행 테스트 옵션을 설정할 수 있습니다.  
  
### <a name="stop-test-execution-after-first-failure"></a>첫 번째 실패 후 테스트 실행을 중지  
테스트 실행 중 오류가 발생 하는 경우 테스트를 중단 하도록 지정 합니다.  
  
-   선택 하면 **예**, 오류가 발생 하면 실행이 중단을 테스트 합니다.  
  
-   선택 하면 **아니요**, 오류가 발생 한 후 테스트 실행이 계속 됩니다.  
  
### <a name="perform-data-rollback"></a>데이터 롤백을 수행합니다  
테스트 실행 후 데이터 자동 롤백을 지원합니다.  
  
-   선택 하면 **예**, 테스트가 실행 된 후 데이터 변경 내용이 손실 됩니다.  
  
-   선택 하면 **아니요**, 모든 데이터 변경 내용이 저장 되는 실행을 테스트 합니다.  
  
### <a name="auxiliary-tables-saving-mode"></a>보조 테이블 절약 모드  
테스트 실행 중 생성 된 보조 테이블에 대 한 저장 모드를 정의 합니다. 보조 테이블에 대 한 설명을 참조는 [테스트 사례 실행 &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md) 항목입니다.  
  
-   선택 하는 경우 **항상 저장**, 보조 테이블 데이터는 나중에 사용할 항상 저장 됩니다.  
  
-   선택 하는 경우 **테이블 비교에 실패 한 경우 저장**, 오류가 발생 하는 경우에 보조 테이블 데이터가 저장 됩니다.  
  
-   선택 하는 경우 **항상 삭제**, 보조 테이블 항상 테스트가 실행 된 후 삭제 합니다.  
  
-   선택 하는 경우 **테이블 비교에 실패 한 경우 사용자에 게 요청**, 오류가 발생 하는 경우 사용자가 필요한 작업을 선택할 수 있습니다.  
  
클릭는 **마침** 에 준비 된 테스트 사례를 저장 하려면 단추 [테스트 리포지토리를 사용 하 여 (OracleToSQL)](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)합니다.  
  
## <a name="see-also"></a>참고 항목  
[테스트 저장소 &#40; OracleToSQL &#41;를 사용 하 여](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[실행 중인 테스트 사례 &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[데이터베이스 개체 &#40; OracleToSQL &#41; 마이그레이션 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

