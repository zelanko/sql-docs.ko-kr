---
title: SQL Server XML 대량 로드 개체 모델 (SQLXML)
description: SQLXML 4.0에서 XML을 대량 로드 하는 데 사용 되는 SQLXMLBulkLoad 개체의 메서드 및 속성에 대해 알아봅니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bc5414ba64ec7a801cf279a4735a2f8e85cd3731
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461734"
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>SQL Server XML 대량 로드 개체 모델(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 대량 로드 개체 모델은 SQLXMLBulkLoad 개체로 구성 됩니다. 이 개체는 다음 메서드 및 속성을 지원합니다.  
  
## <a name="methods"></a>메서드  
 Execute  
 매개 변수로 제공된 스키마 파일 및 데이터 파일(또는 스트림)을 사용하여 데이터를 대량 로드합니다.  
  
## <a name="properties"></a>속성  
 BulkLoad  
 대량 로드를 수행할지 여부를 지정합니다. 이 속성은 스키마만 생성 하 고 (다음에 나오는 SchemaGen, SGDropTables 및 Sgdroptables 속성 참조) 대량 로드를 수행 하지 않으려는 경우에 유용 합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드가 실행되고 FALSE로 설정된 경우 XML 대량 로드가 실행되지 않습니다.  
  
 기본값은 TRUE입니다.  
  
 CheckConstraints  
 XML 대량 로드에서 열에 데이터를 삽입할 때 열에 지정된 제약 조건(예: 열 간의 기본 키/외래 키 관계로 인한 제약 조건)을 검사할지 여부를 지정합니다. 이 속성은 부울 속성입니다.  
  
 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 삽입되는 각 값에 대해 제약 조건을 검사하며 제약 조건이 위반된 경우 오류를 반환합니다.  
  
> [!NOTE]  
>  이 속성을 FALSE로 유지 하려면 대상 테이블에 대 한 **ALTER TABLE** 권한이 있어야 합니다. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 기본값은 FALSE입니다. 이 속성이 FALSE로 설정된 경우 XML 대량 로드에서 삽입 작업 중 제약 조건을 무시합니다. 현재 구현에서는 매핑 스키마에서 기본 키 및 외래 키 관계의 순서로 테이블을 정의해야 합니다. 즉, 외래 키가 있는 대응되는 테이블을 정의하기 전에 기본 키가 있는 테이블을 정의해야 합니다. 그렇지 않으면 XML 대량 로드가 실패합니다.  
  
 ID 전파가 수행 중인 경우에는 이 옵션이 적용되지 않고 제약 조건 검사가 설정된 상태로 유지됩니다. 이는 `KeepIdentity=False`이며, 부모가 ID 필드이고 자식이 생성될 때 자식에 값이 지정되는 관계가 정의된 경우에 발생합니다.  
  
 ConnectionCommand  
 XML 대량 로드에서 사용 해야 하는 기존 연결 개체 (예: ADO 또는 ICommand command 개체)를 식별 합니다. ConnectionString 속성을 사용 하 여 연결 문자열을 지정 하는 대신 ConnectionCommand 속성을 사용할 수 있습니다. ConnectionCommand를 사용 하는 경우 Transaction 속성을 TRUE로 설정 해야 합니다.  
  
 ConnectionString 및 ConnectionCommand 속성을 모두 사용 하는 경우 XML 대량 로드는 마지막으로 지정 된 속성을 사용 합니다.  
  
 기본값은 NULL입니다.  
  
 ConnectionString  
 데이터베이스 인스턴스에 대한 연결을 설정하는 데 필요한 정보를 제공하는 OLE DB 연결 문자열을 식별합니다. ConnectionString 및 ConnectionCommand 속성을 모두 사용 하는 경우 XML 대량 로드는 마지막으로 지정 된 속성을 사용 합니다.  
  
 기본값은 NULL입니다.  
  
 ErrorLogFile  
 XML 대량 로드에서 오류 및 메시지를 기록하는 파일 이름을 지정합니다. 기본값은 빈 문자열이며 이 경우 로깅이 수행되지 않습니다.  
  
 FireTriggers  
 대상 테이블에 정의된 트리거를 대량 로드 작업 중 실행할지 여부를 지정합니다. 기본값은 FALSE입니다.  
  
 TRUE로 설정된 경우 삽입 작업 중 트리거가 실행됩니다.  
  
> [!NOTE]  
>  이 속성을 FALSE로 유지 하려면 대상 테이블에 대 한 **ALTER TABLE** 권한이 있어야 합니다. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 ID 전파가 수행 중인 경우에는 이 옵션이 적용되지 않고 트리거가 설정된 상태로 유지됩니다. 이는 `KeepIdentity=False`이며, 부모가 ID 필드이고 자식이 생성될 때 자식에 값이 지정되는 관계가 정의된 경우에 발생합니다.  
  
 ForceTableLock  
 XML 대량 로드에서 대량 로드 작업이 진행되는 동안 데이터를 복사할 테이블을 잠글지 여부를 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 대량 로드 작업이 진행되는 동안 테이블 잠금을 확보합니다. 이 속성이 FALSE로 설정된 경우에는 XML 대량 로드에서 테이블에 레코드를 삽입할 때마다 테이블 잠금을 확보합니다.  
  
 기본값은 FALSE입니다.  
  
 IgnoreDuplicateKeys  
 중복 값을 키 열에 삽입하려고 할 때 수행할 작업을 지정합니다. 이 속성이 TRUE로 설정된 경우 중복 값이 있는 레코드를 키 열에 삽입하려고 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 해당 레코드를 삽입하지 않습니다. 해당 레코드 이후의 레코드는 삽입하므로 대량 로드 작업이 실패하지 않습니다. 이 속성이 FALSE로 설정된 경우 중복 값을 키 열에 삽입하려고 하면 대량 로드가 실패합니다.  
  
 IgnoreDuplicateKeys 속성을 TRUE로 설정 하면 테이블에 삽입 된 모든 레코드에 대해 COMMIT 문이 실행 됩니다. 이로 인해 성능이 저하됩니다. 트랜잭션 동작이 파일을 사용 하 여 구현 되기 때문에 트랜잭션 속성이 FALSE로 설정 된 경우에만 속성을 TRUE로 설정할 수 있습니다.  
  
 기본값은 FALSE입니다.  
  
 KeepIdentity  
 원본 파일의 ID 유형 열에 대한 값을 처리하는 방법을 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 원본 파일에 지정된 값을 ID 열에 할당합니다. 이 속성이 FALSE로 설정된 경우에는 대량 로드 작업에서 원본에 지정된 ID 열 값을 무시합니다. 이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 ID 열에 값을 할당합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 생성한 값이 저장된 ID 열을 참조하는 외래 키 열이 대량 로드에 포함될 경우 대량 로드에서는 이러한 ID 값을 해당 외래 키 열에 적절하게 전파합니다.  
  
 이 속성 값은 대량 로드에 포함된 모든 열에 적용됩니다. 기본값은 TRUE입니다.  
  
> [!NOTE]  
>  이 속성을 TRUE로 유지 하려면 대상 테이블에 대 한 **ALTER TABLE** 권한이 있어야 합니다. 그렇지 않은 경우에는 값을 FALSE로 설정해야 합니다. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 KeepNulls  
 XML 문서에서 해당 특성이나 자식 요소가 없는 열에 사용할 값을 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 서버에 설정된 열의 기본값(있는 경우)이 아닌 null 값을 열에 할당합니다. 이 속성 값은 대량 로드에 포함된 모든 열에 적용됩니다.  
  
 기본값은 FALSE입니다.  
  
 SchemaGen  
 대량 로드 작업을 수행하기 전에 필요한 테이블을 만들지 여부를 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 매핑 스키마에 식별된 테이블이 생성됩니다. 이 경우 데이터베이스가 있어야 합니다. 하나 이상의 테이블이 데이터베이스에 이미 있는 경우 SGDropTables 속성은 이러한 기존 테이블을 삭제 하 고 다시 만들지 여부를 결정 합니다.  
  
 SchemaGen 속성의 기본값은 FALSE입니다. SchemaGen은 새로 만든 테이블에 PRIMARY KEY 제약 조건을 만들지 않습니다. 그러나 SchemaGen은 매핑 스키마에서 일치 하는 **sql: relationship** 및 **sql: 키-필드** 주석을 찾을 수 있고 키 필드가 단일 열로 구성 된 경우 데이터베이스에서 FOREIGN KEY 제약 조건을 만듭니다.  
  
 SchemaGen 속성을 TRUE로 설정 하면 XML 대량 로드에서 다음을 수행 합니다.  
  
-   요소 및 특성 이름을 사용하여 필요한 테이블을 만듭니다. 따라서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 예약어는 스키마의 요소 및 특성 이름으로 사용하지 않아야 합니다.  
  
-   [Xml 데이터 형식](../../../t-sql/xml/xml-transact-sql.md) 형식의 [sql: 오버플로 필드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md) 를 사용 하 여 지정 된 모든 열에 대 한 오버플로 데이터를 반환 합니다.  
  
 SGDropTables  
 기존 테이블을 삭제하고 다시 만들지 여부를 지정합니다. SchemaGen 속성이 TRUE로 설정 된 경우이 속성을 사용 합니다. SGDropTables가 FALSE 이면 기존 테이블이 유지 됩니다. 이 속성이 TRUE이면 기존 테이블이 삭제되고 다시 생성됩니다.  
  
 기본값은 FALSE입니다.  
  
 SGUseID  
 테이블을 만들 때 PRIMARY KEY 제약 조건을 만들 때 **id** 유형으로 식별 되는 매핑 스키마의 특성을 사용할 수 있는지 여부를 지정 합니다. SchemaGen 속성이 TRUE로 설정 된 경우이 속성을 사용 합니다. SGUseID가 TRUE 이면 SchemaGen 유틸리티는 **dt: type = "id"** 가 기본 키 열로 지정 된 특성을 사용 하 여 테이블을 만들 때 적절 한 primary key 제약 조건을 추가 합니다.  
  
 기본값은 FALSE입니다.  
  
 TempFilePath  
 XML 대량 로드에서 트랜잭션된 대량 로드에 사용할 임시 파일을 만들 파일 경로를 지정합니다. 이 속성은 Transaction 속성이 TRUE로 설정 된 경우에만 유용 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 대량 로드에 사용 되는 계정에이 경로에 대 한 액세스 권한이 있는지 확인 해야 합니다. 이 속성이 설정되지 않은 경우 XML 대량 로드에서는 임시 파일을 TEMP 환경 변수에 지정된 위치에 저장합니다.  
  
 트랜잭션  
 대량 로드를 트랜잭션으로 수행할지 여부를 지정합니다. 트랜잭션으로 수행하면 대량 로드가 실패할 경우 롤백이 수행됩니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 대량 로드가 트랜잭션 컨텍스트에서 수행됩니다. TempFilePath 속성은 Transaction이 TRUE로 설정 된 경우에만 유용 합니다.  
  
> [!NOTE]  
>  이진 데이터를 로드 하는 경우 (예: bin. hex, bin. base64 XML 데이터 형식에서 binary, image [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식으로) 트랜잭션 속성을 FALSE로 설정 해야 합니다.  
  
 기본값은 FALSE입니다.  
  
 XMLFragment  
 원본 데이터가 XML 조각인지 여부를 지정합니다. XML 조각은 단일 최상위(루트) 요소가 없는 XML 문서입니다. 이 속성은 부울 속성입니다. 원본 파일이 XML 조각으로 구성되어 있으면 이 속성을 TRUE로 설정해야 합니다.  
  
 기본값은 FALSE입니다.  
  
  
