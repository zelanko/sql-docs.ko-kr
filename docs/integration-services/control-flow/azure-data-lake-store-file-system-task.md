---
title: "Azure 데이터 레이크 저장소 파일 시스템 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: cbc72958f992e0b5cae12cdfc8c0996378f9708c
ms.contentlocale: ko-kr
ms.lasthandoff: 10/11/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Azure 데이터 레이크 저장소 파일 시스템 태스크

Azure 데이터 레이크 저장소 파일 시스템 태스크에 다양 한 파일 시스템 작업을 수행 하는 사용자가 수 있습니다. [데이터 레이크 저장소 ADLS (Azure)](https://azure.microsoft.com/services/data-lake-store/)합니다.

Azure 데이터 레이크 저장소 파일 시스템 태스크는의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>Azure 데이터 레이크 저장소 파일 시스템 태스크 구성

패키지에는 Azure 데이터 레이크 저장소 파일 시스템 태스크를 추가 하려면 끕니다 SSIS 도구 상자에서 디자이너 캔버스에 해당 합니다. 그런 다음 작업을 두 번 클릭 하거나 작업을 마우스 오른쪽 단추로 클릭을 선택 **편집**, 열려는 **Azure 데이터 레이크 저장소 파일 시스템 태스크 편집기** 대화 상자.

**작업** 속성 파일 시스템 작업을 수행 하려면을 지정 합니다. 다음 작업 중 하나를 선택 합니다.

- **CopyToADLS:** ADLS에 파일을 업로드 합니다.
- **CopyFromADLS:** ADLS에서 파일을 다운로드 합니다.

## <a name="configure-the-properties-for-the-operation"></a>작업에 대 한 속성을 구성 합니다.
모든 작업에 대 한 Azure 데이터 레이크 연결 관리자를 지정 해야 합니다.

다음은 각 작업에는 속성:

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:** 업로드할 파일을 포함 하는 원본 로컬 디렉터리를 지정 합니다.
- **FileNamePattern:** 소스 파일에 대 한 파일 이름 필터를 지정 합니다. 이름이 지정된 된 패턴과 일치 하는 파일만 업로드 됩니다. 와일드 카드 `*` 및 `?` 지원 됩니다.
- **SearchRecursively:** 위해 업로드할 파일에 대 한 원본 디렉터리 내에서 재귀적으로 검색할 것인지 지정 합니다.
- **AzureDataLakeDirectory:** 파일을 업로드 하려면 ADLS 대상 디렉터리를 지정 합니다.
- **FileExpiry:** ADLS에 업로드 한 만료 날짜와 파일에 대 한 시간을 지정 합니다. 이 속성을 나타내는 파일 만료 되지 않도록 비워 둡니다.

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:** 다운로드할 파일을 포함 하는 ADLS 소스 디렉터리를 지정 합니다.
- **SearchRecursively:** 다운로드할 파일에 대 한 원본 디렉터리 내에서 재귀적으로 검색할 것인지 지정 합니다.
- **LocalDirectory:** 다운로드 한 파일을 저장할 대상 디렉터리를 지정 합니다.

