---
title: OLE DB 대상 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdestadapter.connection.f1
helpviewer_keywords:
- OLE DB Destination Editor
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 436b758abdde0c05539bc17aabd2c11b240642df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057142"
---
# <a name="ole-db-destination-editor-connection-manager-page"></a>OLE DB 대상 편집기(연결 관리자 페이지)
  **OLE DB 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 대상에 대한 OLE DB 연결을 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
> [!NOTE]  
>  `CommandTimeout` OLE DB 대상의 속성을 사용할 수 없습니다는 **OLE DB 대상 편집기**를 사용 하 여 설정할 수 있습니다 합니다 **고급 편집기**합니다. 또한 특정 빠른 로드 옵션은 **고급 편집기**에서만 사용할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md)의 OLE DB 대상 섹션을 참조하십시오.  
  
 OLE DB 대상에 대한 자세한 내용은 [OLE DB Destination](data-flow/ole-db-destination.md)을 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **캐시 없음**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 대상으로 데이터를 로드하는 방법을 지정합니다. DBCS(더블바이트 문자 집합) 데이터는 빠른 로드 옵션 중 하나를 사용하여 로드해야 합니다. 대량 삽입에 최적화된 빠른 로드 데이터 액세스 모드에 대한 자세한 내용은 [OLE DB Destination](data-flow/ole-db-destination.md)을 참조하십시오.  
  
|옵션|Description|  
|------------|-----------------|  
|테이블 또는 뷰|OLE DB 대상의 테이블 또는 뷰로 데이터를 로드합니다.|  
|테이블 또는 뷰 - 빠른 로드|빠른 로드 옵션을 사용하여 OLE DB 대상의 테이블 또는 뷰로 데이터를 로드합니다. 대량 삽입에 최적화된 빠른 로드 데이터 액세스 모드에 대한 자세한 내용은 [OLE DB Destination](data-flow/ole-db-destination.md)을 참조하십시오.|  
|테이블 이름 또는 뷰 이름 변수|변수에 테이블 또는 뷰 이름을 지정합니다.<br /><br /> **관련 정보**: [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)|  
|테이블 이름 또는 뷰 이름 변수 - 빠른 로드|변수에 테이블 이름 또는 뷰 이름을 지정하고 빠른 로드 옵션을 사용하여 데이터를 로드합니다. 대량 삽입에 최적화된 빠른 로드 데이터 액세스 모드에 대한 자세한 내용은 [OLE DB Destination](data-flow/ole-db-destination.md)을 참조하십시오.|  
|SQL 명령|SQL 쿼리를 사용하여 OLE DB 대상으로 데이터를 로드합니다.|  
  
 **미리 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
## <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
 각 **데이터 액세스 모드** 설정은 해당 설정에 따라 동적 옵션 집합이 표시됩니다. 다음 섹션에서는 각 **데이터 액세스 모드** 설정에 따라 사용할 수 있는 동적 옵션에 대해 설명합니다.  
  
### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **테이블 또는 뷰 이름**  
 데이터 원본의 사용 가능한 테이블 또는 뷰 목록에서 테이블 또는 뷰 이름을 선택합니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기**를 클릭하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 스토리지를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
### <a name="data-access-mode--table-or-view---fast-load"></a>데이터 액세스 모드 = 테이블 또는 뷰 - 빠른 로드  
 **테이블 또는 뷰 이름**  
 이 목록을 사용하여 데이터베이스에서 테이블 또는 뷰를 선택하거나 **새로 만들기**를 클릭하여 새 테이블을 만듭니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기**를 클릭하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 스토리지를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
 **ID 유지**  
 데이터를 로드할 때 ID 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 `false`입니다.  
  
 **Null 유지**  
 데이터를 로드할 때 Null 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 `false`입니다.  
  
 **테이블 잠금**  
 로드하는 동안 테이블 잠금을 설정할지 여부를 지정합니다. 이 속성의 기본값은 `true`입니다.  
  
 **CHECK 제약 조건**  
 대상에서 데이터를 로드할 때 제약 조건을 검사할지 여부를 지정합니다. 이 속성의 기본값은 `true`입니다.  
  
 **일괄 처리당 행 수**  
 일괄 처리의 행 수를 지정합니다. 이 속성의 기본값은 값이 할당되지 않음을 나타내는 **-1**입니다.  
  
> [!NOTE]  
>  이 속성에 사용자 지정 값을 할당하지 않으려면 **OLE DB 대상 편집기** 에서 해당 입력란의 내용을 지웁니다.  
  
 **최대 삽입 커밋 크기**  
 OLE DB 대상에서 빠른 로드 작업을 수행하는 동안 커밋을 시도하는 일괄 처리 크기를 지정합니다. 값이 **0** 이면 모든 행이 처리된 다음 모든 데이터가 단일 일괄 처리로 커밋됩니다.  
  
> [!NOTE]  
>  OLE DB 대상 및 다른 데이터 흐름 구성 요소에서 동일한 원본 테이블을 업데이트하는 경우 값 **0** 을 지정하면 실행 중인 패키지가 응답하지 않을 수 있습니다. 패키지가 중지하지 않도록 하려면 **최대 삽입 커밋 크기** 옵션을 **2147483647**로 설정합니다.  
  
 이 속성에 값을 지정하면 대상에서 (1) **최대 삽입 커밋 크기**보다 작은 일괄 처리의 행이나 (2) 현재 처리 중인 버퍼에 남아 있는 행이 커밋됩니다.  
  
> [!NOTE]  
>  대상에서 제약 조건에 맞지 않아 오류가 발생하면 **최대 삽입 커밋 크기** 에 의해 정의된 행에 대한 전체 일괄 처리가 실패하게 됩니다.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 테이블 또는 뷰 이름이 포함된 변수를 선택합니다.  
  
### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수 - 빠른 로드  
 **변수 이름**  
 테이블 또는 뷰 이름이 포함된 변수를 선택합니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기**를 클릭하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 스토리지를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
 **ID 유지**  
 데이터를 로드할 때 ID 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 `false`입니다.  
  
 **Null 유지**  
 데이터를 로드할 때 Null 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 `false`입니다.  
  
 **테이블 잠금**  
 로드하는 동안 테이블 잠금을 설정할지 여부를 지정합니다. 이 속성의 기본값은 `false`입니다.  
  
 **CHECK 제약 조건**  
 태스크에서 제약 조건을 검사할지 여부를 지정합니다. 이 속성의 기본값은 `false`입니다.  
  
 **일괄 처리당 행 수**  
 일괄 처리의 행 수를 지정합니다. 이 속성의 기본값은 값이 할당되지 않음을 나타내는 **-1**입니다.  
  
> [!NOTE]  
>  이 속성에 사용자 지정 값을 할당하지 않으려면 **OLE DB 대상 편집기** 에서 해당 입력란의 내용을 지웁니다.  
  
 **최대 삽입 커밋 크기**  
 OLE DB 대상에서 빠른 로드 작업을 수행하는 동안 커밋을 시도하는 일괄 처리 크기를 지정합니다. 기본값은 **2147483647** 이며 이 경우 모든 행이 처리된 다음 모든 데이터가 단일 일괄 처리로 커밋됩니다.  
  
> [!NOTE]  
>  OLE DB 대상 및 다른 데이터 흐름 구성 요소에서 동일한 원본 테이블을 업데이트하는 경우 값 **0** 을 지정하면 실행 중인 패키지가 응답하지 않을 수 있습니다. 패키지가 중지하지 않도록 하려면 **최대 삽입 커밋 크기** 옵션을 **2147483647**로 설정합니다.  
  
### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
> [!NOTE]  
>  OLE DB 대상은 매개 변수를 지원하지 않습니다. 매개 변수가 있는 INSERT 문을 실행해야 하는 경우 OLE DB 명령 변환을 사용하십시오. 자세한 내용은 [OLE DB Command Transformation](data-flow/transformations/ole-db-command-transformation.md)을 참조하세요.  
  
 **쿼리 작성**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
 **쿼리 구문 분석**  
 쿼리 텍스트의 구문을 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [OLE DB 대상 편집기&#40;매핑 페이지&#41;](../../2014/integration-services/ole-db-destination-editor-mappings-page.md)   
 [OLE DB 대상 편집기&#40;오류 출력 페이지&#41;](../../2014/integration-services/ole-db-destination-editor-error-output-page.md)   
 [OLE DB 대상을 사용하여 데이터 로드](data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  
