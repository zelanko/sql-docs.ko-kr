---
title: 컬렉션 집합 보고서 보기(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.reporthistory.calendar.f1
helpviewer_keywords:
- collection sets [SQL Server], viewing reports
- reports [SQL Server], viewing collection set
ms.assetid: c3b1e791-9aa1-4bba-9622-4954568e1820
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 548f6a6a75be51df2ea0de87f4eca91bebf8358b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055504"
---
# <a name="view-a-collection-set-report-sql-server-management-studio"></a>컬렉션 집합 보고서 보기(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  관리 데이터 웨어하우스를 구성한 다음에는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 컬렉션 집합 보고서를 볼 수 있습니다. 설치 프로그램 실행 중 설치되는 시스템 데이터 컬렉션 집합에 대해 보고서가 제공됩니다. 보고서에는 다음이 포함됩니다.  
  
-   디스크 사용 요약  
  
-   쿼리 통계 기록  
  
-   서버 작업 기록  
  
 이 절차에서 **디스크 사용** 컬렉션 집합에 대한 보고서가 표시됩니다. 동일한 일반 절차에 따라 다른 시스템 데이터 컬렉션 집합에 대한 보고서도 볼 수 있습니다.  
  
### <a name="to-view-a-collection-set-report"></a>컬렉션 집합 보고서를 보려면  
  
1.  보고서에 대한 테이블은 수집된 데이터를 처음으로 업로드할 때 생성됩니다. 첫 번째 업로드 전에 보고서를 보려고 하면 오류가 발생하고 보고서가 표시되지 않습니다. 디스크 사용 컬렉션 집합에 대한 데이터를 업로드하려면 개체 탐색기에서 **관리** 폴더, **데이터 컬렉션**, **시스템 데이터 컬렉션 집합**을 차례로 확장하고 **디스크 사용** 컬렉션 집합을 마우스 오른쪽 단추로 클릭한 다음 **지금 수집 및 업로드**를 클릭합니다.  
  
2.  보고서를 보려면 개체 탐색기에서 **관리** 폴더를 확장하고 **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **보고서**, **관리 데이터 웨어하우스**를 차례로 가리키고 **디스크 사용 요약**을 클릭합니다.  
  
    > [!NOTE]  
    >  일부 보고서는 데이터 컬렉션 시간대에 따라 달력 단추를 표시할 수 있습니다. **데이터 컬렉션 보고서 달력**에 액세스하려면 이 단추를 클릭합니다.  
  
#### <a name="data-collection-report-calendar"></a>데이터 컬렉션 보고서 달력  
 이 대화 상자를 사용하여 보고하려는 데이터의 시작 날짜, 시작 시간 및 기간을 지정할 수 있습니다. 예를 들어 지난 수요일의 특정 12시간 동안 서버의 디스크 사용 동작을 보고할 수 있습니다.  
  
 **시작 날짜**  
 보고서 데이터의 시작 날짜를 입력하거나 달력에서 선택합니다.  
  
 **시작 시간**  
 보고서 데이터의 시작 시간을 입력하거나 화살표를 클릭하여 지정합니다.  
  
 **기간**  
 보고서에 포함할 시간 범위를 지정합니다. 기본값은 240분입니다. 선택 가능한 값은 15분, 60분, 240분(4시간), 720분(12시간) 및 1440분(24시간)입니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)   
 [관리 데이터 웨어하우스 구성&#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
