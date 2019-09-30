---
title: OLE DB 원본을 사용하여 데이터 추출 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: 4ca6eeb5-b60e-4b81-86dd-0674be8ae8d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 82bebe29ff6fe9eb385a078aa762d5b8f171783a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292603"
---
# <a name="extract-data-by-using-the-ole-db-source"></a>OLE DB 원본을 사용하여 데이터 추출

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 원본을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크가 이미 들어 있어야 합니다.  
  
### <a name="to-extract-data-using-an-ole-db-source"></a>OLE DB 원본을 사용하여 데이터를 추출하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 OLE DB 원본을 디자인 화면으로 끌어 옵니다.  
  
4.  OLE DB 원본을 두 번 클릭합니다.  
  
5.  **OLE DB 원본 편집기** 대화 상자의 **연결 관리자** 페이지에서 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
6.  다음과 같은 데이터 액세스 방법을 선택합니다.  
  
    -   **테이블 또는 뷰** OLE DB 연결 관리자에서 연결할 데이터베이스의 테이블 또는 뷰를 선택합니다.  
  
    -   **테이블 이름 또는 뷰 이름 변수** OLE DB 연결 관리자에서 연결할 데이터베이스의 테이블 또는 뷰의 이름이 포함된 사용자 정의 변수를 선택합니다.  
  
    -   **SQL 명령** SQL 명령을 입력하거나 **쿼리 작성** 을 클릭하여 **쿼리 작성기**를 사용하여 SQL 명령을 작성합니다.  
  
        > [!NOTE]  
        >  명령에는 매개 변수가 포함될 수 있습니다. 자세한 내용은 [쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)을 참조하세요.  
  
    -   **변수를 사용한 SQL 명령** SQL 명령이 포함된 사용자 정의 변수를 선택합니다.  
  
        > [!NOTE]  
        >  OLE DB 원본이 포함된 동일 데이터 흐름 태스크의 범위나 동일 패키지 범위에 변수가 정의되어 있어야 하며, 변수에는 문자열 데이터 형식이 들어 있어야 합니다.  
  
7.  외부 및 출력 열 사이의 매핑을 업데이트하려면 **열** 을 클릭하고 **외부 열** 목록에서 다른 열을 선택합니다.  
  
8.  필요에 따라 **출력 열** 목록에서 값을 편집하여 출력 열의 이름을 업데이트합니다.  
  
9. 오류 출력을 구성하려면 **오류 출력**을 클릭합니다. 자세한 내용은 [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md)을 참조하세요.  
  
10. **미리 보기** 를 클릭하면 OLE DB 원본에서 추출된 최대 200개의 데이터 행을 볼 수 있습니다.  
  
11. **확인**을 클릭합니다.  
  
12. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [OLE DB 원본](../../integration-services/data-flow/ole-db-source.md)   
 [Integration Services 변환](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](../../integration-services/data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](../../integration-services/control-flow/data-flow-task.md)  
  
  
