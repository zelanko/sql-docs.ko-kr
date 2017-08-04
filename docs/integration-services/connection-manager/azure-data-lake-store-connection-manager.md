---
title: "Azure 데이터 레이크 저장소 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: 39630087acdb2ade2e77d4364e4467f8d740d8d4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 연결 관리자
  **Azure Data Lake Store 연결 관리자** 를 사용하면 두 가지 인증 유형 즉, Azure AD 사용자 ID와 Azure AD 서비스 ID를 통해 SSIS 패키지를 Azure Data Lake Store 서비스에 연결할 수 있습니다.  
  
 **Azure 데이터 레이크 저장소 연결 관리자** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.

>   [!NOTE]
> Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Azure Data Lake Store 원본과 Azure Data Lake Store 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 연결 관리자 구성

 
1.  **SSIS 연결 관리자 추가** 대화 상자에서 **AzureDataLake**를 선택하고 **추가**를 클릭합니다.  
  
2.  Azure Data Lake Store 연결 관리자 편집기 대화 상자에서 **ADLS 호스트** 필드에 Azure Data Lake Store 호스트 URL을 입력합니다. 예를 들어: `https://test.azuredatalakestore.net` 또는 `test.azuredatalakestore.net`합니다.
  
3.  해당 인증 유형을 선택하여 Azure Data Lake Store 데이터에 액세스합니다.

    1.  **Azure AD 사용자 ID** 인증 옵션을 선택한 경우 다음을 수행합니다.
        1. **사용자 이름** 및 **암호** 필드에 값을 지정합니다. 
    
        2. **연결 테스트** 단추를 클릭하여 연결을 테스트합니다. 이전에 사용자 본인과 테넌트 관리자가 Azure Data Lake Store 데이터에 SSIS가 액세스하는 것에 동의하지 않은 경우 팝아웃 대화 상자에서 **동의** 단추를 클릭하여 SSIS가 Azure Data Lake Store 데이터에 액세스하는 것에 동의해야 합니다. 이 동의 환경에 대한 자세한 내용은 [Azure Active Directory와 응용 프로그램 통합](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application)을 참조하세요.
    
        >   [!NOTE] 
        > Azure AD 사용자 ID 인증 옵션에서는 다단계 인증과 Microsoft 계정이 지원되지 않습니다.
    
    2. **Azure AD 서비스 ID** 인증 옵션을 선택한 경우 다음을 수행합니다.
        1. Azure Data Lake 리소스에 액세스할 수 있는 AAD 응용 프로그램 및 서비스 사용자를 만듭니다.
    
        2. 이 AAD 응용 프로그램에 Azure Data Lake 리소스에 액세스할 수 있는 해당 권한을 할당합니다. 이 인증 옵션에 대한 자세한 내용은 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)(리소스에 액세스할 수 있는 Active Directory 응용 프로그램 및 서비스 사용자를 포털에서 만들기)를 참조하세요.
    
        3. **클라이언트 ID**, **보안 키** 및 **테넌트 이름** 필드에 값을 지정합니다.
    
        4. **연결 테스트** 단추를 클릭하여 연결을 테스트합니다.  
  
6.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
    작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.  
  
  
