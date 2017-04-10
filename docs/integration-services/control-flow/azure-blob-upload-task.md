---
title: "Azure Blob 업로드 태스크 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpblobuptask.f1"
  - "sql14.dts.designer.afpblobuptask.f1"
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Azure Blob 업로드 태스크
  SSIS 패키지는 **Azure Blob 업로드 태스크**를 통해 Azure Blob Storage에 파일을 업로드할 수 있습니다.
  
>   [!NOTE] Azure Storage 연결 관리자 및 이를 사용하는 구성 요소(Blob 원본, Blob 대상, Blob 업로드 태스크 및 Blob 다운로드 태스크)에서 범용 저장소 계정과 Blob Storage 계정 모두에 연결할 수 있도록 하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure Feature Pack을 다운로드하세요. 이러한 두 가지 유형의 저장소 계정에 대한 자세한 내용은 [Microsoft Azure Storage 소개](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)를 참조하세요. 
    
**Azure Blob 업로드 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집**을 클릭하여 다음과 같은 **Azure Blob 업로드 태스크 편집기** 대화 상자를 표시합니다.  
  
 **Azure Blob 업로드 태스크**는 SQL Server 2016에 대해 제공되는 Azure용 SSIS(SQL Server Integration Services) 기능 팩의 구성 요소입니다. [여기](http://go.microsoft.com/fwlink/?LinkID=626967)서 기능 팩을 다운로드하세요.  
  
 다음 표에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**Description**|  
|AzureStorageConnection|기존 Azure 저장소 연결 관리자를 지정하거나 Blob 파일이 호스트되는 위치를 가리키는 Azure 저장소 계정을 참조하는 저장소 연결 관리자를 새로 만듭니다.|  
|BlobContainer|blob으로 업로드된 파일이 저장되는 blob 컨테이너의 이름을 지정합니다.|  
|BlobDirectory|업로드한 파일이 블록 blob으로 저장되는 blob 디렉터리를 지정합니다. Blob 디렉터리는 가상 계층 구조입니다. 이미 있는 Blob은 업로드한 Blob으로 바뀝니다.|  
|LocalDirectory|업로드할 파일이 포함된 로컬 디렉터리를 지정합니다.|  
|FileName|이름 필터를 지정하여 지정된 이름 패턴의 파일을 선택합니다. 예를 들어 MySheet*.xls\*는 MySheet001.xls 및 MySheetABC.xlsx와 같은 파일을 포함합니다.|  
|TimeRangeFrom/TimeRangeTo|시간 범위 필터를 지정합니다. **TimeRangeFrom**에서 **TimeRangeTo** 사이에 수정된 파일이 포함됩니다.|  
  
  