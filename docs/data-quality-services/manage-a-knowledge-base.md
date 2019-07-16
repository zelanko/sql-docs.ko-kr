---
title: 기술 자료 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 83a57141151caa544fd0d29c470b17818b687ffb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991941"
---
# <a name="manage-a-knowledge-base"></a>기술 자료 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )의 기술 자료에 대해 관리 기능을 수행하는 방법에 대해 설명합니다. 기술 자료에 대해 삭제, 잠금 해제, 작업 취소, 이름 바꾸기 및 속성 표시 기능을 수행할 수 있습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 기술 자료를 관리하려면 기술 자료가 이미 생성되어 있고 게시되었거나(다른 사람이 생성한 경우) 닫혀 있어야 합니다(본인이 생성한 경우).  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 기술 자료를 열려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Manage"></a> 기술 자료 관리  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **기술 자료 열기**를 클릭합니다.  
  
3.  기술 자료 테이블에서 특정 기술 자료를 마우스 오른쪽 단추로 클릭합니다.  
  
4.  상황에 맞는 메뉴에서 다음과 같은 작업을 할 수 있습니다.  
  
    1.  **열기**: **작업 선택** 창에서 선택한 작업의 기술 자료를 열려면 클릭합니다.  
  
    2.  **잠금 해제**: 사용자가 도메인 관리, 기술 자료 검색 및 일치 정책 작업 단계 중 하나에서 기술 자료에서 작동 하 고 종결 하는 경우 기술 자료를 잠금을 해제할 수 있습니다. 기술 자료를 언로드할 경우 다른 사람이 열어서 작업할 수 있습니다. 기술 자료가 작업 상태가 아닌 경우 이 명령을 사용할 수 없습니다. 자세한 내용은 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)을 참조하세요.  
  
    3.  **작업 취소**: 기술 자료를 상태일 때 작업 중인 테이블의 상태 필드 항목에에서 표시를 클릭 합니다. 기술 자료가 작업 상태가 아닌 경우, 기술 자료가 잠긴 경우에는 이 명령을 사용할 수 없습니다. 자세한 내용은 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)을 참조하세요.  
  
    4.  **이름 바꾸기**: 테이블의 기술 자료 필드를 마우스 기술 자료의 편집할 수 있도록 하려면 클릭 합니다. 이름을 변경한 다음 해당 기술 자료를 클릭하고 필드의 다른 기술 자료를 클릭하여 이름 변경을 적용합니다.  
  
    5.  **삭제**: DQS_MAIN 데이터베이스에서 기술 자료를 제거 하려면 클릭 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]합니다.  
  
    6.  **속성**: 읽기 전용 화면에서 데이터베이스에 대 한 속성을 표시 하려면 클릭 합니다.  
  
        1.  **원본 기술 자료**: 이 데이터베이스가 기반으로 하는 기술 자료입니다. 이 옵션은 선택적입니다.  
  
        2.  **상태**: 마지막으로 닫힌 시간을 기준으로 기술 자료가 **작업 중**이고 특정 기술 자료 관리 작업 상태인지를 나타냅니다. 상태는 기술 자료가 기술 자료 관리 세션에서 열렸지만 특정 작업 상태가 아닌 **작업 중**상태이거나 기술 자료가 기술 자료 관리 세션에서 열렸고 특정 작업 상태인 **작업 중** 상태에 해당 기술 자료 관리 작업이 함께 표시될 수 있습니다.  
  
        3.  **잠김**: 기술 자료가 잠긴 경우 **True**, 그렇지 않은 경우 **False**  
  
        4.  **게시되지 않은 내용 포함**: 기술 자료가 없습니다 경우에 게시의 경우 False에서 저장 되지 않은 콘텐츠가 포함 하는 경우 true  
  
        5.  **잠근 사람**: 기술 자료를 닫은 후 잠근 사용자의 이름  
  
        6.  **잠근 날짜**: 잠긴 날짜  
  
        7.  **만든 사람**: 자신이 속한 네트워크를 사용하여 기술 자료를 만든 사용자의 이름  
  
        8.  **만든 날짜**: 생성된 날짜  
  
##  <a name="FollowUp"></a> 후속 작업: 기술 자료 관리 후  
 기술 자료 관리 후 다음 단계는 기술 자료에 대해 수행한 작업에 따라 달라집니다.  
  
-   기술 자료를 연 경우 선택한 작업이 계속됩니다.  
  
-   기술 자료의 잠금을 해제한 경우 다른 사람이 지정된 상태에서 열고 작업할 수 있습니다.  
  
-   기술 자료에 대한 작업을 취소한 경우 마지막으로 게시된 상태의 기술 자료를 사용할 수 있습니다.  
  
-   기술 자료의 이름을 바꾼 경우 이름이 바뀐 기술 자료를 열어 작업해야 합니다.  
  
-   기술 자료를 삭제한 경우 작업할 다른 기술 자료를 선택하거나 새 기술 자료를 만들어야 합니다.  
  
  
