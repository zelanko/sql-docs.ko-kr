---
title: 마이그레이션된 데이터베이스 개체 (OracleToSQL) 테스트 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 771e9a4553679ae2afa0dd58d83b1d15ccf0fd62
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684321"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>마이그레이션된 데이터베이스 개체 테스트(OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA 테스터) Oracle 테스터를 위한 데이터베이스 개체를 변환 하 고 SSMA 수행한 데이터 마이그레이션에 자동으로 테스트 합니다. 모든 SSMA 마이그레이션 단계가 완료 되 면 모든 데이터가 제대로 전송 된 및 변환 된 개체가 동일한 방식으로 작동 하는지 확인 하려면 SSMA 테스터를 사용 합니다.  
  
다음 개체 형식 SSMA 테스터를 사용 하 여 테스트할 수 있습니다.  
  
-   테이블  
  
-   패키지 된 프로시저를 비롯 한 저장된 프로시저입니다.  
  
-   사용자 정의 함수를 포함 하 여 함수를 패키지 합니다.  
  
-   뷰.  
  
-   독립 실행형 문입니다.  
  
Oracle과의 해당 요소에 대해 테스트를 위해 선택한 개체를 실행 하는 SSMA 테스터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 그 다음 조건에 따라 결과를 비교합니다.  
  
-   동일한 테이블 데이터의 변경 사항은?  
  
-   프로시저 및 함수에 대 한 출력 매개 변수 값은 동일?  
  
-   함수는 동일한 결과 반환지 않습니다?  
  
-   결과 집합이 동일한?  
  
> [!NOTE]  
> 주의! 프로덕션 시스템에서 SSMA 테스터를 사용 하지 않습니다. 테스터가 실행 하는 동안 소스 스키마와 데이터 수정 됩니다. 한편, 원래 상태 전체 복원 테스트 된 코드의 일부 형식에 대 한 가능한 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
SSMA 테스터를 사용 하려는 경우 사용 하 여 SSMA Oracle 확장 팩을 설치 합니다 **테스터 데이터베이스 설치** 옵션을 설정 합니다.  
  
결과 테이블 데이터의 비교를 사용 하도록 설정 하려면 설정 합니다 **ROWID 생성 열** 옵션을 **예** 스키마 변환을 시작 하기 전에 합니다. SSMA 실행 하는 동안 모든 테이블에 행 ID 열에 추가 됩니다는 **스키마 변환** 명령입니다.  
  
또한 다음을 확인 합니다.  
  
-   Oracle 클라이언트 도구가 컴퓨터에 설치 되어 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 합니다.  
  
-   공용 언어 런타임 (CLR) 통합을 사용 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진입니다.  
  
SSMA 테스터의 현재 버전은 동일한 원본 또는 대상 서버에서 다른 사용자가 병렬 실행을 지원 하지 note 합니다.  
  
## <a name="getting-started"></a>시작  
[테스트 사례 만들기 &#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 SSMA 구성 요소를 설치 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[프로젝트 설정 &#40;변환&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
