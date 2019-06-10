---
title: .dqs 파일로 기술 자료 내보내기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: 1ec0c02863422565edd8a35ddc39bc653f778b2f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776647"
---
# <a name="export-a-knowledge-base-to-a-dqs-file"></a>.dqs 파일로 기술 자료 내보내기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 .dqs 데이터 파일로 전체 기술 자료를 내보내는 방법에 대해 설명합니다. 도메인 또는 전체 기술 자료를 데이터 파일로 내보낼 수 있습니다. 도메인 내보내기에 대한 자세한 내용은 [.dqs 파일로 도메인 내보내기](../data-quality-services/export-a-domain-to-a-dqs-file.md)를 참조하세요.  
  
 기술 자료를 .dqs 파일로 내보낸 다음 다른 기술 자료로 가져오면 기술 자료 생성 프로세스가 간소화되어 시간과 노력을 절감할 수 있습니다. 기술 자료와 정보를 다른 사람과 공유할 수 있습니다. .dqs 파일에는 연결된 참조 데이터 정보를 제외하고 도메인 및 일치 정책을 포함한 모든 기술 자료 정보가 포함됩니다. 필요한 경우 .dqs 파일을 가져온 후 필요한 도메인을 적절한 참조 데이터 서비스에 다시 연결해야 합니다. 기술 자료에 게시된 데이터와 게시되지 않은 데이터를 모두 내보냅니다.  
  
 내보내기 프로세스에서 만든 .dqs 데이터 파일은 암호화되므로 내용을 볼 수 없습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 기술 자료를 .dqs 데이터 파일로 내보내려면 기술 자료를 만들고 열어 두어야 합니다. 기술 자료를 내보낼 .dqs 파일은 자동으로 생성되므로 필요하지 않습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 기술 자료를 .dqs 데이터 파일로 내보내려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Export"></a> .dqs 파일로 기술 자료 내보내기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면의 도메인 관리 작업에서 기술 자료를 엽니다.  
  
3.  도메인 관리 페이지(원하는 탭 선택)에서 도메인 목록 위의 **기술 자료 데이터를 내보냅니다** 아이콘을 클릭한 다음 **기술 자료 내보내기**를 클릭합니다. 또는 **도메인** 목록에서 마우스 오른쪽 단추를 클릭하고 **내보내기**위로 마우스를 이동한 후 **기술 자료 내보내기**를 클릭할 수도 있습니다.  
  
4.  **데이터 파일로 내보내기** 대화 상자에서 파일을 저장할 폴더로 이동하여 파일의 이름을 지정하거나 기술 자료 이름을 유지한 후 **다른 이름으로 저장** 형식으로 **DQS 데이터 파일(\*.dqs)** 을 지정하고 **저장**을 클릭합니다.  
  
5.  **기술 자료 내보내기** 대화 상자에서 상태 줄에 내보내기가 완료되었다고 표시되는지 확인합니다. **확인**을 클릭합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 도메인을.dqs 파일로 내보낸 후  
 기술 자료를 .dqs 파일로 내보낸 후 기술 자료를 동일한 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (새 이름 적용) 또는 다른 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]로 가져올 수 있습니다.  
  
  
