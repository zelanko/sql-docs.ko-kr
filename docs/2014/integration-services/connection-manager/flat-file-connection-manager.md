---
title: 플랫 파일 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4466ebd24647520c7cbba2bf0baa93a0f60a72bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833823"
---
# <a name="flat-file-connection-manager"></a>Flat File Connection Manager
  플랫 파일 연결 관리자를 사용하면 패키지에서 플랫 파일의 데이터에 액세스할 수 있습니다. 예를 들어 플랫 파일 원본 및 대상은 플랫 파일 연결 관리자를 사용하여 데이터를 추출 및 로드할 수 있습니다.  
  
 플랫 파일 연결 관리자는 하나의 파일만 액세스할 수 있습니다. 파일을 여러 개 참조하려면 플랫 파일 연결 관리자 대신 다중 플랫 파일 연결 관리자를 사용하십시오. 자세한 내용은 [Multiple Flat Files Connection Manager](multiple-flat-files-connection-manager.md)을 참조하세요.  
  
## <a name="column-length"></a>열 길이  
 기본적으로 플랫 파일 연결 관리자는 문자열 열의 길이를 50자로 설정합니다. **플랫 파일 연결 관리자 편집기** 대화 상자에서 샘플 데이터를 평가하고 이러한 열의 길이를 자동으로 조정하여 데이터가 잘리지 않거나 열 너비를 초과하지 않도록 할 수 있습니다. 또한 플랫 파일 원본 또는 변환에서 열 길이를 나중에 조정하지 않는 한 문자열 열 길이가 데이터 흐름 전체에서 동일하게 유지됩니다. 이러한 문자열 열이 보다 좁은 대상 열에 매핑되면 사용자 인터페이스에 경고가 나타나고 런타임 시 데이터 잘림으로 인한 오류가 발생할 수 있습니다. 오류나 잘림이 발생하지 않도록 하기 위해 플랫 파일 연결 관리자, 플랫 파일 원본 또는 변환에서 대상 열과 호환 가능하도록 열 크기를 조정할 수 있습니다. 출력 열의 길이를 수정 하려면 `Length` **고급 편집기** 대화 상자의 **입/출력 속성** 탭에서 출력 열의 속성을 설정 합니다.  
  
 연결 관리자를 사용하는 플랫 파일 원본을 추가 및 구성한 후에 플랫 파일 연결 관리자에서 열 길이를 업데이트한 경우에는 플랫 파일 원본에서 출력 열의 크기를 수동으로 조정하지 않아도 됩니다. **플랫 파일 원본** 대화 상자를 열면 플랫 파일 원본에 열 메타데이터를 동기화하는 옵션이 제공됩니다.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>플랫 파일 연결 관리자 구성  
 패키지에 플랫 파일 연결 관리자를 추가 하면에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에 플랫 파일 연결로 확인 되는 연결 관리자를 만들고, 플랫 파일 연결 속성을 설정 하 고, 플랫 파일 연결 관리자를 패키지의 `Connections` 컬렉션에 추가 합니다.  
  
 연결 관리자의 `ConnectionManagerType` 속성이 `FLATFILE`로 설정됩니다.  
  
 기본적으로 플랫 파일 연결 관리자는 따옴표로 표시되지 않은 데이터에서 항상 행 구분자를 검사하고 행 구분자를 찾으면 새 행을 시작합니다. 그러면 연결 관리자가 열 필드가 누락된 행을 사용하여 파일을 올바르게 구문 분석할 수 있습니다.  
  
 일부 경우에는 이 기능을 비활성화해야 패키지 성능이 향상될 수 있습니다. 플랫 파일 연결 관리자 속성인 **AlwaysCheckForRowDelimiters**을로 `False`설정 하 여이 기능을 사용 하지 않도록 설정할 수 있습니다.  
  
 다음과 같은 방법으로 플랫 파일 연결 관리자를 구성할 수 있습니다.  
  
-   사용할 파일, 로캘 및 코드 페이지를 지정합니다. 로캘은 날짜 같은 로캘 구분 데이터를 해석하는 데 사용되고 코드 페이지는 문자열 데이터를 유니코드로 변환하는 데 사용됩니다.  
  
-   파일 형식을 지정합니다. 구분 기호로 분리된 형식, 고정 폭 형식 또는 왼쪽 정렬 형식을 사용할 수 있습니다.  
  
-   머리글 행, 데이터 행 및 열 구분 기호를 지정합니다. 열 구분 기호는 파일 수준에서 설정하고 열 수준에서 덮어쓸 수 있습니다.  
  
-   파일의 첫 번째 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
-   텍스트 한정자 문자를 지정합니다. 텍스트 한정자를 인식하도록 각 열을 구성할 수 있습니다.  
  
     한정자 문자를 사용하여 한정된 문자열에 한정자 문자를 포함하는 기능이 이제 지원됩니다. 텍스트 한정자가 두 번 나올 경우 해당 문자열이 한 번 나온 것처럼 리터럴로 해석됩니다. 예를 들어 텍스트 한정자가 작은따옴표이고 입력 데이터가 'abc', 'def', 'g'hi'인 경우 출력 데이터는 abc, def, g'hi입니다.  
  
-   개별 열에 대해 이름, 데이터 형식 및 최대 너비와 같은 속성을 설정합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 속성 창에 식을 지정하여 플랫 파일 연결 관리자에 대한 ConnectionString 속성을 설정할 수 있습니다. 유효성 검사 오류를 방지하려면 다음을 수행합니다.  
  
-   식을 사용해서 파일을 지정할 경우, **플랫 파일 연결 관리자 편집기** 의 **파일 이름**상자에 파일 경로를 추가합니다.  
  
-   플랫 파일 연결 관리자에서 **DelayValidation** 속성을 **True**로 설정합니다.  
  
 플랫 파일 연결 관리자에서 플랫 파일 대상에 식을 사용하여 런타임에 파일 이름을 만들 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
-   [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
-   [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
  
