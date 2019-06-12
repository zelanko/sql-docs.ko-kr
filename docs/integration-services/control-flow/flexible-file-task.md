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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d01304a36f7676f53ffef3f6c6e3c600cb87cb6
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411100"
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
현재는 **복사** 작업만 지원됩니다.

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
