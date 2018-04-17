---
title: 대량 복사 작업 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [SQL Server Native Client]
- data access [SQL Server Native Client], bulk copy operations
- SQL Server Native Client, bulk copy operations
- SQLNCLI, bulk copy operations
ms.assetid: 50d8456b-e6a1-4b25-bc7e-56946ed654a7
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7876fcc39108f5b94bd3c63cdcf6547b568fdbab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="performing-bulk-copy-operations"></a>대량 복사 작업 수행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대량 복사 기능은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블 또는 뷰와의 대량 데이터 전송을 지원합니다. SELECT 문을 지정하여 데이터를 전송할 수도 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 ASCII 파일과 같은 운영 체제 데이터 파일 간에 데이터를 이동할 수 있습니다. 데이터 파일은 다른 형식을 가질 수 있습니다. 형식은 형식 파일에서 대량 복사로 정의됩니다. 필요에 따라 데이터를 프로그램 변수로 로드하고 대량 복사 함수와 메서드를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전송할 수 있습니다.  
  
 이 기능을 보여 주는 샘플 응용 프로그램을 참조 하십시오. [대량 복사 데이터를 사용 하 여 IRowsetFastLoad &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)합니다.  
  
 응용 프로그램은 보통 다음 두 가지 방법 중 하나로 대량 복사를 사용합니다.  
  
-   Transact-SQL 문의 테이블, 뷰 또는 결과 집합에서 데이터가 테이블 또는 뷰와 동일한 형식으로 저장되는 데이터 파일로 대량 복사합니다.  
  
     이것을 기본 모드 데이터 파일이라고 합니다.  
  
-   Transact-SQL 문의 테이블, 뷰 또는 결과 집합에서 데이터가 테이블 또는 뷰 중 하나와 다른 형식으로 저장되는 데이터 파일로 대량 복사합니다.  
  
     이 경우 데이터 파일에 저장되는 각 열의 특징(데이터 형식, 위치, 길이, 종결자 등)을 정의하는 별도의 형식 파일이 만들어집니다. 모든 열이 문자 형식으로 변환된 경우 결과 파일을 문자 모드 데이터 파일이라고 합니다.  
  
-   데이터 파일에서 테이블 또는 뷰로 대량 복사합니다.  
  
     필요한 경우 형식 파일을 사용하여 데이터 파일의 레이아웃을 결정합니다.  
  
-   데이터를 프로그램 변수로 로드한 다음 한 번에 한 행씩, 대량 복사하기 위한 대량 복사 함수를 사용하여 데이터를 테이블 또는 뷰로 가져옵니다.  
  
 다른 대량 복사 프로그램에서 대량 복사 함수에 사용되는 데이터 파일을 만들 필요는 없습니다. 대량 복사 정의에 따라 다른 모든 시스템에서 데이터 파일과 형식 파일을 생성할 수 있습니다. 이러한 파일을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대량 복사 프로그램과 함께 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 가져올 수 있습니다. 예를 들어 탭으로 구분된 파일의 스프레드시트에서 데이터를 내보내고, 탭으로 구분된 파일을 설명하는 형식 파일을 작성한 다음 대량 복사 프로그램을 사용하여 신속하게 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 가져올 수 있습니다. 대량 복사에서 생성된 데이터 파일을 다른 응용 프로그램으로 가져올 수도 있습니다. 예를 들어 대량 복사 함수를 사용하여 테이블 또는 뷰의 데이터를 탭으로 구분된 파일로 내보낸 다음 스프레드시트에 로드할 수 있습니다.  
  
 대량 복사 함수를 사용할 응용 프로그램을 코딩하는 프로그래머가 우수한 대량 복사 성능을 얻으려면 일반 규칙을 따라야 합니다. 대량 복사 작업에 대 한 지원에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 참조 [대량 데이터 가져오기 및 내보내기의 &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 CLR UDT(사용자 정의 형식)를 이진 데이터로 바인딩해야 합니다. 형식 파일에서 SQLCHAR를 대상 UDT 열의 데이터 형식으로 지정하는 경우에도 BCP 유틸리티는 해당 데이터를 이진으로 처리합니다.  
  
 대량 복사 작업에는 SET FMTONLY OFF를 사용하지 마십시오. SET FMTONLY OFF로 인해 대량 복사 작업이 실패하거나 예기치 않은 결과를 제공할 수도 있습니다.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 대량 복사 작업을 수행 하기 위한 두 메서드를 구현 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스입니다. 첫 번째 방법은 사용 하 여는 [IRowsetFastLoad](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 메모리 기반 대량 복사 작업 하 고 두 번째 인터페이스를 사용 하는 것은 [IBCPSession](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md) 파일 기반 대량 복사 작업에 대 한 인터페이스입니다.  
  
### <a name="using-memory-based-bulk-copy-operations"></a>메모리 기반 대량 복사 작업 사용  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 구현 하는 **IRowsetFastLoad** 인터페이스에 대 한 지원을 공개 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 메모리 기반 대량 복사 작업입니다. **IRowsetFastLoad** 구현는 [irowsetfastload:: Commit](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) 및 [irowsetfastload:: Insertrow](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md) 메서드.  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>IRowsetFastLoad에 세션 사용  
 소비자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자별 데이터 원본 속성 SSPROP_ENABLEFASTLOAD를 VARIANT_TRUE로 설정하여 대량 복사가 필요하다는 것을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 알립니다. 데이터 원본의 속성 집합을 사용하여 소비자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션을 만듭니다. 새 세션에 소비자 액세스할 수 있습니다는 **IRowsetFastLoad** 인터페이스입니다.  
  
> [!NOTE]  
>  경우는 **IDataInitialize** SSPROP_IRowsetFastLoad 속성을 설정 해야 하는 다음 인터페이스는 데이터 원본 초기화에 사용 되는 *rgPropertySets* 의 매개 변수는  **Iopenrowset:: Openrowset** 메서드, 그렇지 않으면에 대 한 호출에서 **OpenRowset** 메서드 하면 e_nointerface가 반환 됩니다.  
  
 대량 복사에 세션을 사용하면 세션의 인터페이스에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 지원이 제한됩니다. 대량 복사 사용 세션은 다음과 같은 인터페이스만 노출합니다.  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 대량 복사 사용 행 집합을 만들지 않고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션이 표준 처리로 돌아가게 하려면 SSPROP_ENABLEFASTLOAD를 VARIANT_FALSE로 다시 설정합니다.  
  
#### <a name="irowsetfastload-rowsets"></a>IRowsetFastLoad 행 집합  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 대량 복사 행 집합은 쓰기 전용이지만 소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블의 구조를 결정할 수 있도록 하는 인터페이스를 노출합니다. 대량 복사 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 행 집합에는 다음과 같은 인터페이스가 노출됩니다.  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 공급자별 속성 SSPROP_FASTLOADOPTIONS, SSPROP_FASTLOADKEEPNULLS 및 SSPROP_FASTLOADKEEPIDENTITY는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 대량 복사 행 집합의 동작을 제어합니다. 속성에 지정 된 된 *rgProperties* 의 멤버는 * rgPropertySets ***IOpenRowset**매개 변수 멤버입니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|열: 아니요<br /><br /> R/w: 읽기/쓰기<br /><br /> 형식: VT_BOOL<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 소비자가 제공한 id 값 유지 관리 합니다.<br /><br /> VARIANT_FALSE: id 열에 대 한 값은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 의해 생성 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 열에서 무시 됩니다에 대 한 바인딩된 모든 값은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.<br /><br /> VARIANT_TRUE: 소비자에 대 한 값을 제공 하는 접근자를 바인딩하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] id 열입니다. Identity 속성에서 사용할 수 없으면 소비자가 각 고유한 값을 제공 하므로 NULL을 허용 하는 열 **irowsetfastload:: Insert** 호출 합니다.|  
|SSPROP_FASTLOADKEEPNULLS|열: 아니요<br /><br /> R/w: 읽기/쓰기<br /><br /> 형식: VT_BOOL<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: DEFAULT 제약 조건이 있는 열에 NULL을 유지 합니다. NULL을 허용하고 DEFAULT 제약 조건이 적용된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열에만 영향을 줍니다.<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 열에 대해 NULL이 포함된 행을 삽입하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 열의 기본값을 삽입합니다.<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 열에 대해 NULL이 포함된 행을 삽입하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 열 값으로 NULL을 삽입합니다.|  
|SSPROP_FASTLOADOPTIONS|열: 아니요<br /><br /> R/w: 읽기/쓰기<br /><br /> 유형: VT_BSTR<br /><br /> 기본값: 없음<br /><br /> 설명:이 속성은 동일는 **-h** "*힌트*[,... *n*] "의 옵션은 **bcp** 유틸리티입니다. 데이터를 테이블로 대량 복사할 때 다음 문자열을 옵션으로 사용할 수 있습니다.<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,... *n*]): 데이터 파일의 데이터의 순서를 정렬 합니다. 로드되는 데이터 파일을 테이블의 클러스터형 인덱스에 따라 정렬하면 대량 복사 성능이 향상됩니다.<br /><br /> **ROWS_PER_BATCH** = *bb*: 일괄 처리당 데이터 행 수 (으로 *bb*). 서버는 *bb*값에 따라 대량 로드를 최적화합니다. 기본적으로 **ROWS_PER_BATCH** 를 알 수 없습니다.<br /><br /> **KILOBYTES_PER_BATCH** = *cc*: 수 (cc)으로 일괄 처리당 데이터의 크기 (KB)입니다. 기본적으로 **KILOBYTES_PER_BATCH** 를 알 수 없습니다.<br /><br /> **TABLOCK**: 대량 복사 작업 동안 테이블 수준 잠금이 획득 됩니다. 대량 복사 작업 동안에만 잠금을 사용하면 테이블의 잠금 경쟁이 줄어들기 때문에 이 옵션을 사용하면 성능이 훨씬 향상됩니다. 테이블 동시 로드할 수 있습니다 여러 클라이언트에서 테이블에 인덱스가 없는 경우 및 **TABLOCK** 지정 됩니다. 기본적으로 잠금 동작은 테이블 옵션에 의해 결정 **테이블에 대량 로드 잠금**합니다.<br /><br /> **CHECK_CONSTRAINTS**: 대 한 제약 조건을 *table_name* 대량 복사 작업 동안 확인 됩니다. 기본적으로 제약 조건은 무시됩니다.<br /><br /> **FIRE_TRIGGER**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 트리거에 대 한 행 버전 관리를 사용 하 고는 버전 저장소에 행 버전을 저장 **tempdb**합니다. 따라서 트리거가 사용되는 경우에도 대량 로깅 최적화를 사용할 수 있습니다. 크기를 확장 해야 할 수 있는 많은 수의 행 일괄 처리 트리거가 설정 된 상태 가져오기 대량, 전에 **tempdb**합니다.|  
  
### <a name="using-file-based-bulk-copy-operations"></a>파일 기반 대량 복사 작업 사용  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 구현 하는 **IBCPSession** 인터페이스에 대 한 지원을 공개 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 파일 기반 대량 복사 작업입니다. **IBCPSession** 구현는 [ibcpsession:: Bcpcolfmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md), [ibcpsession:: Bcpcolumns](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md), [ibcpsession:: Bcpcontrol](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md), [Ibcpsession:: Bcpdone](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md), [ibcpsession:: Bcpexec](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md), [ibcpsession:: Bcpinit](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md), [ibcpsession:: Bcpreadfmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md), 및 [ibcpsession:: Bcpwritefmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)메서드.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC 드라이버에 포함된 대량 복사 작업에 대해 동일한 지원을 유지합니다. 사용 하 여 대량 복사 작업에 대 한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 참조 [대량 복사 작업 수행 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [데이터 원본 속성 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 가져오기 성능 최적화](http://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  
  
  
