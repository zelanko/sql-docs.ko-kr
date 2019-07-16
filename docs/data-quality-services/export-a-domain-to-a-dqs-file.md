---
title: .dqs 파일로 도메인 내보내기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a3722234ec1e82431bbefae355391a614c7e980a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992073"
---
# <a name="export-a-domain-to-a-dqs-file"></a>.dqs 파일로 도메인 내보내기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 .dqs 파일로 도메인을 내보내는 방법에 대해 설명합니다. 도메인 또는 전체 기술 자료를 데이터 파일로 내보낼 수 있습니다. 기술 자료 내보내기에 대한 자세한 내용은 [.dqs 파일로 기술 자료 내보내기](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)를 참조하세요.  
  
 한 기술 자료의 도메인을 .dqs 데이터 파일로 내보낸 다음 다른 기술 자료로 가져오면 기술 자료 생성 프로세스가 간소화되어 시간과 노력을 절감할 수 있습니다. 도메인과 정보를 다른 사람과 공유할 수 있습니다.  
  
 단일 도메인 또는 복합 도메인을 내보낼 수 있습니다. 단일 도메인을 포함하는 .dqs 파일에는 연결된 참조 데이터 정보를 제외하고 도메인 속성, 값 및 규칙을 비롯하여 모든 도메인 데이터가 포함됩니다. 복합 도메인을 포함하는 .dqs 파일에는 참조 데이터 정보를 제외하고 복합 도메인에 포함된 도메인에 대한 모든 도메인 데이터와 복합 도메인 속성, 관계 및 규칙을 비롯하여 모든 복합 도메인 데이터가 포함됩니다. 필요한 경우 .dqs 파일을 가져온 후 도메인 또는 복합 도메인을 적절한 참조 데이터 서비스에 다시 연결해야 합니다. 게시된 데이터와 게시되지 않은 데이터를 모두 내보냅니다.  
  
 내보내기 프로세스에서 만든 .dqs 데이터 파일은 암호화되므로 내용을 볼 수 없습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 도메인을 .dqs 데이터 파일로 내보내려면 단일 도메인 또는 여러 개의 단일 도메인이 포함된 복합 도메인을 만들고 선택해야 합니다. 기술 자료를 내보낼 .dqs 파일은 자동으로 생성되므로 필요하지 않습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 도메인을 .dqs 데이터 파일로 내보내려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Export"></a> Export a domain to a .dqs file  
 모든 도메인 관리 페이지에서 내보낼 수 있습니다. 내보내기 명령은 사용자 인터페이스의 컨트롤과 도메인 목록 창의 상황에 맞는 메뉴에 있는 명령에서 사용할 수 있습니다.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면의 도메인 관리 작업에서 기술 자료를 엽니다.  
  
3.  **도메인 관리 페이지** (임의의 탭이 선택되어 있음)의 **도메인** 목록에서 단일 도메인 또는 복합 도메인을 선택합니다.  
  
4.  도메인 목록 위의 **기술 자료 데이터 내보내기** 아이콘을 클릭한 다음 **도메인 내보내기**를 클릭합니다. 또는 **도메인** 목록에서 도메인을 마우스 오른쪽 단추를 클릭하고 **내보내기**를 가리킨 다음 **도메인 내보내기**를 클릭할 수도 있습니다.  
  
5.  **데이터 파일로 내보내기** 대화 상자에서 파일을 저장할 폴더로 이동하여 파일의 이름을 지정하거나 기본 이름을 유지한 후 **다른 이름으로 저장** 형식으로 **DQS 데이터 파일(\*.dqs)** 을 지정하고 **저장**을 클릭합니다.  
  
6.  **도메인 내보내기** 대화 상자에서 상태 줄에 내보내기가 완료되었다고 표시되는지 확인합니다. **확인**을 클릭합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 도메인을.dqs 파일로 내보낸 후  
 도메인을 .dqs 파일로 내보낸 후 다른 기술 자료로 해당 도메인을 가져올 수 있습니다.  
  
  
