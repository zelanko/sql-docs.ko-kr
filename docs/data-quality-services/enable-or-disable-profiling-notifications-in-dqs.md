---
title: DQS에서 프로파일링 알림 설정 또는 해제 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- enable notifications
- notifications,enable
- notifications,disable
ms.assetid: e439bb29-60cc-4afd-a79a-f629b8d843c1
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 583ccac2604216c88f14aa9c460437a2aa24c03c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022154"
---
# <a name="enable-or-disable-profiling-notifications-in-dqs"></a>DQS에서 프로파일링 알림 설정 또는 해제

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 프로파일링 알림을 설정하거나 해제하는 방법에 대해 설명합니다. 기본적으로 프로파일링 알림은 DQS에서 사용하도록 설정됩니다. 프로파일링 알림은 데이터 원본에 대한 중요한 사실과 데이터에 대해 수행된 현재 작업의 효과를 알려 줍니다. 자세한 내용은 [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md)을 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 알림을 설정하려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Enable"></a> 프로파일링 알림 설정 또는 해제  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client 애플리케이션을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **구성**을 클릭합니다.  
  
3.  그런 다음 **일반 설정** 탭을 클릭합니다.  
  
4.  **알림 사용** 확인란을 선택하거나 선택 취소하여 DQS에서의 여러 작업에 대해 프로파일링 알림을 설정하거나 해제합니다.  
  
5.  **닫기**를 클릭합니다.  
  
  
