---
title: 테스트 사례 (OracleToSQL) 실행 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 537865967d0e43b7dd9501f9fbb7b9605f5b9367
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625802"
---
# <a name="running-test-cases-oracletosql"></a>테스트 사례 실행(OracleToSQL)
SSMA 테스터는 테스트 사례를 실행 하면 테스트를 위해 선택한 개체를 실행 하 고 확인 결과 대 한 보고서를 만듭니다. 결과 두 플랫폼 모두에서 동일한 경우 테스트에 성공 합니다. Oracle 간에 개체의 관계 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 SSMA 프로젝트에 스키마 매핑 설정에 따라 결정 됩니다.  
  
성공적인 테스트에 대 한 필요한 요구 사항은 모든 Oracle 개체 변환 되 고 대상 데이터베이스에 로드입니다. 또한 두 플랫폼 모두에서 테이블의 내용을 동기화 되도록 테이블 데이터를 마이그레이션할 수 해야 합니다.  
  
## <a name="run-test-case"></a>테스트 사례 실행  
준비 테스트 사례를 실행 합니다.  
  
1.  클릭 합니다 **실행** 단추입니다.  
  
2.  에 **Oracle에 연결** 대화 상자에서 연결 정보를 입력 한 다음 클릭 **Connect**합니다.  
  
테스트가 완료 되 면 테스트 사례 보고서가 생성 됩니다. 클릭 합니다 **보고서** 보려면 단추를 [테스트 사례 보고서](viewing-test-case-reports-oracletosql.md)합니다. 테스트 (테스트 사례 보고서)의 결과에 자동으로 저장 되는 [테스트 결과 리포지토리](using-test-repositories-oracletosql.md) 나중에 사용할 수 있습니다.  
  
## <a name="test-case-execution-steps"></a>테스트 사례 실행 단계  
  
### <a name="prerequisites"></a>사전 요구 사항  
SSMA 테스터는 테스트를 시작 하기 전에 테스트 실행에 대 한 모든 필수 조건이 충족 하는 경우를 확인 합니다. 일부 조건이 충족 되지 않은 경우 오류 메시지가 표시 됩니다.  
  
### <a name="initialization"></a>초기화  
이 단계에서 SSMA 테스터는 Oracle 서버의 SSMATESTER_ORACLE 스키마의 보조 개체 (테이블, 트리거 및 뷰)를 만듭니다. 확인을 위해 선택한 영향을 받는 개체에서 변경 추적 수 있습니다.  
  
확인 된 테이블 USER_TABLE를 지정 하 고는 가정 합니다. 이러한 테이블에 대해 다음과 같은 보조 개체는 Oracle에서 생성 됩니다.  
  
||||  
|-|-|-|  
|이름|형식|Description|  
|USER_TABLE$Trg|트리거|확인 된 테이블의 변경 내용을 감사 하는 트리거.|  
|USER_TABLE$ AUD|테이블|테이블을 삭제 하 고 덮어쓸 행을 저장 합니다.|  
|USER_TABLE$ AUDID|테이블|새로운 기능과 변경 된 행을 저장 하는 테이블입니다.|  
|USER_TABLE|뷰|테이블 수정의 간소화 된 표현입니다.|  
|새 USER_TABLE $|뷰|삽입 되거나 덮어쓸 행의 간소화 된 표현입니다.|  
|USER_TABLE$NEW_ID|뷰|삽입 되거나 변경 된 행의 id입니다.|  
|USER_TABLE$ 이전|뷰|행을 삭제 하 고 덮어쓸의 간소화 된 표현입니다.|  
  
다음 개체에 확인 된 테이블의 스키마에 만들어집니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
||||  
|-|-|-|  
|이름|형식|Description|  
|USER_TABLE$Trg|트리거|확인 된 테이블의 변경 내용을 감사 하는 트리거.|  
  
다음 개체에서 생성 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ssmatesterdb 데이터베이스에 있습니다.  
  
||||  
|-|-|-|  
|이름|형식|Description|  
|USER_TABLE$Aud|테이블|테이블을 삭제 하 고 덮어쓸 행을 저장 합니다.|  
|USER_TABLE$AudID|테이블|새로운 기능과 변경 된 행을 저장 하는 테이블입니다.|  
|USER_TABLE|뷰|테이블 수정의 간소화 된 표현입니다.|  
|USER_TABLE$new|뷰|삽입 되거나 덮어쓸 행의 간소화 된 표현입니다.|  
|USER_TABLE$new_id|뷰|삽입 되거나 변경 된 행의 id입니다.|  
|USER_TABLE$old|뷰|행을 삭제 하 고 덮어쓸의 간소화 된 표현입니다.|  
  
### <a name="test-object-calls"></a>테스트 개체 호출  
이 단계에서 SSMA 테스터 호출 테스트를 위해 선택한 개체 마다, 결과 비교 하 고 보고서를 보여 줍니다.  
  
### <a name="finalization"></a>종료  
종료 하는 동안 SSMA 테스터에서 만든 보조 개체를 정리 합니다 **초기화** 단계입니다.  
  
## <a name="next-step"></a>다음 단계  
[테스트 사례 보고서 보기 &#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>관련 항목  
[테스트할 개체 선택 및 구성 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[영향을 받는 개체 선택 및 구성 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[마이그레이션된 데이터베이스 개체 테스트 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
