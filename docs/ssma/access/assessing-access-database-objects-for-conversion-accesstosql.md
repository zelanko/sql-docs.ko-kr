---
title: "데이터베이스 개체에 액세스 (AccessToSQL) 변환에 대 한 평가 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "16"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b56dec5144daf0531fa630c2d6fc016903c5eeaa
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>데이터베이스 개체에 액세스 (AccessToSQL) 변환에 대 한 평가
개체를 로드 하 고 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure 결정 해야 얼마나 또는 마이그레이션 성공적으로 수행 됩니다, 하며 변환 시간 걸릴 수 있습니다. SSMA를 성공적으로 변환 된 개체의 비율을 표시 하는 평가 보고서를 만들 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 마이그레이션을 수행 하기 위한 예상 하는 SQL Azure 구문 및 시간입니다. 또한 SSMA 변환 실패를 발생 시킨 특정 문제를 볼 수 있습니다.  
  
## <a name="creating-assessment-reports"></a>평가 보고서 만들기  
SSMA를 선택한 액세스 데이터베이스 개체를 변환 평가 보고서를 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 구문과 다음 결과 표시 합니다.  
  
**평가 보고서를 만들려면**  
  
1.  액세스 메타 데이터 탐색기에서 데이터베이스 또는 평가 하려는 데이터베이스를 선택 합니다.  
  
2.  개별 개체를 생략 하려면 평가 하지 않을 개체 옆의 확인란 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **보고서 만들기**합니다.  
  
    개체를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체를 분석할 수도 있습니다 **보고서 만들기**합니다.  
  
    SSMA는 창의 맨 아래에 상태 표시줄에 진행률이 표시 됩니다. 출력 창 보이는 경우 메시지가 출력 창에 나타납니다.  
  
평가가 완료 되 면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Access: 평가 보고서 창이 나타납니다.  
  
## <a name="using-assessment-reports"></a>평가 보고서를 사용 하 여  
평가 보고서 창에는 세 개의 창이 있습니다: 탐색기, 세부 정보 창 및 메시지 창.  
  
-   탐색기 창 평가 된 개체를 찾아볼 수 있습니다. 개별 테이블, 인덱스 및 키를이 창에 있는 항목을 클릭 수 있습니다.  
  
-   세부 정보 창에는 선택한 개체에 대 한 변환 통계가 표시 됩니다.  
  
-   메시지 창에 오류, 경고 및 변환에 대 한 정보 메시지를 표시 하 고 마이그레이션 및 개별 오류 수정 단계를 수행 하기 위한 예상 시간 키를 누릅니다.  
  
평가 보고서를 다시 실행 하거나 스키마를 변환 하기 전에 오류를 수정 해야 합니다. 오류를 찾으려면 클릭는 **오류** 메시지 창 단추를 선택한 다음 오류가 발생 하는 개체의 목록을 볼 수 있는 각 오류를 확장 합니다. 메시지 창에서 개체를 선택 하는 경우 모든 오류와 해당 개체에 대 한 경고 세부 정보 창에 나타납니다.  
  
## <a name="next-step"></a>다음 단계  
[Access 데이터베이스 개체 변환](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
