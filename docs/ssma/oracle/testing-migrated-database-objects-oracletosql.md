---
title: 마이그레이션된 데이터베이스 개체 테스트 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 858c564c965fe7105c86a3087923887097e4ddac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266476"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>마이그레이션된 데이터베이스 개체 테스트(OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle 테스터 (SSMA 테스터)의 Migration Assistant는 데이터베이스 개체 변환과 SSMA에서 수행한 데이터 마이그레이션을 자동으로 테스트 합니다. 모든 SSMA 마이그레이션 단계를 완료 한 후 SSMA 테스터를 사용 하 여 변환 된 개체가 동일한 방식으로 작동 하 고 모든 데이터가 제대로 전송 되었는지 확인 합니다.  
  
SSMA 테스터를 사용 하 여 다음 개체 유형을 테스트할 수 있습니다.  
  
-   테이블  
  
-   패키지 프로시저를 비롯 한 저장 프로시저  
  
-   패키지 된 함수를 포함 하는 사용자 정의 함수  
  
-   뷰.  
  
-   독립 실행형 문.  
  
SSMA 테스터는 Oracle에서 테스트를 위해 선택한 개체와의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]해당 개체를 실행 합니다. 그 후에는 다음 기준에 따라 결과를 비교 합니다.  
  
-   테이블 데이터의 변경 내용이 동일 합니까?  
  
-   프로시저 및 함수에 대 한 출력 매개 변수 값이 동일 한가요?  
  
-   함수는 동일한 결과를 반환 하나요?  
  
-   결과 집합이 동일 합니까?  
  
> [!NOTE]  
> 주의! 프로덕션 시스템에서는 SSMA 테스터를 사용 하지 마세요. 테스터를 실행 하는 동안 원본 스키마와 데이터가 수정 됩니다. 한편, 일부 형식의 테스트 된 코드에서는 원래 상태의 전체 복원을 수행할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
SSMA 테스터를 사용 하려는 경우에는 **테스터 데이터베이스 설치** 옵션이 설정 된 상태로 Ssma Oracle 확장 팩을 설치 합니다.  
  
결과 테이블 데이터의 비교를 사용 하려면 스키마 변환이 시작 되기 전에 **ROWID 열 생성** 옵션을 **예** 로 설정 합니다. SSMA는 **스키마 변환** 명령을 실행 하는 동안 모든 테이블에 ROWID 열을 추가 합니다.  
  
또한 다음을 확인 합니다.  
  
-   Oracle 클라이언트 도구는를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 하는 컴퓨터에 설치 됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에서 CLR (공용 언어 런타임) 통합을 사용 하도록 설정 했습니다.  
  
현재 버전의 SSMA 테스터는 동일한 원본 또는 대상 서버에 있는 다른 사용자의 병렬 실행을 지원 하지 않습니다.  
  
## <a name="getting-started"></a>시작하기  
[OracleToSQL&#41;&#40;테스트 사례 만들기](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SQL Server &#40;OracleToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[프로젝트 설정 &#40;변환&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
