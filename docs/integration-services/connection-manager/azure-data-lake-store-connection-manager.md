---
title: "Azure 데이터 레이크 저장소 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 0a84b10114d785c9216a0902b2eefbcb0bd3f4c8
ms.contentlocale: ko-kr
ms.lasthandoff: 10/11/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 연결 관리자
SQL Server Integration Services (SSIS) 패키지는 다음 두 가지 인증 유형 중 하나가 지정 된 Azure 데이터 레이크 저장소 서비스에 연결 하는 데 Azure 데이터 레이크 저장소 연결 관리자를 사용할 수 있습니다.
-   Azure AD 사용자 Id
-   Azure AD 서비스 Id 

Azure 데이터 레이크 저장소 연결 관리자의 구성 요소인는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.

>   [!NOTE]
> Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Azure Data Lake Store 원본과 Azure Data Lake Store 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 연결 관리자 구성

1.  에 **SSIS 연결 관리자 추가** 대화 상자에서 **AzureDataLake**를 선택한 후 **추가**합니다. **Azure 데이터 레이크 저장소 연결 관리자 편집기** 대화 상자가 열립니다.
  
2.  에 **Azure 데이터 레이크 저장소 연결 관리자 편집기** 대화 상자는 **ADLS 호스트** 필드 Azure 데이터 레이크 저장소 호스트 URL을 입력 합니다. 예를 들어: `https://test.azuredatalakestore.net` 또는 `test.azuredatalakestore.net`합니다.
  
3.  에 **인증** 필드 Azure 데이터 레이크 저장소의 데이터에 액세스 하려면 적절 한 인증 유형을 선택 합니다.

    1.  선택 하는 경우는 **Azure AD 사용자 Id** 인증 옵션에서 다음을 수행 합니다.
        1. 에 대 한 값을 제공 된 **사용자 이름** 및 **암호** 필드입니다. 
    
        2. 연결을 테스트 하려면 선택 **연결 테스트**합니다. 사용자 또는 테 넌 트 관리자 SSIS를 Azure 데이터 레이크 저장소 데이터에 액세스할 수 있도록 이전에 동의 하지 않은 경우 **Accept** 대화 상자가 나타나면 합니다. 이 동의 환경에 대한 자세한 내용은 [Azure Active Directory와 응용 프로그램 통합](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application)을 참조하세요.
    
        >   [!NOTE] 
        > 선택 하는 경우는 **Azure AD 사용자 Id** 인증 옵션, multi-factor authentication 및 Microsoft 계정 인증 지원 되지 않습니다.
    
    2. 선택 하는 경우는 **Azure AD 서비스 Id** 인증 옵션에서 다음을 수행 합니다.
        1. Azure Active Directory (AAD) 응용 프로그램 및 서비스 Azure 데이터 레이크 데이터에 액세스 하려면 보안 주체를 만듭니다.
    
        2. 이 AAD 응용 프로그램 Azure 데이터 레이크 리소스에 액세스할 수 있도록 적절 한 권한을 할당 합니다. 이 인증 옵션에 대한 자세한 내용은 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)(리소스에 액세스할 수 있는 Active Directory 응용 프로그램 및 서비스 사용자를 포털에서 만들기)를 참조하세요.
    
        3. 에 대 한 값을 제공 된 **클라이언트 Id**, **비밀 키**, 및 **테 넌 트 이름** 필드입니다.
    
        4. 연결을 테스트 하려면 선택 **연결 테스트**합니다.  
  
6.  선택 **확인** 를 닫으려면는 **Azure 데이터 레이크 저장소 연결 관리자 편집기** 대화 상자.  

## <a name="view-the-properties-of-the-connection-manager"></a>연결 관리자의 속성 보기
작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.  
  
  

