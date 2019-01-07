---
title: 조회 변환 편집기 (연결 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.referencetable.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: e90d6b69-5a26-43c5-8433-5c3c9588e08c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9ecacc7fa89256cf5efb42ee792a08251a9af013
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063713"
---
# <a name="lookup-transformation-editor-connection-page"></a>조회 변환 편집기(연결 페이지)
  **조회 변환 편집기** 대화 상자의 **연결** 페이지를 사용하여 연결 관리자를 선택할 수 있습니다. OLE DB 연결 관리자를 선택하면 쿼리, 테이블 또는 뷰를 선택하여 참조 데이터 세트를 생성할 수도 있습니다.  
  
 조회 변환에 대한 자세한 내용은 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **조회 변환 편집기** 대화 상자의 일반 페이지에서 **전체 캐시** 및 **캐시 연결 관리자** 를 선택하는 경우 다음 옵션을 사용할 수 있습니다.  
  
 **전체 캐시**  
 목록에서 기존 캐시 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **캐시 연결 관리자 편집기** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **조회 변환 편집기**대화 상자의 일반 페이지에서 **전체 캐시**, **부분 캐시**또는 **캐시 없음**및 **OLE DB 연결 관리자** 를 선택하는 경우 다음 옵션을 사용할 수 있습니다.  
  
 **캐시 없음**  
 목록에서 기존 OLE DB 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **테이블 또는 뷰 사용**  
 목록에서 기존 테이블 또는 뷰를 선택하거나 **새로 만들기**를 클릭하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **조회 변환 편집기** 의 **고급**페이지에서 SQL 문을 지정하는 경우 해당 SQL 문이 여기서 선택한 테이블 이름을 재정의하고 대체합니다. 자세한 내용은 [조회 변환 편집기 &#40;고급 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)합니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
 **SQL 쿼리 결과 사용**  
 기존 쿼리를 찾아보고 새 쿼리를 작성하고 쿼리 구문을 검사하고 쿼리 결과를 미리 보려면 선택합니다.  
  
 **쿼리 작성**  
 데이터를 찾아보는 방법으로 쿼리를 만드는 데 사용되는 그래픽 도구인 **쿼리 작성기**를 사용하여 실행할 Transact-SQL 문을 만듭니다.  
  
 **찾아보기**  
 파일로 저장된 기존 쿼리를 찾아보려면 이 옵션을 사용합니다.  
  
 **쿼리 구문 분석**  
 쿼리의 구문을 검사합니다.  
  
 **미리 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 이 옵션은 최대 200개의 행을 표시합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 blogs.msdn.com의 블로그 항목 - [조회 캐시 모드](http://go.microsoft.com/fwlink/?LinkId=219518)  
  
## <a name="see-also"></a>관련 항목  
 [조회 변환 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [조회 변환 편집기&#40;열 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [조회 변환 편집기 &#40;고급 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [조회 변환 편집기 &#40;오류 출력 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [유사 항목 조회 변환](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
