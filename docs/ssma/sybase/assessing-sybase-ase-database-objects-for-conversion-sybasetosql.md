---
title: "Sybase ASE 데이터베이스 개체 (SybaseToSQL) 변환에 대 한 평가 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9683542427256511b961ad8f6ffd74af43eb23d5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="assessing-sybase-ase-database-objects-for-conversion-sybasetosql"></a>Sybase ASE 데이터베이스 개체 (SybaseToSQL) 변환에 대 한 평가
개체를 로드 하 고 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 복잡 한 정도 마이그레이션 되 고 시간 결정 해야 SQL Azure 마이그레이션 걸립니다. SSMA 개체 및를 성공적으로 변환 되는 프로시저의 비율을 표시 하는 평가 보고서를 만들 수 [!INCLUDE[tsql](../../includes/tsql_md.md)]합니다. 또한 SSMA 변환 실패를 발생 시키는 특정 문제를 볼 수 있습니다.  
  
## <a name="creating-assessment-reports"></a>평가 보고서 만들기  
SSMA 변환 선택한 Sybase 적응형 Server Enterprise (ASE) 데이터베이스 개체를이 평가 보고서를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 구문과 다음 결과 표시 합니다.  
  
**평가 보고서를 만들려면**  
  
1.  Sybase 메타 데이터 탐색기에서 데이터베이스를 평가 하려는 선택 합니다.  
  
2.  개별 개체를 생략 하려면 평가 하지 않을 개체 옆의 확인란 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **보고서 만들기**합니다.  
  
    개체를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체를 분석할 수도 있습니다 **보고서 만들기**합니다.  
  
    SSMA는 창의 맨 아래에 상태 표시줄에 진행률이 표시 됩니다. 출력 창 보이는 경우 메시지가 출력 창에 나타납니다.  
  
    평가가 완료 되 면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Sybase: 평가 보고서 창에 표시 됩니다.  
  
## <a name="using-assessment-reports"></a>평가 보고서를 사용 하 여  
평가 보고서 창에는 세 개의 창이 포함 됩니다.  
  
-   왼쪽된 창에서 평가 보고서에 포함 된 개체의 계층 구조를 포함 합니다. 계층 구조를 찾아보고 개체 및 변환 통계 보기와 코드를 개체의 범주를 선택 수 있습니다.  
  
-   오른쪽 창의 내용이 왼쪽된 창에서 선택한 항목에 따라 달라 집니다.  
  
    이러한 스키마 또는 테이블을 선택한 개체의 그룹을 선택 하면 오른쪽 창 범주 창에서 변환 통계 창 및 개체를 포함 합니다. 변환 통계 창에는 선택한 개체에 대 한 변환 통계가 표시 됩니다. 범주 창에서 개체에는 개체 또는 개체의 범주에 대 한 변환 통계가 표시 됩니다.  
  
    저장된 프로시저, 뷰 또는 트리거를 선택 하면 오른쪽 창 통계, 소스 코드 및 대상 코드를 포함 합니다.  
  
    -   맨 위에 개체에 대 한 전체 통계를 보여 줍니다. 확장 해야 할 수도 **통계** 이 정보를 볼 수 있습니다.  
  
    -   소스 영역 왼쪽된 창에서 선택 된 개체의 소스 코드를 보여 줍니다. 강조 표시 된 영역 문제가 있는 소스 코드를 보여 줍니다.  
  
    -   대상 영역 변환된 코드를 보여 줍니다. 빨간색 텍스트 문제가 되는 코드 및 오류 메시지를 보여 줍니다.  
  
-   아래쪽 창에는 변환 메시지, 메시지 수로 그룹화 되어 표시 됩니다. 클릭할 수 있는 **오류**, **경고**, 또는 **정보** 를 메시지의 범주를 표시 한 다음 메시지 그룹을 확장 합니다. 왼쪽된 창에서 개체를 선택 하 고 오른쪽 창에서 세부 정보를 표시 하는 개별 메시지를 클릭 합니다.  
  
## <a name="analyzing-conversion-problems-using-the-assessment-report"></a>평가 보고서를 사용 하 여 변환 문제를 분석 합니다.  
변환 통계 창 변환 통계를 표시합니다. 100% 보다 작은 모든 범주에 대 한 백분율을 사용 하는 경우는 변환이 성공 하지 못한 이유에 결정 해야 합니다.  
  
**변환 문제를 보려면**  
  
1.  이전 절차의 지침을 사용 하 여 평가 보고서를 만듭니다.  
  
2.  왼쪽된 창에서 스키마 나 빨간색 오류 아이콘에 있는 폴더를 확장 합니다. 계속 변환 실패 한 개별 항목을 선택할 때까지 항목을 확장 합니다.  
  
3.  소스 창 위쪽에 클릭 **다음 문제점**합니다.  
  
    문제가 있는 코드가 대상 탐색 창에서와 관련된 된 코드를 있는 그대로 강조 표시 됩니다.  
  
4.  모든 오류 메시지를 검토 확인 한 다음 변환 문제가 발생 한 개체를 사용 하 여 수행할 대상:  
  
    -   SSMA는 ASE 구문을 업데이트 합니다. 저장된 프로시저 및 트리거에 대해서만 구문을 업데이트할 수 있습니다. 구문을 업데이트 하려면 Sybase 메타 데이터 탐색기 창에서 개체를 선택, 클릭는 **SQL** 탭을 선택한 다음 SQL 코드를 편집 합니다. 항목 벗어나 탐색 하면 업데이트 된 구문 저장할 묻는 메시지가 나타납니다. 개체에 대해 보고 된 오류를 볼 수 있습니다는 **보고서** 탭 합니다.  
  
    -   ASE를 제거 하거나 문제가 있는 코드를 수정 하려면 ASE 개체를 변경할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 참조 [Sybase ASE &#40;에 연결 SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure 메타 데이터 탐색기와 Sybase 메타 데이터 탐색기 확인란의 선택을 취소 항목 옆에 개체를 로드 하기 전에 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터 ASE를 마이그레이션합니다.  
  
## <a name="next-step"></a>다음 단계  
[Sybase ASE 데이터베이스 개체 &#40; 변환 SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>참고 항목  
[Azure SQL DB &#40; SQL Server-Sybase ASE 데이터베이스 마이그레이션 SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

