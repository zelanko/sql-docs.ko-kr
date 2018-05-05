---
title: SQL Server XML 대량 로드 개체 모델 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 43ca8f3b345f5db9c0d11217caef744e9172bd22
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>SQL Server XML 대량 로드 개체 모델(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLXMLBulkLoad 개체의 XML 대량 로드 개체 모델은 구성 합니다. 이 개체는 다음 메서드 및 속성을 지원합니다.  
  
## <a name="methods"></a>메서드  
 Parameter  
 매개 변수로 제공된 스키마 파일 및 데이터 파일(또는 스트림)을 사용하여 데이터를 대량 로드합니다.  
  
## <a name="properties"></a>속성  
 BulkLoad  
 대량 로드를 수행할지 여부를 지정합니다. 이 속성 (다음에 나오는 SchemaGen, SGDropTables, 및 SGUseID 속성 참조) 스키마만 생성 하 고 대량 로드를 수행 하지 하려는 경우에 유용 합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드가 실행되고 FALSE로 설정된 경우 XML 대량 로드가 실행되지 않습니다.  
  
 기본값은 TRUE입니다.  
  
 CheckConstraints  
 XML 대량 로드에서 열에 데이터를 삽입할 때 열에 지정된 제약 조건(예: 열 간의 기본 키/외래 키 관계로 인한 제약 조건)을 검사할지 여부를 지정합니다. 이 속성은 부울 속성입니다.  
  
 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 삽입되는 각 값에 대해 제약 조건을 검사하며 제약 조건이 위반된 경우 오류를 반환합니다.  
  
> [!NOTE]  
>  이 속성을 유지 하려면이 FALSE로, 있어야 **ALTER TABLE** 대상 테이블에 대 한 권한. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 기본값은 FALSE입니다. 이 속성이 FALSE로 설정된 경우 XML 대량 로드에서 삽입 작업 중 제약 조건을 무시합니다. 현재 구현에서는 매핑 스키마에서 기본 키 및 외래 키 관계의 순서로 테이블을 정의해야 합니다. 즉, 외래 키가 있는 대응되는 테이블을 정의하기 전에 기본 키가 있는 테이블을 정의해야 합니다. 그렇지 않으면 XML 대량 로드가 실패합니다.  
  
 ID 전파가 수행 중인 경우에는 이 옵션이 적용되지 않고 제약 조건 검사가 설정된 상태로 유지됩니다. 이는 `KeepIdentity=False`이며, 부모가 ID 필드이고 자식이 생성될 때 자식에 값이 지정되는 관계가 정의된 경우에 발생합니다.  
  
 ConnectionCommand  
 XML 대량 로드 사용 해야 하는 기존 연결 개체 (예를 들어 ADO 또는 ICommand 명령 개체)를 식별 합니다. ConnectionString 속성이 연결 문자열을 지정 하는 대신 ConnectionCommand 속성을 사용할 수 있습니다. ConnectionCommand를 사용 하는 경우 트랜잭션 속성을 TRUE로 설정 되어야 합니다.  
  
 ConnectionString 및 ConnectionCommand 속성을 사용 하는 경우 XML 대량 로드는 지정된 된 마지막 속성을 사용 합니다.  
  
 기본값은 NULL입니다.  
  
 ConnectionString  
 데이터베이스 인스턴스에 대한 연결을 설정하는 데 필요한 정보를 제공하는 OLE DB 연결 문자열을 식별합니다. ConnectionString 및 ConnectionCommand 속성을 사용 하는 경우 XML 대량 로드는 지정된 된 마지막 속성을 사용 합니다.  
  
 기본값은 NULL입니다.  
  
 ErrorLogFile  
 XML 대량 로드에서 오류 및 메시지를 기록하는 파일 이름을 지정합니다. 기본값은 빈 문자열이며 이 경우 로깅이 수행되지 않습니다.  
  
 FireTriggers  
 대상 테이블에 정의된 트리거를 대량 로드 작업 중 실행할지 여부를 지정합니다. 기본값은 FALSE입니다.  
  
 TRUE로 설정된 경우 삽입 작업 중 트리거가 실행됩니다.  
  
> [!NOTE]  
>  이 속성을 유지 하려면이 FALSE로, 있어야 **ALTER TABLE** 대상 테이블에 대 한 권한. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 ID 전파가 수행 중인 경우에는 이 옵션이 적용되지 않고 트리거가 설정된 상태로 유지됩니다. 이는 `KeepIdentity=False`이며, 부모가 ID 필드이고 자식이 생성될 때 자식에 값이 지정되는 관계가 정의된 경우에 발생합니다.  
  
 ForceTableLock  
 XML 대량 로드에서 대량 로드 작업이 진행되는 동안 데이터를 복사할 테이블을 잠글지 여부를 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 대량 로드 작업이 진행되는 동안 테이블 잠금을 확보합니다. 이 속성이 FALSE로 설정된 경우에는 XML 대량 로드에서 테이블에 레코드를 삽입할 때마다 테이블 잠금을 확보합니다.  
  
 기본값은 FALSE입니다.  
  
 IgnoreDuplicateKeys  
 중복 값을 키 열에 삽입하려고 할 때 수행할 작업을 지정합니다. 이 속성이 TRUE로 설정된 경우 중복 값이 있는 레코드를 키 열에 삽입하려고 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 해당 레코드를 삽입하지 않습니다. 해당 레코드 이후의 레코드는 삽입하므로 대량 로드 작업이 실패하지 않습니다. 이 속성이 FALSE로 설정된 경우 중복 값을 키 열에 삽입하려고 하면 대량 로드가 실패합니다.  
  
 IgnoreDuplicateKeys 속성이 TRUE로 설정 되어 테이블에 삽입 된 모든 레코드에 대해 COMMIT 문이 발급 됩니다. 이로 인해 성능이 저하됩니다. 속성은 트랜잭션 동작 파일을 사용 하 여 구현 되기 때문에 트랜잭션 속성이 FALSE로 설정 된 경우에 TRUE로 설정할 수 있습니다.  
  
 기본값은 FALSE입니다.  
  
 KeepIdentity  
 원본 파일의 ID 유형 열에 대한 값을 처리하는 방법을 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 원본 파일에 지정된 값을 ID 열에 할당합니다. 이 속성이 FALSE로 설정된 경우에는 대량 로드 작업에서 원본에 지정된 ID 열 값을 무시합니다. 이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 ID 열에 값을 할당합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 생성한 값이 저장된 ID 열을 참조하는 외래 키 열이 대량 로드에 포함될 경우 대량 로드에서는 이러한 ID 값을 해당 외래 키 열에 적절하게 전파합니다.  
  
 이 속성 값은 대량 로드에 포함된 모든 열에 적용됩니다. 기본값은 TRUE입니다.  
  
> [!NOTE]  
>  이 속성을 유지 하려면이 TRUE로, 있어야 **ALTER TABLE** 대상 테이블에 대 한 권한. 그렇지 않은 경우에는 값을 FALSE로 설정해야 합니다. 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 KeepNulls  
 XML 문서에서 해당 특성이나 자식 요소가 없는 열에 사용할 값을 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 XML 대량 로드에서 서버에 설정된 열의 기본값(있는 경우)이 아닌 null 값을 열에 할당합니다. 이 속성 값은 대량 로드에 포함된 모든 열에 적용됩니다.  
  
 기본값은 FALSE입니다.  
  
 SchemaGen  
 대량 로드 작업을 수행하기 전에 필요한 테이블을 만들지 여부를 지정합니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 매핑 스키마에 식별된 테이블이 생성됩니다. 이 경우 데이터베이스가 있어야 합니다. 하나 이상의 테이블에에서 이미 있으면 데이터베이스를 SGDropTables 속성은 기존 테이블 삭제 하 고 다시 만들지 여부를 결정 합니다.  
  
 SchemaGen 속성의 기본값은 FALSE입니다. SchemaGen 새로 만든된 테이블에 PRIMARY KEY 제약 조건을 만들지 않습니다. 그러나 SchemaGen는 만듭니다 FOREIGN KEY 제약 조건이 데이터베이스에 일치 하는 찾을 수 있는 경우 **sql: relationship** 및 **sql:-필드** 매핑 스키마에 주석 및 키 필드 이루어져 단일 열입니다.  
  
 SchemaGen 속성을 TRUE로 설정한 경우 XML 대량 로드는 다음 note:  
  
-   요소 및 특성 이름을 사용하여 필요한 테이블을 만듭니다. 따라서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 예약어는 스키마의 요소 및 특성 이름으로 사용하지 않아야 합니다.  
  
-   오버플로 사용 하 여 지정 된 모든 열에 대 한 데이터를 반환 된 [sql:overflow-필드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md) 에 [xml 데이터 형식](../../../t-sql/xml/xml-transact-sql.md) 형식입니다.  
  
 SGDropTables  
 기존 테이블을 삭제하고 다시 만들지 여부를 지정합니다. SchemaGen 속성을 TRUE로 설정 된 경우이 속성을 사용 합니다. SGDropTables가 FALSE 이면 기존 테이블이 유지 됩니다. 이 속성이 TRUE이면 기존 테이블이 삭제되고 다시 생성됩니다.  
  
 기본값은 FALSE입니다.  
  
 SGUseID  
 특성 매핑 스키마에는 인지 지정로 식별 **id** 종류는 테이블을 만들 때 PRIMARY KEY 제약 조건을 만드는 데 사용할 수 있습니다. SchemaGen 속성을 TRUE로 설정 된 경우이 속성을 사용 합니다. SchemaGen 유틸리티 특성에서 사용 하는 대 한 SGUseID 결과가 TRUE 이면 **dt: type = "id"** 기본 키 열으로 지정 되 고 테이블을 만들 때 적절 한 PRIMARY KEY 제약 조건을 추가 합니다.  
  
 기본값은 FALSE입니다.  
  
 TempFilePath  
 XML 대량 로드에서 트랜잭션된 대량 로드에 사용할 임시 파일을 만들 파일 경로를 지정합니다. 이 속성은 Transaction 속성이 TRUE로 설정된 경우에만 유용합니다. XML 대량 로드에 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 계정에 이 경로에 대한 액세스 권한이 있어야 합니다. 이 속성이 설정되지 않은 경우 XML 대량 로드에서는 임시 파일을 TEMP 환경 변수에 지정된 위치에 저장합니다.  
  
 트랜잭션  
 대량 로드를 트랜잭션으로 수행할지 여부를 지정합니다. 트랜잭션으로 수행하면 대량 로드가 실패할 경우 롤백이 수행됩니다. 이 속성은 부울 속성입니다. 이 속성이 TRUE로 설정된 경우 대량 로드가 트랜잭션 컨텍스트에서 수행됩니다. TempFilePath 속성이 트랜잭션이 TRUE로 설정 하는 경우에 유용 합니다.  
  
> [!NOTE]  
>  이진 데이터를 로드 하는 경우 (bin.hex, bin.base64 XML 데이터 형식부터 binary, 이미지 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식), 트랜잭션 속성을 FALSE로 설정 해야 합니다.  
  
 기본값은 FALSE입니다.  
  
 XMLFragment  
 원본 데이터가 XML 조각인지 여부를 지정합니다. XML 조각은 단일 최상위(루트) 요소가 없는 XML 문서입니다. 이 속성은 부울 속성입니다. 원본 파일이 XML 조각으로 구성되어 있으면 이 속성을 TRUE로 설정해야 합니다.  
  
 기본값은 FALSE입니다.  
  
  
