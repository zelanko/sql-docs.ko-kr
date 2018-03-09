---
title: "SQL Server 테이블 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1e7dbe9bee95c52ac0e34a79c92e93fd51f48e2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="creating-sql-server-tables"></a>SQL Server 테이블 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 된 **itabledefinition:: Createtable** 함수, 사용자가를 만들 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블. 소비자가 사용 하 여 **CreateTable** 가 생성 한 고유한 이름을 사용 하 여 소비자가 명명 한 영구 테이블을 영구 또는 임시 테이블을 만들려면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.  
  
 소비자가 호출 하는 경우 **itabledefinition:: Createtable**DBPROP_TBL_TEMPTABLE 속성의 값은 VARIANT_TRUE 인 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 소비자 대신 임시 테이블 이름을 생성 합니다. 소비자는 *pTableID* 의 매개 변수는 **CreateTable** NULL로 메서드. 에 의해 생성 된 이름 가진 임시 테이블은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 표시 되지 않습니다는 **테이블** 행 집합을 통해 액세스할 수 있지만 **IOpenRowset** 인터페이스입니다.  
  
 소비자는 테이블 이름을 지정 하는 경우는 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pTableID* 매개 변수를는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 이름의 테이블. 이때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 명명 제약 조건이 적용되며 테이블 이름은 영구 테이블이나 로컬 또는 전역 임시 테이블을 나타낼 수 있습니다. 자세한 내용은 참조 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)합니다. *ppTableID* 매개 변수는 NULL 일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 영구 또는 임시 테이블의 이름을 생성할 수 있습니다. 소비자가 설정 하는 경우는 *pTableID* 매개 변수를 NULL이 고 집합 *ppTableID* 올바른 DBID를 가리키도록\*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 있는 테이블의 기본 이름 반환는 *pwszName* 의 멤버는 *uName* 값을 가리키는 DBID의 합집합 *ppTableID*합니다. 만들려면를 임시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 명명 테이블 소비자는 OLE DB 테이블 속성 DBPROP_TBL_TEMPTABLE 설정에서 참조 되는 테이블 속성에 포함는 *rgPropertySets* 매개 변수입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 이름이 지정 된 임시 테이블은 로컬입니다.  
  
 **CreateTable** 이 DB_E_BADTABLEID를 반환 된 *eKind* 의 멤버는 *pTableID* 매개 변수는 DBKIND_NAME을 나타내지 않습니다.  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 사용  
 소비자 중 하나를 사용 하 여 열 데이터 형식을 나타낼 수 있습니다는 *pwszTypeName* 멤버 또는 *wType* 멤버입니다. 소비자에서 데이터 형식을 지정 하는 경우 *pwszTypeName*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 값을 무시 *wType*합니다.  
  
 사용 하는 경우는 *pwszTypeName* 멤버, 소비자를 사용 하 여 데이터 형식을 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 이름입니다. 올바른 데이터 형식 이름은 PROVIDER_TYPES 스키마 행 집합의 TYPE_NAME 열에 반환되는 값입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 OLE DB가 열거 하는 DBTYPE 값의 일부만 인식는 *wType* 멤버입니다. 자세한 내용은 참조 [ITableDefinition의 데이터 형식 매핑](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)합니다.  
  
> [!NOTE]  
>  **CreateTable** DB_E_BADTYPE을 반환 하거나 설정 하는 소비자는 *pTypeInfo* 또는 *pclsid* 멤버 열 데이터 형식을 지정 합니다.  
  
 소비자에 열 이름 지정의 *pwszName* 의 멤버는 *uName* 는 DBCOLUMNDESC의 union *dbcid* 멤버입니다. 열 이름은 유니코드 문자열로 지정합니다. *eKind* 소속 *dbcid* DBKIND_NAME 이어야 합니다. **CreateTable** DB_E_BADCOLUMNID를 반환 *eKind* 유효 하지 않을 경우 *pwszName* 가 NULL 인 경우 값 *pwszName* 유효 하지 않거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자입니다.  
  
 모든 열 속성을 테이블에 대해 정의된 모든 열에 사용할 수 있습니다. **CreateTable** 속성 값 설정이 충돌 하는 경우 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED 반환할 수 있습니다. **CreateTable** 잘못 된 열 속성을 설정 하는 경우 오류를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 만들기에 실패 합니다.  
  
 DBCOLUMNDESC의 열 속성이 나타내는 의미는 다음과 같습니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 만든 열에 identity 속성을 설정 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ID 속성은 테이블 내의 단일 열에 대해서만 유효합니다. 두 개 이상의 오류를 생성 하는 단일 열에 대 한 속성을 variant_true로 설정 하면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에서 테이블을 만들려고 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identity 속성에 대 한 에서만 유효는 **정수**, **숫자**, 및 **10 진수** 는 소수 자릿수가 0 인 경우 형식입니다. 다른 데이터 형식의 열에 속성을 variant_true로 설정 하면 오류가 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에서 테이블을 만들려고 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_AUTOINCREMENT 및 DBPROP_COL_NULLABLE이 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 및 *dwOption* dbprop_col_nullable이 dbpropoptions_required가 아니면 합니다. DBPROP_COL_AUTOINCREMENT 및 DBPROP_COL_NULLABLE이 모두 VARIANT_TRUE DB_E_ERRORSOCCURRED가 반환 및 *dwOption* 이 dbpropoptions_required 이면 dbprop_col_nullable 합니다. 열이 정의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identity 속성과 고 DBPROP_COL_NULLABLE *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정 됩니다.|  
|DBPROP_COL_DEFAULT|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명: 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열에 대 한 DEFAULT 제약 조건입니다.<br /><br /> *vValue* DBPROP 멤버 많은 형식 중 하나일 수 있습니다. *vValue.vt* 멤버에는 열의 데이터 형식과 호환 되는 유형을 지정 해야 합니다. 예를 들어 DBTYPE_WSTR로 정의된 열의 기본값으로 BSTR N/A를 정의하는 것은 서로 호환되므로 가능합니다. DBTYPE_R8 오류가 발생 하는 대로 정의 된 열에서 정의 하는 동일한 기본 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에서 테이블을 만들려고 합니다.|  
|DBPROP_COL_DESCRIPTION|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명: DBPROP_COL_DESCRIPTION 열 속성 구현 되지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.<br /><br /> *dwStatus* 소비자는 속성 값을 쓰려고 시도할 때 DBPROP 구조의 멤버가 DBPROPSTATUS_NOTSUPPORTED를 반환 합니다.<br /><br /> 속성 설정에 대 한 치명적인 오류를 구성 하지 않으며는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. 다른 매개 변수 값이 모두 올바르기만 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이 생성됩니다.|  
|DBPROP_COL_FIXEDLENGTH|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명:는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBPROP_COL_FIXEDLENGTH 소비자를 사용 하 여 열의 데이터 형식을 정의 하는 경우 데이터 형식 매핑을 확인 하는 *wType* 는 DBCOLUMNDESC의 멤버입니다. 자세한 내용은 참조 [ITableDefinition의 데이터 형식 매핑](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)합니다.|  
|DBPROP_COL_NULLABLE|R/w: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명: 테이블을 만들 때의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 속성을 설정 하는 경우 열 null 값을 허용 해야 하는지 여부를 나타냅니다. 해당 속성이 설정되어 있지 않으면 열의 NULL 값 허용 여부가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 기본 데이터베이스 옵션을 통해 확인됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 ISO 규격 공급자입니다. 연결된 세션에서는 ISO 동작을 따르므로 소비자가 DBPROP_COL_NULLABLE을 설정하지 않은 경우 열은 null 값을 허용합니다.|  
|DBPROP_COL_PRIMARYKEY|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 때 VARIANT_TRUE 이면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 PRIMARY KEY 제약 조건이 있는 열을 만듭니다.<br /><br /> 열 속성으로 정의된 경우 단일 열만 이 제약 조건을 확인할 수 있습니다. 두 개 이상의 오류를 반환 하는 단일 열에 VARIANT_TRUE 속성을 설정 하면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 유지 하려고 합니다.는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.<br /><br /> 참고: 소비자를 사용할 수 **iindexdefinition:: Createindex** 두 개 이상의 열에 PRIMARY KEY 제약 조건을 만들려고 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 및 *dwOption* DBPROP_COL_UNIQUE이 dbpropoptions_required가 아니면 합니다.<br /><br /> DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE DB_E_ERRORSOCCURRED가 반환 및 *dwOption* DBPROP_COL_UNIQUE이 dbpropoptions_required 이면 합니다. 열이 정의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identity 속성과 고 DBPROP_COL_PRIMARYKEY *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정 됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_NULLABLE이 모두 VARIANT_TRUE Native Client OLE DB 공급자는 오류를 반환 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 오류를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 잘못 된 열에 PRIMARY KEY 제약 조건을 만들 하려고 할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. PRIMARY KEY 제약 조건을 사용 하 여 만든 열에 정의할 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 **비트**, **텍스트**, **ntext**, 및 **이미지**합니다.|  
|DBPROP_COL_UNIQUE|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 적용 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열에 UNIQUE 제약 조건입니다.<br /><br /> 열 속성으로 정의된 경우 이 제약 조건은 단일 열에만 적용됩니다. 소비자 צ ְ ײ **iindexdefinition:: Createindex** 조합 된 값의 두 개 이상의 열에 UNIQUE 제약 조건을 적용 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 하 고 *dwOption* 이 dbpropoptions_required가 아니면 합니다.<br /><br /> DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE DB_E_ERRORSOCCURRED가 반환 하 고 *dwOption* 이 dbpropoptions_required 이면 합니다. 열이 정의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identity 속성과 고 DBPROP_COL_PRIMARYKEY *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정 됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_NULLABLE 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 하 고 *dwOption* 이 dbpropoptions_required가 아니면 합니다.<br /><br /> DBPROP_COL_NULLABLE 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE DB_E_ERRORSOCCURRED가 반환 하 고 *dwOption* 이 dbpropoptions_required 이면 합니다. 열이 정의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identity 속성과 고 DBPROP_COL_NULLABLE *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정 됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 오류를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 잘못 된 열에 UNIQUE 제약 조건을 만들 하려고 할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. UNIQUE 제약 조건을 사용 하 여 만든 열에 정의할 수 없습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **비트** 데이터 형식입니다.|  
  
 소비자가 호출 하는 경우 **itabledefinition:: Createtable**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 테이블 속성을 다음과 같이 해석 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 기본적으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 명명 한 테이블을 만듭니다. 때 VARIANT_TRUE 이면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 소비자 대신 임시 테이블 이름을 생성 합니다. 소비자는 *pTableID* 의 매개 변수 **CreateTable** NULL로 합니다. *ppTableID* 매개 변수에 대 한 유효한 포인터를 포함 되어야 합니다.|  
  
 소비자는 행 집합에 성공적으로 만든된 테이블에서 열 수를 요청 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 커서 지원 행 집합을 엽니다. 행 집합 속성은 전달하는 속성 집합에서 표시할 수 있습니다.  
  
 이 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만듭니다.  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 인덱스](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
