---
title: "OLE DB 대상을 사용하여 데이터 로드 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- loading data
- OLE DB destination [Integration Services]
- destinations [Integration Services], OLE DB
ms.assetid: 78899498-725e-4300-a7af-f983f4ea384b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 692bc6f90cee09f2bff680fe3e19ed3c433f8707
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="load-data-by-using-the-ole-db-destination"></a>OLE DB 대상을 사용하여 데이터 로드
  OLE DB 대상을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 원본이 이미 들어 있어야 합니다.  
  
### <a name="to-load-data-using-an-ole-db-destination"></a>OLE DB 대상을 사용하여 데이터를 로드하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 OLE DB 대상을 디자인 화면으로 끌어 옵니다.  
  
4.  데이터 원본 또는 이전 변환에서 연결선을 대상으로 끌어 와서 OLE DB 대상을 데이터 흐름에 연결합니다.  
  
5.  OLE DB 대상을 두 번 클릭합니다.  
  
6.  **OLE DB 대상 편집기** 대화 상자의 **연결 관리자** 페이지에서 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)을 참조하세요.  
  
7.  다음과 같은 데이터 액세스 방법을 선택합니다.  
  
    -   **테이블 또는 뷰** 데이터베이스에서 데이터가 포함된 테이블 또는 뷰를 선택합니다.  
  
    -   **테이블 또는 뷰 - 빠른 로드** 데이터베이스에서 데이터가 포함된 테이블 또는 뷰를 선택한 후에 **ID 유지**, **Null 유지**, **테이블 잠금**, **CHECK 제약 조건**, **일괄 처리당 행 수**또는 **최대 삽입 커밋 크기**중에서 빠른 로드 옵션을 설정합니다.  
  
    -   **테이블 이름 또는 뷰 이름 변수** 데이터베이스의 테이블 또는 뷰 이름이 포함된 사용자 정의 변수를 선택합니다.  
  
    -   **테이블 이름 또는 뷰 이름 변수 - 빠른 로드** 데이터베이스에서 데이터가 포함된 테이블 또는 뷰의 이름이 포함된 사용자 정의 변수를 선택한 후 빠른 로드 옵션을 설정합니다.  
  
    -   **SQL 명령** SQL 명령을 입력하거나 **쿼리 작성** 을 클릭하고 **쿼리 작성기**를 사용하여 SQL 명령을 작성합니다.  
  
8.  **매핑** 을 클릭한 후 **사용 가능한 입력 열** 목록의 열을 **사용 가능한 대상 열** 목록의 열로 끌어서 매핑합니다.  
  
    > [!NOTE]  
    >  OLE DB 대상은 같은 이름의 열로 자동으로 매핑됩니다.  
  
9. 오류 출력을 구성하려면 **오류 출력**을 클릭합니다. 자세한 내용은 [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md)을 참조하세요.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [OLE DB 대상](../../integration-services/data-flow/ole-db-destination.md)   
 [Integration Services 변환](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](../../integration-services/data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](../../integration-services/control-flow/data-flow-task.md)  
  
  
