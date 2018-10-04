---
title: 쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a02dbe6174af6dbfefb472b7dddfb878fb569d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228773"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑
  매개 변수가 있는 쿼리를 사용하도록 OLE DB 원본을 구성할 경우 매개 변수를 변수에 매핑할 수 있습니다.  
  
 OLE DB 원본은 데이터 원본에 연결될 때 매개 변수가 있는 쿼리를 사용하여 데이터를 필터링합니다.  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>쿼리 매개 변수를 변수에 매핑하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 OLE DB 원본을 디자인 화면으로 끌어 옵니다.  
  
4.  OLE DB 원본을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
5.  **OLE DB 원본 편집기**에서 데이터 원본에 연결하는 데 사용할 OLE DB 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 OLE DB 연결 관리자를 만듭니다.  
  
6.  데이터 액세스 모드에 대해 **SQL 명령** 옵션을 선택한 다음 **SQL 명령 텍스트** 창에 매개 변수가 있는 쿼리를 입력합니다.  
  
7.  **매개 변수**를 클릭합니다.  
  
8.  **쿼리 매개 변수 설정** 대화 상자에서 **매개 변수** 목록의 각 매개 변수를 **변수** 목록의 변수에 매핑하거나 **\<새 변수>** 를 클릭하여 새 변수를 만듭니다. **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  패키지, Foreach 루프와 같은 부모 컨테이너 또는 데이터 흐름 구성 요소가 포함된 데이터 흐름 태스크의 범위에 속하는 사용자 정의 변수와 시스템 변수만 매핑에 사용할 수 있습니다. 변수는 매개 변수가 할당된 WHERE 절의 열과 호환되는 데이터 형식이어야 합니다.  
  
9. **미리 보기** 를 클릭하면 쿼리에서 반환되는 데이터 행을 최대 200개까지 표시할 수 있습니다.  
  
10. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 원본](ole-db-source.md)   
 [조회 변환](transformations/lookup-transformation.md)  
  
  
