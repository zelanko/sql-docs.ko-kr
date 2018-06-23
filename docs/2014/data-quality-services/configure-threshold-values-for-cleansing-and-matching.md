---
title: 정리 및 일치에 대한 임계값 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 19425baf1fcf1f3fef0a4cf630242d8b16a35f9e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089980"
---
# <a name="configure-threshold-values-for-cleansing-and-matching"></a>정리 및 일치에 대한 임계값 구성
  이 항목에서는 컴퓨터 기반 정리 및 일치 작업 중에 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 사용할 임계값을 구성하는 방법에 대해 설명합니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 이러한 임계값을 구성하려면 DQS_MAIN 데이터베이스에 대한 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Configure"></a> 임계값 구성  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **구성**을 클릭합니다.  
  
3.  그런 다음 **일반 설정** 탭을 클릭합니다. 이 탭에서 정리 및 일치 작업에 대한 임계값을 지정할 수 있습니다.  
  
4.  정리 작업에 대한 임계값을 지정하려면 **대화형 정리** 영역 아래의 다음 상자에 적절한 값을 지정합니다.  
  
    -   **제안 최소 점수**: 컴퓨터 기반 정리 프로세스 중에 DQS에서 대체 값을 제안하는 데 사용할 최소 점수 또는 신뢰도 수준입니다. 해당 백분율 값의 10진수 표기법으로 값을 입력합니다. 예를 들어 75%의 경우 0.75를 입력합니다. 이 값은 **자동 수정 최소 점수** 상자에 지정된 값보다 작거나 같아야 합니다. 기본값은 0.7입니다.  
  
    -   **자동 수정 최소 점수**: 컴퓨터 기반 정리 프로세스 중에 DQS에서 값을 자동으로 수정하는 데 사용할 최소 점수 또는 신뢰도 수준입니다. 해당 백분율 값의 10진수 표기법으로 값을 입력합니다. 예를 들어 90%의 경우 0.9를 입력합니다. 기본값은 0.8입니다.  
  
5.  일치 작업에 대한 임계값을 지정하려면 **일치** 영역 아래의 **최소 레코드 점수** 상자에 값을 지정합니다. 이 값은 레코드가 다른 레코드와 일치하는 것으로 간주되는 최소 점수를 나타냅니다. 기본값은 80%입니다.  
  
6.  **닫기**를 클릭합니다.  
  
  