---
title: SQL Server 테이블 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 72a278a142889d8b9d1e43976939f06b002689d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069742"
---
# <a name="creating-sql-server-tables"></a>SQL Server 테이블 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **itabledefinition:: Createtable** 함수를 만들려면 소비자를 허용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 소비자가 사용 하 여 **CreateTable** 가 생성 한 고유한 이름을 사용 하 여 소비자가 명명 한 영구 테이블을 영구 또는 임시 테이블을 만들려면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.  
  
 소비자가 호출 하는 경우 **itabledefinition:: Createtable**DBPROP_TBL_TEMPTABLE 속성의 값은 VARIANT_TRUE 인 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 임시 테이블 이름을 생성 합니다. 소비자는 **CreateTable** 메서드의 *pTableID* 매개 변수를 NULL로 설정합니다. 가 생성 한 이름 가진 임시 테이블은는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 표시 되지 않습니다는 **테이블** 행 집합을 통해 액세스할 수 있지만 합니다 **IOpenRowset** 인터페이스.  
  
 소비자에서 테이블 이름을 지정 하는 경우는 *pwszName* 의 멤버는 *uName* 공용 구조체의 *pTableID* 매개 변수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 이름 가진 테이블입니다. 이때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 명명 제약 조건이 적용되며 테이블 이름은 영구 테이블이나 로컬 또는 전역 임시 테이블을 나타낼 수 있습니다. 자세한 내용은 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요. *ppTableID* 매개 변수는 NULL일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 영구 또는 임시 테이블의 이름을 생성할 수 있습니다. 소비자가 설정 하는 경우는 *pTableID* 매개 변수를 NULL 집합 *ppTableID* 올바른 DBID를 가리키도록\*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 생성 된 이름을 반환 합니다 테이블에 *pwszName* 의 멤버는 *uName* 의 값을 가리키는 DBID의 합집합 *ppTableID*합니다. 임시 키를 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 명명 테이블 소비자는 OLE DB 테이블 속성 DBPROP_TBL_TEMPTABLE는 테이블 속성에서 참조 된 집합에 포함 된 *rgPropertySets* 매개 변수입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 라는 임시 테이블은 로컬입니다.  
  
 *pTableID* 매개 변수의 *eKind* 멤버가 DBKIND_NAME을 나타내지 않으면 **CreateTable**이 DB_E_BADTABLEID를 반환합니다.  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 사용  
 소비자는 *pwszTypeName* 멤버나 *wType* 멤버를 사용하여 열 데이터 형식을 나타낼 수 있습니다. 소비자의 데이터 형식을 지정 하는 경우 *pwszTypeName*서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 값을 무시 *wType*합니다.  
  
 *pwszTypeName* 멤버를 사용하는 경우 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 이름을 사용하여 데이터 형식을 지정합니다. 올바른 데이터 형식 이름은 PROVIDER_TYPES 스키마 행 집합의 TYPE_NAME 열에 반환되는 값입니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 OLE DB가 열거 하는 DBTYPE 값의 하위 집합을 인식 합니다 *wType* 멤버입니다. 자세한 내용은 [ITableDefinition의 데이터 형식 매핑](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)합니다.  
  
> [!NOTE]  
>  소비자가 *pTypeInfo* 또는 *pclsid* 멤버를 설정하여 열 데이터 형식을 지정하면 **CreateTable**이 DB_E_BADTYPE을 반환합니다.  
  
 소비자는 DBCOLUMNDESC *dbcid* 멤버의 *uName* 공용 구조체에 있는 *pwszName* 멤버에 열 이름을 지정합니다. 열 이름은 유니코드 문자열로 지정합니다. *dbcid*의 *eKind* 멤버는 DBKIND_NAME이어야 합니다. *eKind*가 올바르지 않고 *pwszName*이 NULL이거나 *pwszName* 값이 올바른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자가 아니면 **CreateTable**이 DB_E_BADCOLUMNID를 반환합니다.  
  
 모든 열 속성을 테이블에 대해 정의된 모든 열에 사용할 수 있습니다. 속성 값 설정이 충돌될 경우 **CreateTable**이 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED를 반환할 수 있습니다. 잘못된 열 속성 설정으로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 생성에 실패할 경우 **CreateTable**이 오류를 반환합니다.  
  
 DBCOLUMNDESC의 열 속성이 나타내는 의미는 다음과 같습니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 생성 된 열에 identity 속성을 설정 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ID 속성은 테이블 내의 단일 열에 대해서만 유효합니다. 단일 열에 오류가 발생 하는 보다 자세한 속성을 variant_true로 설정 하면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에서 테이블을 만들려고 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성은 소수 자릿수가 0인 **integer**, **numeric** 및 **decimal** 형식에 대해서만 유효합니다. 다른 데이터 형식의 열에 속성을 variant_true로 설정 해도 오류가 발생 하면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에서 테이블을 만들려고 합니다.<br /><br /> 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_AUTOINCREMENT 및 DBPROP_COL_NULLABLE이 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 하며 *dwOption* dbprop_col_nullable 아닙니다 DBPROPOPTIONS_ 필수. DBPROP_COL_AUTOINCREMENT 및 DBPROP_COL_NULLABLE이 모두 VARIANT_TRUE이고 DBPROP_COL_NULLABLE의 *dwOption*이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_NULLABLE *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.|  
|DBPROP_COL_DEFAULT|R/W: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명: 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열의 기본 제약 조건입니다.<br /><br /> *vValue* DBPROP 멤버에는 개수에 관계없이 유형을 얼마든지 지정할 수 있습니다. *vValue.vt* 멤버에는 열 데이터 형식과 호환되는 유형을 지정해야 합니다. 예를 들어 DBTYPE_WSTR로 정의된 열의 기본값으로 BSTR N/A를 정의하는 것은 서로 호환되므로 가능합니다. 오류가 dbtype_r8로 정의 된 열에 동일한 기본 정의 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에서 테이블을 만들려고 합니다.|  
|DBPROP_COL_DESCRIPTION|R/W: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명: DBPROP_COL_DESCRIPTION 열 속성 구현 되지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.<br /><br /> 소비자가 속성 값을 쓰려고 하면 DBPROP 구조의 *dwStatus* 멤버가 DBPROPSTATUS_NOTSUPPORTED를 반환합니다.<br /><br /> 속성 설정에 대 한 심각한 오류를 구성 하지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. 다른 매개 변수 값이 모두 올바르기만 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이 생성됩니다.|  
|DBPROP_COL_FIXEDLENGTH|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBPROP_COL_FIXEDLENGTH를 통해 소비자를 사용 하 여 열의 데이터 형식을 정의 하는 경우 데이터 형식 매핑을 확인 합니다 *wType* DBCOLUMNDESC의 멤버입니다. 자세한 내용은 [ITableDefinition의 데이터 형식 매핑](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)합니다.|  
|DBPROP_COL_NULLABLE|R/W: 읽기/쓰기<br /><br /> 기본값: 없음<br /><br /> 설명: 테이블을 만들 때의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 속성을 설정 하는 경우는 열의 null 값을 허용 해야 하는지 여부를 나타냅니다. 해당 속성이 설정되어 있지 않으면 열의 NULL 값 허용 여부가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 기본 데이터베이스 옵션을 통해 확인됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 ISO 규격 공급자입니다. 연결된 세션에서는 ISO 동작을 따르므로 소비자가 DBPROP_COL_NULLABLE을 설정하지 않은 경우 열은 null 값을 허용합니다.|  
|DBPROP_COL_PRIMARYKEY|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 때 VARIANT_TRUE 이면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 PRIMARY KEY 제약 조건을 사용 하 여 열을 만듭니다.<br /><br /> 열 속성으로 정의된 경우 단일 열만 이 제약 조건을 확인할 수 있습니다. 오류를 반환 하는 단일 열 보다 자세한 VARIANT_TRUE 속성을 설정 때 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 만들려고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.<br /><br /> 참고: 소비자가 사용할 수 있습니다 **iindexdefinition:: Createindex** 두 개 이상의 열에 PRIMARY KEY 제약 조건을 만들려면.<br /><br /> 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 하며 *dwOption* DBPROP_COL_UNIQUE이 dbpropoptions_required가 아니면 합니다.<br /><br /> DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE이고 DBPROP_COL_UNIQUE의 *dwOption*이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_PRIMARYKEY *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_NULLABLE이 모두 VARIANT_TRUE Native Client OLE DB 공급자 오류를 반환 합니다.<br /><br /> 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 오류를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 잘못 된 열에 PRIMARY KEY 제약 조건을 만들 하려고 할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. **bit**, **text**, **ntext**, **image** 등의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 사용하여 만든 열에 대해서는 PRIMARY KEY 제약 조건을 정의할 수 없습니다.|  
|DBPROP_COL_UNIQUE|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 적용 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열에 UNIQUE 제약 조건입니다.<br /><br /> 열 속성으로 정의된 경우 이 제약 조건은 단일 열에만 적용됩니다. 소비자는 **IIndexDefinition::CreateIndex**를 사용하여 둘 이상의 결합된 열 값에 대해 UNIQUE 제약 조건을 적용할 수 있습니다.<br /><br /> 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 하 고 *dwOption* 이 dbpropoptions_required가 아니면 합니다.<br /><br /> DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE이고 *dwOption*이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_PRIMARYKEY *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.<br /><br /> 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_NULLABLE 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE Native Client OLE DB 공급자가 DB_S_ERRORSOCCURRED를 반환 하 고 *dwOption* 이 dbpropoptions_required가 아니면 합니다.<br /><br /> DBPROP_COL_NULLABLE 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE이고 *dwOption*이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_NULLABLE *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.<br /><br /> 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 오류를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 잘못 된 열에 UNIQUE 제약 조건을 만들 하려고 할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** 데이터 형식을 사용하여 만든 열에 대해서는 UNIQUE 제약 조건을 정의할 수 없습니다.|  
  
 소비자가 호출 하는 경우 **itabledefinition:: Createtable**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 테이블 속성을 다음과 같이 해석 합니다.  
  
|속성 ID|설명|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 명명 한 테이블을 만듭니다. 때 VARIANT_TRUE 이면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 임시 테이블 이름을 생성 합니다. 소비자는 **CreateTable**의 *pTableID* 매개 변수를 NULL로 설정합니다. *ppTableID* 매개 변수는 올바른 포인터를 포함해야 합니다.|  
  
 소비자가 행 집합을 성공적으로 생성된 된 테이블에서 열 수를 요청 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 커서 지원 행 집합을 엽니다. 행 집합 속성은 전달하는 속성 집합에서 표시할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [테이블 및 인덱스](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
