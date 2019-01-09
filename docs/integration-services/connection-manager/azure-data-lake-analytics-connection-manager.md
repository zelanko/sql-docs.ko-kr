---
title: Azure Data Lake Analytics 연결 관리자 | Microsoft Docs
description: SSIS(SQL Server Integration Services) 패키지는 Azure Data Lake Analytics 연결 관리자를 사용하여 Data Lake Analytics 계정에 연결할 수 있습니다.
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: douglasl
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 3d544999b83645e40b7579d7c5e049cff2d36439
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782065"
---
# <a name="azure-data-lake-analytics-connection-manager"></a>Azure Data Lake Analytics 연결 관리자

SSIS(SQL Server Integration Services) 패키지는 Azure Data Lake Analytics 연결 관리자를 사용하여 다음 두 가지 인증 유형 중 하나로 Data Lake Analytics 계정에 연결할 수 있습니다.
-   Azure AD(Azure Active Directory) 사용자 ID
-   Azure AD 서비스 ID 

Data Lake Analytics 연결 관리자는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.
 
## <a name="configure-the-connection-manager"></a>연결 관리자 구성

1. **SSIS 연결 관리자 추가** 대화 상자에서 **AzureDataLakeAnalytics** > **추가**를 선택합니다. **Azure Data Lake Analytics 연결 관리자 편집기** 대화 상자가 열립니다.
  
2. **Azure Data Lake Analytics 연결 관리자 편집기** 대화 상자의 **ADLA 계정 이름** 필드에서 Data Lake Analytics 계정 이름을 입력합니다. 예를 들면 myadlaaccountname입니다.
  
3. **인증** 필드에서 Data Lake Analytics의 데이터에 액세스하기 위한 적절한 인증 유형을 선택합니다.

   1. **Azure AD 사용자 ID** 인증 옵션을 선택하는 경우:
   
      i. **사용자 이름** 및 **암호** 필드에 값을 제공합니다.    
      ii. 연결을 테스트하려면 **연결 테스트**를 선택합니다. 사용자 또는 테넌트 관리자가 SSIS를 Data Lake Analytics 계정에 액세스할 수 있도록 이전에 동의하지 않은 경우 메시지가 표시되면 **동의**를 선택합니다. 이 동의 환경에 대한 자세한 내용은 [Azure Active Directory와 애플리케이션 통합](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application)을 참조하세요.
    
   > [!NOTE] 
   > **Azure AD 사용자 ID** 인증 옵션을 선택하는 경우 다단계 인증과 Microsoft 계정 인증이 지원되지 않습니다.
    
   2. **Azure AD 서비스 ID** 인증 옵션을 선택하는 경우:
   
      i. Data Lake Analytics 계정에 액세스하기 위한 Azure Active Directory 애플리케이션 및 서비스 사용자를 만듭니다. 이 인증 옵션에 대한 자세한 내용은 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)(리소스에 액세스할 수 있는 Active Directory 애플리케이션 및 서비스 사용자를 포털에서 만들기)를 참조하세요.    
      ii. 이 Azure Active Directory 애플리케이션에 Data Lake Analytics 계정에 액세스할 수 있는 적절한 권한을 할당합니다. [사용자 추가 마법사](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user)를 사용하여 Data Lake Analytics 계정에 사용 권한을 부여하는 방법을 알아봅니다.    
      iii. **애플리케이션 ID**, **인증 키** 및 **테넌트 ID** 필드에 값을 입력합니다.    
      iv. 연결을 테스트하려면 **연결 테스트**를 선택합니다.  

4. **확인**을 선택하여 **Azure Data Lake Analytics 연결 관리자 편집기** 대화 상자를 닫습니다.  

## <a name="view-the-properties-of-the-connection-manager"></a>연결 관리자의 속성 보기
작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.  
  
  
