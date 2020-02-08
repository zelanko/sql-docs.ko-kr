---
title: Azure Storage 연결 관리자 | Microsoft Docs
description: Azure Storage 연결 관리자를 사용하여 SSIS 패키지가 Azure Storage 계정에 연결할 수 있습니다.
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6d3912e2b5cbf8051348191cf3efb6ed2d20d551
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74687200"
---
# <a name="azure-storage-connection-manager"></a>Azure Storage 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Azure Storage 연결 관리자를 사용하여 SQL Server Integration Services(SSIS) 패키지가 Azure Storage 계정에 연결할 수 있습니다. 이 연결 관리자는 [Azure용 SQL Server Integration Services(SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다. 
  
**SSIS 연결 관리자 추가** 대화 상자에서 **AzureStorage** > **추가**를 클릭합니다.  
  
사용할 수 있는 속성은 다음과 같습니다.

- **서비스:** 연결할 스토리지 서비스를 지정합니다.
- **계정 이름**: 스토리지 계정 이름을 지정합니다.
- **인증:** 사용할 인증 방법을 지정합니다. AccessKey 및 ServicePrincipal 인증이 지원됩니다.
    - **AccessKey:** 이 인증 방법에 대해 **계정 키**를 지정합니다.
    - **ServicePrincipal:** 이 인증 방법에 대해 서비스 사용자의 **애플리케이션 ID**, **애플리케이션 키**, **테넌트 ID**를 지정합니다.
      **테스트 연결**이 작동하려면 서비스 사용자에게 최소한 스토리지 계정에 대한 **Storage Blob 데이터 읽기 권한자** 역할을 할당해야 합니다.
      자세한 내용은 [Azure Portal에서 RBAC로 Azure Blob 및 큐 데이터에 대한 액세스 권한 부여](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal)를 참조하세요.
- **환경:** 스토리지 계정을 호스팅하는 클라우드 환경을 지정합니다.

## <a name="managed-identities-for-azure-resources-authentication"></a>Azure 리소스 인증을 위한 관리 ID
[Azure Data Factory의 Azure-SSIS 통합 런타임](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)에 서 SSIS 패키지를 실행하는 경우 Azure Storage 인증을 위해 데이터 팩터리와 연결된 [관리 ID](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity)를 사용할 수 있습니다. 지정된 팩터리는 이 ID를 사용하여 스토리지 계정에 액세스하고 해당 데이터베이스에 대해 데이터를 복사할 수 있습니다.

일반적으로 Azure Storage 인증을 위해 [Azure Active Directory를 사용하여 Azure Storage에 대한 액세스 인증](https://docs.microsoft.com/azure/storage/common/storage-auth-aad)을 참조하세요. Azure Storage에 관리 ID 인증을 사용하려면 다음을 수행합니다.

1. [Azure Portal에서 데이터 팩터리 관리 ID를 찾습니다](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). 데이터 팩터리의 **속성**으로 이동합니다. **관리 ID 애플리케이션 ID**(**관리 ID 개체 ID**가 아닌)를 복사합니다.

1. 관리 ID에 스토리지 계정에 대한 적절한 권한을 부여합니다. 역할에 대한 자세한 내용은 [RBAC를 사용하여 Azure Storage 데이터에 대한 액세스 권한 관리](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal)를 참조하세요.

    - **원본으로** 액세스 제어(IAM)에서 최소한 **Storage Blob 데이터 읽기 권한자** 역할을 부여합니다.
    - **대상으로** 액세스 제어(IAM)에서 최소한 **Storage Blob 데이터 기여자** 역할을 부여합니다.

그런 후 Azure Storage 연결 관리자에 대해 관리 ID 인증을 구성합니다. 다음은 이 작업을 수행하는 옵션입니다.

- **디자인 타임에 구성합니다.** SSIS 디자이너에서 Azure Storage 연결 관리자를 두 번 클릭하여 **Azure Storage 연결 관리자 편집기**를 엽니다. **관리 ID를 사용하여 Azure에 인증**을 선택합니다.
    > [!NOTE]
    >  현재 이 옵션은 SSIS 디자이너 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server에서 SSIS 패키지를 실행하는 경우 적용되지 않습니다(관리 ID 인증이 작동하지 않음).
    
- **런타임에 구성합니다.** [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 또는 [Azure Data Factory SSIS 패키지 실행 작업](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)을 통해 패키지를 실행하는 경우 Azure Storage 연결 관리자를 찾습니다. `ConnectUsingManagedIdentity` 속성을 `True`로 업데이트합니다.
    > [!NOTE]
    >  Azure-SSIS 통합 런타임에서 Azure Storage 연결 관리자에 미리 구성된 모든 다른 인증 방법(예: 액세스 키, 서비스 사용자)은 관리 ID 인증을 스토리지 작업에 사용하는 경우 재정의됩니다.

> [!NOTE]
>  기존 패키지에서 관리 ID 인증을 구성하는 가장 좋은 방법은 [최신 SSIS 디자이너](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)로 SSIS 프로젝트를 한 번 이상 다시 빌드하는 것입니다. SSIS 프로젝트의 모든 Azure Storage 연결 관리자에 새 연결 관리자 속성 `ConnectUsingManagedIdentity`가 자동으로 추가되도록 SSIS 프로젝트를 Azure SSIS 통합 런타임에 다시 배포합니다. 또 다른 방법은 런타임에 속성 경로 **\Package.Connections[{연결 관리자의 이름}].Properties[ConnectUsingManagedIdentity]** 에 속성 재정의를 직접 사용하는 것입니다.

## <a name="secure-network-traffic-to-your-storage-account"></a>스토리지 계정에 대한 네트워크 트래픽 보안
Azure Data Factory는 이제 Azure 스토리지에 대한 [신뢰할 수 있는 Microsoft 서비스](https://docs.microsoft.com/azure/storage/common/storage-network-security#trusted-microsoft-services)입니다. 관리 ID 인증을 사용하는 경우 [선택한 네트워크에 대한 액세스를 제한](https://docs.microsoft.com/azure/storage/common/storage-network-security#change-the-default-network-access-rule)하여 스톡리지 계정을 보호하면서도 데이터 팩터리가 스토리지 계정에 액세스할 수 있게 허용할 수 있습니다. 지침은 [예외 관리](https://docs.microsoft.com/azure/storage/common/storage-network-security#managing-exceptions)를 참조하세요.

## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)
