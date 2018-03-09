---
title: "Azure Data Lake Store 파일 시스템 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b04b005bde1b6ef3f930de614c8e7fb003b0985
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 파일 시스템 태스크

Azure Data Lake Store 파일 시스템 태스크를 통해 사용자는 [ADLS(Azure Data Lake Store)](https://azure.microsoft.com/services/data-lake-store/)에서 다양한 파일 시스템 작업을 수행할 수 있습니다.

Azure Data Lake Store 파일 시스템 태스크는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 파일 시스템 태스크 구성

패키지에 Azure Data Lake Store 파일 시스템 태스크를 추가하려면 SSIS 도구 상자에서 디자이너 캔버스로 끕니다. 그런 다음 태스크를 두 번 클릭하거나 태스크를 마우스 오른쪽 단추로 클릭하고 **편집**을 선택하여 **Azure Data Lake Store 파일 시스템 태스크 편집기** 대화 상자를 엽니다.

**작업** 속성은 수행할 파일 시스템 작업을 지정합니다. 다음 작업 중 하나를 선택합니다.

- **CopyToADLS:** ADLS에 파일을 업로드합니다.
- **CopyFromADLS:** ADLS에서 파일을 다운로드합니다.

## <a name="configure-the-properties-for-the-operation"></a>작업에 대한 속성 구성
모든 작업의 경우 Azure Data Lake 연결 관리자를 지정해야 합니다.

다음은 각 작업에 해당하는 속성입니다.

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:** 업로드할 파일을 포함하는 원본 로컬 디렉터리를 지정합니다.
- **FileNamePattern:** 원본 파일에 대한 파일 이름 필터를 지정합니다. 지정된 패턴과 일치하는 이름의 파일만 업로드됩니다. 와일드카드 `*` 및 `?`가 지원됩니다.
- **SearchRecursively:** 업로드할 파일에 대한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정합니다.
- **AzureDataLakeDirectory:** 파일을 업로드할 ADLS 대상 디렉터리를 지정합니다.
- **FileExpiry:** ADLS에 업로드한 파일에 대한 만료 날짜 및 시간을 지정합니다. 파일이 만료되지 않음을 나타내도록 이 속성을 비워 둡니다.

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:** 다운로드할 파일을 포함하는 ADLS 소스 디렉터리를 지정합니다.
- **SearchRecursively:** 다운로드할 파일에 대한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정합니다.
- **LocalDirectory:** 다운로드한 파일을 저장할 대상 디렉터리를 지정합니다.
