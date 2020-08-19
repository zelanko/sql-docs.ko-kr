---
description: 테스트 리포지토리 사용(SybaseToSQL)
title: 테스트 리포지토리 사용 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b05dac0ec74bb6c0cd9c9e99d8bb631b0a242eb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418249"
---
# <a name="using-test-repositories-sybasetosql"></a>테스트 리포지토리 사용(SybaseToSQL)
SSMA 테스트 리포지토리는 나중에 사용 하기 위해 SSMA 테스터 테스트 사례와 테스트 결과를 저장 합니다. 리포지토리 데이터는 **ssmatesterdb_syb** 데이터베이스의 스키마 **Ssma_sybase_utilities** SQL Server 테이블 **TestCaseRepository** 및 **RunTestCaseResultRepository** 에 저장 됩니다.  
  
다음 단추는 테스트 사례 리포지토리 대화 상자에서 사용할 수 있습니다.  
  
-   **새로 고침** 단추를 클릭 하 여 테스트 사례 또는 테스트 결과 목록을 새로 고칩니다.  
  
-   **닫기** 단추를 클릭 하 여 테스트 사례의 리포지토리를 닫습니다. 대화 상자  
  
## <a name="test-cases-repository"></a>테스트 사례 리포지토리  
**테스터** 메뉴에서 **테스트 사례 ...** 를 클릭 하 여 테스트 사례 리포지토리를 볼 수 있습니다. 그러면 SSMA **는 테스트 사례 페이지에** 저장 된 테스트 사례 목록과 함께 **테스트 사례 리포지토리** 대화 상자 창을 표시 합니다.  
  
표에는 각 테스트 사례에 대 한 다음과 같은 정보가 표시 됩니다.  
  
-   이름: 테스트 사례 이름입니다.  
  
-   만든 날짜: 테스트 사례를 만든 날짜입니다.  
  
-   수정 됨: 테스트 사례 마지막 수정 날짜입니다.  
  
-   설명: 테스트 사례 설명입니다.  
  
다음 단추는 테스트 사례 페이지에서 사용할 수 있습니다.  
  
-   **추가** 단추를 클릭 하 여 테스트 사례 마법사를 실행 하 고 새 테스트를 만듭니다.  
  
-   선택한 테스트를 리포지토리에서 삭제 하려면 **제거** 단추를 클릭 합니다. 테스트 사례를 삭제 하면 관련 된 모든 테스트 결과도 삭제 됩니다.  
  
-   **편집** 단추를 클릭 하 여 테스트 사례 마법사를 실행 하 고 선택한 테스트를 변경 합니다.  
  
-   **실행** 단추를 클릭 하 여 [실행 중인 테스트 사례 &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md) 대화 상자를 열고 선택한 테스트를 실행 합니다.  
  
## <a name="test-results-repository"></a>테스트 결과 리포지토리  
**테스트 사례 창의 리포지토리의** **테스트 결과** 페이지에서 테스트 결과 리포지토리를 볼 수 있습니다. **테스터** 메뉴에서 **테스트 결과 ...** 을 클릭 하 여 엽니다.  
  
**테스트 결과** 페이지에서 두 개의 필터를 사용할 수 있습니다.  
  
-   테스트 사례 이름 필터: 테스트 결과를 테스트 사례 이름별로 선택할 수 있습니다. 이 필터의 **모든 테스트 사례** 값을 통해 모든 테스트 사례에 대 한 테스트 결과를 표시할 수 있습니다.  
  
-   테스트 사례 실행 날짜 필터: 저장 된 날짜를 기준으로 테스트 결과를 필터링 합니다. 이 필터의 **모든 기간** 값을 사용 하면 저장 된 날짜에 대 한 테스트 결과를 표시할 수 있습니다.  
  
테스트 결과에 대 한 다음 정보가 표에 표시 됩니다.  
  
-   이름: 테스트 사례 이름입니다.  
  
-   Started: 실행 중인 테스트 사례 날짜입니다.  
  
-   Result: 테스트 실행에 대 한 간단한 요약입니다 (이 셀의 도구 팁은 테스트 실행의 전체 요약을 표시 합니다).  
  
테스트 결과 페이지에서 사용할 수 있는 단추는 다음과 같습니다.  
  
-   **보기** 단추를 클릭 하 여 [테스트 사례 보고서 보기 &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md) 현재 테스트 사례 결과를 엽니다.  
  
-   선택한 테스트 결과를 삭제 하려면 **삭제** 단추를 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
[테스트 사례 실행 &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
