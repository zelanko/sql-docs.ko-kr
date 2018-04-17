---
title: SQL Server 인덱스 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 11b93f96ba5e508310e27616d4f4c869adf5d05e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="creating-sql-server-indexes"></a>SQL Server 인덱스 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 된 **iindexdefinition:: Createindex** 소비자에 새 인덱스를 정의할 수 있는 함수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 인덱스나 제약 조건으로 테이블 인덱스를 만듭니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 테이블 소유자, 데이터베이스 소유자 및 특정 관리 역할이 멤버에게 제약 조건 생성 권한을 부여합니다. 기본적으로 테이블 소유자만 테이블에 인덱스를 만들 수 있습니다. 따라서의 성공 또는 실패 **CreateIndex** 뿐만 아니라 응용 프로그램 사용자의 액세스 권한 뿐만 작성 된 인덱스의 형식에 따라 달라 집니다.  
  
 소비자의 유니코드 문자열에서 테이블 이름을 지정는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *pTableID* 매개 변수입니다. *eKind* 소속 *pTableID* DBKIND_NAME 이어야 합니다.  
  
 *pIndexID* null, null, 및 인 경우 매개 변수 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 인덱스에 대 한 고유 이름을 만듭니다. 소비자는 DBID에 대 한 유효한 포인터를 지정 하 여 인덱스의 이름을 캡처할 수는 *ppIndexID* 매개 변수입니다.  
  
 소비자의 유니코드 문자열 인덱스 이름을 지정할 수는 *pwszName* 의 멤버는 *uName* 의 공용 구조체는 *pIndexID* 매개 변수입니다. *eKind* 소속 *pIndexID* DBKIND_NAME 이어야 합니다.  
  
 소비자는 인덱스에 참여하는 열을 이름으로 지정합니다. 에 사용 된 각 DBINDEXCOLUMNDESC 구조에 대 한 **CreateIndex**, *eKind* 의 멤버는 *pColumnID* DBKIND_NAME 이어야 합니다. 열 이름은 유니코드 문자열에으로 지정 됩니다는 *pwszName* 의 멤버는 *uName* 공용 구조체는 *pColumnID*합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스의 값에 대해 오름차순을 지원 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 임의의 DBINDEXCOLUMNDESC 구조에 DBINDEX_COL_ORDER_DESC를 지정 하는 경우 Native Client OLE DB 공급자는 E_INVALIDARG를 반환 합니다.  
  
 **CreateIndex** 인덱스 속성을 다음과 같이 해석 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 속성을 지원 하지 않습니다. 속성을 설정 하려고 **CreateIndex** DB_S_ERRORSOCCURRED 반환 값이 발생 합니다. *dwStatus* 속성 구조체의 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_CLUSTERED|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 인덱스 클러스터링을 제어 합니다.<br /><br /> VARIANT_TRUE:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 클러스터형된 인덱스를 만들려고 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 각 테이블에서 클러스터형 인덱스 한 개만 지원합니다.<br /><br /> VARIANT_FALSE:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 비클러스터형 인덱스를 만들려고 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.|  
|DBPROP_INDEX_FILLFACTOR|R/w: 읽기/쓰기<br /><br /> 기본값: 0<br /><br /> 설명: 저장소에 사용 되는 인덱스 페이지의 비율을 지정 합니다. 자세한 내용은 참조 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)합니다.<br /><br /> 변형 유형은 VT_I4입니다. 값은 1 이상 100 이하여야 합니다.|  
|DBPROP_INDEX_INITIALIZE|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 속성을 지원 하지 않습니다. 속성을 설정 하려고 **CreateIndex** DB_S_ERRORSOCCURRED 반환 값이 발생 합니다. *dwStatus* 속성 구조체의 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_NULLCOLLATION|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 속성을 지원 하지 않습니다. 속성을 설정 하려고 **CreateIndex** DB_S_ERRORSOCCURRED 반환 값이 발생 합니다. *dwStatus* 속성 구조체의 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_NULLS|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 속성을 지원 하지 않습니다. 속성을 설정 하려고 **CreateIndex** DB_S_ERRORSOCCURRED 반환 값이 발생 합니다. *dwStatus* 속성 구조체의 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_PRIMARYKEY|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 참조 무결성, PRIMARY KEY 제약 조건으로 인덱스를 만듭니다.<br /><br /> VARIANT_TRUE: 인덱스 테이블의 PRIMARY KEY 제약 조건을 지원 하기 위해 생성 됩니다. 열은 Null이 아니어야 합니다.<br /><br /> VARIANT_FALSE:의 인덱스가 사용 되지 않습니다는 PRIMARY KEY 제약 조건으로 테이블의 행 값에 대 한 합니다.|  
|DBPROP_INDEX_SORTBOOKMARKS|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 속성을 지원 하지 않습니다. 속성을 설정 하려고 **CreateIndex** DB_S_ERRORSOCCURRED 반환 값이 발생 합니다. *dwStatus* 속성 구조체의 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_TEMPINDEX|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 속성을 지원 하지 않습니다. 속성을 설정 하려고 **CreateIndex** DB_S_ERRORSOCCURRED 반환 값이 발생 합니다. *dwStatus* 속성 구조체의 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_TYPE|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 속성을 지원 하지 않습니다. 속성을 설정 하려고 **CreateIndex** DB_S_ERRORSOCCURRED 반환 값이 발생 합니다. *dwStatus* 속성 구조체의 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_UNIQUE|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 참여 열 또는 열에 UNIQUE 제약 조건으로 인덱스를 만듭니다.<br /><br /> VARIANT_TRUE: 고유 테이블의 행 값을 제한 하는 인덱스가 사용 됩니다.<br /><br /> VARIANT_FALSE: 인덱스는 고유 하 게 제한 하지 행 값.|  
  
 공급자별 속성 집합 dbpropset_sqlserverindex에 다음과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음 데이터 원본 정보 속성을 정의 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|형식: VT_BOOL (R/W)<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명:이 속성 iindexdefinition:: Createindex에 variant_true 값을 지정 하는 경우 만들어지는 인덱싱되는 열에 해당 하는 기본 xml 인덱스에 발생 합니다. 이 속성이 VARIANT_TRUE이면 cIndexColumnDescs는 1이어야 합니다. 그렇지 않으면 오류가 발생합니다.|  
  
 다음 예에서는 기본 키 인덱스를 만듭니다.  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 인덱스](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
