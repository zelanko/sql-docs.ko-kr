---
title: "테스트 리포지토리 (OracleToSQL)를 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c3d2c6665c6d1852b291e69d2494343b5000ac06
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="using-test-repositories-oracletosql"></a>테스트 리포지토리 (OracleToSQL) 사용 하 고
SSMA 테스트 리포지토리 저장소 SSMA 테스터가 테스트 사례 및 테스트 결과 나중에 사용할 수 있습니다. 리포지토리 데이터는 SQL Server 테이블에 저장 됩니다 **TestCaseRepository** 및 **RunTestCaseResultRepository** 스키마에 **ssma_oracle_utilities** 의 **ssmatesterdb** 데이터베이스입니다.  
  
테스트 사례 저장소 대화 상자에서 다음 단추를 사용할 수 있습니다:  
  
-   클릭는 **새로 고침** 단추 테스트 사례 또는 테스트 결과 목록을 새로 고칩니다.  
  
-   클릭는 **닫습니다** 단추 테스트 사례 저장소 대화 상자를 닫습니다.  
  
## <a name="test-cases-repository"></a>테스트 사례 리포지토리  
클릭 하 여 테스트 사례 리포지토리를 볼 수 있습니다 **테스트 사례 중...** **테스터** 메뉴. SSMA 다음 표시는 **저장소의 테스트 사례** 에 저장 된 테스트 사례의 목록 사용 하 여 대화 상자 창에서 **테스트 사례** 페이지.  
  
눈금에는 각 테스트 사례에 대 한 다음 정보가 표시 됩니다.  
  
-   이름: 테스트 사례 이름입니다.  
  
-   만든: 테스트 사례를 만든 날짜.  
  
-   수정 된: 테스트 사례 마지막으로 수정한 날짜입니다.  
  
-   설명: 테스트 사례 설명입니다.  
  
테스트 사례 페이지에서 사용할 수는 다음과 같은 단추가 있습니다.  
  
-   클릭는 **추가** 단추 테스트 사례 마법사를 실행 하 고 새 테스트를 만들어야 합니다.  
  
-   클릭는 **제거** 단추 저장소에서 선택된 된 테스트를 선택 합니다. 테스트 사례를 삭제 하면 모든 관련된 테스트 결과 삭제 됩니다.  
  
-   클릭는 **편집** 단추를 테스트 사례 마법사를 실행 하 고 선택한 테스트를 변경 합니다.  
  
-   클릭는 **실행** 버튼을 클릭은 [테스트 사례 실행 (OracleToSQL)](http://msdn.microsoft.com/en-us/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02) 대화 하 고 선택한 테스트를 실행 합니다.  
  
## <a name="test-results-repository"></a>테스트 결과 리포지토리  
테스트 결과 리포지토리를 볼 수 있습니다는 **테스트 결과** 의 페이지는 **테스트 사례 리포지토리** 창. 클릭 하 여 열 **테스트 결과 중...** **테스터** 메뉴.  
  
두 개의 필터를 사용 하 여에 **테스트 결과** 페이지:  
  
-   테스트 사례 이름 필터: 테스트 사례 이름으로 테스트 결과 선택 합니다. 이 필터 **모든 테스트 사례** 값을 사용 하면 모든 테스트 사례에 대 한 테스트 결과 표시 합니다.  
  
-   테스트 사례 실행 날짜 필터: 필터 테스트 결과 저장의 날짜입니다. 이 필터 **모든 기간** 값을 사용 하면 저장의 모든 날짜에 대 한 테스트 결과 표시 합니다.  
  
테스트 결과 대 한 다음 정보는 표에 표시 됩니다.  
  
-   이름: 테스트 사례 이름입니다.  
  
-   저장: 테스트 사례 날짜를 저장 합니다.  
  
-   결과: (이 셀의 도구 설명 테스트 실행의 전체 요약을 표시 하는 데 사용) 테스트 실행의 짧은 요약 합니다.  
  
테스트 결과 페이지에서 사용할 수는 다음과 같은 단추가 있습니다.  
  
-   클릭는 **보기** 버튼을 클릭 [테스트 사례 보고서 보기 &#40; OracleToSQL &#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) 현재 테스트 사례 결과입니다.  
  
-   클릭는 **삭제** 선택한 테스트 결과 삭제 하려면 단추  
  
## <a name="see-also"></a>관련 항목:  
[실행 중인 테스트 사례 &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[데이터베이스 개체 &#40; OracleToSQL &#41; 마이그레이션 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

