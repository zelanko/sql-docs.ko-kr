---
description: Azure 구독 연결 관리자
title: Azure 구독 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5940e7b45288913bbda4930c267f1f806ed4937d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477992"
---
# <a name="azure-subscription-connection-manager"></a>Azure 구독 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  SSIS 패키지는 **Azure 구독 연결 관리자** 를 통해 속성에 대해 지정된 값(Azure 구독 ID 및 관리 인증서)을 사용하여 Azure 구독에 연결할 수 있습니다.  
  
 **Azure 구독 연결 관리자**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.
  
1.  위에 나와 있는 **SSIS 연결 관리자 추가** 대화 상자에서 **Azure 구독**을 선택하고 **추가**를 클릭합니다.  다음과 같은 **Azure 구독 연결 관리자 편집기** 대화 상자가 표시됩니다.  
  
    ![SSIS-AzureSubscriptionConnectionManager](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  **Azure 구독 ID**에 Azure 구독을 고유하게 식별하는 Azure 구독 ID를 입력합니다.  이 값은 [Azure 관리 포털](https://manage.windowsazure.com) 의 **설정** 페이지에서 확인할 수 있습니다.  
  
    ![SSIS-AzureSettings-SubscriptionID](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  드롭다운 목록에서 **관리 인증서 저장소 위치** 및 **관리 인증서 저장소 이름** 을 선택합니다.  
  
4.  **관리 인증서 지문**을 입력하거나 **찾아보기...** 를 클릭하여 선택한 저장소에서 인증서를 선택합니다. 인증서는 구독용 관리 인증서로 업로드해야 합니다. 이렇게 하려면 Azure Portal의 다음 페이지에서 **업로드**를 클릭합니다. 자세한 내용은 이 [MSDN 게시물](https://msdn.microsoft.com/library/azure/gg551722.aspx)을 참조하세요.  
  
     ![SSIS-AzureSettings-ManagementCertificate](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  **연결 테스트** 를 클릭하여 연결을 테스트합니다.  
  
6.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
  
