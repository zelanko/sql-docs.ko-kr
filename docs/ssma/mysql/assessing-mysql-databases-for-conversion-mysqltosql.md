---
title: MySQL 데이터베이스 변환 (MySQLToSQL)에 대 한 평가 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9983edb500e424be6bbb4f85ff005af00fd65aaf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253246"
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>변환을 위해 MySQL 데이터베이스 평가(MySQLToSQL)
개체를 로드 하 고 데이터를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 복잡 한 마이그레이션 되며 시간 결정 해야 SQL Azure 마이그레이션 걸립니다. SSMA는 성공적으로 변환 하는 개체의 비율을 표시 하는 평가 보고서를 만들 수 있습니다. 또한 SSMA 변환 오류가 발생 하는 특정 문제를 볼 수 있습니다.  
  
## <a name="creating-assessment-reports"></a>평가 보고서 만들기  
SSMA 변환 선택한 MySQL 데이터베이스 개체를이 평가 보고서를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문과 다음 결과 표시 합니다.  
  
**평가 보고서를 만들려면**  
  
1.  MySQL 메타 데이터 탐색기에서 스키마 평가를 선택 합니다.  
  
2.  개별 개체를 생략 하려면 옆에 확인란의 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **스키마**를 선택한 후 **보고서 만들기**합니다.  
  
    개별 개체를 분석 하는 개체를 마우스 오른쪽 단추로 클릭 합니다. 그런 다음 선택 **보고서 만들기**합니다.  
  
    SSMA는 창의 맨 아래에서 상태 표시줄에 진행률이 표시 됩니다. 출력 창 표시 인 경우 출력 창에는 메시지가 나타납니다.  
  
    평가가 완료 되 면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for MySQL을 평가 보고서 창이 표시 됩니다.  
  
## <a name="using-assessment-reports"></a>평가 보고서를 사용 하 여  
평가 보고서 창에는 세 가지 창이 있습니다.  
  
-   왼쪽된 창에는 평가 보고서에 포함 된 개체 계층을 포함 합니다. 계층을 찾아 개체 및 종류의 변환 통계 및 코드를 보려면 개체를 선택할 수 있습니다.  
  
-   오른쪽 창 내용의 왼쪽된 창에서 선택한 항목에 따라 달라 집니다.  
  
    스키마와 같은 개체의 그룹을 선택 하는 경우 오른쪽 창 범주 창에서 변환 통계 창 및 개체 포함 합니다. 변환 통계 창 선택한 개체에 대 한 변환 통계를 보여 줍니다. 범주 창에서 개체에서 개체 또는 개체의 범주에 대 한 변환 통계를 보여 줍니다.  
  
    함수, 프로시저, 테이블 또는 뷰를 선택 하면 오른쪽 창 통계, 소스 코드 및 대상 코드를 포함 합니다.  
  
    -   위쪽 영역에는 개체에 대 한 전체 통계를 보여 줍니다. 확장 해야 할 수 있습니다 **통계** 이 정보를 볼 수 있습니다.  
  
    -   소스 영역에는 왼쪽된 창에서 선택한 개체의 소스 코드를 보여 줍니다. 강조 표시 된 영역 문제가 있는 소스 코드를 표시 합니다.  
  
    -   대상 영역에는 변환 된 코드를 보여 줍니다. 빨간색 텍스트 문제가 있는 코드 및 오류 메시지를 보여 줍니다.  
  
-   아래쪽 창에는 메시지 번호별로 그룹화 된 변환 메시지를 보여 줍니다. 클릭할 수 **오류**를 **경고**, 또는 **정보** 메시지의 범주를 표시 하 여 메시지 그룹을 차례로 확장 합니다. 왼쪽된 창에서 개체를 선택 하 고 오른쪽 창에서 세부 정보를 표시 하는 개별 메시지를 클릭 합니다.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>평가 보고서를 사용 하 여 변환 문제 분석  
변환 통계 창 변환 통계를 보여 줍니다. 모든 범주의 비율을 100% 보다 작은 경우 변환에 성공 하지 못한 이유에 결정 해야 합니다.  
  
**변환 문제를 보려면**  
  
1.  이전 절차의 지침을 사용 하 여 평가 보고서를 만듭니다.  
  
2.  왼쪽된 창에서 스키마 또는 빨간색 오류 아이콘이 있는 폴더를 확장 합니다. 변환에 실패 한 개별 항목을 선택할 때까지 항목을 확장을 계속 합니다.  
  
3.  소스 창 맨 위에 있는 클릭 **문제**합니다.  
  
    문제가 되는 코드는 대상 탐색 창에서 관련된 코드를 강조 표시 됩니다.  
  
4.  모든 오류 메시지를 검토 하 고 변환 문제를 발생 시킨 개체를 사용 하 여 수행 하려는 항목을 결정 합니다.  
  
-   SSMA는 MySQL 구문을 업데이트 합니다. 프로시저 및 함수에 대해서만 구문을 업데이트할 수 있습니다. 구문을 업데이트 하려면 MySQL 메타 데이터 탐색기 창에서 개체를 선택를 클릭 합니다 **SQL** 탭 한 다음 SQL 코드를 수정 합니다. 항목에서로 이동 하면 업데이트 된 구문 저장할 묻는 메시지가 나타납니다. 개체에 대해 보고 된 오류를 볼 수 있습니다 합니다 **보고서** 탭 합니다.  
  
-   MySQL에서 MySQL 개체를 제거 하거나 수정 하는 문제가 있는 코드를 수정할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하는 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)합니다.  
  
-   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지우십시오. SQL Azure 메타 데이터 탐색기 및 MySQL 메타 데이터 탐색기 항목 옆의 확인란에 개체를 로드 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure MySQL에서 데이터를 마이그레이션합니다.  
  
## <a name="next-step"></a>다음 단계  
[MySQL 데이터베이스 변환 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB로 마이그레이션 MySQL 데이터베이스 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
