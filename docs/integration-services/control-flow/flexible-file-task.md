---
title: 유연한 파일 작업 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4ed8ba34e8e50d6414d68cae4aa386848f88b6d5
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72807415"
---
# <a name="flexible-file-task"></a>유연한 파일 작업

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Flexible File Task를 사용하면 사용자가 지원되는 다양한 스토리지 서비스에서 파일 작업을 수행할 수 있습니다.
현재 지원되는 스토리지 서비스는 다음과 같습니다.

- 로컬 파일 시스템
- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

Flexible File Task는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.

패키지에 Flexible File Task를 추가하려면 SSIS 도구 상자에서 디자이너 캔버스로 끕니다. 그런 다음, 작업을 두 번 클릭하거나 마우스 오른쪽 단추로 클릭하고 **편집**을 선택하여 **Flexible File Task 편집기** 대화 상자를 엽니다.

**작업** 속성은 수행할 파일 작업을 지정합니다.
현재 지원되는 작업은 다음과 같습니다.
- **복사** 작업
- **삭제** 작업

**복사** 작업에 사용할 수 있는 속성은 다음과 같습니다.

- **SourceConnectionType:** 원본 연결 관리자 유형을 지정합니다.
- **SourceConnection:** 원본 연결 관리자를 지정합니다.
- **SourceFolderPath:** 원본 폴더 경로를 지정합니다.
- **SourceFileName:** 원본 파일 이름을 지정합니다. 빈 상태로 둔 경우 원본 폴더가 복사됩니다.
- **SearchRecursively:** 재귀적으로 하위 폴더를 복사할지 여부를 지정합니다.
- **DestinationConnectionType:** 대상 연결 관리자 유형을 지정합니다.
- **DestinationConnection** 대상 연결 관리자를 지정합니다.
- **DestinationFolderPath:** 대상 폴더 경로를 지정합니다.
- **DestinationFileName:** 대상 파일 이름을 지정합니다.

**삭제** 작업에 사용할 수 있는 속성은 다음과 같습니다.
- **ConnectionType:** 연결 관리자 유형을 지정합니다.
- **Connection:** 연결 관리자를 지정합니다.
- **FolderPath:** 폴더 경로를 지정합니다.
- **FileName:** 파일 이름을 지정합니다. 빈 상태로 두면 폴더가 삭제됩니다. Azure Blob Storage에서는 폴더 삭제가 지원되지 않습니다.

***서비스 사용자 권한 구성에 대한 참고 사항***

**테스트 연결**이 이뤄지려면(Blob Storage 또는 Data Lake Storage Gen2) 서비스 사용자에게 스토리지 계정에 대한 **Storage Blob 데이터 읽기 권한자** 역할을 하나 이상 할당해야 합니다.
이 작업은 [RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal)를 사용하여 수행됩니다.

Blob Storage의 경우 최소한 **Storage Blob 데이터 읽기 권한자** 및 **Storage Blob 데이터 기여자** 역할을 각각 할당하여 읽기 및 쓰기 권한을 부여합니다.

Data Lake Storage Gen2의 경우 RBAC 및 [ACL](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer)을 통해 사용 권한이 결정됩니다.
ACL은 [여기](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal)에 자세히 설명된 대로 앱 등록에 서비스 사용자의 OID(개체 ID)를 사용하여 구성된다는 것에 주의합니다.
RBAC 구성에 사용되는 애플리케이션(클라이언트) ID와는 다릅니다.
기본 제공 역할 또는 사용자 지정 역할을 통해 보안 주체에 RBAC 데이터 권한이 부여된 경우 요청의 권한 부여 시 먼저 이러한 사용 권한이 평가됩니다.
보안 주체의 RBAC 할당을 통해 요청한 작업의 권한이 부여된 경우 권한 부여가 즉시 확인되고 추가 ACL 검사가 수행되지 않습니다.
또는 보안 주체에 RBAC 할당이 없거나 요청한 작업이 할당된 사용 권한과 일치하지 않는 경우 ACL 검사를 통해 보안 주체가 요청된 작업을 수행할 수 있는 권한이 있는지 확인합니다.

- 읽기 권한의 경우 복사할 파일에 대한 **읽기** 권한과 함께 원본 파일 시스템부터 최소한 **실행** 권한을 부여합니다. 또는 RBAC를 사용하여 최소한 **Storage Blob 데이터 읽기 권한자** 역할을 부여합니다.
- 쓰기 권한의 경우 싱크 폴더에 대한 **쓰기** 권한과 함께 싱크 파일 시스템부터 최소한 **실행** 권한을 부여합니다. 또는 RBAC를 사용하여 최소한 **Storage Blob 데이터 기여자** 역할을 부여합니다.

자세한 내용은 [이](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control) 문서를 참조하세요.
