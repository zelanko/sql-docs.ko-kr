---
title: 테스트 사례 준비 (OracleToSQL) 완료 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 1b66f63b66066831d7e0276049d774136c1b5138
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743821"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>테스트 사례 준비 완료(OracleToSQL)
마법사의 마지막 페이지를 테스트 사례 설명 및 테스트에 관련 된 개체에 대 한 정보를 표시합니다. 또한이 페이지에서 설정할 수 있습니다 테스트 실행 옵션.  
  
합니다 **테스트 사례 정보** 섹션에는 테스트 사례 이름 및 설명을 보여 줍니다.  
  
합니다 **개체 선택에 테스트할** 섹션에 명명 된 개체 유형별로 그룹화 된 테스트 거친된 개체 목록이 포함 되어 있습니다.  
  
합니다 **개체의 영향을 하 여 테스트를 분석할** 섹션에는 데이터 변경 내용을 테스트 개체 실행 후 비교 해야 하는 개체의 명명 된 목록이 표시 됩니다.  
  
## <a name="test-case-settings"></a>테스트 사례 설정  
에 **테스트 사례 설정** 섹션 다음 실행 테스트 옵션을 설정할 수 있습니다.  
  
### <a name="stop-test-execution-after-first-failure"></a>첫 번째 실패 후 테스트 실행을 중지  
테스트 실행 중에 오류가 발생 하는 경우 테스트를 중단 하도록 지정 합니다.  
  
-   선택 하면 **예**, 오류가 발생 하면 실행이 중단을 테스트 합니다.  
  
-   선택 하면 **No**, 오류가 발생 한 후 테스트 실행이 계속 됩니다.  
  
### <a name="perform-data-rollback"></a>데이터 롤백 수행  
테스트 실행 후 자동 데이터 롤백을 수 있습니다.  
  
-   선택 하면 **예**, 테스트 실행 후 데이터 변경 내용이 손실 됩니다.  
  
-   선택 하면 **No**, 모든 테스트 실행 데이터 변경 내용이 저장 됩니다.  
  
### <a name="auxiliary-tables-saving-mode"></a>보조 테이블 절약 모드  
테스트 실행 중 생성 된 보조 테이블에 대 한 저장 모드를 정의 합니다. 보조 테이블에 대 한 설명을 참조 합니다 [테스트 사례 실행 &#40;OracleToSQL&#41; ](../../ssma/oracle/running-test-cases-oracletosql.md) 항목입니다.  
  
-   선택 하는 경우 **항상 저장**, 나중에 사용할 항상 보조 테이블 데이터가 저장 됩니다.  
  
-   선택 하는 경우 **저장 테이블 비교에 실패 한 경우**, 오류가 발생 하는 경우에 보조 테이블 데이터가 저장 됩니다.  
  
-   선택 하는 경우 **언제 든 지 삭제할**, 항상 보조 테이블 테스트가 실행 된 후 삭제할 수 있습니다.  
  
-   선택 하는 경우 **테이블 비교에 실패 한 경우 사용자에 게**, 오류가 발생 하는 경우에 필요한 작업을 선택할 수 있습니다.  
  
클릭 합니다 **완료** 준비 테스트 사례를 저장 하려면 단추 [테스트 리포지토리 사용 (OracleToSQL)](http://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)합니다.  
  
## <a name="see-also"></a>관련 항목  
[테스트 리포지토리를 사용 하 여 &#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[테스트 사례 실행 &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[마이그레이션된 데이터베이스 개체 테스트 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
