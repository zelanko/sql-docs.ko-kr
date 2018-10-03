---
title: 파일 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ea35467bd5b5209a2e625adc081774ef39492439
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119973"
---
# <a name="file-connection-manager"></a>파일 연결 관리자
  파일 연결 관리자를 사용하면 패키지에서 기존 파일 또는 폴더를 참조하거나 런타임에 파일 또는 폴더를 만들 수 있습니다. 예를 들어 Excel 파일을 참조할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 일부 구성 요소는 파일에 있는 정보를 사용하여 작업을 수행합니다. 예를 들어 SQL 실행 태스크에서는 해당 태스크가 실행하는 SQL 문이 포함된 파일을 참조할 수 있습니다. 다른 구성 요소는 파일에 대한 작업을 수행합니다. 예를 들어 파일 시스템 태스크는 파일을 참조하여 새 위치로 복사할 수 있습니다.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>파일 연결 관리자의 사용 유형  
 `FileUsageType` 파일 연결 관리자의 속성 파일 연결을 사용 하는 방법을 지정 합니다. 파일 연결 관리자에서는 파일이나 폴더를 만들고 기존 파일 또는 기존 폴더를 사용할 수 있습니다.  
  
 다음 표에서 값을 나열 `FileUsageType`합니다.  
  
|값|Description|  
|-----------|-----------------|  
|`0`|파일 연결 관리자에서 기존 파일을 사용합니다.|  
|`1`|파일 연결 관리자에서 파일을 만듭니다.|  
|`2`|파일 연결 관리자에서 기존 폴더를 사용합니다.|  
|`3`|파일 연결 관리자에서 폴더를 만듭니다.|  
  
## <a name="multiple-file-or-folder-connections"></a>다중 파일 또는 폴더 연결  
 파일 연결 관리자는 파일 또는 폴더를 하나만 참조할 수 있습니다. 파일이나 폴더를 여러 개 참조하려면 파일 연결 관리자 대신 다중 파일 연결 관리자를 사용하십시오. 자세한 내용은 [Multiple Files Connection Manager](multiple-files-connection-manager.md)을(를) 참조하세요.  
  
## <a name="configuration-of-the-file-connection-manager"></a>파일 연결 관리자 구성  
 패키지에 파일 연결 관리자를 추가 하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결, 런타임에 파일 연결으로 확인 됩니다 하 고, 파일 연결 속성을 설정 하 고, 파일 연결을 추가 하는 관리자를 만들고는 `Connections` 패키지의 컬렉션입니다.  
  
 합니다 `ConnectionManagerType` 연결 관리자의 속성이 `FILE`합니다.  
  
 다음과 같은 방법으로 파일 연결 관리자를 구성할 수 있습니다.  
  
-   사용 유형을 지정합니다.  
  
-   파일 또는 폴더를 지정합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 속성 창에 식을 지정하여 파일 연결 관리자에 대한 ConnectionString 속성을 설정할 수 있습니다. 그러나 식을 사용하여 파일 또는 폴더를 지정할 때 유효성 검사 오류가 발생하지 않도록 하려면 **파일 연결 관리자 편집기**에서 **파일/폴더**에 대해 파일 또는 폴더 경로를 추가합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [파일 연결 관리자 편집기](../file-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성 하는 방법에 대 한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 하 고 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)합니다.  
  
  
