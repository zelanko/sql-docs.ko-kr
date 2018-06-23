---
title: Azure Blob 다운로드 작업 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.afpblobdltask.f1
- sql11.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 680d2efd5d2f5cbc52539c0340539d33f1c6bcb3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182313"
---
# <a name="azure-blob-download-task"></a>Azure Blob 다운로드 작업
  Azure Blob 다운로드 작업을 사용하면 SSIS 패키지에서 Azure Blob Storage의 파일을 다운로드할 수 있습니다.   
**Azure Blob 다운로드 작업**을 추가하려면 이 작업을 SSIS 디자이너로 끌어다 놓고 두 번 클릭하거나 **편집** 을 클릭하여 다음과 같은 **Azure Blob 다운로드 작업 편집기** 대화 상자를 표시합니다.  
  
 다음 표에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**설명**|  
|AzureStorageConnection|기존 Azure 저장소 연결 관리자를 지정하거나 Blob 파일이 호스트되는 위치를 가리키는 Azure 저장소 계정을 참조하는 저장소 연결 관리자를 새로 만듭니다.|  
|BlobContainer|다운로드할 Blob 파일을 포함하는 Blob 컨테이너의 이름을 지정합니다.|  
|BlobDirectory|다운로드할 Blob 파일을 포함하는 Blob 디렉터리를 지정합니다. Blob 디렉터리는 가상 계층 구조입니다.|  
|LocalDirectory|다운로드한 Blob 파일을 저장할 로컬 디렉터리를 지정합니다.|  
|FileName|이름 필터를 지정하여 지정된 이름 패턴의 파일을 선택합니다. 예를 들어 MySheet*.xls\* 는 MySheet001.xls 및 MySheetABC.xlsx와 같은 파일을 포함합니다.|  
|TimeRangeFrom/TimeRangeTo|시간 범위 필터를 지정합니다. **TimeRangeFrom** 에서 **TimeRangeTo** 사이에 수정된 파일이 포함됩니다.|  
  
  