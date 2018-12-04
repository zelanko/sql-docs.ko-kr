---
title: 데이터 품질 프로젝트 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dqproject.newdqproject.f1
helpviewer_keywords:
- create,data quality project
- data quality project,create
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c2b2adb2a1dc2c4c668bb094553f0961dc74439d
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52616814"
---
# <a name="create-a-data-quality-project"></a>데이터 품질 프로젝트 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]를 사용하여 데이터 품질 프로젝트를 만드는 방법에 대해 설명합니다. 데이터 품질 프로젝트는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 정리 또는 일치 작업을 실행하는 데 사용됩니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 데이터 품질 프로젝트에서 정리 및 일치 작업을 수행하는 데 사용할 관련 기술 자료가 있어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터 품질 프로젝트를 만들려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_kb_operator 역할이 있어야 합니다.  
  
##  <a name="Create"></a> 데이터 품질 프로젝트 만들기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **새 데이터 품질 프로젝트**를 클릭합니다.  
  
3.  **새 데이터 품질 프로젝트** 화면에서  
  
    1.  **이름** 상자에 새 데이터 품질 프로젝트의 이름을 입력합니다.  
  
    2.  (옵션) **설명** 상자에 새 데이터 품질 프로젝트에 대한 설명을 입력합니다.  
  
    3.  **기술 자료 사용** 목록에서 데이터 품질 프로젝트에 사용할 기술 자료를 선택합니다. 오른쪽 **기술 자료 정보: <Knowledge_Base_Name>** 영역에 선택한 기술 자료에서 사용할 수 있는 도메인 이름이 표시됩니다.  
  
    4.  **작업 선택** 영역에서 이 데이터 품질 프로젝트를 사용하여 수행할 작업을 클릭합니다.  
  
        -   **정리**: 원본 데이터를 정리하려면 이 작업을 선택합니다.  
  
        -   **일치**: 일치를 수행하려면 이 작업을 선택합니다. 데이터 품질 프로젝트를 위해 선택한 기술 자료에 일치 정책이 포함된 경우에만 이 작업을 사용할 수 있습니다.  
  
4.  **만들기** 를 클릭하여 데이터 품질 프로젝트를 만듭니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 데이터 품질 프로젝트를 만든 후  
 데이터 품질 프로젝트를 만든 후에는 선택한 작업(정리 또는 일치)을 수행하는 데 사용할 마법사가 나타납니다. 정리 및 일치 작업에 대한 자세한 내용은 [데이터 정리](../data-quality-services/data-cleansing.md) 및 [데이터 일치](../data-quality-services/data-matching.md)를 참조하세요.  
  
  
