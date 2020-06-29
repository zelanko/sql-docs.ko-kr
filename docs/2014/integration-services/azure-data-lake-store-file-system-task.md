---
title: Azure Data Lake Store 파일 시스템 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2d01c61521bf746076b359c65103e0ea46ec0f1b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439410"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 파일 시스템 태스크

사용자는 **Azure Data Lake Store 파일 시스템 태스크** 를 사용 하 여 [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/)에서 다양 한 파일 시스템 작업을 수행할 수 있습니다.

패키지에 Azure Data Lake Store 파일 시스템 태스크를 추가하려면 SSIS 도구 상자에서 디자이너 캔버스로 끕니다. 그런 다음 태스크를 두 번 클릭 하거나 태스크를 마우스 오른쪽 단추로 클릭 하 고 **편집**을 선택 하 여 태스크 편집기 대화 상자를 엽니다.

**작업** 속성은 수행할 파일 시스템 작업을 지정합니다. 다음 작업이 지원됩니다.

* **CopyToADLS:** ADLS에 파일을 업로드합니다.
* **CopyFromADLS:** ADLS에서 파일을 다운로드합니다.

모든 작업의 경우 Azure Data Lake 연결 관리자를 지정해야 합니다.

각 작업과 관련 된 속성에 대 한 설명은 다음과 같습니다.

## <a name="copytoadls"></a>CopyToADLS

* **Localdirectory:** 업로드할 파일이 포함 된 원본 디렉터리를 지정 합니다.
* **FileNamePattern:** 원본 파일에 대한 파일 이름 필터를 지정합니다. 지정 된 패턴과 일치 하는 이름을 가진 파일만 업로드 됩니다. 와일드카드 `*` 및 `?`가 지원됩니다.
* **SearchRecursively:** 업로드할 파일에 대한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정합니다.
* **AzureDataLakeDirectory:** 파일을 업로드할 ADLS 대상 디렉터리를 지정합니다.
* **Fileexpiry:** ADLS에 업로드 된 파일의 만료 날짜 및 시간을 지정 하거나이 속성을 비워 두어 파일이 만료 되지 않음을 나타냅니다.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** 다운로드할 파일을 포함하는 ADLS 소스 디렉터리를 지정합니다.
* **SearchRecursively:** 다운로드할 파일에 대한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정합니다.
* **LocalDirectory:** 다운로드한 파일을 저장할 대상 디렉터리를 지정합니다.
