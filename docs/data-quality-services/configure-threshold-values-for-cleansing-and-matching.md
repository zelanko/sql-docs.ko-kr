---
title: 정리 및 일치에 대 한 임계값 구성
description: DQS (SQL Server Data Quality Services에서 활동의 컴퓨터 기반 정리 및 일치 작업 중에 사용할 임계값을 구성 하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4fcbc8e4e6d6a9c1df07d8e1b1aa68c08c162817
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557895"
---
# <a name="configure-threshold-values-for-cleansing-and-matching---data-quality-services-dqs"></a>정리 및 일치-DQS (Data Quality Services)에 대 한 임계값 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 컴퓨터 기반 정리 및 일치 작업 중에 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 사용할 임계값을 구성하는 방법에 대해 설명합니다.  
  
##  <a name="BeforeYouBegin"></a>시작 하기 전에  
  
###  <a name="Security"></a>보안  
  
####  <a name="Permissions"></a>권한에  
 이러한 임계값을 구성하려면 DQS_MAIN 데이터베이스에 대한 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Configure"></a>임계값 구성  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client 응용 프로그램을 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **구성**을 클릭합니다.  
  
3.  그런 다음 **일반 설정** 탭을 클릭 합니다. 이 탭에서 정리 및 일치 작업에 대 한 임계값을 지정할 수 있습니다.  
  
4.  정리 작업에 대한 임계값을 지정하려면 **대화형 정리** 영역 아래의 다음 상자에 적절한 값을 지정합니다.  
  
    -   **제안 최소 점수**: 컴퓨터 기반 정리 프로세스 중에 DQS에서 대체 값을 제안 하는 데 사용 되는 최소 점수 또는 신뢰도 수준입니다. 해당 백분율 값의 10진수 표기법으로 값을 입력합니다. 예를 들어 75%의 경우 0.75를 입력합니다. 이 값은 **자동 수정 최소 점수** 상자에 지정된 값보다 작거나 같아야 합니다. 기본값은 0.7입니다.  
  
    -   **자동 수정 최소 점수**: 컴퓨터 기반 정리 프로세스 중에 DQS에서 값을 자동으로 수정 하는 데 사용할 최소 점수 또는 신뢰도 수준입니다. 해당 백분율 값의 10진수 표기법으로 값을 입력합니다. 예를 들어 90%의 경우 0.9를 입력합니다. 기본값은 0.8입니다.  
  
5.  일치 작업에 대한 임계값을 지정하려면 **일치** 영역 아래의 **최소 레코드 점수** 상자에 값을 지정합니다. 이 값은 레코드가 다른 레코드와 일치하는 것으로 간주되는 최소 점수를 나타냅니다. 기본값은 80%입니다.  
  
6.  
  **닫기**를 클릭합니다.  
  
  
