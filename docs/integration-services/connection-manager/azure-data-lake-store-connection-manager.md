---
description: Azure Data Lake Store 연결 관리자
title: Azure Data Lake Store 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: Lingxi-Li
ms.author: lingxl
ms.reviewer: maghan
ms.openlocfilehash: aff32d53b663aa34b036fcfdb9202f7dadcd1ff5
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130623"
---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


SSIS(SQL Server Integration Services) 패키지는 Azure Data Lake Store 연결 관리자를 사용하여 다음 두 가지 인증 유형 중 하나로 Azure Data Lake Storage Gen1 계정에 연결할 수 있습니다.
-   Azure AD 사용자 ID
-   Azure AD 서비스 ID 

Azure Data Lake Store 연결 관리자는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.

> [!NOTE]
> Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Data Lake Storage Gen1 원본과 Data Lake Storage Gen1 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 연결 관리자 구성

1.  **SSIS 연결 관리자 추가** 대화 상자에서 **AzureDataLake** 를 선택한 다음 **추가** 를 선택합니다. **Azure Data Lake Store 연결 관리자 편집기** 대화 상자가 열립니다.
  
2.  **Azure Data Lake Store 연결 관리자 편집기** 대화 상자의 **ADLS 호스트** 필드에 Data Lake Storage Gen1 호스트 URL을 제공합니다. 예를 들어 `https://test.azuredatalakestore.net` 또는 `test.azuredatalakestore.net`입니다.
  
3.  **인증** 필드에서 Data Lake Storage Gen1의 데이터에 액세스하기 위한 적절한 인증 유형을 선택합니다.

    1.  **Azure AD 사용자 ID** 인증 옵션을 선택한 경우 다음을 수행합니다.
        1. **사용자 이름** 및 **암호** 필드에 값을 제공합니다. 
    
        2. 연결을 테스트하려면 **연결 테스트** 를 선택합니다. 사용자 또는 테넌트 관리자가 SSIS를 Data Lake Storage Gen1 데이터에 액세스할 수 있도록 이전에 동의하지 않은 경우 메시지가 표시되면 **동의** 를 선택합니다. 이 동의 환경에 대한 자세한 내용은 [Azure Active Directory와 애플리케이션 통합](/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad)을 참조하세요.
    
        > [!NOTE] 
        > **Azure AD 사용자 ID** 인증 옵션을 선택하는 경우 다단계 인증과 Microsoft 계정 인증이 지원되지 않습니다.
    
    2. **Azure AD 서비스 ID** 인증 옵션을 선택한 경우 다음을 수행합니다.
        1. Data Lake Storage Gen1 데이터에 액세스하기 위한 AAD(Azure Active Directory) 애플리케이션 및 서비스 사용자를 만듭니다.
    
        2. 이 AAD 애플리케이션에 Data Lake Storage Gen1 리소스에 액세스할 수 있는 적절한 권한을 할당합니다. 이 인증 옵션에 대한 자세한 내용은 [Use portal to create Active Directory application and service principal that can access resources](/azure/azure-resource-manager/resource-group-create-service-principal-portal)(리소스에 액세스할 수 있는 Active Directory 애플리케이션 및 서비스 사용자를 포털에서 만들기)를 참조하세요.
    
        3. **클라이언트 ID**, **비밀 키** 및 **테넌트 이름** 필드에 값을 제공합니다.
    
        4. 연결을 테스트하려면 **연결 테스트** 를 선택합니다.  
  
6.  **확인** 을 선택하여 **Azure Data Lake Store 연결 관리자 편집기** 대화 상자를 닫습니다.  

## <a name="view-the-properties-of-the-connection-manager"></a>연결 관리자의 속성 보기
작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.  
  
