---
title: "데이터 품질 프로젝트 열기, 잠금 해제, 이름 바꾸기 및 삭제 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00e34abfcc2162483023fd4eace52581c12a1e30
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="open-unlock-rename-and-delete-a-data-quality-project"></a>데이터 품질 프로젝트 열기, 잠금 해제, 이름 바꾸기 및 삭제
  이 항목에서는 데이터 품질 프로젝트 열기, 잠금 해제, 이름 바꾸기, 삭제 등 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 를 사용하여 데이터 품질 프로젝트를 관리하는 방법에 대해 설명합니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
  
-   다른 사용자가 만든 잠긴 프로젝트는 열 수 없습니다.  
  
-   다른 사용자가 만든 데이터 품질 프로젝트는 잠금을 해제하거나 이름을 바꾸거나 삭제할 수 없습니다.  
  
-   잠긴 데이터 품질 프로젝트는 삭제할 수 없습니다. 삭제하려면 먼저 잠금을 해제해야 합니다.  
  
-   자신이 만든 데이터 품질 프로젝트만 잠금을 해제할 수 있습니다.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 관리할 데이터 품질 프로젝트가 하나 이상 있어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 데이터 품질 프로젝트를 관리하려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_kb_operator 역할이 있어야 합니다.  
  
##  <a name="Open"></a> 데이터 품질 프로젝트 열기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **데이터 품질 프로젝트 열기**를 클릭합니다. **프로젝트 열기** 화면이 나타납니다.  
  
     또는 **최근 데이터 품질 프로젝트** 영역 아래에 나열된 데이터 품질 프로젝트를 클릭하여 바로 열 수 있습니다.  
  
3.  **프로젝트 열기** 화면에서 열려는 데이터 품질 프로젝트를 클릭하여 선택하고 **다음**을 클릭합니다.  
  
4.  데이터 품질 프로젝트가 마지막으로 닫힌 작업 상태에서 열립니다. 데이터 품질 프로젝트의 상태는 다음과 같습니다.  
  
    -   **정리** 작업의 경우 데이터 품질 프로젝트의 상태는 **정리 중 - 매핑**, **정리 중 - 정리**, **정리 – 결과 관리 및 보기**및 **정리 – 내보내기**중 하나일 수 있습니다.  
  
    -   **일치** 작업의 경우 데이터 품질 프로젝트의 상태는 **일치 -매핑**, **일치 - 일치**, **일치 - Survivorship**, 및 **일치 - 내보내기**중 하나일 수 있습니다.  
  
##  <a name="Unlock"></a> 데이터 품질 프로젝트 잠금 해제  
 데이터 품질 프로젝트를 만드는 경우 다른 사용자가 사용하거나 수정하지 못하도록 프로젝트가 잠긴 상태로 있습니다. 다른 사용자가 데이터 품질 프로젝트에서 작업할 수 있도록 하려면 작업을 완료한 후 데이터 품질 프로젝트의 잠금을 해제해야 합니다. 잠긴 프로젝트에는 자물쇠 기호가 표시됩니다.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **데이터 품질 프로젝트 열기**를 클릭합니다. **프로젝트 열기** 화면이 나타납니다.  
  
3.  **프로젝트 열기** 화면에서 자신이 만든 잠긴 데이터 품질 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **잠금 해제** 를 클릭합니다. 프로젝트에 잠금이 해제되었음을 나타내는 녹색 확인 표시가 표시됩니다.  
  
##  <a name="Rename"></a> 데이터 품질 프로젝트 이름 바꾸기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **데이터 품질 프로젝트 열기**를 클릭합니다. **프로젝트 열기** 화면이 나타납니다.  
  
3.  **프로젝트 열기** 화면에서 자신이 만든 데이터 품질 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **이름 바꾸기** 를 클릭합니다.  
  
4.  데이터 품질 프로젝트 이름이 **이름** 열에서 편집할 수 있게 됩니다. 새 이름을 입력하고 Enter 키를 누릅니다.  
  
##  <a name="Delete"></a> 데이터 품질 프로젝트 삭제  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **데이터 품질 프로젝트 열기**를 클릭합니다. **프로젝트 열기** 화면이 나타납니다.  
  
3.  **프로젝트 열기** 화면에서 자신이 만든 잠겨 있지 않은 데이터 품질 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **삭제** 를 클릭합니다.  
  
4.  확인 메시지가 나타납니다. **예**를 클릭합니다.  
  
  
