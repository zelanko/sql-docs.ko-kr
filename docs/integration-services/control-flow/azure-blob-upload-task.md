---
title: "Azure Blob 업로드 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 07/25/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cec51398ac521abc0345e90b3c6ed156b542b5f1
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-upload-task"></a>Azure Blob 업로드 태스크
SSIS 패키지는 **Azure Blob 업로드 태스크** 를 통해 Azure Blob Storage에 파일을 업로드할 수 있습니다.
    
**Azure Blob 업로드 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 다음과 같은 **Azure Blob 업로드 태스크 편집기** 대화 상자를 표시합니다.  
  
 **Azure Blob 업로드 태스크** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.
  
 다음 표에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**Description**|  
|AzureStorageConnection|기존 Azure 저장소 연결 관리자를 지정하거나 Blob 파일이 호스트되는 위치를 가리키는 Azure 저장소 계정을 참조하는 저장소 연결 관리자를 새로 만듭니다.|  
|BlobContainer|Blob으로 업로드 된 파일을 포함 하는 blob 컨테이너의 이름을 지정 합니다.|  
|BlobDirectory|블록 blob으로 업로드 된 파일이 저장 된 blob 디렉터리를 지정 합니다. Blob 디렉터리는 가상 계층 구조입니다. Blob가 이미 있는 경우 자동으로 바뀝니다.|  
|LocalDirectory|업로드할 파일이 포함된 로컬 디렉터리를 지정합니다.|  
|FileName|이름 필터를 지정하여 지정된 이름 패턴의 파일을 선택합니다. 예를 들어 `MySheet*.xls\*` 와 같은 파일 포함 `MySheet001.xls` 및 `MySheetABC.xlsx`합니다.|  
|TimeRangeFrom/TimeRangeTo|시간 범위 필터를 지정합니다. 수정 된 파일이 **TimeRangeFrom** 하기 전에 **TimeRangeTo** 포함 됩니다.|  
  
  

