---
title: "데이터베이스 개체 (OracleToSQL) 마이그레이션 테스트 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 4b5f343234e77639e0b10eb07bce8281da9010f4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="testing-migrated-database-objects-oracletosql"></a>데이터베이스 개체 (OracleToSQL) 마이그레이션 테스트
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA 테스터) Oracle 테스터를 위한 데이터베이스 개체 변환 및 SSMA 수행한 데이터 마이그레이션에 자동으로 테스트 합니다. 모든 SSMA 마이그레이션 단계가 완료 되 면 SSMA 테스터를 사용 하 여 변환 된 개체가 같은 방식으로 작동 하는지 되 고 모든 데이터가 제대로 전송 되었습니다.  
  
개체 유형 SSMA 테스터를 테스트할 수 있습니다.  
  
-   테이블  
  
-   패키지에 포함 된 프로시저를 비롯 한 저장된 프로시저입니다.  
  
-   사용자 정의 함수를 포함 하 여 패키지 기능.  
  
-   뷰.  
  
-   독립 실행형 문입니다.  
  
Oracle 및 해당 항목에 대해 테스트를 위해 선택한 개체를 실행 하는 SSMA 테스터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 그 후 다음 기준에 따라 결과 비교 합니다.  
  
-   동일한 테이블 데이터에 변경 내용을 있습니까?  
  
-   프로시저 및 함수에 대 한 출력 매개 변수 값 동일는 무엇입니까?  
  
-   함수는 동일한 결과 반환 수행?  
  
-   동일한 결과 집합은?  
  
> [!NOTE]  
> 주의! 프로덕션 시스템에서 SSMA 테스터를 사용 하지 마십시오. 테스터 실행 하는 동안 소스 스키마와 데이터 수정 됩니다. 한편, 원래 상태로의 전체 restoring 일부 유형의 테스트 된 코드에 대 한 가능한 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA 테스터를 사용 하려는 경우와 SSMA Oracle 확장 팩을 설치는 **테스터 데이터베이스 설치** 옵션을 설정 합니다.  
  
결과 테이블 데이터의 비교를 사용 하도록 설정 하기 위해 설정 된 **생성 행 ID 열** 옵션을 **예** 스키마 변환을 시작 하기 전에. SSMA 실행 하는 동안 모든 테이블에 행 ID 열에 추가 됩니다는 **변환 스키마** 명령입니다.  
  
또한 다음을 확인 합니다.  
  
-   Oracle 클라이언트 도구가 컴퓨터에 설치 되어 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 실행 합니다.  
  
-   에 대해 공용 언어 런타임 (CLR) 통합이 활성화는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 엔진입니다.  
  
Note SSMA 테스터의 현재 버전 동일한 원본 또는 대상 서버에 여러 사용자가 병렬 실행을 지원 하지 않습니다.  
  
## <a name="getting-started"></a>시작  
[테스트 사례 &#40; OracleToSQL &#41; 만들기](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server &#40; OracleToSQL &#41;에 SSMA 구성 요소 설치](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[프로젝트 설정 &#40; 변환 &#41; &#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
