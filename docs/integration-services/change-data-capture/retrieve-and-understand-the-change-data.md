---
title: 변경 데이터 검색 및 이해 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],retrieving data
ms.assetid: af366697-6942-42bb-aea5-18fdef018965
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 112c94119959410509bb2381b472c1fc0a6a66ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084345"
---
# <a name="retrieve-and-understand-the-change-data"></a>변경 데이터 검색 및 이해

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  변경 데이터를 증분 로드하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 첫 번째 태스크는 변경 데이터를 검색하는 쿼리를 실행하는 것입니다. 데이터 흐름 태스크의 원본 구성 요소 내에서 이 쿼리를 실행합니다. 그런 다음 다운스트림 변환 및 대상을 사용하여 대상에 변경 데이터를 적용할 수 있습니다.  
  
> [!NOTE]  
>  테이블 반환 함수를 포함하는 쿼리 생성 작업은 변경 데이터를 증분 로드하는 패키지 생성 프로세스의 세 번째 단계입니다. 이 쿼리에 대한 자세한 내용은 [변경 데이터 검색을 위한 함수 만들기](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)를 참조하세요. 변경 데이터를 증분 로드하는 패키지를 만드는 전체 프로세스에 대한 설명은 [변경 데이터 캡처&#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)를 참조하세요.  
  
## <a name="adding-the-data-flow-task"></a>데이터 흐름 태스크 추가  
 패키지의 데이터 흐름에서 변경 데이터를 검색하고 발생한 변경 내용 유형을 기반으로 행을 구분한 다음 대상에 변경 내용을 적용합니다.  
  
#### <a name="to-add-a-data-flow-task-to-the-package"></a>패키지에 데이터 흐름 태스크를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **제어 흐름** 탭에서 데이터 흐름 태스크를 추가합니다.  
  
2.  쿼리 문자열을 준비한 이전 태스크를 데이터 흐름 태스크에 연결합니다.  
  
## <a name="configuring-the-source-component-to-query-for-changes"></a>변경 내용을 쿼리하도록 원본 구성 요소 구성  
 원본 구성 요소는 변수에 준비되어 저장된 쿼리 문자열을 사용하여 변경된 데이터를 검색하는 테이블 반환 함수를 호출합니다.  
  
> [!NOTE]  
>  변수에 준비되어 저장된 쿼리 문자열에 대한 자세한 내용은 [변경 데이터에 대한 쿼리 준비](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)를 참조하세요. 변경 데이터를 검색하는 테이블 반환 함수에 대한 자세한 내용은 [변경 데이터 검색을 위한 함수 만들기](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)를 참조하세요.  
  
#### <a name="to-configure-an-ole-db-source-to-retrieve-the-change-data"></a>변경 데이터를 검색하도록 OLE DB 원본을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **데이터 흐름** 탭에서 OLE DB 원본을 추가합니다.  
  
2.  **OLE DB 원본 편집기**의 **연결 관리자** 페이지에서 다음 옵션을 선택합니다.  
  
    1.  원본 데이터베이스에 대한 올바른 연결을 구성합니다.  
  
    2.  **데이터 액세스 모드**에 **변수를 사용한 SQL 명령**을 선택합니다.  
  
    3.  **변수 이름**에 **User::SqlDataQuery**를 선택합니다.  
  
3.  **OLE DB 원본 편집기**의 **열** 페이지에서 원하는 모든 열이 출력 열에 매핑되어 있는지 확인합니다.  
  
## <a name="next-step"></a>다음 단계  
 변경 데이터를 검색하도록 OLE DB 원본을 구성한 후 다음 단계는 패키지의 데이터 흐름 디자인을 시작하는 것입니다.  
  
 **다음 항목:** [삽입, 업데이트 및 삭제 처리](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)  
  
  
