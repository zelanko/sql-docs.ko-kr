---
title: (AccessToSQL) 변환을 위해 Access 데이터베이스 개체를 평가 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7d265ea1bd3b2461219858d39fd0b9164999cc30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650981"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>(AccessToSQL) 변환을 위해 Access 데이터베이스 개체를 평가
개체를 로드 하 고 데이터를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 결정 얼마나 또는 마이그레이션의 성공 하면 되며 변환 시간 걸릴 수 있습니다. SSMA를 성공적으로 변환 된 개체의 비율을 표시 하는 평가 보고서를 만들 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문과 시간 마이그레이션을 수행 하는 것에 대 한 예상치입니다. 또한 SSMA 변환 실패를 야기 하는 특정 문제를 볼 수 있습니다.  
  
## <a name="creating-assessment-reports"></a>평가 보고서 만들기  
SSMA 선택한 Access 데이터베이스 개체를 변환 평가 보고서를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문과 다음 결과 표시 합니다.  
  
**평가 보고서를 만들려면**  
  
1.  액세스 메타 데이터 탐색기에서 데이터베이스 또는 평가 하려는 데이터베이스를 선택 합니다.  
  
2.  개별 개체를 생략 하려면 평가 하지 않으려는 개체 옆의 확인란의 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **보고서 만들기**합니다.  
  
    개체를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체를 분석할 수도 있습니다 **보고서 만들기**합니다.  
  
    SSMA는 창의 맨 아래에서 상태 표시줄에서 진행률을 표시합니다. 출력 창 표시 인 경우 출력 창에는 메시지가 나타납니다.  
  
평가가 완료 되 면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Access: 평가 보고서 창이 나타납니다.  
  
## <a name="using-assessment-reports"></a>평가 보고서를 사용 하 여  
평가 보고서 창에는 세 개의 창이 있습니다: 탐색기를, 메시지 창 및 세부 정보 창.  
  
-   탐색기 창 평가 된 개체를 찾아볼 수 있습니다. 개별 테이블, 인덱스 및 키로 드릴 다운을이 창의 항목을 클릭 수 있습니다.  
  
-   세부 정보 창에 선택한 개체에 대 한 변환 통계를 보여 줍니다.  
  
-   마이그레이션 및 개별 오류 수정 단계를 수행 하는 것에 대 한 추정 시간 및 오류, 경고 및 정보 메시지 변환에 대 한 메시지 창을 보여 줍니다.  
  
평가 보고서를 다시 실행 하거나 스키마로 변환 하기 전에 오류를 해결 해야 합니다. 오류를 찾으려면 클릭 합니다 **오류** 메시지 창, 단추 및 오류가 발생 하는 개체의 목록을 보려면 각 오류를 차례로 확장 합니다. 메시지 창에서 개체를 클릭 하면 모든 오류 및 해당 개체에 대 한 경고 세부 정보 창에 나타납니다.  
  
## <a name="next-step"></a>다음 단계  
[Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
