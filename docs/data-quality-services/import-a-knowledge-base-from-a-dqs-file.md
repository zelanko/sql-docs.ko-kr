---
title: .dqs 파일에서 기술 자료 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: d1dbd724cca4025d34b673e3181ff7be3fdb9c89
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776604"
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>.dqs 파일에서 기술 자료 가져오기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 .dqs 데이터 파일의 전체 기술 자료를 가져오는 방법에 대해 설명합니다. [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램 내에서 기존 기술 자료를 내보내서 데이터 파일을 만듭니다([.dqs 파일로 기술 자료 내보내기](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md) 참조).  
  
 .dqs 데이터 파일을 사용하여 기술 자료의 내용을 내보낸 다음 동일한 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 또는 다른 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 에서 다른 기술 자료로 내용을 가져오면 기술 자료 생성 프로세스가 간소화되어 시간과 노력을 절감할 수 있습니다. 기술 자료와 정보를 다른 사람과 공유하여 다른 사람의 시간을 절감할 수도 있습니다. .dqs 파일에는 연결된 참조 데이터 정보를 제외하고 도메인 및 일치 정책을 포함한 모든 기술 자료 정보가 포함됩니다. 게시된 데이터와 게시되지 않은 데이터를 가져올 수 있습니다.  
  
 .dqs 데이터 파일은 암호화되어 있으므로 볼 수 없습니다.  
  
 기술 자료를 가져올 때는 클라이언트 애플리케이션에 기술 자료 이름이 이미 있어 이름을 바꾸어야 하는 경우를 제외하고 동일한 이름을 사용할 수 있습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 .dqs 파일에서 기술 자료를 가져오려면 기술 자료를 .dqs 파일로 이미 내보낸 상태여야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 .dqs 데이터 파일에서 기술 자료를 가져오려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Import"></a> .dqs 파일에서 기술 자료 가져오기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **새 기술 자료**를 클릭합니다.  
  
3.  기술 자료의 이름을 입력합니다.  
  
4.  **기술 자료 만들기**에 대해 아래쪽 화살표를 클릭한 다음 **DQS 파일에서 가져오기**를 선택합니다.  
  
5.  **데이터 파일 선택**에서 **찾아보기**를 클릭합니다.  
  
6.  **데이터 파일에서 가져오기** 대화 상자에서 가져올 .dqs 파일이 있는 폴더로 이동한 다음 파일의 이름을 클릭합니다. **열기**를 클릭합니다.  
  
7.  **도메인** 목록에 올바른 기술 자료와 도메인이 표시되는지 확인합니다.  
  
8.  수행할 작업을 선택한 다음 **만들기**를 클릭합니다.  
  
9. **기술 자료 가져오기** 대화 상자에서 상태 줄에 가져오기가 완료되었다고 표시되는지 확인합니다. **확인**을 클릭합니다.  
  
10. 수행해야 하는 기술 자료 검색, 도메인 관리 또는 일치 정책 태스크를 완료한 다음 **마침**을 클릭합니다.  
  
11. **게시** 를 클릭하여 기술 자료의 정보를 게시하거나 **아니요** 를 클릭하여 게시하지 않습니다.  
  
12. 기술 자료를 게시한 경우 **확인**을 클릭합니다.  
  
13. Data Quality Services 홈 페이지에서 **최근 기술 자료**에 해당 기술 자료가 나열되는지 확인합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: .Dqs 파일에서 기술 자료를 가져온 후  
 .dqs 파일에서 기술 자료를 가져온 후 기술 자료에 정보를 추가하거나 기술 자료의 내용에 따라 정리 또는 일치 프로젝트에서 기술 자료를 사용할 수 있습니다. 자세한 내용은 [기술 자료 검색 수행](../data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../data-quality-services/managing-a-domain.md), [복합 도메인 관리](../data-quality-services/managing-a-composite-domain.md), [일치 정책 만들기](../data-quality-services/create-a-matching-policy.md), [데이터 정리](../data-quality-services/data-cleansing.md) 또는 [데이터 일치](../data-quality-services/data-matching.md)를 참조하세요.  
  
  
