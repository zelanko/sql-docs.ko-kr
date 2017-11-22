---
title: "변환 (MySQLToSQL)에 대 한 MySQL 데이터베이스를 평가 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58df45157252c3fc54fe54d91edce69cbcb0bd28
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>변환 (MySQLToSQL)에 대 한 MySQL 데이터베이스를 평가합니다.
개체를 로드 하 고 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 복잡 한 정도 마이그레이션 되 고 시간 결정 해야 SQL Azure 마이그레이션 걸립니다. SSMA는 성공적으로 변환 하는 개체의 비율을 보여주는 평가 보고서를 만들 수 있습니다. 또한 SSMA 변환 오류가 발생 하는 특정 문제를 볼 수 있습니다.  
  
## <a name="creating-assessment-reports"></a>평가 보고서 만들기  
SSMA 변환 선택한 MySQL 데이터베이스 개체를이 평가 보고서를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 구문과 다음 결과 표시 합니다.  
  
**평가 보고서를 만들려면**  
  
1.  MySQL 메타 데이터 탐색기에서 평가 하기 위해 스키마를 선택 합니다.  
  
2.  개별 개체를 생략 하는 것 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **스키마**를 선택한 후 **보고서 만들기**합니다.  
  
    개별 개체를 분석 하는 개체를 마우스 오른쪽 단추로 클릭 합니다. 그런 다음 선택 **보고서 만들기**합니다.  
  
    SSMA는 창의 맨 아래에 상태 표시줄에 진행률이 표시 됩니다. 출력 창 보이는 경우 메시지가 출력 창에 나타납니다.  
  
    평가가 완료 되 면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for MySQL 평가 보고서 창이 표시 됩니다.  
  
## <a name="using-assessment-reports"></a>평가 보고서를 사용 하 여  
평가 보고서 창에는 세 개의 창이 포함 됩니다.  
  
-   왼쪽된 창에서 평가 보고서에 포함 된 개체의 계층 구조를 포함 합니다. 계층 구조를 찾아보고 개체 및 변환 통계 및 코드를 볼 개체의 범주를 선택 수 있습니다.  
  
-   오른쪽 창의 콘텐츠 왼쪽된 창에서 선택한 항목에 따라 달라 집니다.  
  
    스키마에 같은 개체 그룹을 선택한 경우 오른쪽 창 변환 통계 창 및 개체 범주 창으로 포함 합니다. 변환 통계 창에는 선택한 개체에 대 한 변환 통계가 표시 됩니다. 범주 창에서 개체에는 개체 또는 개체의 범주에 대 한 변환 통계가 표시 됩니다.  
  
    함수, 프로시저, 테이블 또는 뷰를 선택 하는 경우 오른쪽 창 통계, 소스 코드 및 대상 코드를 포함 합니다.  
  
    -   맨 위에 개체에 대 한 전체 통계를 보여 줍니다. 확장 해야 할 수도 **통계** 이 정보를 볼 수 있습니다.  
  
    -   소스 영역 왼쪽된 창에서 선택 된 개체의 소스 코드를 보여 줍니다. 강조 표시 된 영역 문제가 있는 소스 코드를 보여 줍니다.  
  
    -   대상 영역 변환된 코드를 보여 줍니다. 빨간색 텍스트 문제가 되는 코드 및 오류 메시지를 보여 줍니다.  
  
-   아래쪽 창에는 변환 메시지, 메시지 수로 그룹화 되어 표시 됩니다. 클릭할 수 있는 **오류**, **경고**, 또는 **정보** 를 메시지의 범주를 표시 한 다음 메시지 그룹을 확장 합니다. 왼쪽된 창에서 개체를 선택 하 고 오른쪽 창에서 세부 정보를 표시 하는 개별 메시지를 클릭 합니다.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>평가 보고서를 사용 하 여 변환 문제 분석  
변환 통계 창에는 변환 통계가 표시 됩니다. 100% 보다 작은 모든 범주에 대 한 백분율을 사용 하는 경우는 변환이 성공 하지 못한 이유에 결정 해야 합니다.  
  
**변환 문제를 보려면**  
  
1.  이전 절차의 지침을 사용 하 여 평가 보고서를 만듭니다.  
  
2.  왼쪽된 창에서 스키마 나 빨간색 오류 아이콘에 있는 폴더를 확장 합니다. 계속 변환 실패 한 개별 항목을 선택할 때까지 항목을 확장 합니다.  
  
3.  소스 창 위쪽에 클릭 **다음 문제점**합니다.  
  
    문제가 있는 코드가 대상 탐색 창에서와 관련된 된 코드를 있는 그대로 강조 표시 됩니다.  
  
4.  모든 오류 메시지를 검토 하 고 변환 문제가 발생 한 개체를 사용 하 여 수행할 대상를 확인 합니다.  
  
-   SSMA는 MySQL 구문을 업데이트 합니다. 프로시저 및 함수에 대해서만 구문을 업데이트할 수 있습니다. 구문을 업데이트 하려면 MySQL 메타 데이터 탐색기 창에서 개체를 선택, 클릭는 **SQL** 탭을 선택한 다음 SQL 코드를 수정 합니다. 항목 벗어나 탐색 하면 업데이트 된 구문 저장할 묻는 메시지가 나타납니다. 개체에 대해 보고 된 오류를 볼 수 있습니다는 **보고서** 탭 합니다.  
  
-   MySQL을 제거 하거나 문제가 있는 코드를 수정 하려면 MySQL 개체를 수정할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 참조 [MySQL &#40;에 연결 MySQLToSQL &#41; ](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure 메타 데이터 탐색기 및 MySQL 메타 데이터 탐색기 확인란의 선택을 취소 항목 옆에 개체를 로드 하기 전에 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure 또는 MySQL의 데이터를 마이그레이션합니다.  
  
## <a name="next-step"></a>다음 단계  
[MySQL 데이터베이스 &#40; 변환 MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
