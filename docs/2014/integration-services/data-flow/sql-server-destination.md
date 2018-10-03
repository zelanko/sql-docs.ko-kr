---
title: SQL Server 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdest.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ad8750547ff9744b525d8d6d234f02f0bb78375
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159893"
---
# <a name="sql-server-destination"></a>SQL Server 대상
  SQL Server 대상은 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 및 뷰로 데이터를 대량 로드합니다. 원격 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 액세스하는 패키지에서는 SQL Server 대상을 사용할 수 없습니다. 이러한 패키지에서는 대신 OLE DB 대상을 사용해야 합니다. 자세한 내용은 [OLE DB Destination](ole-db-destination.md)을 참조하세요.  
  
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
  
 대량 로드 옵션에 대한 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)를 참조하세요.  
  
#### <a name="performance-improvements"></a>성능 향상  
 대량 삽입의 성능과 대량 삽입 작업 중의 테이블 액세스를 향상시키려면 기본 옵션을 다음과 같이 변경해야 합니다.  
  
-   대량 가져오기 작업 중에 대상 테이블 또는 뷰의 제약 조건을 검사하지 마십시오.  
  
-   대량 로드 작업 중에 대상 테이블에서 정의된 삽입 트리거를 실행하지 마십시오.  
  
-   테이블에 잠금을 적용하지 마십시오. 이렇게 하면 대량 삽입 작업 중에 다른 사용자 및 응용 프로그램이 테이블을 사용할 수 있습니다.  
  
## <a name="configuration-of-the-sql-server-destination"></a>SQL Server 대상 구성  
 다음과 같은 방법으로 SQL Server 대상을 구성할 수 있습니다.  
  
-   데이터를 대량 로드할 테이블 또는 뷰를 지정합니다.  
  
-   제약 조건 검사 여부와 같은 옵션을 지정하여 대량 로드 작업을 사용자 지정합니다.  
  
-   한 일괄 처리의 모든 행을 커밋할지 지정하거나 한 일괄 처리로 커밋할 행의 최대 수를 설정합니다.  
  
-   대량 로드 작업에 대한 제한 시간을 지정합니다.  
  
 이 대상은 OLE DB 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자가 사용할 OLE DB Provider를 지정합니다. 자세한 내용은 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트는 또한 OLE DB 연결 관리자를 만들 수 있는 데이터 원본 개체를 제공합니다. 그러면 SQL Server 대상에서 데이터 원본과 데이터 원본 뷰를 사용할 수 있습니다.  
  
 SQL Server 대상은 하나의 입력을 갖습니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **SQL Server 대상 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [SQL 대상 편집기 &#40;연결 관리자 페이지&#41;](../sql-destination-editor-connection-manager-page.md)  
  
-   [SQL 대상 편집기 &#40;매핑 페이지&#41;](../sql-destination-editor-mappings-page.md)  
  
-   [SQL 대상 편집기 &#40;고급 페이지&#41;](../sql-destination-editor-advanced-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../common-properties.md)  
  
-   [SQL Server 대상 사용자 지정 속성](sql-server-destination-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [SQL Server 대상을 사용하여 데이터 대량 로드](sql-server-destination.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [SQL Server 대상을 사용하여 데이터 대량 로드](sql-server-destination.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   support.microsoft.com의 기술 문서 - [UAC 사용 시스템에서 "데이터 삽입을 위해 SSIS 대량 삽입을 준비할 수 없습니다." 오류가 발생할 수 있습니다.](http://go.microsoft.com/fwlink/?LinkId=199482)  
  
-   msdn.microsoft.com의 기술 문서 - [데이터 로드 성능 가이드](http://go.microsoft.com/fwlink/?LinkId=233700)  
  
-   simple-talk.com의 기술 문서, [SQL Server Integration Services를 사용하여 데이터 대량 로드](http://go.microsoft.com/fwlink/?LinkId=233701)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 흐름](data-flow.md)  
  
  
