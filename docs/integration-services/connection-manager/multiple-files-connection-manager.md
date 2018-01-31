---
title: "다중 파일 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- Multiple Files connection manager
- connection managers [Integration Services], Multiple Files
- connections [Integration Services], files
- multiple file connections
ms.assetid: 10bdc56e-c5cd-4ddb-b2f7-375fe57fe8b2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ff3fcef1362333dc1ac2de5774d63ce025b8557
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="multiple-files-connection-manager"></a>다중 파일 연결 관리자
  다중 파일 연결 관리자를 사용하면 패키지에서 기존 파일 및 폴더를 참조하거나 런타임에 파일 및 폴더를 만들 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 기본 제공 태스크 및 데이터 흐름 구성 요소는 다중 파일 연결 관리자를 사용하지 않습니다. 그러나 스크립트 태스크와 스크립트 구성 요소에서 이 연결 관리자를 사용할 수 있습니다. 스크립트 태스크에서 연결 관리자를 사용하는 방법은 [Connecting to Data Sources in the Script Task](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)을 참조하십시오. 스크립트 구성 요소에서 연결 관리자를 사용하는 방법은 [Connecting to Data Sources in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)을 참조하십시오.  
  
## <a name="usage-types-of-the-multiple-files-connection-manager"></a>다중 파일 연결 관리자의 사용 유형  
 다중 파일 연결 관리자의 **FileUsageType** 속성은 연결 사용 방법을 지정합니다. 다중 파일 연결 관리자에서는 파일이나 폴더를 만들고 기존 파일 또는 기존 폴더를 사용할 수 있습니다.  
  
 다음 표에서는 **FileUsageType**값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|다중 파일 연결 관리자에서 기존 파일을 사용합니다.|  
|**1**|다중 파일 연결 관리자에서 파일을 만듭니다.|  
|**2**|다중 파일 연결 관리자에서 기존 폴더를 사용합니다.|  
|**3**|다중 파일 연결 관리자에서 폴더를 만듭니다.|  
  
## <a name="configuration-of-the-multiple-files-connection-manager"></a>다중 파일 연결 관리자 구성  
 패키지에 다중 파일 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 다중 파일 연결로 확인되는 연결 관리자를 만들고, 다중 파일 연결 속성을 설정하고, 다중 파일 연결을 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **MULTIFILE**로 설정됩니다.  
  
 다음과 같은 방법으로 다중 파일 연결 관리자를 구성할 수 있습니다.  
  
-   파일 및 폴더의 사용 유형을 지정합니다.  
  
-   파일 및 폴더를 지정합니다.  
  
-   다중 파일 또는 폴더를 사용하는 경우 파일 및 폴더가 액세스되는 순서를 지정합니다.  
  
 다중 파일 연결 관리자에서 다중 파일 및 폴더를 참조하는 경우 파일 및 폴더의 경로는 세로줄 문자(|)로 구분됩니다. 연결 관리자의 **ConnectionString** 속성은 다음 형식을 갖습니다.  
  
 \<*경로*>|\<*경로*>  
  
 또한 와일드카드 문자를 사용하여 다중 파일이나 폴더를 지정할 수 있습니다. 예를 들어 C 드라이브의 모든 텍스트 파일을 참조하려면 **ConnectionString** 속성 값을 C:\\*.txt로 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [파일 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)을 참조하십시오.  
  
  
