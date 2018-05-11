---
title: 대량 삽입 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.bulkinserttask.f1
- sql13.dts.designer.bulkinserttask.connection.f1
- sql13.dts.designer.bulkinserttask.general.f1
- sql13.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4f98d9b778c31a409a103cb13fccdefe1372b2d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="bulk-insert-task"></a>대량 삽입 태스크
  대량 삽입 태스크는 많은 양의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 또는 뷰에 복사할 수 있는 효율적인 방법을 제공합니다. 예를 들어 회사에서 백만 개 행으로 구성된 제품 목록을 메인프레임 시스템에 저장하지만 회사의 전자 상거래 시스템이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 웹 페이지를 채운다고 가정합니다. 또한 메인프레임의 마스터 제품 목록을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 테이블을 매일 밤 업데이트해야 합니다. 테이블을 업데이트하려면 제품 목록을 탭 구분 형식으로 저장하고 대량 삽입 태스크를 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 직접 복사합니다.  
  
 데이터를 고속으로 복사하려면 원본 파일에서 테이블 또는 뷰로 데이터가 이동하는 동안 데이터 변환을 수행할 수 없습니다.  
  
## <a name="usage-considerations"></a>사용 시 고려 사항  
 대량 삽입 태스크를 사용하기 전에 다음을 고려합니다.  
  
-   대량 삽입 태스크는 텍스트 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 또는 뷰로만 데이터를 전송할 수 있습니다. 대량 삽입 태스크를 사용하여 DBMS(데이터베이스 관리 시스템)에서 데이터를 전송하려면 원본 데이터를 텍스트 파일로 내보낸 다음 텍스트 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 또는 뷰로 데이터를 가져와야 합니다.  
  
-   대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블 또는 뷰여야 합니다. 대상 테이블 또는 뷰에 이미 데이터가 포함되어 있으면 대량 삽입 태스크가 실행될 때 새 데이터가 기존 데이터에 추가됩니다. 데이터를 대체하려면 대량 삽입 태스크를 실행하기 전에 DELETE 또는 TRUNCATE 문을 실행하는 SQL 실행 태스크를 실행합니다. 자세한 내용은 [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md)을 참조하세요.  
  
-   대량 삽입 태스크 개체에 서식 파일을 사용할 수 있습니다. **bcp** 유틸리티로 만든 서식 파일이 있으면 대량 삽입 태스크에 해당 경로를 지정할 수 있습니다. 대량 삽입 태스크는 XML 서식 파일과 비XML 서식 파일을 모두 지원합니다. 서식 파일에 대한 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
-   대량 삽입 태스크가 포함된 패키지는 sysadmin 고정 서버 역할의 멤버만 실행할 수 있습니다.  
  
## <a name="bulk-insert-task-with-transactions"></a>트랜잭션의 대량 삽입 태스크  
 일괄 처리 크기를 설정하지 않으면 전체 대량 복사 작업이 하나의 트랜잭션으로 처리됩니다. 일괄 처리 크기가 **0** 이면 데이터는 하나의 일괄 처리로 삽입됩니다. 일괄 처리 크기를 설정한 경우 각 일괄 처리는 일괄 처리 실행이 완료될 때 커밋되는 트랜잭션을 나타냅니다.  
  
 트랜잭션과 관련이 있으므로 대량 삽입 태스크의 동작은 태스크의 패키지 트랜잭션 조인 여부에 따라 달라집니다. 대량 삽입 태스크가 패키지 트랜잭션을 조인하지 않으면 오류가 없는 각 일괄 처리는 다음 일괄 처리가 시도되기 전에 하나의 단위로 커밋됩니다. 대량 삽입 태스크가 패키지 트랜잭션을 조인하면 오류가 없는 일괄 처리는 태스크의 마지막에 트랜잭션에 남게 됩니다. 이러한 일괄 처리는 패키지의 커밋 또는 롤백 작업에 따릅니다.  
  
 대량 삽입 태스크가 실패해도 성공적으로 로드된 일괄 처리는 자동으로 롤백되지 않습니다. 이와 마찬가지로 태스크가 성공해도 일괄 처리가 자동으로 커밋되지는 않습니다. 커밋 및 롤백 작업은 패키지 및 워크플로 속성 설정에 대한 응답으로만 발생합니다.  
  
## <a name="source-and-destination"></a>원본 및 대상  
 텍스트 원본 파일의 위치를 지정하는 경우 다음을 고려합니다.  
  
-   서버에 파일과 대상 데이터베이스에 모두 액세스할 수 있는 권한이 있어야 합니다.  
  
-   대량 삽입 태스크는 서버에서 실행되므로 태스크에 사용되는 모든 서식 파일이 서버에 있어야 합니다.  
  
-   대량 삽입 태스크가 로드하는 원본 파일은 데이터가 삽입될 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 동일한 서버나 원격 서버에 위치할 수 있습니다. 원본 파일이 원격 서버에 있을 경우 경로에 UNC(Universal Naming Convention) 이름을 사용하여 파일 이름을 지정해야 합니다.  
  
## <a name="performance-optimization"></a>성능 최적화  
 성능을 최적화하려면 다음을 고려합니다.  
  
-   데이터가 삽입될 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 동일한 컴퓨터에 텍스트 파일이 있으면 데이터가 네트워크를 통해 이동하지 않으므로 복사 작업이 훨씬 빠른 속도로 수행됩니다.  
  
-   대량 삽입 태스크는 오류를 일으키는 행을 로깅하지 않습니다. 이 정보를 캡처해야 하는 경우 데이터 흐름 구성 요소의 오류 출력을 사용하여 오류를 일으키는 행을 예외 파일에 캡처할 수 있습니다.  
  
## <a name="custom-log-entries-available-on-the-bulk-insert-task"></a>대량 삽입 태스크에 사용할 수 있는 사용자 지정 로그 항목  
 다음 표에서는 대량 삽입 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**BulkInsertTaskBegin**|대량 삽입이 시작되었음을 나타냅니다.|  
|**BulkInsertTaskEnd**|대량 삽입이 완료되었음을 나타냅니다.|  
|**BulkInsertTaskInfos**|태스크에 대한 설명 정보를 제공합니다.|  
  
## <a name="bulk-insert-task-configuration"></a>대량 삽입 태스크 구성  
 다음과 같은 방법으로 대량 삽입 태스크를 구성할 수 있습니다.  
  
-   OLE DB 연결 관리자에서 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 데이터가 삽입될 테이블 또는 뷰에 연결하도록 지정합니다. 대량 삽입 태스크에서는 대상 데이터베이스에 대한 OLE DB 연결만 사용할 수 있습니다.  
  
-   파일 또는 플랫 파일 연결 관리자를 지정하여 원본 파일에 액세스하십시오. 대량 삽입 태스크의 경우 원본 파일의 위치에 대해서만 연결 관리자를 사용하고 연결 관리자 편집기에서 선택한 다른 옵션은 무시합니다.  
  
-   서식 파일을 사용하거나 원본 데이터의 열 및 행 구분 기호를 정의하여 대량 삽입 태스크에 사용되는 서식을 정의합니다. 서식 파일을 사용하는 경우 파일 연결 관리자에서 서식 파일에 액세스하도록 지정합니다.  
  
-   태스크에서 데이터를 삽입할 때 대상 테이블 또는 뷰에 대해 수행할 동작을 지정합니다. 제약 조건 확인, ID 삽입 가능, Null 유지, 트리거 발생 또는 테이블 잠금 옵션이 있습니다.  
  
-   일괄 처리 크기, 파일에서 삽입할 첫 번째 행과 마지막 행, 태스크가 행 삽입을 중지하기까지 발생할 수 있는 삽입 오류 수, 정렬될 열 이름 등 삽입할 일괄 처리 데이터에 대한 정보를 제공합니다.  
  
 대량 삽입 태스크에서 플랫 파일 연결 관리자를 사용하여 원본 파일에 액세스하는 경우 태스크는 플랫 파일 연결 관리자에서 지정한 서식을 사용하지 않습니다. 대신 대량 삽입 태스크에서는 서식 파일에 지정된 서식이나 태스크의 RowDelimiter 및 ColumnDelimiter 속성 값을 사용합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>대량 삽입 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="related-content"></a>관련 내용  
  
-   support.microsoft.com의 기술 문서 - [UAC 사용 시스템에서 "데이터 삽입을 위해 SSIS 대량 삽입을 준비할 수 없습니다." 오류가 발생할 수 있습니다.](http://go.microsoft.com/fwlink/?LinkId=233693)  
  
-   msdn.microsoft.com의 기술 문서 - [데이터 로드 성능 가이드](http://go.microsoft.com/fwlink/?LinkId=233700)  
  
-   simple-talk.com의 기술 문서, [SQL Server Integration Services를 사용하여 데이터 대량 로드](http://go.microsoft.com/fwlink/?LinkId=233701)  
  
## <a name="bulk-insert-task-editor-connection-page"></a>대량 삽입 태스크 편집기(연결 페이지)
  **대량 삽입 태스크 편집기** 대화 상자의 **연결** 페이지를 사용하여 대량 삽입 태스크의 원본 및 대상과 사용할 서식을 지정할 수 있습니다.  
  
 대량 삽입 작업에 대해 알아보려면 [대량 삽입 태스크](../../integration-services/control-flow/bulk-insert-task.md) 및 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
### <a name="options"></a>변수  
 **대량 삽입 태스크 편집기**  
 목록에서 OLE DB 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결을 만듭니다.  
  
 **관련 항목:** [OLE DB 연결 관리자 구성](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
 **DestinationTable**  
 대상 테이블 또는 뷰의 이름을 입력하거나 목록에서 테이블 또는 뷰를 선택합니다.  
  
 **형식**  
 대량 삽입을 위한 서식의 원본을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 사용**|서식 지정을 포함하는 파일을 선택합니다. 이 옵션을 선택하면 동적 옵션 **FormatFile**이 표시됩니다.|  
|**지정**|서식을 지정합니다. 이 옵션을 선택하면 동적 옵션 **RowDelimiter** 및 **ColumnDelimiter**가 표시됩니다.|  
  
 **최근에 사용한 파일**  
 목록에서 파일 또는 플랫 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결을 만듭니다.  
  
 파일 위치는 이 태스크를 위해 연결 관리자에 지정된 SQL Server 데이터베이스 엔진의 상대적 위치입니다. 텍스트 파일은 서버의 로컬 하드 드라이브에서 또는 SQL Server에 매핑된 드라이브 또는 공유 드라이브를 통해 SQL Server 데이터베이스 엔진이 액세스할 수 있어야 합니다. 이 파일은 SSIS 런타임으로 액세스되지 않습니다.  
  
 플랫 파일 연결 관리자를 사용하여 원본 파일에 액세스할 경우 대량 삽입 태스크에서는 플랫 파일 연결 관리자에서 지정한 서식을 사용하지 않습니다. 대신 대량 삽입 태스크에서는 서식 파일에 지정된 서식이나 태스크의 RowDelimiter 및 ColumnDelimiter 속성 값을 사용합니다.  
  
 **관련 항목:** [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md), [플랫 파일 연결 관리자](../../integration-services/connection-manager/flat-file-connection-manager.md) 
  
 **테이블 새로 고침**  
 테이블 및 뷰 목록을 새로 고칩니다.  
  
### <a name="format-dynamic-options"></a>Format 동적 옵션  
  
#### <a name="format--use-file"></a>Format = 파일 사용  
 **FormatFile**  
 서식 파일의 경로를 입력하거나 줄임표 단추 **(...)** 를 클릭하여 서식 파일을 찾습니다.  
  
#### <a name="format--specify"></a>Format = 지정  
 **RowDelimiter**  
 원본 파일의 행 구분 기호를 지정합니다. 기본값은 **{CR}{LF}** 입니다.  
  
 **ColumnDelimiter**  
 원본 파일의 열 구분 기호를 지정합니다. 기본값은 **탭**입니다.  
  
## <a name="bulk-insert-task-editor-general-page"></a>대량 삽입 태스크 편집기(일반 페이지)
  **대량 삽입 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 대량 삽입 태스크를 명명 및 설명할 수 있습니다.  
  
### <a name="options"></a>변수  
 **이름**  
 대량 삽입 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 대량 삽입 태스크에 대한 설명을 입력합니다.  
 
## <a name="bulk-insert-task-editor-options-page"></a>대량 삽입 태스크 편집기(옵션 페이지)
  **대량 삽입 태스크 편집기** 대화 상자의 **옵션** 페이지를 사용하여 대량 삽입 작업에 대한 옵션을 설정할 수 있습니다. 대량 삽입 태스크는 대량의 데이터를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 또는 뷰로 복사합니다.  
  
 대량 삽입 작업에 대한 자세한 내용은 [대량 삽입 태스크](../../integration-services/control-flow/bulk-insert-task.md) 및 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
### <a name="options"></a>변수  
 **CodePage**  
 데이터 파일에서 데이터의 코드 페이지를 지정합니다.  
  
 **DataFileType**  
 로드 작업에 사용할 데이터 형식 값을 지정합니다.  
  
 **BatchSize**  
 일괄 처리의 행 수를 지정합니다. 전체 데이터 파일이 기본값입니다. **BatchSize** 를 0으로 설정하면 데이터가 단일 일괄 처리로 로드됩니다.  
  
 **LastRow**  
 복사할 마지막 행을 지정합니다.  
  
 **FirstRow**  
 복사를 시작할 처음 행을 지정합니다.  
  
 **대량 삽입 태스크 편집기**  
 |용어|정의|  
|----------|----------------|  
|**CHECK 제약 조건**|테이블 및 열 제약 조건을 확인하려면 선택합니다.|  
|**Null 유지**|대량 삽입 작업 중에 빈 열에 기본값을 삽입하는 대신 Null 값을 유지하려면 선택합니다.|  
|**ID 삽입 가능**|기존 값을 ID 열에 삽입하려면 선택합니다.|  
|**테이블 잠금**|대량 삽입 중에 테이블을 잠그려면 선택합니다.|  
|**트리거 실행**|테이블에 삽입, 업데이트 또는 삭제 트리거를 발생시키려면 선택합니다.|  
  
 **SortedData**  
 대량 삽입 문에 ORDER BY 절을 지정합니다. 사용자가 제공한 열 이름은 대상 테이블에서 유효한 열이어야 합니다. 기본값은 **false**입니다. 즉, 데이터는 ORDER BY 절로 정렬되지 않습니다.  
  
 **MaxErrors**  
 대량 삽입 작업이 취소되는 최대 오류 발생 횟수를 지정합니다. 값을 0으로 지정하면 오류가 무한으로 발생해도 작업이 취소되지 않습니다.  
  
> [!NOTE]  
>  대량 로드 작업으로 가져올 수 없는 각 행은 하나의 오류로 간주됩니다.  
  
