---
title: SQL Server 인덱스 만들기 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하는 SQL Server 인덱스 만들기
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
- adding indexes
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: bdb8b8f48a4a54a185f6ffae03cf129e4549641b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612922"
---
# <a name="creating-sql-server-indexes"></a>SQL Server 인덱스 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Serve 용 OLE DB 드라이버는 소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 새 인덱스를 정의할 수 있도록 **IIndexDefinition::CreateIndex** 함수를 노출합니다.  
  
 OLE DB Driver for SQL Server 테이블 인덱스를 인덱스나 제약 조건으로 만듭니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 테이블 소유자, 데이터베이스 소유자 및 특정 관리 역할이 멤버에게 제약 조건 생성 권한을 부여합니다. 기본적으로 테이블 소유자만 테이블에 인덱스를 만들 수 있습니다. 따라서 **CreateIndex**의 성공 또는 실패 여부는 애플리케이션 사용자의 액세스 권한뿐만 아니라 생성되는 인덱스의 유형에 따라서도 영향을 받습니다.  
  
 소비자는 *pTableID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 테이블 이름을 유니코드 문자열로 지정합니다. *pTableID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다.  
  
 *pIndexID* 매개 변수는 NULL일 수 있으며, 이 경우 SQL Serve용 OLE DB 드라이버가 인덱스의 고유 이름을 만듭니다. 소비자는 *ppIndexID* 매개 변수에 DBID에 대한 유효한 포인터를 지정하여 인덱스의 이름을 캡처할 수 있습니다.  
  
 소비자는 *pIndexID* 매개 변수의 에서 *uName* 공용 구조체에 있는 *pwszName*멤버에 인덱스 이름을 유니코드 문자열로 지정합니다. *pIndexID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다.  
  
 소비자는 인덱스에 참여하는 열을 이름으로 지정합니다. **CreateIndex**에 사용된 각 DBINDEXCOLUMNDESC 구조에 대해 *pColumnID*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다. 열 이름은 *pColumnID*의 *uName* 공용 구조체에 있는 *pwszName* 멤버에 유니코드 문자열로 지정됩니다.  
  
 OLE DB Driver for SQL Server 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인덱스의 값에 대해 오름차순을 지원 합니다. 소비자가 임의의 DBINDEXCOLUMNDESC 구조에 DBINDEX_COL_ORDER_DESC를 지정하면 SQL Serve용 OLE DB 드라이버는 E_INVALIDARG를 반환합니다.  
  
 **CreateIndex**는 인덱스 속성을 다음과 같이 해석합니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 OLE DB Driver for SQL Server는이 속성을 지원 하지 않습니다. **CreateIndex**에서 속성을 설정하려고 하면 DB_S_ERRORSOCCURRED 값이 반환됩니다. 속성 구조의 *dwStatus* 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_CLUSTERED|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 인덱스 클러스터링을 제어 합니다.<br /><br /> VARIANT_TRUE:는 OLE DB Driver for SQL Server에서 클러스터형된 인덱스를 만들려고 시도 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 각 테이블에서 클러스터형 인덱스 한 개만 지원합니다.<br /><br /> VARIANT_FALSE:는 OLE DB Driver for SQL Server에서 비클러스터형 인덱스를 만들려고 시도 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블입니다.|  
|DBPROP_INDEX_FILLFACTOR|R/w: 읽기/쓰기<br /><br /> 기본값: 0<br /><br /> 설명: 스토리지에 사용되는 인덱스 페이지의 백분율을 지정합니다. 자세한 내용은 [CREATE INDEX](../../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.<br /><br /> 변형 유형은 VT_I4입니다. 값은 1 이상 100 이하여야 합니다.|  
|DBPROP_INDEX_INITIALIZE|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 OLE DB Driver for SQL Server는이 속성을 지원 하지 않습니다. **CreateIndex**에서 속성을 설정하려고 하면 DB_S_ERRORSOCCURRED 값이 반환됩니다. 속성 구조의 *dwStatus* 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_NULLCOLLATION|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 OLE DB Driver for SQL Server는이 속성을 지원 하지 않습니다. **CreateIndex**에서 속성을 설정하려고 하면 DB_S_ERRORSOCCURRED 값이 반환됩니다. 속성 구조의 *dwStatus* 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_NULLS|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 OLE DB Driver for SQL Server는이 속성을 지원 하지 않습니다. **CreateIndex**에서 속성을 설정하려고 하면 DB_S_ERRORSOCCURRED 값이 반환됩니다. 속성 구조의 *dwStatus* 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_PRIMARYKEY|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 무결성, PRIMARY KEY 제약 조건으로 인덱스를 만듭니다.<br /><br /> VARIANT_TRUE: 테이블의 PRIMARY KEY 제약 조건을 지원하기 위해 인덱스가 생성됩니다. 열은 Null이 아니어야 합니다.<br /><br /> VARIANT_FALSE: 인덱스가 테이블의 행 값에 대한 PRIMARY KEY 제약 조건으로 사용되지 않습니다.|  
|DBPROP_INDEX_SORTBOOKMARKS|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 OLE DB Driver for SQL Server는이 속성을 지원 하지 않습니다. **CreateIndex**에서 속성을 설정하려고 하면 DB_S_ERRORSOCCURRED 값이 반환됩니다. 속성 구조의 *dwStatus* 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_TEMPINDEX|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 OLE DB Driver for SQL Server는이 속성을 지원 하지 않습니다. **CreateIndex**에서 속성을 설정하려고 하면 DB_S_ERRORSOCCURRED 값이 반환됩니다. 속성 구조의 *dwStatus* 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_TYPE|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명:는 OLE DB Driver for SQL Server는이 속성을 지원 하지 않습니다. **CreateIndex**에서 속성을 설정하려고 하면 DB_S_ERRORSOCCURRED 값이 반환됩니다. 속성 구조의 *dwStatus* 멤버는 DBPROPSTATUS_BADVALUE를 나타냅니다.|  
|DBPROP_INDEX_UNIQUE|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 참여하는 열의 UNIQUE 제약 조건으로 인덱스를 만듭니다.<br /><br /> VARIANT_TRUE: 인덱스를 사용하여 테이블의 행 값을 고유하게 제한합니다.<br /><br /> VARIANT_FALSE: 인덱스가 행 값을 고유하게 제한하지 않습니다.|  
  
 공급자별 속성 집합 DBPROPSET_SQLSERVERINDEX에서 SQL Server용 OLE DB 드라이버는 다음과 같은 데이터 원본 정보 속성을 정의합니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|형식: VT_BOOL (R/W)<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: IIndexDefinition::CreateIndex에 VARIANT_TRUE 값을 사용하여 이 속성을 지정하면 인덱싱되는 열에 해당하는 기본 XML 인덱스가 생성됩니다. 이 속성이 VARIANT_TRUE이면 cIndexColumnDescs는 1이어야 합니다. 그렇지 않으면 오류가 발생합니다.|  
  
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
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
