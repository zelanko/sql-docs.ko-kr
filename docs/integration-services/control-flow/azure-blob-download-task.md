---
title: Azure Blob 다운로드 작업 | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a1a8c8c23519ca6f0ceb4ab1d2a3e587f7a86f8
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283167"
---
# <a name="azure-blob-download-task"></a>Azure Blob 다운로드 작업
Azure Blob 다운로드 작업을 사용하면 SSIS 패키지에서 Azure Blob Storage의 파일을 다운로드할 수 있습니다.

**Azure Blob 다운로드 태스크**를 추가하려면 이 작업을 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 다음과 같은 **Azure Blob 다운로드 태스크 편집기** 대화 상자를 표시합니다.  
  
 **Azure Blob 다운로드 태스크**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.  
  
 다음 표에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**설명**|  
|AzureStorageConnection|기존 Azure Storage 연결 관리자를 지정하거나 Blob 파일이 호스트되는 위치를 가리키는 Azure Storage 계정을 참조하는 스토리지 연결 관리자를 새로 만듭니다.|  
|BlobContainer|다운로드할 Blob 파일을 포함하는 Blob 컨테이너의 이름을 지정합니다.|  
|BlobDirectory|다운로드할 Blob 파일을 포함하는 Blob 디렉터리를 지정합니다. Blob 디렉터리는 가상 계층 구조입니다.|  
|LocalDirectory|다운로드한 Blob 파일을 저장할 로컬 디렉터리를 지정합니다.|  
|FileName|이름 필터를 지정하여 지정된 이름 패턴의 파일을 선택합니다. 예를 들어 `MySheet*.xls\*`는 `MySheet001.xls` 및 `MySheetABC.xlsx`와 같은 파일을 포함합니다.|  
|TimeRangeFrom/TimeRangeTo|시간 범위 필터를 지정합니다. **TimeRangeFrom**에서 **TimeRangeTo** 사이에 수정된 파일이 포함됩니다.|  
  
  
