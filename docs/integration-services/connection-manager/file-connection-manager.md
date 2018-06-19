---
title: 파일 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f22b22f3134122b733a9d2f233054445d1898c3
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35333517"
---
# <a name="file-connection-manager"></a>파일 연결 관리자
  파일 연결 관리자를 사용하면 패키지에서 기존 파일 또는 폴더를 참조하거나 런타임에 파일 또는 폴더를 만들 수 있습니다. 예를 들어 Excel 파일을 참조할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 일부 구성 요소는 파일에 있는 정보를 사용하여 작업을 수행합니다. 예를 들어 SQL 실행 태스크에서는 해당 태스크가 실행하는 SQL 문이 포함된 파일을 참조할 수 있습니다. 다른 구성 요소는 파일에 대한 작업을 수행합니다. 예를 들어 파일 시스템 태스크는 파일을 참조하여 새 위치로 복사할 수 있습니다.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>파일 연결 관리자의 사용 유형  
 파일 연결 관리자의 **FileUsageType** 속성은 파일 연결 사용 방법을 지정합니다. 파일 연결 관리자에서는 파일이나 폴더를 만들고 기존 파일 또는 기존 폴더를 사용할 수 있습니다.  
  
 다음 표에서는 **FileUsageType**값을 나열합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0**|파일 연결 관리자에서 기존 파일을 사용합니다.|  
|**1.**|파일 연결 관리자에서 파일을 만듭니다.|  
|**2**|파일 연결 관리자에서 기존 폴더를 사용합니다.|  
|**3**|파일 연결 관리자에서 폴더를 만듭니다.|  
  
## <a name="multiple-file-or-folder-connections"></a>다중 파일 또는 폴더 연결  
 파일 연결 관리자는 파일 또는 폴더를 하나만 참조할 수 있습니다. 파일이나 폴더를 여러 개 참조하려면 파일 연결 관리자 대신 다중 파일 연결 관리자를 사용하십시오. 자세한 내용은 [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md)을(를) 참조하세요.  
  
## <a name="configuration-of-the-file-connection-manager"></a>파일 연결 관리자 구성  
 패키지에 파일 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 파일 연결로 확인되는 연결 관리자를 만들고, 파일 연결 속성을 설정하고, 파일 연결을 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **FILE**로 설정됩니다.  
  
 다음과 같은 방법으로 파일 연결 관리자를 구성할 수 있습니다.  
  
-   사용 유형을 지정합니다.  
  
-   파일 또는 폴더를 지정합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 속성 창에 식을 지정하여 파일 연결 관리자에 대한 ConnectionString 속성을 설정할 수 있습니다. 그러나 식을 사용하여 파일 또는 폴더를 지정할 때 유효성 검사 오류가 발생하지 않도록 하려면 **파일 연결 관리자 편집기**에서 **파일/폴더**에 대해 파일 또는 폴더 경로를 추가합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [파일 연결 관리자 편집기](../../integration-services/connection-manager/file-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="file-connection-manager-editor"></a>파일 연결 관리자 편집기
  **파일 연결 관리자 편집기** 대화 상자를 사용하여 파일이나 폴더에 연결할 때 사용할 속성을 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 속성 창에 식을 지정하여 파일 연결 관리자에 대한 ConnectionString 속성을 설정할 수 있습니다. 그러나 식을 사용하여 파일 또는 폴더를 지정할 때 유효성 검사 오류가 발생하지 않도록 하려면 **파일 연결 관리자 편집기**에서 **파일/폴더**에 대해 파일 또는 폴더 경로를 추가합니다.  
  
 파일 연결 관리자에 대한 자세한 내용은 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>변수  
 **사용 유형**  
 **파일 연결 관리자** 가 기존 파일 또는 폴더에 연결하는지 또는 새 파일 또는 폴더에 연결하는지 여부를 지정합니다.  
  
|값|설명|  
|-----------|-----------------|  
|파일 만들기|런타임에 새 파일을 만듭니다.|  
|기존 파일|기존 파일을 사용합니다.|  
|폴더 만들기|런타임에 새 폴더를 만듭니다.|  
|기존 폴더|기존 폴더를 사용합니다.|  
  
 **파일/폴더**  
 **파일**을 선택한 경우 사용할 파일을 지정합니다.  
  
 **폴더**를 선택한 경우 사용할 폴더를 지정합니다.  
  
 **찾아보기**  
 **파일 선택** 이나 **폴더 찾아보기** 대화 상자를 사용하여 파일이나 폴더를 선택합니다.  
  
  
