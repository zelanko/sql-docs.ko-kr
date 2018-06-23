---
title: Azure Data Lake Store 파일 시스템 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.openlocfilehash: 240780efd1b12596b0ebb6156ad98c508f0e8051
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078844"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 파일 시스템 태스크
**Azure 데이터 레이크 저장소 파일 시스템 태스크** 사용자가을 다양 한 파일 시스템 작업을 수행할 수 있도록 [데이터 레이크 저장소 ADLS (Azure)](https://azure.microsoft.com/en-us/services/data-lake-store/)합니다.

패키지에 Azure Data Lake Store 파일 시스템 태스크를 추가하려면 SSIS 도구 상자에서 디자이너 캔버스로 끕니다. 그런 다음 작업을 두 번 클릭 하거나 작업을 마우스 오른쪽 단추로 클릭을 선택 **편집**, 작업 편집기 대화 상자를 엽니다.

**작업** 속성은 수행할 파일 시스템 작업을 지정합니다. 다음 작업이 지원 됩니다.

* **CopyToADLS:** ADLS에 파일을 업로드합니다.
* **CopyFromADLS:** ADLS에서 파일을 다운로드합니다.

모든 작업의 경우 Azure Data Lake 연결 관리자를 지정해야 합니다.

다음은 각 작업에는 속성의 설명입니다.

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** 업로드할 파일을 포함 하는 소스 디렉터리를 지정 합니다.
* **FileNamePattern:** 원본 파일에 대한 파일 이름 필터를 지정합니다. 이름이 지정된 된 패턴과 일치 하는 파일만 업로드 됩니다. 와일드카드 `*` 및 `?`가 지원됩니다.
* **SearchRecursively:** 업로드할 파일에 대한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정합니다.
* **AzureDataLakeDirectory:** 파일을 업로드할 ADLS 대상 디렉터리를 지정합니다.
* **FileExpiry:** 파일 ADLS에 업로드 하거나이 속성을 비워 파일 만료 되지 않도록 나타내려면에 대 한 만료 날짜 및 시간을 지정 합니다.

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:** 다운로드할 파일을 포함하는 ADLS 소스 디렉터리를 지정합니다.
* **SearchRecursively:** 다운로드할 파일에 대한 원본 디렉터리 내에서 재귀적으로 검색할지 여부를 지정합니다.
* **LocalDirectory:** 다운로드한 파일을 저장할 대상 디렉터리를 지정합니다.
