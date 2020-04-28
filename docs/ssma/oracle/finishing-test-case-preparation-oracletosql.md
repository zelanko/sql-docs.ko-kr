---
title: 테스트 사례 준비 완료 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: bc5693c71ac6061f12ee90386b3c135a45a14e09
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266069"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>테스트 사례 준비 완료(OracleToSQL)
마법사의 마지막 페이지에는 테스트 사례 설명 및 테스트와 관련 된 개체에 대 한 정보가 표시 됩니다. 또한이 페이지에서 테스트 실행 옵션을 설정할 수 있습니다.  
  
테스트 **사례 정보** 섹션에는 테스트 사례 이름과 설명이 표시 됩니다.  
  
**테스트 하도록 선택한 개체** 섹션에는 개체 유형별로 그룹화 된 테스트 된 개체의 명명 된 목록이 포함 되어 있습니다.  
  
**분석할 테스트의 영향을 받는 개체** 섹션에는 테스트 된 개체 실행 후 데이터 변경 내용을 비교 해야 하는 개체의 명명 된 목록이 표시 됩니다.  
  
## <a name="test-case-settings"></a>테스트 사례 설정  
**테스트 사례 설정** 섹션에서 다음 실행 테스트 옵션을 설정할 수 있습니다.  
  
### <a name="stop-test-execution-after-first-failure"></a>첫 번째 실패 후 테스트 실행 중지  
테스트를 실행 하는 동안 오류가 발생 하는 경우 테스트를 중단 하도록 지정 합니다.  
  
-   **예**를 선택 하면 오류가 발생 하는 경우 테스트 실행이 중단 됩니다.  
  
-   **아니요**를 선택 하면 오류 발생 후 테스트 실행이 계속 됩니다.  
  
### <a name="perform-data-rollback"></a>데이터 롤백 수행  
테스트 실행 후 자동 데이터 롤백을 사용 하도록 설정 합니다.  
  
-   **예**를 선택 하면 테스트 실행 후 데이터 변경 내용이 손실 됩니다.  
  
-   **아니요**를 선택 하면 모든 테스트 실행 데이터 변경 내용이 저장 됩니다.  
  
### <a name="auxiliary-tables-saving-mode"></a>보조 테이블 저장 모드  
테스트 실행 중에 생성 된 보조 테이블의 저장 모드를 정의 합니다. [실행 중인 테스트 사례 &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md) 항목에서 보조 테이블의 설명을 참조 하세요.  
  
-   **항상 저장**을 선택 하는 경우 보조 테이블 데이터는 나중에 사용할 수 있도록 항상 저장 됩니다.  
  
-   **테이블 비교가 실패 한 경우 저장**을 선택 하면 오류가 발생 하는 경우에만 보조 테이블 데이터가 저장 됩니다.  
  
-   **항상 삭제**를 선택 하는 경우 테스트 실행 후 보조 테이블이 항상 삭제 됩니다.  
  
-   **테이블 비교가 실패 한 경우 사용자에 게 요청**을 선택 하면 오류가 발생 하는 경우 사용자가 필요한 작업을 선택할 수 있습니다.  
  
[테스트 리포지토리 (OracleToSQL)를 사용 하 여](https://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4)준비 된 테스트 사례를 저장 하려면 **마침** 단추를 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
[OracleToSQL&#41;&#40;테스트 리포지토리 사용](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[OracleToSQL&#41;&#40;테스트 사례 실행](../../ssma/oracle/running-test-cases-oracletosql.md)  
[OracleToSQL&#41;&#40;마이그레이션된 데이터베이스 개체 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
