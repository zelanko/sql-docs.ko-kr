---
description: 마이그레이션된 데이터베이스 개체 테스트(SybaseToSQL)
title: 마이그레이션된 데이터베이스 개체 테스트 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cfe57d436eac38052542eb2ed6c2133aab7ca07b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480400"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>마이그레이션된 데이터베이스 개체 테스트(SybaseToSQL)
Sybase 테스터 (SSMA 테스터)의 Microsoft SQL Server Migration Assistant는 데이터베이스 개체 변환과 SSMA에서 수행한 데이터 마이그레이션을 자동으로 테스트 합니다. 모든 SSMA 마이그레이션 단계를 완료 한 후 SSMA 테스터를 사용 하 여 변환 된 개체가 동일한 방식으로 작동 하 고 모든 데이터가 제대로 전송 되었는지 확인 합니다.  
  
> [!NOTE]  
> Azure 연결의 경우 테스터 구성 요소를 사용할 수 없습니다.  
  
SSMA 테스터를 사용 하 여 다음 개체 유형을 테스트할 수 있습니다.  
  
-   테이블  
  
-   저장 프로시저  
  
-   뷰.  
  
-   독립 실행형 문.  
  
SSMA 테스터는 Sybase에서 테스트 하기 위해 선택한 개체와 SQL Server의 해당 개체를 실행 합니다. 그 후에는 다음 기준에 따라 결과를 비교 합니다.  
  
-   테이블 데이터의 변경 내용이 동일 합니까?  
  
-   프로시저 및 함수에 대 한 출력 매개 변수 값이 동일 한가요?  
  
-   함수는 동일한 결과를 반환 하나요?  
  
-   결과 집합이 동일 합니까?  
  
> [!NOTE]  
> 주의! 프로덕션 시스템에서는 SSMA 테스터를 사용 하지 마세요. 테스터를 실행 하는 동안 원본 스키마와 데이터가 수정 됩니다. 한편, 일부 형식의 테스트 된 코드에서는 원래 상태의 전체 복원을 수행할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
SSMA 테스터를 사용 하려는 경우에는 **테스터 데이터베이스 설치** 옵션이 설정 된 상태로 Ssma Sybase 확장 팩을 설치 합니다.  
  
또한 다음을 확인 합니다.  
  
-   Sybase OLE DB 공급자는가 실행 되는 컴퓨터에 설치 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   데이터베이스 엔진에서 CLR (공용 언어 런타임) 통합을 사용 하도록 설정 했습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
현재 버전의 SSMA 테스터는 동일한 원본 또는 대상 서버에 있는 다른 사용자의 병렬 실행을 지원 하지 않습니다.  
  
## <a name="getting-started"></a>시작하기  
[&#40;SybaseToSQL&#41;테스트 사례 만들기 ](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SQL Server &#40;SybaseToSQL&#41;에 SSMA 구성 요소 설치 ](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[프로젝트 설정 &#40;변환&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
