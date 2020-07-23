---
title: 캐시 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.cacheconnection.f1
helpviewer_keywords:
- Cache connection manager
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 21cc4725f69d35043734da6d9210bac0a6b65e4d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920829"
---
# <a name="cache-connection-manager"></a>캐시 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  캐시 연결 관리자는 캐시 변환이나 캐시 파일(.caw)에서 데이터를 읽고 이를 캐시 파일에 저장할 수 있습니다. 캐시 연결 관리자가 캐시 파일을 사용하도록 구성했는지 여부에 관계없이 데이터는 항상 메모리에 저장됩니다.  
  
 캐시 변환은 데이터 흐름에 있는 연결된 데이터 원본의 데이터를 캐시 연결 관리자에 기록합니다. 패키지의 조회 변환은 데이터에 대해 조회를 수행합니다.  
  
> [!NOTE]  
>  캐시 연결 관리자는 BLOB(Binary Large Object) 데이터 형식 DT_TEXT, DT_NTEXT 및 DT_IMAGE를 지원하지 않습니다. 참조 데이터 세트에 BLOB 데이터 형식이 있으면 패키지를 실행할 때 구성 요소가 실패합니다. **캐시 연결 관리자 편집기** 를 사용하여 열 데이터 형식을 수정할 수 있습니다. 자세한 내용은 [Cache Connection Manager Editor](cache-connection-manager-editor.md)을 참조하세요.  
  
> [!NOTE]  
>  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
## <a name="configuration-of-the-cache-connection-manager"></a>캐시 연결 관리자 구성  
 다음과 같은 방법으로 캐시 연결 관리자를 구성할 수 있습니다.  
  
-   캐시 파일을 사용할지 여부를 나타냅니다.  
  
     캐시 파일을 사용하도록 캐시 연결 관리자를 구성하면 연결 관리자는 다음 동작 중 하나를 수행합니다.  
  
    -   캐시 변환이 데이터 흐름에 있는 데이터 원본의 데이터를 캐시 연결 관리자에 기록하도록 구성된 경우 데이터를 파일에 저장합니다.  
  
    -   캐시 파일에서 데이터를 읽습니다.  
  
     자세한 내용은 [Cache Transform](../../integration-services/data-flow/transformations/cache-transform.md)을 참조하세요.  
  
-   캐시에 저장된 열의 메타데이터를 변경합니다.  
  
-   런타임에 ConnectionString 속성을 설정하는 식을 사용하여 캐시 파일 이름을 업데이트합니다. 자세한 내용은 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)를 참조하세요.  
  
## <a name="cache-connection-manager-editor"></a>캐시 연결 관리자 편집기
  캐시 연결 관리자는 캐시 변환이나 캐시 파일(.caw)에서 참조 데이터 세트를 읽고 데이터를 캐시 파일에 저장할 수 있습니다. 데이터는 항상 메모리에 저장됩니다.  
  
> [!NOTE]  
>  캐시 연결 관리자는 BLOB(Binary Large Object) 데이터 형식 DT_TEXT, DT_NTEXT 및 DT_IMAGE를 지원하지 않습니다. 참조 데이터 세트에 BLOB 데이터 형식이 있으면 패키지를 실행할 때 구성 요소가 실패합니다. **캐시 연결 관리자 편집기** 를 사용하여 열 데이터 형식을 수정할 수 있습니다.  
  
 조회 변환은 참조 데이터 세트에 대해 조회를 수행합니다.  
  
 **캐시 연결 관리자 편집기** 대화 상자에는 다음과 같은 탭이 있습니다.  
  
###  <a name="general-tab"></a><a name="generaltab"></a> 일반 탭  
 **캐시 연결 관리자 편집기** 대화 상자의 **일반** 탭을 사용하여 파일에서 캐시를 읽을지 아니면 파일에 캐시를 저장할지 여부를 나타낼 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **연결 관리자 이름**  
 워크플로의 캐시 연결에 고유한 이름을 지정합니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **설명**  
 연결에 대한 설명을 입력합니다. 해당 연결의 용도를 설명하여 패키지를 이해하기 쉽고 유지 관리하기 편하도록 만드는 것이 가장 좋습니다.  
  
 **파일 캐시 사용**  
 캐시 파일을 사용할지 여부를 나타냅니다.  
  
> [!NOTE]  
>  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
 캐시 파일을 사용하도록 캐시 연결 관리자를 구성하면 연결 관리자는 다음 동작 중 하나를 수행합니다.  
  
-   캐시 변환이 데이터 흐름에 있는 데이터 원본의 데이터를 캐시 연결 관리자에 기록하도록 구성된 경우 데이터를 파일에 저장합니다. 자세한 내용은 [Cache Transform](../../integration-services/data-flow/transformations/cache-transform.md)을 참조하세요.  
  
-   캐시 파일에서 데이터를 읽습니다.  
  
 **파일 이름**  
 캐시 파일의 경로와 파일 이름을 입력합니다.  
  
 **찾아보기**  
 캐시 파일을 찾습니다.  
  
 **메타데이터 새로 고침**  
 캐시 연결 관리자에서 열 메타데이터를 삭제하고 선택한 캐시 파일의 열 메타데이터로 캐시 연결 관리자를 채웁니다.  
  
###  <a name="columns-tab"></a><a name="columnstab"></a> 열 탭  
 **캐시 연결 관리자 편집기** 대화 상자의 **열** 탭을 사용하여 캐시에 있는 각 열의 속성을 구성할 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **열**  
 열 이름을 지정합니다.  
  
 **인덱스 위치**  
 각 열의 인덱스 위치를 지정하여 인덱스 열이 되는 열을 지정합니다. 인덱스는 하나 이상의 열로 이루어집니다.  
  
 비인덱스 열의 경우 인덱스 위치는 0입니다.  
  
 인덱스 열의 경우 인덱스 위치는 일련의 양수입니다. 이 번호는 조회 변환이 참조 데이터 세트의 행을 입력 데이터 원본의 행과 비교하는 순서를 나타냅니다. 가장 고유한 값을 포함하는 열의 인덱스 위치는 가장 낮아야 합니다.  
  
> [!NOTE]  
>  조회 변환은 캐시 연결 관리자를 사용하도록 구성된 경우 참조 데이터 세트의 인덱스 열만 입력 열에 매핑할 수 있습니다. 또한 모든 인덱스 열을 매핑해야 합니다.  
  
 **형식**  
 열의 데이터 형식을 지정합니다.  
  
 **길이**  
 열 데이터 형식을 지정합니다. 데이터 형식에 적용 가능한 경우 **Length**를 업데이트할 수 있습니다.  
  
 **정밀도**  
 특정 열 데이터 형식에 대한 전체 자릿수를 지정합니다. 전체 자릿수는 숫자의 모든 자릿수이고 데이터 형식에 적용 가능한 경우 **Precision**를 업데이트할 수 있습니다.  
  
 **규모**  
 특정 열 데이터 형식에 대한 소수 자릿수를 지정합니다. 소수 자릿수는 숫자에서 소수점 오른쪽에 있는 자릿수입니다. 데이터 형식에 적용 가능한 경우 **Scale**를 업데이트할 수 있습니다.  
  
 **코드 페이지**  
 열 형식에 대한 코드 페이지를 지정합니다. 데이터 형식에 적용 가능한 경우 **Code Page**를 업데이트할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [캐시 연결 관리자 변환을 사용하여 전체 캐시 모드에서 조회 변환 구현](lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
  
