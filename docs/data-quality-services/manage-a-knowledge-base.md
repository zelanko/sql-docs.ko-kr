---
title: 기술 자료 관리
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 1fda81ac39233435dbcd0546e452878cc6767b33
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247145"
---
# <a name="manage-a-knowledge-base"></a>기술 자료 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )의 기술 자료에 대해 관리 기능을 수행하는 방법에 대해 설명합니다. 기술 자료에 대해 삭제, 잠금 해제, 작업 취소, 이름 바꾸기 및 속성 표시 기능을 수행할 수 있습니다.  
  
##  <a name="BeforeYouBegin"></a>시작 하기 전에  
  
###  <a name="Prerequisites"></a>사전  
 기술 자료를 관리하려면 기술 자료가 이미 생성되어 있고 게시되었거나(다른 사람이 생성한 경우) 닫혀 있어야 합니다(본인이 생성한 경우).  
  
###  <a name="Security"></a>보안  
  
####  <a name="Permissions"></a>권한에  
 기술 자료를 열려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Manage"></a>기술 자료 관리  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client 응용 프로그램을 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **기술 자료 열기**를 클릭합니다.  
  
3.  기술 자료 테이블에서 특정 기술 자료를 마우스 오른쪽 단추로 클릭합니다.  
  
4.  상황에 맞는 메뉴에서 다음과 같은 작업을 할 수 있습니다.  
  
    1.  **열기**: **작업 선택** 창에서 선택한 작업의 기술 자료를 열려면 클릭 합니다.  
  
    2.  **잠금 해제**: 도메인 관리, 기술 자료 검색 및 일치 정책 작업 단계 중 하나에서 기술 자료에 대해 작업 중 이었던 사용자 인 경우 기술 자료의 잠금을 해제 하 고 닫을 수 있습니다. 기술 자료를 언로드할 경우 다른 사람이 열어서 작업할 수 있습니다. 기술 자료가 작업 상태가 아닌 경우 이 명령을 사용할 수 없습니다. 자세한 내용은 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)을 참조하세요.  
  
    3.  **작업 삭제**: 테이블의 상태 필드 항목에 표시 된 것 처럼 기술 자료가 작업 중인 상태 이면 클릭 합니다. 기술 자료가 작업 상태가 아닌 경우, 기술 자료가 잠긴 경우에는 이 명령을 사용할 수 없습니다. 자세한 내용은 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)을 참조하세요.  
  
    4.  **이름 바꾸기**: 마우스 오른쪽 단추로 클릭 한 기술 자료에 대해 테이블의 기술 자료 필드를 편집 가능한 상태로 만들려면 클릭 합니다. 이름을 변경한 다음 해당 기술 자료를 클릭하고 필드의 다른 기술 자료를 클릭하여 이름 변경을 적용합니다.  
  
    5.  **삭제**:의 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]DQS_MAIN 데이터베이스에서 기술 자료를 제거 하려면 클릭 합니다.  
  
    6.  **속성**: 읽기 전용 화면에서 데이터베이스에 대 한 속성을 표시 하려면 클릭 합니다.  
  
        1.  **원본 기술 자료**:이 데이터베이스가 기반으로 하는 기술 자료입니다. 선택 사항입니다.  
  
        2.  **상태**: 기술 자료가 **작업 중** 이 고 특정 기술 자료 관리 작업에 있는지 여부를 나타냅니다 .이 작업은 마지막으로 닫힌 시점에 결정 됩니다. 상태는 기술 자료가 기술 자료 관리 세션에서 열렸지만 특정 작업 상태가 아닌 **작업 중**상태이거나 기술 자료가 기술 자료 관리 세션에서 열렸고 특정 작업 상태인 **작업 중** 상태에 해당 기술 자료 관리 작업이 함께 표시될 수 있습니다.  
  
        3.  **잠김**: 기술 자료가 잠겨 있으면 **True** 이 고, 그렇지 않으면 **False** 입니다.  
  
        4.  게시 되지 않은 **내용 포함**: 기술 자료에 게시를 통해 저장 되지 않은 콘텐츠가 포함 되어 있으면 True이 고, 그렇지 않으면 False입니다.  
  
        5.  **잠근 사람**: 기술 자료를 닫은 사용자의 이름을 잠그고 잠급니다.  
  
        6.  **잠긴 날짜**: 잠긴 날짜  
  
        7.  **만든 사람**: 기술 자료를 만든 사용자의 이름으로, 자신이 속한 네트워크를 사용 합니다.  
  
        8.  **만든 날짜**: 만든 날짜  
  
##  <a name="FollowUp"></a>후속 작업: 기술 자료를 관리 한 후  
 기술 자료 관리 후 다음 단계는 기술 자료에 대해 수행한 작업에 따라 달라집니다.  
  
-   기술 자료를 연 경우 선택한 작업이 계속됩니다.  
  
-   기술 자료의 잠금을 해제한 경우 다른 사람이 지정된 상태에서 열고 작업할 수 있습니다.  
  
-   기술 자료에 대한 작업을 취소한 경우 마지막으로 게시된 상태의 기술 자료를 사용할 수 있습니다.  
  
-   기술 자료의 이름을 바꾼 경우 이름이 바뀐 기술 자료를 열어 작업해야 합니다.  
  
-   기술 자료를 삭제한 경우 작업할 다른 기술 자료를 선택하거나 새 기술 자료를 만들어야 합니다.  
  
  
