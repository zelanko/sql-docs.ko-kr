---
title: 대량 복사 작업 수행 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 대량 복사 작업 수행
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], bulk copy operations
- OLE DB Driver for SQL Server, bulk copy operations
- MSOLEDBSQL, bulk copy operations
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 55c72303a53059cde4d05b48bcd53731f70ca97b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036803"
---
# <a name="performing-bulk-copy-operations"></a>대량 복사 작업 수행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대량 복사 기능은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블 또는 뷰와의 대량 데이터 전송을 지원합니다. SELECT 문을 지정하여 데이터를 전송할 수도 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 ASCII 파일과 같은 운영 체제 데이터 파일 간에 데이터를 이동할 수 있습니다. 데이터 파일은 다른 형식을 가질 수 있습니다. 형식은 형식 파일에서 대량 복사로 정의됩니다. 필요에 따라 데이터를 프로그램 변수로 로드하고 대량 복사 함수와 메서드를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전송할 수 있습니다.  
  
 이 기능을 보여 주는 샘플 응용 프로그램을 참조 하세요 [대량 복사 데이터를 사용 하 여 IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)합니다.  
  
 응용 프로그램은 보통 다음 두 가지 방법 중 하나로 대량 복사를 사용합니다.  
  
-   Transact-SQL 문의 테이블, 뷰 또는 결과 집합에서 데이터가 테이블 또는 뷰와 동일한 형식으로 저장되는 데이터 파일로 대량 복사합니다.  
  
     이것을 기본 모드 데이터 파일이라고 합니다.  
  
-   Transact-SQL 문의 테이블, 뷰 또는 결과 집합에서 데이터가 테이블 또는 뷰 중 하나와 다른 형식으로 저장되는 데이터 파일로 대량 복사합니다.  
  
     이 경우 데이터 파일에 저장되는 각 열의 특징(데이터 형식, 위치, 길이, 종결자 등)을 정의하는 별도의 형식 파일이 만들어집니다. 모든 열이 문자 형식으로 변환된 경우 결과 파일을 문자 모드 데이터 파일이라고 합니다.  
  
-   데이터 파일에서 테이블 또는 뷰로 대량 복사합니다.  
  
     필요한 경우 형식 파일을 사용하여 데이터 파일의 레이아웃을 결정합니다.  
  
-   데이터를 프로그램 변수로 로드한 다음 한 번에 한 행씩, 대량 복사하기 위한 대량 복사 함수를 사용하여 데이터를 테이블 또는 뷰로 가져옵니다.  
  
 다른 대량 복사 프로그램에서 대량 복사 함수에 사용되는 데이터 파일을 만들 필요는 없습니다. 대량 복사 정의에 따라 다른 모든 시스템에서 데이터 파일과 형식 파일을 생성할 수 있습니다. 이러한 파일을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대량 복사 프로그램과 함께 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 가져올 수 있습니다. 예를 들어 탭으로 구분된 파일의 스프레드시트에서 데이터를 내보내고, 탭으로 구분된 파일을 설명하는 형식 파일을 작성한 다음 대량 복사 프로그램을 사용하여 신속하게 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 가져올 수 있습니다. 대량 복사에서 생성된 데이터 파일을 다른 응용 프로그램으로 가져올 수도 있습니다. 예를 들어 대량 복사 함수를 사용하여 테이블 또는 뷰의 데이터를 탭으로 구분된 파일로 내보낸 다음 스프레드시트에 로드할 수 있습니다.  
  
 대량 복사 함수를 사용할 응용 프로그램을 코딩하는 프로그래머가 우수한 대량 복사 성능을 얻으려면 일반 규칙을 따라야 합니다. 대량 복사 작업에 대 한 지원에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 참조 하세요 [대량 데이터 가져오기 및 내보내기의 &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 CLR UDT(사용자 정의 형식)를 이진 데이터로 바인딩해야 합니다. 형식 파일에서 SQLCHAR를 대상 UDT 열의 데이터 형식으로 지정하는 경우에도 BCP 유틸리티는 해당 데이터를 이진으로 처리합니다.  
  
 대량 복사 작업에는 SET FMTONLY OFF를 사용하지 마십시오. SET FMTONLY OFF로 인해 대량 복사 작업이 실패하거나 예기치 않은 결과를 제공할 수도 있습니다.  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버 
 OLE DB Driver for SQL Server 대량 복사 작업을 수행 하기 위한 두 메서드를 구현 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스입니다. 첫 번째 방법은 메모리 기반 대량 복사 작업에 [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) 인터페이스를 사용하고 두 번째 방법은 파일 기반 대량 복사 작업에 [IBCPSession](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md) 인터페이스를 사용합니다.  
  
### <a name="using-memory-based-bulk-copy-operations"></a>메모리 기반 대량 복사 작업 사용  
 SQL Server용 OLE DB 드라이버는 **IRowsetFastLoad** 인터페이스를 구현하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 메모리 기반 대량 복사 작업에 대한 지원을 노출합니다. **IRowsetFastLoad** 인터페이스는 [IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) 및 [IRowsetFastLoad::InsertRow](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md) 메서드를 구현합니다.  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>IRowsetFastLoad에 세션 사용  
 소비자는 OLE DB Driver for SQL Server 관련 데이터 원본 속성 SSPROP_ENABLEFASTLOAD variant_true로 설정 하 여 대량 복사가 필요 하다는 SQL Server에 대 한 OLE DB 드라이버에 알립니다. 데이터 원본에 설정 속성을 사용 하 여 소비자는 SQL Server 세션에 대 한 OLE DB 드라이버를 만듭니다. 새 세션을 사용하여 소비자는 **IRowsetFastLoad** 인터페이스에 액세스할 수 있습니다.  
  
> [!NOTE]  
>  **IDataInitialize** 인터페이스가 데이터 원본 초기화에 사용되는 경우 **IOpenRowset::OpenRowset** 메서드의 *rgPropertySets* 매개 변수에 있는 SSPROP_IRowsetFastLoad 속성을 설정해야 합니다. 그렇지 않으면 **OpenRowset** 메서드를 호출할 때 E_NOINTERFACE가 반환됩니다.  
  
 OLE DB 드라이버 인터페이스에 대 한 SQL Server 지원에 대 한 세션에서 제한 대량 복사에 대 한 세션을 사용 하도록 설정 합니다. 대량 복사 사용 세션은 다음과 같은 인터페이스만 노출합니다.  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 대량 복사 사용 행 집합을 만들지 않고 SQL Server용 OLE DB 드라이버 세션이 표준 처리로 돌아가게 하려면 SSPROP_ENABLEFASTLOAD를 VARIANT_FALSE로 다시 설정합니다.  
  
#### <a name="irowsetfastload-rowsets"></a>IRowsetFastLoad 행 집합  
 SQL Server용 OLE DB 드라이버 대량 복사 행 집합은 쓰기 전용이지만 소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블의 구조를 결정할 수 있도록 하는 인터페이스를 노출합니다. 다음 인터페이스는 대량 복사 사용에서 노출 된 OLE DB Driver for SQL Server 행 집합:  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 공급자별 속성 SSPROP_FASTLOADOPTIONS, SSPROP_FASTLOADKEEPNULLS 및 SSPROP_FASTLOADKEEPIDENTITY는 SQL Server용 OLE DB 드라이버 대량 복사 행 집합의 동작을 제어합니다. 속성은 *rgPropertySets* **IOpenRowset** 매개 변수 멤버의 *rgProperties* 멤버에 지정됩니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|열: 아니요<br /><br /> R/w: 읽기/쓰기<br /><br /> 형식: VT_BOOL<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 소비자가 제공한 ID 값을 유지합니다.<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 있는 ID 열의 값은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 생성됩니다. 열에 바인딩된 모든 값은 SQL Server 용 OLE DB 드라이버에서 무시 됩니다.<br /><br /> VARIANT_TRUE: 소비자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ID 열의 값을 제공하는 접근자를 바인딩합니다. NULL을 허용하는 열에서는 ID 속성을 사용할 수 없으므로 소비자가 **IRowsetFastLoad::Insert**를 호출할 때마다 고유한 값을 제공합니다.|  
|SSPROP_FASTLOADKEEPNULLS|열: 아니요<br /><br /> R/w: 읽기/쓰기<br /><br /> 형식: VT_BOOL<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: DEFAULT 제약 조건이 있는 열에 대해 NULL을 유지합니다. NULL을 허용하고 DEFAULT 제약 조건이 적용된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열에만 영향을 줍니다.<br /><br /> VARIANT_FALSE: SQL Server용 OLE DB 드라이버 소비자가 열에 대해 NULL이 포함된 행을 삽입하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 열의 기본값을 삽입합니다.<br /><br /> VARIANT_TRUE: SQL Server용 OLE DB 드라이버 소비자가 열에 대해 NULL이 포함된 행을 삽입하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 열 값으로 NULL을 삽입합니다.|  
|SSPROP_FASTLOADOPTIONS|열: 아니요<br /><br /> R/w: 읽기/쓰기<br /><br /> 유형: VT_BSTR<br /><br /> 기본값: 없음<br /><br /> 설명: 이 속성은 **bcp** 유틸리티의 **-h** "*hint*[,...*n*]" 옵션과 같습니다. 데이터를 테이블로 대량 복사할 때 다음 문자열을 옵션으로 사용할 수 있습니다.<br /><br /> **순서**(*열*[**ASC** &#124; **DESC**] [,... *n*]): 데이터 파일에서 데이터의 순서를 정렬 합니다. 로드되는 데이터 파일을 테이블의 클러스터형 인덱스에 따라 정렬하면 대량 복사 성능이 향상됩니다.<br /><br /> **ROWS_PER_BATCH** = *bb*: 일괄 처리당 데이터 행 수 (으로 *bb*). 서버는 *bb*값에 따라 대량 로드를 최적화합니다. 기본적으로 **ROWS_PER_BATCH**는 알 수 없습니다.<br /><br /> **KILOBYTES_PER_BATCH** = *cc*: 수 (cc)으로 일괄 처리당 데이터의 크기 (KB)입니다. 기본적으로 **KILOBYTES_PER_BATCH**는 알 수 없습니다.<br /><br /> **TABLOCK**: 대량 복사 작업이 지속되는 동안 테이블 수준 잠금이 유지됩니다. 대량 복사 작업 동안에만 잠금을 사용하면 테이블의 잠금 경쟁이 줄어들기 때문에 이 옵션을 사용하면 성능이 훨씬 향상됩니다. 테이블에 인덱스가 없고 **TABLOCK**이 지정되어 있으면 여러 클라이언트가 동시에 테이블을 로드할 수 있습니다. 기본적으로 잠금 동작은 **table lock on bulk load** 테이블 옵션에 의해 결정됩니다.<br /><br /> **CHECK_CONSTRAINTS**: 대량 복사 작업 동안 *table_name*의 모든 제약 조건이 확인됩니다. 기본적으로 제약 조건은 무시됩니다.<br /><br /> **FIRE_TRIGGER**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 트리거에 대해 행 버전 관리를 사용하고 **tempdb**의 버전 저장소에 행 버전을 저장합니다. 따라서 트리거가 사용되는 경우에도 대량 로깅 최적화를 사용할 수 있습니다. 트리거를 사용하여 많은 행이 포함된 일괄 처리를 대량 가져오기 전에 **tempdb**의 크기를 확장해야 할 수도 있습니다.|  
  
### <a name="using-file-based-bulk-copy-operations"></a>파일 기반 대량 복사 작업 사용  
 SQL Server용 OLE DB 드라이버는 **IBCPSession** 인터페이스를 구현하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 파일 기반 대량 복사 작업에 대한 지원을 노출합니다. **IBCPSession** 인터페이스는 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md), [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md), [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md), [IBCPSession::BCPDone](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md), [IBCPSession::BCPExec](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md), [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md), [IBCPSession::BCPReadFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) 및 [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) 메서드를 구현합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [데이터 원본 속성&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 가져오기 성능 최적화](http://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  

