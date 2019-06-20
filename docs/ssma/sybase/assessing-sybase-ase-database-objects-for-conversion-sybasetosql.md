---
title: SAP ASE 데이터베이스 개체 변환 (SybaseToSQL)에 대 한 평가 | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e7d1b0b68835fe8b909369a87814a3d1c41e07d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240244"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>변환 (SybaseToSQL)에 대 한 SAP ASE 데이터베이스 개체를 평가합니다.
개체를 로드 하 고 데이터를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL, 결정 하는 방법을 마이그레이션 복잡성 및 얼마나 많은 시간이 걸립니다. SSMA 개체 및 절차를 성공적으로 변환할 수의 비율을 표시 하는 평가 보고서를 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 또한 SSMA 변환 오류를 일으킬 수 있는 특정 문제를 볼 수 있습니다.  
  
## <a name="create-assessment-reports"></a>평가 보고서 만들기  
SSMA 변환 선택한 SAP 적응형 Server Enterprise (ASE) 데이터베이스 개체를이 평가 보고서를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL 구문과 다음 결과 표시 합니다.  
  
**평가 보고서를 만들려면**  
  
1.  Sybase 메타 데이터 탐색기에서 평가 하려는 데이터베이스를 선택 합니다.  
  
2.  개별 개체를 생략 하려면 평가 하지 않으려는 개체 옆의 확인란의 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **보고서 만들기**합니다.  
  
    개체를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체를 분석할 수도 있습니다 **보고서 만들기**합니다.  
  
    SSMA는 창의 맨 아래에서 상태 표시줄에서 진행률을 표시합니다. 출력 창 표시 이면 모든 관련된 메시지가 나타납니다.  
  
    평가가 완료 되 면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Sybase: 평가 보고서 창이 표시 됩니다.  
  
## <a name="use-assessment-reports"></a>사용 하 여 평가 보고서  
평가 보고서 창에는 세 가지 창이 있습니다.  
  
-   왼쪽된 창에는 평가 보고서에 포함 된 개체 계층을 포함 합니다. 계층을 탐색할 수 있으며 개체 및 변환 통계 및 코드를 보려면 개체 범주 선택.  
  
-   오른쪽 창 내용의 왼쪽된 창에서 선택한 항목을에 따라 다릅니다.  
  
    개체 (예: 스키마) 또는 테이블의 그룹을 선택 하면 오른쪽 창에 두 개의 창이 표시 됩니다. 합니다 **변환 통계** 창에 선택한 개체에 대 한 변환 통계 표시 합니다. 합니다 **범주별으로 개체** 창에서 개체 또는 개체의 범주에 대 한 변환 통계를 보여 줍니다. 합니다.  
  
    저장된 프로시저, 뷰 또는 트리거를 선택 하면 오른쪽 창 통계, 소스 코드 및 대상 코드를 포함 합니다.  
  
    -   위쪽 영역에는 개체에 대 한 전체 통계를 보여 줍니다. 확장 해야 할 수 있습니다 **통계** 이 정보를 볼 수 있습니다. 
    -   소스 영역에는 왼쪽된 창에서 선택한 개체의 소스 코드를 보여 줍니다. 강조 표시 된 영역 문제가 있는 소스 코드를 표시 합니다.  
    -   대상 영역에는 변환 된 코드를 보여 줍니다. 빨간색 텍스트 문제가 있는 코드 및 오류 메시지를 보여 줍니다.  
  
-   아래쪽 창에는 메시지 번호별로 그룹화 된 변환 메시지를 보여 줍니다. 선택 **오류**를 **경고**, 또는 **정보** 메시지의 범주를 표시 하 여 메시지 그룹을 차례로 확장 합니다. 오른쪽 창에서 세부 정보를 표시 한 다음 왼쪽된 창에서 개체를 선택 하는 개별 메시지를 클릭 합니다.  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>평가 보고서를 사용 하 여 변환 문제를 분석 합니다.  
합니다 **변환 통계 창** 변환 통계를 표시 합니다. 모든 범주의 비율을 100% 보다 작은 경우 변환에 성공 하지 못한 이유에 결정 해야 합니다.  
  
**변환 문제를 보려면**  
  
1.  이전 절차의 지침을 사용 하 여 평가 보고서를 만듭니다.  
  
2.  왼쪽된 창에서 스키마 또는 빨간색 오류 아이콘이 있는 폴더를 확장 합니다. 변환에 실패 한 개별 항목을 선택할 때까지 항목을 확장을 계속 합니다.  
  
3.  소스 창 맨 위에 있는 선택 **문제**합니다.  
    문제가 되는 코드는 강조 표시와 관련된 된 코드에서 있는 그대로 합니다 **대상 탐색** 창입니다.  
  
4.  모든 오류 메시지를 검토 하 고 변환 문제를 발생 시킨 개체를 사용 하 여 수행 하려는 결정 합니다.  
  
    -   SSMA는 ASE 구문을 업데이트 합니다. 저장된 프로시저와 트리거에 대해서만 구문을 업데이트할 수 있습니다. 구문을 업데이트 Sybase 메타 데이터 탐색기 창에서 개체를 선택를 클릭 합니다 **SQL** 탭을 선택한 다음 SQL 코드를 편집 합니다. 항목에서로 이동 하면 업데이트 된 구문을 저장 하 라는 메시지가 표시 됩니다. 개체에 대해 보고 된 오류를 확인 합니다 **보고서** 탭 합니다.  
  
    -   ASE에서 ASE 개체를 제거 하거나 수정 하는 문제가 있는 코드를 변경할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하는 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [Sybase ASE에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)합니다.  
  
    -   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL 메타 데이터 탐색기 및 Sybase 메타 데이터 탐색기 확인란의 선택을 취소 항목 옆에 있는 개체를 로드 하기 전에 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL ASE에서 데이터를 마이그레이션합니다.
  
## <a name="next-steps"></a>다음 단계  
[SAP ASE 데이터베이스 개체 변환 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB로 SAP ASE 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
