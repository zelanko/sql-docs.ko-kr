---
title: 조회 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptrans.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d0dcebe1fa634678fa754b74be04d1dd5e1bcac5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298813"
---
# <a name="lookup-transformation"></a>조회 변환
  조회 변환은 입력 열의 데이터를 참조 데이터 집합의 열과 조인하여 조회합니다. 조회를 사용하면 공통 열의 값을 기반으로 하는 관련 테이블의 추가 정보에 액세스할 수 있습니다.  
  
 참조 데이터 집합은 캐시 파일, 기존 테이블이나 뷰, 새 테이블 또는 SQL 쿼리의 결과일 수 있습니다. 조회 변환은 OLE DB 연결 관리자 또는 캐시 연결 관리자를 사용하여 참조 데이터 집합에 연결합니다. 자세한 내용은 [OLE DB Connection Manager](../../connection-manager/ole-db-connection-manager.md) 및 [Cache Connection Manager](../../connection-manager/cache-connection-manager.md)을 참조하세요.  
  
 다음과 같은 방법으로 조회 변환을 구성할 수 있습니다.  
  
-   사용하려는 연결 관리자를 선택합니다. 데이터베이스에 연결하려면 OLE DB 연결 관리자를 선택합니다. 캐시 파일에 연결하려면 캐시 연결 관리자를 선택합니다.  
  
-   참조 데이터 집합이 포함된 테이블 또는 뷰를 지정합니다.  
  
-   SQL 문을 지정하여 참조 데이터 집합을 생성합니다.  
  
-   입력과 참조 데이터 집합 간의 조인을 지정합니다.  
  
-   참조 데이터 집합의 열을 조회 변환 출력에 추가합니다.  
  
-   캐싱 옵션을 구성합니다.  
  
 조회 변환은 OLE DB 연결 관리자에 대해 다음과 같은 데이터베이스 공급자를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 조회 변환은 변환 입력 값과 참조 데이터 집합 값 간에 동등 조인을 수행합니다. 동등 조인을 사용하는 경우 변환 입력의 각 행이 참조 데이터 집합의 행과 하나 이상 일치해야 합니다. 동등 조인을 사용할 수 없는 경우 조회 변환은 다음 동작 중 하나를 수행합니다.  
  
-   참조 데이터 집합에 일치하는 항목이 없으면 조인이 발생하지 않습니다. 기본적으로 조회 변환은 일치하는 항목이 없는 행을 오류로 간주합니다. 하지만 이러한 행을 불일치 항목 출력으로 리디렉션하도록 조회 변환을 구성할 수 있습니다. 자세한 내용은 [조회 변환 편집기&#40;일반 페이지&#41;](../../lookup-transformation-editor-general-page.md) 및 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../../lookup-transformation-editor-error-output-page.md)를 참조하세요.  
  
-   참조 테이블에 일치하는 항목이 여러 개 있을 경우 조회 변환은 조회 쿼리에서 반환된 첫 번째 일치 항목만 반환합니다. 일치하는 항목이 여러 개 발견되면 변환이 모든 참조 데이터 집합을 캐시에 로드하도록 구성된 경우에만 조회 변환에서 오류 또는 경고가 발생합니다. 이 경우 변환이 캐시를 채울 때 여러 개의 일치 항목이 발견되면 조회 변환에서 경고가 발생합니다.  
  
 복합 조인을 사용하면 변환 입력의 여러 열을 참조 데이터 집합의 열에 조인할 수 있습니다. 이 변환은 DT_R4, DT_R8, DT_TEXT, DT_NTEXT 또는 DT_IMAGE를 제외한 모든 데이터 형식의 조인 열을 지원합니다. 자세한 내용은 [Integration Services Data Types](../integration-services-data-types.md)을 참조하세요.  
  
 일반적으로 참조 데이터 집합의 값이 변환 출력에 추가됩니다. 예를 들어 조회 변환은 입력 열의 값을 사용하여 테이블에서 제품 이름을 추출한 다음 변환 출력에 제품 이름을 추가할 수 있습니다. 참조 테이블의 값은 열 값을 대체하거나 새 열에 추가될 수 있습니다.  
  
 조회 변환에서 수행하는 조회는 대/소문자를 구분합니다. 데이터의 대/소문자 차이로 인한 조회 오류를 방지하려면 먼저 문자표 변환을 사용하여 데이터를 대문자 또는 소문자로 변환합니다. 그런 다음 참조 테이블을 생성하는 SQL 문에 UPPER 또는 LOWER 함수를 포함시킵니다. 자세한 내용은 [문자표 변환](character-map-transformation.md), [UPPER&#40;Transact-SQL&#41;](/sql/t-sql/functions/upper-transact-sql) 및 [LOWER&#40;Transact-SQL&#41;](/sql/t-sql/functions/lower-transact-sql)를 참조하세요.  
  
 조회 변환에는 다음과 같은 입력 및 출력이 있습니다.  
  
-   입력.  
  
-   일치 항목 출력. 일치 항목 출력은 참조 데이터 집합과 하나 이상의 항목이 일치하는 변환 입력 행을 처리합니다.  
  
-   불일치 항목 출력. 불일치 항목 출력은 참조 데이터 집합과 하나의 항목도 일치하지 않는 입력 행을 처리합니다. 일치하는 항목이 없는 행을 오류로 처리하도록 조회 변환을 구성하면 해당 행이 오류 출력으로 리디렉션됩니다. 그렇지 않으면 변환이 이러한 행을 불일치 항목 출력으로 리디렉션합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]에서는 조회 변환에 하나의 출력만 제공합니다. 만든 조회 변환을 실행 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]를 참조 하세요 [조회 변환 업그레이드](../../../sql-server/install/upgrade-lookup-transformations.md)합니다.  
  
-   오류 출력.  
  
## <a name="caching-the-reference-dataset"></a>참조 데이터 집합 캐싱  
 메모리 내 캐시는 참조 데이터 집합과 이러한 데이터를 인덱싱하는 해시 테이블을 저장합니다. 캐시는 패키지 실행이 완료될 때까지 메모리에 남아 있습니다. 캐시를 캐시 파일(.caw)로 저장할 수 있습니다.  
  
 캐시를 파일로 저장하면 시스템에서 캐시를 더 빠르게 로드할 수 있습니다. 따라서 조회 변환 및 패키지의 성능도 향상됩니다. 캐시 파일을 사용할 때는 데이터베이스에 있는 현재 데이터가 아닌 다른 데이터를 사용하고 있다는 점을 유념하십시오.  
  
 캐시를 파일로 저장할 경우의 추가 이점은 다음과 같습니다.  
  
-   ***여러 패키지에서 캐시 파일을 공유합니다. 자세한 내용은 ***[캐시 연결 관리자 변환을 사용하여 전체 캐시 모드에서 조회 변환 구현](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)***을 참조하세요.***  
  
-   패키지와 함께 캐시 파일을 배포합니다. ***그러면 데이터를 여러 컴퓨터에서 사용할 수 있습니다.*** 자세한 내용은 [조회 변환에 대한 캐시 만들기 및 배포](create-and-deploy-a-cache-for-the-lookup-transformation.md)를 참조하세요.  
  
-   원시 파일 원본을 사용하여 캐시 파일에서 데이터를 읽습니다. 그러면 다른 데이터 흐름 구성 요소를 사용하여 데이터를 변환하거나 이동할 수 있습니다. 자세한 내용은 [Raw File Source](../raw-file-source.md)을 참조하세요.  
  
    > [!NOTE]  
    >  캐시 연결 관리자는 원시 파일 대상을 사용하여 캐시 파일을 만들거나 수정하도록 지원하지 않습니다.  
  
-   파일 시스템 태스크를 사용하여 캐시 파일에서 작업을 수행하고 특성을 설정합니다. 자세한 내용은 [File System Task](../../control-flow/file-system-task.md)를 참조하십시오.  
  
 캐싱 옵션은 다음과 같습니다.  
  
-   조회 변환이 실행되기 전에 테이블, 뷰 또는 SQL 쿼리를 사용하여 참조 데이터 집합이 생성되고 캐시에 로드됩니다. OLE DB 연결 관리자를 사용하여 데이터 집합에 액세스할 수 있습니다.  
  
     이 캐싱 옵션은 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]의 조회 변환에서 제공되는 전체 캐싱 옵션과 호환됩니다.  
  
-   조회 변환이 실행되기 전에 데이터 흐름의 연결된 데이터 원본 또는 캐시 파일로부터 참조 데이터 집합이 생성되고 캐시에 로드됩니다. 캐시 연결 관리자 및 캐시 변환(선택 사항)을 사용하여 데이터 집합에 액세스할 수 있습니다. 자세한 내용은 [Cache Connection Manager](../../connection-manager/cache-connection-manager.md) 및 [Cache Transform](cache-transform.md)를 참조하세요.  
  
-   조회 변환이 실행되는 동안 테이블, 뷰 또는 SQL 쿼리를 사용하여 참조 데이터 집합이 생성됩니다. 참조 데이터 집합과 일치하는 항목이 있는 행과 일치하는 항목이 없는 행이 캐시에 로드됩니다.  
  
     캐시의 메모리 크기를 초과하면 조회 변환은 자동으로 캐시에서 가장 사용 빈도가 낮은 행을 제거합니다.  
  
     이 캐싱 옵션은 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]의 조회 변환에서 제공되는 부분 캐싱 옵션과 호환됩니다.  
  
-   조회 변환이 실행되는 동안 테이블, 뷰 또는 SQL 쿼리를 사용하여 참조 데이터 집합이 생성됩니다. 캐시되는 데이터는 없습니다.  
  
     이 캐싱 옵션은 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]의 조회 변환에서 제공되는 캐싱 없음 옵션과 호환됩니다.  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 문자열 비교 방식에는 차이가 있습니다. 조회 변환이 실행되기 전에 참조 데이터 집합을 캐시로 로드하도록 조회 변환이 구성된 경우 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 는 캐시에서 조회 비교를 수행합니다. 그렇지 않으면 조회 작업에서 매개 변수가 있는 SQL 문을 사용하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 조회 비교를 수행합니다. 이는 캐시 유형에 따라 조회 변환이 동일한 조회 테이블에서 다른 개수의 일치하는 항목을 반환할 수 있다는 것을 의미합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [캐시 없음 또는 부분 캐시 모드로 조회 구현](implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [캐시 연결 관리자 변환을 사용하여 전체 캐시 모드에서 조회 변환 구현](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [OLE DB 연결 관리자를 사용하여 전체 캐시 모드에서 조회 변환 구현](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   msdn.microsoft.com의 비디오 - [방법: 전체 캐시 모드에서 조회 변환 구현](http://go.microsoft.com/fwlink/?LinkId=131031)  
  
-   blogs.msdn.com의 블로그 항목 - [조회 변환 캐시 모드를 사용하는 최선의 구현 방법(Best Practices for Using the Lookup Transformation Cache Modes)](http://go.microsoft.com/fwlink/?LinkId=146623)  
  
-   blogs.msdn.com의 블로그 항목 - [조회 패턴: 대/소문자 구분 안 함](http://go.microsoft.com/fwlink/?LinkId=157782)  
  
-   msftisprodsamples.codeplex.com의 예제 - [조회 변환](http://go.microsoft.com/fwlink/?LinkId=267528)  
  
     [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 제품 예제 및 예제 데이터베이스를 설치하는 방법은 [SQL Server Integration Services 제품 예제](http://go.microsoft.com/fwlink/?LinkId=267527)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [유사 항목 조회 변환](fuzzy-lookup-transformation.md)   
 [용어 조회 변환](term-lookup-transformation.md)   
 [데이터 흐름](../data-flow.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
