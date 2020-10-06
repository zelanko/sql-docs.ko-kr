---
description: 조회 변환 전체 캐시 모드 - OLE DB 연결 관리자
title: 조회 변환 전체 캐시 모드 - OLE DB 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation [Integration Services]
ms.assetid: c4150e1b-bdff-4f7a-af4c-3401c34def83
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 55a439be88d422130e8a511a5c1d2071ece7fc2c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91719783"
---
# <a name="lookup-transformation-full-cache-mode---ole-db-connection-manager"></a>조회 변환 전체 캐시 모드 - OLE DB 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  전체 캐시 모드와 OLE DB 연결 관리자를 사용하도록 조회 변환을 구성할 수 있습니다. 전체 캐시 모드에서는 조회 변환이 실행되기 전에 참조 데이터 세트가 캐시에 로드됩니다.  
  
 조회 변환은 연결된 데이터 원본의 입력 열에 있는 데이터를 참조 데이터 세트의 열과 조인하여 조회합니다. 자세한 내용은 [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md)을(를) 참조하세요.  
  
 OLE DB 연결 관리자를 사용하도록 조회 변환을 구성할 때 참조 데이터 세트를 생성할 테이블, 뷰 또는 SQL 쿼리를 선택합니다.  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-by-using-ole-db-connection-manager"></a>OLE DB 연결 관리자를 사용하여 전체 캐시 모드에서 조회 변환을 구현하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 열고 솔루션 탐색기에서 패키지를 두 번 클릭합니다.  
  
2.  **데이터 흐름** 탭의 **도구 상자**에서 조회 변환을 디자인 화면으로 끌어 옵니다.  
  
3.  원본이나 이전 변환에서 연결선을 조회 변환으로 끌어서 조회 변환을 데이터 흐름에 연결합니다.  
  
    > [!NOTE]  
    >  조회 변환이 빈 데이터 필드가 포함된 플랫 파일에 연결되면 이러한 조회 변환의 유효성을 검사하지 못할 수 있습니다. 변환의 유효성 검사 여부는 플랫 파일의 연결 관리자가 Null 값을 유지하도록 구성되었는지 여부에 따라 결정됩니다. 조회 변환의 유효성 검사가 수행되도록 하려면 **플랫 파일 원본 편집기**의 **연결 관리자 페이지**에서 **원본의 Null 값을 데이터 흐름의 Null 값으로 유지** 옵션을 선택합니다.  
  
4.  원본이나 이전 변환을 두 번 클릭하여 구성 요소를 구성합니다.  
  
5.  조회 변환을 두 번 클릭한 다음 **조회 변환 편집기**의 **일반** 페이지에서 **전체 캐시**를 선택합니다.  
  
6.  **연결 형식** 영역에서 **OLE DB 연결 관리자**를 선택합니다.  
  
7.  **일치하는 항목이 없는 행 처리 방법 지정** 목록에서 일치하는 항목이 없는 행에 대한 오류 처리 옵션을 선택합니다.  
  
8.  연결 페이지에서, **OLE DB 연결 관리자** 목록에서 연결 관리자를 선택하거나 **새로 만들기** 를 클릭하여 새 연결 관리자를 만듭니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
9. 다음 태스크 중 하나를 수행합니다.  
  
    -   **테이블 또는 뷰 사용**을 클릭한 다음 테이블이나 뷰를 선택하거나, **새로 만들기** 를 클릭하여 테이블이나 뷰를 만듭니다.  
  
         또는  
  
    -   **SQL 쿼리 결과 사용**을 클릭한 후 **SQL 명령** 창에서 쿼리를 작성하거나 **쿼리 작성** 을 클릭하여 **쿼리 작성기** 에서 제공하는 그래픽 도구를 사용하여 쿼리를 작성합니다.  
  
         또는  
  
    -   또는 **찾아보기** 를 클릭하여 파일에서 SQL 문을 가져옵니다.  
  
     SQL 쿼리의 유효성을 검사하려면 **쿼리 구문 분석**을 클릭합니다.  
  
     데이터 예제를 보려면 **미리 보기**를 클릭합니다.  
  
10. **열** 페이지를 클릭한 다음 **사용 가능한 입력 열** 목록에 있는 하나 이상의 열을 **사용 가능한 조회 열** 목록에 있는 열로 끌어 옵니다.  
  
    > [!NOTE]  
    >  조회 변환은 이름과 데이터 형식이 같은 열을 자동으로 매핑합니다.  
  
    > [!NOTE]  
    >  열을 매핑하려면 데이터 형식이 일치해야 합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
11. 다음 태스크를 수행하여 출력에 조회 열을 포함시킵니다.  
  
    1.  **사용 가능한 조회 열** 목록에서 열을 선택합니다.  
  
    2.  **조회 작업** 목록에서 조회 열의 값으로 입력 열의 값을 교체하거나 새 열에 기록할지 여부를 지정합니다.  
  
12. 오류 출력을 구성하려면 **오류 출력** 페이지를 클릭하고 오류 처리 옵션을 설정합니다. 자세한 내용은 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../data-flow/transformations/lookup-transformation.md)를 참조하세요.  
  
13. 조회 변환의 변경 내용을 저장한 다음 패키지를 실행하려면 **확인** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [캐시 연결 관리자 변환을 사용하여 전체 캐시 모드에서 조회 변환 구현](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)   
 [캐시 없음 또는 부분 캐시 모드로 조회 구현](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)   
 [Integration Services 변환](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
