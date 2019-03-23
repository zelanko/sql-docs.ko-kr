---
title: Azure Data Lake Store 파일 시스템 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aeabdcfa1fd36adf9bd4291623c56fbfecf0520e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390251"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 파일 시스템 태스크

합니다 **Azure Data Lake Store 파일 시스템 태스크** 에서 다양 한 파일 시스템 작업을 수행할 수 있습니다 [Azure Data Lake 저장소 (ADLS)](https://azure.microsoft.com/services/data-lake-store/)합니다.

패키지에 Azure Data Lake Store 파일 시스템 태스크를 추가하려면 SSIS 도구 상자에서 디자이너 캔버스로 끕니다. 다음 태스크를 두 번 클릭 하거나 태스크를 마우스 오른쪽 단추로 클릭 및 선택 **편집**, 작업 편집기 대화 상자를 엽니다.

**작업** 속성은 수행할 파일 시스템 작업을 지정합니다. 다음 작업이 지원 됩니다.

* **CopyToADLS:** ADLS에 파일을 업로드 합니다.
* **CopyFromADLS:** ADLS에서 파일을 다운로드 합니다.

모든 작업의 경우 Azure Data Lake 연결 관리자를 지정해야 합니다.

다음은 각 작업에 특정 속성에 설명 합니다.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** 업로드할 파일을 포함 하는 원본 디렉터리를 지정 합니다.
* **FileNamePattern:** 소스 파일에 대 한 파일 이름 필터를 지정합니다. 이름이 지정된 된 패턴과 일치 하는 파일만 업로드 됩니다. 와일드카드 `*` 및 `?`가 지원됩니다.
* **SearchRecursively:** 업로드할 파일에 대 한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정 합니다.
* **AzureDataLakeDirectory:** 파일을 업로드할 ADLS 대상 디렉터리를 지정 합니다.
* **FileExpiry:** ADLS에 업로드 또는이 속성을 비워 파일 만료 되지 않도록 나타내려면 만료 날짜 및 시간 파일을 지정 합니다.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** 다운로드할 파일을 포함 하는 ADLS 소스 디렉터리를 지정 합니다.
* **SearchRecursively:** 파일 다운로드에 대 한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정 합니다.
* **LocalDirectory:** 다운로드 한 파일을 저장할 대상 디렉터리를 지정 합니다.
