---
title: 변환을 위해 Access 데이터베이스 개체를 평가 하는 방법 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4c2f5bc6953ab0e96397ca728391cbe22a73dd50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910696"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>변환을 위해 Access 데이터베이스 개체를 평가 하는 방법 (AccessToSQL)
개체를 로드 하 고 데이터를 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure로 마이그레이션하려면 먼저 마이그레이션의 양과 변환에 소요 되는 기간을 결정 해야 합니다. SSMA는 성공적으로 변환 된 개체의 비율을 표시 하는 평가 보고서를 만들거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 마이그레이션을 수행 하기 위한 구문 및 시간 추정치를 SQL Azure 수 있습니다. SSMA를 사용 하 여 변환 실패를 일으킨 특정 문제를 확인할 수도 있습니다.  
  
## <a name="creating-assessment-reports"></a>평가 보고서 만들기  
평가 보고서를 만들 때 SSMA는 선택한 Access 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문으로 변환한 다음 결과를 표시 합니다.  
  
**평가 보고서를 만들려면**  
  
1.  액세스 메타 데이터 탐색기에서 평가 하려는 데이터베이스를 선택 합니다.  
  
2.  개별 개체를 생략 하려면 평가 하지 않으려는 개체 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  **데이터베이스**를 마우스 오른쪽 단추로 클릭 한 다음 **보고서 만들기**를 선택 합니다.  
  
    개체를 마우스 오른쪽 단추로 클릭 한 다음 **보고서 만들기**를 선택 하 여 개별 개체를 분석할 수도 있습니다.  
  
    SSMA는 창의 아래쪽에 있는 상태 표시줄에 진행률을 표시 합니다. 출력 창이 표시 되 면 출력 창에도 메시지가 표시 됩니다.  
  
평가가 완료 되 면 액세스에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 Migration Assistant: 평가 보고서 창이 표시 됩니다.  
  
## <a name="using-assessment-reports"></a>평가 보고서 사용  
평가 보고서 창에는 탐색기, 세부 정보 창 및 메시지 창과 같은 세 개의 창이 있습니다.  
  
-   탐색기 창에서 평가 된 개체를 찾아볼 수 있습니다. 이 창에서 항목을 클릭 하 여 개별 테이블, 인덱스 및 키로 드릴 다운할 수 있습니다.  
  
-   세부 정보 창에 선택한 개체에 대 한 변환 통계가 표시 됩니다.  
  
-   메시지 창에는 변환에 대 한 오류, 경고 및 정보 메시지와 마이그레이션 및 개별 오류 수정 단계를 수행 하는 데 필요한 시간에 대 한 정보가 표시 됩니다.  
  
평가 보고서를 다시 실행 하거나 스키마를 변환 하기 전에 오류를 수정 해야 합니다. 오류를 찾으려면 메시지 창에서 **오류 단추를** 클릭 한 다음 각 오류를 확장 하 여 오류가 발생 한 개체의 목록을 표시 합니다. 메시지 창에서 개체를 클릭 하면 해당 개체에 대 한 모든 오류 및 경고가 세부 정보 창에 표시 됩니다.  
  
## <a name="next-step"></a>다음 단계  
[Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
