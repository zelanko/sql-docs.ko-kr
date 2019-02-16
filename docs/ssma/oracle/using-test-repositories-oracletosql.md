---
title: 테스트 리포지토리 (OracleToSQL)를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cae34190da8179663996c7a385cc13541353ee0d
ms.sourcegitcommit: 769b71f01052ec9b4fc5eb02d9da9a1a58118029
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56319244"
---
# <a name="using-test-repositories-oracletosql"></a>테스트 리포지토리 사용(OracleToSQL)
SSMA 테스트 리포지토리 저장소 SSMA 테스터가 테스트 사례와 나중에 사용할 테스트 결과입니다. 리포지토리 데이터를 SQL Server 테이블에 저장 됩니다 **TestCaseRepository** 하 고 **RunTestCaseResultRepository** 스키마에서 **ssma_oracle_utilities** 의**ssmatesterdb** 데이터베이스입니다.  
  
테스트 사례 저장소 대화 상자에서 다음 단추는 사용할 수 있습니다.  
  
-   클릭 합니다 **새로 고침** 테스트 사례 또는 테스트 결과 목록을 새로 고치려면 단추입니다.  
  
-   클릭 합니다 **닫습니다** 테스트 사례 저장소 대화 상자를 닫으려면 단추입니다.  
  
## <a name="test-cases-repository"></a>테스트 사례 리포지토리  
클릭 하 여 테스트 사례 저장소를 볼 수 있습니다 **테스트 사례는 중...**  에서 합니다 **테스터** 메뉴. SSMA 다음 표시는 **리포지토리의 테스트 사례** 에 저장 된 테스트 사례의 목록 사용 하 여 대화 상자 창 합니다 **테스트 사례** 페이지.  
  
표 형식으로 각 테스트 사례에 대 한 다음 정보를 표시 합니다.  
  
-   이름: 테스트 사례 이름입니다.  
  
-   만들어집니다. 테스트 사례 생성 날짜입니다.  
  
-   수정한 날짜: 테스트 사례를 마지막으로 수정한 날짜입니다.  
  
-   설명: 테스트 사례 설명입니다.  
  
다음 단추는 테스트 사례 페이지 에서도 다운로드 가능:  
  
-   클릭 합니다 **추가** 단추를 테스트 사례 마법사를 실행 하 고 새 테스트를 만듭니다.  
  
-   클릭 합니다 **제거** 리포지토리에서 선택한 테스트를 삭제 하려면 단추입니다. 테스트 사례를 삭제 하면 모든 관련된 테스트 결과 삭제 됩니다.  
  
-   클릭 합니다 **편집** 테스트 사례 마법사를 실행 하 고 선택한 테스트를 변경 하는 단추입니다.  
  
-   클릭 합니다 **실행** 버튼을 클릭 하는 [테스트 사례 실행 (OracleToSQL)](https://msdn.microsoft.com/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02) 대화 하 고 선택한 테스트를 실행 합니다.  
  
## <a name="test-results-repository"></a>테스트 결과 리포지토리  
테스트 결과 리포지토리를 볼 수 있습니다 합니다 **테스트 결과** 페이지의 **저장소의 테스트 사례** 창. 클릭 하 여 열 **테스트 결과 중...**  에서 합니다 **테스터** 메뉴.  
  
두 개의 필터를 사용할 수 있습니다 **테스트 결과** 페이지:  
  
-   테스트 사례 이름 필터: 테스트 사례 이름으로 테스트 결과 선택할 수 있습니다. 이 필터 **모든 테스트 사례** 값을 사용 하면 모든 테스트 사례에 대 한 테스트 결과 표시 합니다.  
  
-   테스트 사례 실행 날짜 필터: 필터 저장 하는 날짜별으로 결과 테스트합니다. 이 필터 **모든 기간** 값을 사용 하면 저장 하는 모든 날짜에 대 한 테스트 결과 표시 합니다.  
  
테스트 결과 대해 다음 정보는 표에 표시 됩니다.  
  
-   이름: 테스트 사례 이름입니다.  
  
-   저장: 저장 하는 테스트 사례 날짜입니다.  
  
-   결과: (이 셀의 도구 설명 전체 테스트 실행 요약을 표시 하는 데 사용) 테스트 실행의 한 간단한 요약입니다.  
  
다음 단추는 테스트 결과 페이지에서 사용할 수 있습니다.  
  
-   클릭 합니다 **보기** 버튼을 클릭 하 [테스트 사례 보고서 보기 &#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) 현재 테스트 사례 결과입니다.  
  
-   클릭 합니다 **삭제** 선택한 테스트 결과 삭제 하려면 단추  
  
## <a name="see-also"></a>관련 항목  
[테스트 사례 실행 &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[마이그레이션된 데이터베이스 개체 테스트 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
