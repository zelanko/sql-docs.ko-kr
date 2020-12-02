---
description: SQL Server 대상
title: SQL Server 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlserverdest.f1
- sql13.dts.designer.sqlserverdestadapter.connection.f1
- sql13.dts.designer.sqlserverdestadapter.mappings.f1
- sql13.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2e7bc60bcfd7578d70528d92ef025370c28134e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194757"
---
# <a name="sql-server-destination"></a>SQL Server 대상

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  SQL Server 대상은 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 및 뷰로 데이터를 대량 로드합니다. 원격 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 액세스하는 패키지에서는 SQL Server 대상을 사용할 수 없습니다. 이러한 패키지에서는 대신 OLE DB 대상을 사용해야 합니다. 자세한 내용은 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 SQL Server 대상이 포함된 패키지를 실행하는 사용자는 "전역 개체 만들기" 권한이 있어야 합니다. **관리 도구** 메뉴에서 연 로컬 보안 정책 도구를 사용하여 사용자에게 이 사용 권한을 부여할 수 있습니다. SQL Server 대상을 사용하는 패키지를 실행할 때 오류 메시지가 표시되면 패키지를 실행 중인 계정에 "전역 개체 만들기" 권한이 있는지 확인합니다.  
  
## <a name="bulk-inserts"></a>대량 삽입  
 SQL Server 대상을 사용하여 원격 SQL Server 데이터베이스에 데이터를 대량으로 로드하려고 하면 "OLE DB 레코드를 사용할 수 있습니다. 원본: "Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 설명: "SSIS 파일 매핑 개체 'Global\DTSQLIMPORT'을(를) 열 수 없으므로 대량 로드할 수 없습니다. 운영 체제 오류 코드 2(시스템에서 지정한 파일을 찾을 수 없습니다.)입니다. Windows 보안을 통해 로컬 서버에 액세스하고 있는지 확인하십시오.""와 유사한 오류 메시지가 나타납니다.  
  
 SQL Server 대상은 대량 삽입 태스크가 제공하는 것과 동일하게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 고속 데이터 삽입 기능을 제공하지만 SQL Server 대상을 사용하면 데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 로드되기 전에 패키지에서 열 데이터에 변환을 적용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터를 로드하려면 OLE DB 대상 대신 SQL Server 대상을 사용하는 것이 좋습니다.  
  
### <a name="bulk-insert-options"></a>대량 삽입 옵션  
 SQL Server 대상이 빠른 로드 데이터 액세스 모드를 사용할 경우 다음과 같은 빠른 로드 옵션을 지정할 수 있습니다.  
  
-   가져온 데이터 파일에서 ID 값을 유지하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 할당된 고유 값을 사용합니다.  
  
-   대량 로드 작업 중에 발생한 Null 값을 유지합니다.  
  
-   대량 가져오기 작업 중에 대상 테이블 또는 뷰의 제약 조건을 검사합니다.  
  
-   대량 로드 작업이 지속되는 동안 테이블 수준 잠금을 획득합니다.  
  
-   대량 로드 작업 중에 대상 테이블에 정의된 삽입 트리거를 실행합니다.  
  
-   대량 삽입 작업 중에 입력에서 로드할 첫 번째 행의 번호를 지정합니다.  
  
-   대량 삽입 작업 중에 입력에서 로드할 마지막 행의 번호를 지정합니다.  
  
-   대량 삽입 작업을 취소하기 전에 허용되는 최대 오류 개수를 지정합니다. 가져올 수 없는 행은 각각 하나의 오류로 카운트됩니다.  
  
-   입력에서 정렬된 데이터가 포함된 열을 지정합니다.  
  
 대량 로드 옵션에 대한 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
#### <a name="performance-improvements"></a>성능 향상  
 대량 삽입의 성능과 대량 삽입 작업 중의 테이블 액세스를 향상시키려면 기본 옵션을 다음과 같이 변경해야 합니다.  
  
-   대량 가져오기 작업 중에 대상 테이블 또는 뷰의 제약 조건을 검사하지 마십시오.  
  
-   대량 로드 작업 중에 대상 테이블에서 정의된 삽입 트리거를 실행하지 마십시오.  
  
-   테이블에 잠금을 적용하지 마십시오. 이렇게 하면 대량 삽입 작업 중에 다른 사용자 및 애플리케이션이 테이블을 사용할 수 있습니다.  
  
## <a name="configuration-of-the-sql-server-destination"></a>SQL Server 대상 구성  
 다음과 같은 방법으로 SQL Server 대상을 구성할 수 있습니다.  
  
-   데이터를 대량 로드할 테이블 또는 뷰를 지정합니다.  
  
-   제약 조건 검사 여부와 같은 옵션을 지정하여 대량 로드 작업을 사용자 지정합니다.  
  
-   한 일괄 처리의 모든 행을 커밋할지 지정하거나 한 일괄 처리로 커밋할 행의 최대 수를 설정합니다.  
  
-   대량 로드 작업에 대한 제한 시간을 지정합니다.  
  
 이 대상은 OLE DB 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자가 사용할 OLE DB Provider를 지정합니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트는 또한 OLE DB 연결 관리자를 만들 수 있는 데이터 원본 개체를 제공합니다. 그러면 SQL Server 대상에서 데이터 원본과 데이터 원본 뷰를 사용할 수 있습니다.  
  
 SQL Server 대상은 하나의 입력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
-   [SQL Server 대상 사용자 지정 속성](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [SQL Server 대상을 사용하여 데이터 대량 로드](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [SQL Server 대상을 사용하여 데이터 대량 로드](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   support.microsoft.com의 기술 문서 - [UAC 사용 시스템에서 "데이터 삽입을 위해 SSIS 대량 삽입을 준비할 수 없습니다." 오류가 발생할 수 있습니다.](https://go.microsoft.com/fwlink/?LinkId=199482)  
  
-   msdn.microsoft.com의 기술 문서 - [데이터 로드 성능 가이드](/previous-versions/sql/sql-server-2008/dd425070(v=sql.100))  
  
-   simple-talk.com의 기술 문서, [SQL Server Integration Services를 사용하여 데이터 대량 로드](https://go.microsoft.com/fwlink/?LinkId=233701)  
  
## <a name="sql-destination-editor-connection-manager-page"></a>SQL 대상 편집기(연결 관리자 페이지)
  **SQL 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 데이터 원본 정보를 지정하고 결과를 미리 볼 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블이나 뷰로 데이터를 로드합니다.  
  
### <a name="options"></a>옵션  
 **캐시 없음**  
 목록에서 기존 연결을 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **테이블 또는 뷰 사용**  
 목록에서 기존 테이블 또는 뷰를 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기** 를 클릭하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 스토리지를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
 **미리 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
## <a name="sql-destination-editor-mappings-page"></a>SQL 대상 편집기(매핑 페이지)
  **SQL 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 입력 열을 대상 열에 매핑합니다.  
  
 **사용 가능한 대상 열**  
 사용 가능한 대상 열의 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 대상 열을 입력 열에 매핑합니다.  
  
 **입력 열**  
 위 테이블에서 선택한 입력 열을 표시합니다. **사용 가능한 입력 열** 의 목록을 사용하여 매핑을 변경할 수 있습니다.  
  
 **대상 열**  
 매핑 여부에 관계없이 사용 가능한 각 대상 열을 표시합니다.  
  
## <a name="sql-destination-editor-advanced-page"></a>SQL 대상 편집기(고급 페이지)
  **SQL 대상 편집기** 대화 상자의 **고급** 페이지를 사용하여 고급 대량 삽입 옵션을 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **ID 유지**  
 태스크에서 ID 열에 값을 삽입할지 여부를 지정합니다. 이 속성의 기본값은 **False** 입니다.  
  
 **Null 유지**  
 태스크에서 Null 값을 유지할지 여부를 지정합니다. 이 속성의 기본값은 **False** 입니다.  
  
 **테이블 잠금**  
 데이터를 로드할 때 테이블을 잠글지 여부를 지정합니다. 이 속성의 기본값은 **True** 입니다.  
  
 **CHECK 제약 조건**  
 태스크에서 제약 조건을 확인할지 여부를 지정합니다. 이 속성의 기본값은 **True** 입니다.  
  
 **트리거 실행**  
 대량 삽입에서 테이블에 대해 트리거를 실행할지 여부를 지정합니다. 이 속성의 기본값은 **False** 입니다.  
  
 **첫 번째 행**  
 삽입할 첫 번째 행을 지정합니다. 이 속성의 기본값은 **-1** 이며 이 경우 값이 할당되지 않습니다.  
  
> [!NOTE]  
>  이 속성에 값을 할당하지 않으려면 **SQL 대상 편집기** 에서 해당 입력란의 내용을 지웁니다. **속성** 창, **고급 편집기** 및 개체 모델에 -1을 사용합니다.  
  
 **마지막 행**  
 삽입할 마지막 행을 지정합니다. 이 속성의 기본값은 **-1** 이며 이 경우 값이 할당되지 않습니다.  
  
> [!NOTE]  
>  이 속성에 값을 할당하지 않으려면 **SQL 대상 편집기** 에서 해당 입력란의 내용을 지웁니다. **속성** 창, **고급 편집기** 및 개체 모델에 -1을 사용합니다.  
  
 **최대 오류 개수**  
 대량 삽입이 중지되기 전에 발생할 수 있는 오류 수를 지정합니다. 이 속성의 기본값은 **-1** 이며 이 경우 값이 할당되지 않습니다.  
  
> [!NOTE]  
>  이 속성에 값을 할당하지 않으려면 **SQL 대상 편집기** 에서 해당 입력란의 내용을 지웁니다. **속성** 창, **고급 편집기** 및 개체 모델에 -1을 사용합니다.  
  
 **Timeout**  
 시간이 초과되어 대량 삽입이 중지되기까지 기다리는 시간(초)을 지정합니다.  
  
 **열 순서 지정**  
 정렬 열의 이름을 입력합니다. 각 열을 오름차순이나 내림차순으로 정렬할 수 있습니다. 여러 정렬 열을 사용하는 경우 쉼표로 목록을 구분합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
