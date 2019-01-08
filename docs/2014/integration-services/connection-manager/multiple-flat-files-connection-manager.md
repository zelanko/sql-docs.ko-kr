---
title: 다중 플랫 파일 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 575bf85a81557e7a0a974dd1fc2210e58f34bde0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790535"
---
# <a name="multiple-flat-files-connection-manager"></a>다중 플랫 파일 연결 관리자
  다중 플랫 파일 연결 관리자를 사용하면 패키지에서 다중 플랫 파일의 데이터에 액세스할 수 있습니다. 예를 들어 데이터 흐름 태스크가 For 루프 컨테이너와 같은 루프 컨테이너 내부에 있는 경우 플랫 파일 원본에서 다중 플랫 파일 연결 관리자를 사용할 수 있습니다. 각 컨테이너 루프에서 플랫 파일 원본은 다중 플랫 파일 연결 관리자가 제공하는 다음 파일 이름에서 데이터를 로드합니다.  
  
 패키지에 다중 플랫 파일 연결 관리자를 추가 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결 집합의 다중 플랫 파일 연결 관리자 속성을 런타임에 다중 플랫 파일 연결으로 확인 되는 관리자를 만들고 및 다중 플랫 파일 연결 관리자를 추가 합니다 `Connections` 패키지의 컬렉션입니다.  
  
 연결 관리자의 `ConnectionManagerType` 속성이 `MULTIFLATFILE`로 설정됩니다.  
  
 다음과 같은 방법으로 다중 플랫 파일 연결 관리자를 구성할 수 있습니다.  
  
-   사용할 파일, 로캘 및 코드 페이지를 지정합니다. 로캘은 날짜 같은 로캘 구분 데이터를 해석하는 데 사용되고 코드 페이지는 문자열 데이터를 유니코드로 변환하는 데 사용됩니다.  
  
-   파일 형식을 지정합니다. 구분 기호로 분리된 형식, 고정 폭 형식 또는 왼쪽 정렬 형식을 사용할 수 있습니다.  
  
-   머리글 행, 데이터 행 및 열 구분 기호를 지정합니다. 열 구분 기호는 파일 수준에서 설정하고 열 수준에서 덮어쓸 수 있습니다.  
  
-   파일의 첫 번째 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
-   텍스트 한정자 문자를 지정합니다. 텍스트 한정자를 인식하도록 각 열을 구성할 수 있습니다.  
  
-   개별 열에 대해 이름, 데이터 형식 및 최대 너비와 같은 속성을 설정합니다.  
  
 다중 플랫 파일 연결 관리자에서 다중 파일을 참조하는 경우 파일의 경로는 세로줄 문자(|)로 구분됩니다. 연결 관리자의 `ConnectionString` 속성은 다음 형식을 갖습니다.  
  
 \<*경로*>|\<*경로*>  
  
 또한 와일드카드 문자를 사용하여 다중 파일을 지정할 수 있습니다. 예를 들어, C의 모든 텍스트 파일을 드라이브의 값을 참조 하려면 합니다 `ConnectionString` c:로 속성을 설정할 수 있습니다\\*.txt.  
  
 다중 플랫 파일 연결 관리자에서 다중 파일을 참조하는 경우 모든 파일은 형식이 동일해야 합니다.  
  
 기본적으로 다중 플랫 파일 연결 관리자는 문자열 길이를 50자로 설정합니다. **다중 플랫 파일 연결 관리자 편집기** 대화 상자에서 예제 데이터를 평가하고 이러한 열의 길이를 자동으로 조정하여 데이터가 잘리지 않거나 열 너비를 초과하지 않도록 할 수 있습니다. 플랫 파일 원본 또는 변환에서 열 길이를 조정하지 않으면 열 길이가 데이터 흐름 전체에서 동일하게 유지됩니다. 이러한 열이 보다 좁은 대상 열에 매핑되면 사용자 인터페이스에 경고가 나타나며 런타임 시 데이터 잘림으로 인한 오류가 발생할 수 있습니다. 플랫 파일 연결 관리자, 플랫 파일 원본 또는 변환에서 대상 열과 호환 가능하도록 열 크기를 조정할 수 있습니다. 설정한 출력 열의 길이 수정 하려면 합니다 `Length` 에서 출력 열의 속성을 **입 / 출력 속성** 탭에서 **고급 편집기** 대화 상자.  
  
 연결 관리자를 사용하는 플랫 파일 원본을 추가 및 구성한 후에 다중 플랫 파일 연결 관리자에서 열 길이를 업데이트한 경우에는 플랫 파일 원본에서 출력 열의 크기를 수동으로 조정하지 않아도 됩니다. **플랫 파일 원본** 대화 상자를 열면 플랫 파일 원본에 열 메타데이터를 동기화하는 옵션이 제공됩니다.  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>다중 플랫 파일 연결 관리자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [다중 플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [다중 플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [다중 플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [다중 플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [플랫 파일 원본](../data-flow/flat-file-source.md)   
 [플랫 파일 대상](../data-flow/flat-file-destination.md)   
 [Integration Services&#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
