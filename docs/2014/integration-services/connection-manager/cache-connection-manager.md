---
title: 캐시 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Cache connection manager
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c0d3513446c930d41ef9163708e60ad063244479
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064283"
---
# <a name="cache-connection-manager"></a>캐시 연결 관리자
  캐시 연결 관리자는 캐시 변환이나 캐시 파일(.caw)에서 데이터를 읽고 이를 캐시 파일에 저장할 수 있습니다. 캐시 연결 관리자가 캐시 파일을 사용하도록 구성했는지 여부에 관계없이 데이터는 항상 메모리에 저장됩니다.  
  
 캐시 변환은 데이터 흐름에 있는 연결된 데이터 원본의 데이터를 캐시 연결 관리자에 기록합니다. 패키지의 조회 변환은 데이터에 대해 조회를 수행합니다.  
  
> [!NOTE]  
>  캐시 연결 관리자는 BLOB(Binary Large Object) 데이터 형식 DT_TEXT, DT_NTEXT 및 DT_IMAGE를 지원하지 않습니다. 참조 데이터 집합에 BLOB 데이터 형식이 있으면 패키지를 실행할 때 구성 요소가 실패합니다. **캐시 연결 관리자 편집기** 를 사용하여 열 데이터 형식을 수정할 수 있습니다. 자세한 내용은 [Cache Connection Manager Editor](../cache-connection-manager-editor.md)을 참조하세요.  
  
> [!NOTE]  
>  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../access-to-files-used-by-packages.md)를 참조하세요.  
  
## <a name="configuration-of-the-cache-connection-manager"></a>캐시 연결 관리자 구성  
 다음과 같은 방법으로 캐시 연결 관리자를 구성할 수 있습니다.  
  
-   캐시 파일을 사용할지 여부를 나타냅니다.  
  
     캐시 파일을 사용하도록 캐시 연결 관리자를 구성하면 연결 관리자는 다음 동작 중 하나를 수행합니다.  
  
    -   캐시 변환이 데이터 흐름에 있는 데이터 원본의 데이터를 캐시 연결 관리자에 기록하도록 구성된 경우 데이터를 파일에 저장합니다.  
  
    -   캐시 파일에서 데이터를 읽습니다.  
  
     자세한 내용은 [Cache Transform](../data-flow/transformations/cache-transform.md)을 참조하세요.  
  
-   캐시에 저장된 열의 메타데이터를 변경합니다.  
  
-   런타임에 ConnectionString 속성을 설정하는 식을 사용하여 캐시 파일 이름을 업데이트합니다. 자세한 내용은 [패키지에서 속성 식 사용](../expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [캐시 연결 관리자 편집기](../cache-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [캐시 연결 관리자 변환을 사용하여 전체 캐시 모드에서 조회 변환 구현](lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
  
