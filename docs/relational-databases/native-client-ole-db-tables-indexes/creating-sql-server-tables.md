---
title: SQL Server 테이블 만들기 (Native Client OLE DB 공급자) | Microsoft Docs
description: SQL Server Native Client OLE DB 공급자가 소비자가 SQL Server 테이블을 만들 수 있도록 하는 함수를 노출 하는 방법에 대해 알아봅니다.
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a777ec24b0099e6ad4c98ed4f9d42d38f785de36
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484935"
---
# <a name="creating-sql-server-native-client-tables"></a>SQL Server Native Client 테이블 만들기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 **Itabledefinition:: CreateTable** 함수를 제공 하 여 소비자가 테이블을 만들 수 있도록 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 소비자는 **CreateTable** 을 사용 하 여 소비자 이름 영구 테이블을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 생성 한 고유한 이름을 가진 영구 또는 임시 테이블을 만듭니다.  
  
 소비자가 **Itabledefinition:: CreateTable** 를 호출 하는 경우 DBPROP_TBL_TEMPTABLE 속성 값이 VARIANT_TRUE 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 소비자에 대 한 임시 테이블 이름을 생성 합니다. 소비자는 **CreateTable** 메서드의 *pTableID* 매개 변수를 NULL로 설정합니다. Native Client OLE DB 공급자에 의해 생성 된 이름을 가진 임시 테이블은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **테이블** 행 집합에 표시 되지 않지만 **iopenrowset** 인터페이스를 통해 액세스할 수 있습니다.  
  
 소비자가 *pTableID* 매개 변수에서 *uName* 공용 구조체의 *pwszName* 멤버에 테이블 이름을 지정 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해당 이름의 테이블을 만듭니다. 이때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 명명 제약 조건이 적용되며 테이블 이름은 영구 테이블이나 로컬 또는 전역 임시 테이블을 나타낼 수 있습니다. 자세한 내용은 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요. *ppTableID* 매개 변수는 NULL일 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 영구 또는 임시 테이블의 이름을 생성할 수 있습니다. 소비자가 *pTableID* 매개 변수를 NULL로 설정 하 고 *ppTableID* 를 설정 하 여 유효한 dbid를 가리키도록 하면 \* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 *ppTableID* 값이 가리키는 DBID의 *uName* 공용 구조체의 *pwszName* 멤버에 생성 된 테이블 이름을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *RgPropertySets* 매개 변수에서 참조 하는 테이블 속성 집합에 DBPROP_TBL_TEMPTABLE OLE DB 테이블 속성을 포함 하는 임시 Native Client OLE DB 공급자 이름 테이블을 만듭니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 이름 임시 테이블은 로컬입니다.  
  
 *pTableID* 매개 변수의 *eKind* 멤버가 DBKIND_NAME을 나타내지 않으면 **CreateTable** 이 DB_E_BADTABLEID를 반환합니다.  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 사용  
 소비자는 *pwszTypeName* 멤버나 *wType* 멤버를 사용하여 열 데이터 형식을 나타낼 수 있습니다. 소비자가 *pwszTypeName* 에서 데이터 형식을 지정 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 *wtype* 의 값을 무시 합니다.  
  
 *pwszTypeName* 멤버를 사용하는 경우 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 이름을 사용하여 데이터 형식을 지정합니다. 올바른 데이터 형식 이름은 PROVIDER_TYPES 스키마 행 집합의 TYPE_NAME 열에 반환되는 값입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 *wtype* 멤버에서 OLE DB 열거 DBTYPE 값의 하위 집합을 인식 합니다. 자세한 내용은 [ITableDefinition의 데이터 형식 매핑](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)을 참조하세요.  
  
> [!NOTE]  
>  소비자가 *pTypeInfo* 또는 *pclsid* 멤버를 설정하여 열 데이터 형식을 지정하면 **CreateTable** 이 DB_E_BADTYPE을 반환합니다.  
  
 소비자는 DBCOLUMNDESC *dbcid* 멤버의 *uName* 공용 구조체에 있는 *pwszName* 멤버에 열 이름을 지정합니다. 열 이름은 유니코드 문자열로 지정합니다. *dbcid* 의 *eKind* 멤버는 DBKIND_NAME이어야 합니다. *eKind* 가 올바르지 않고 *pwszName* 이 NULL이거나 *pwszName* 값이 올바른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자가 아니면 **CreateTable** 이 DB_E_BADCOLUMNID를 반환합니다.  
  
 모든 열 속성을 테이블에 대해 정의된 모든 열에 사용할 수 있습니다. 속성 값 설정이 충돌될 경우 **CreateTable** 이 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED를 반환할 수 있습니다. 잘못된 열 속성 설정으로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 생성에 실패할 경우 **CreateTable** 이 오류를 반환합니다.  
  
 DBCOLUMNDESC의 열 속성이 나타내는 의미는 다음과 같습니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE 설명: 생성된 열에 대한 ID 속성을 설정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ID 속성은 테이블 내의 단일 열에 대해서만 유효합니다. 단일 열에 대 한 속성을 VARIANT_TRUE로 설정 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에 테이블을 만들려고 할 때 오류가 발생 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성은 소수 자릿수가 0인 **integer**, **numeric** 및 **decimal** 형식에 대해서만 유효합니다. 다른 데이터 형식의 열에 대 한 속성을 VARIANT_TRUE로 설정 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에 테이블을 만들려고 할 때 오류가 발생 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 DBPROP_COL_AUTOINCREMENT와 DBPROP_COL_NULLABLE 모두 VARIANT_TRUE이 고 DBPROP_COL_NULLABLE의 *dwoption* 이 DBPROPOPTIONS_REQUIRED 되지 않은 경우 DB_S_ERRORSOCCURRED을 반환 합니다. DBPROP_COL_AUTOINCREMENT 및 DBPROP_COL_NULLABLE이 모두 VARIANT_TRUE이고 DBPROP_COL_NULLABLE의 *dwOption* 이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_NULLABLE *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.|  
|DBPROP_COL_DEFAULT|R/W: 읽기/쓰기<br /><br /> Default: None<br /><br /> 설명: 열에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DEFAULT 제약 조건을 만듭니다.<br /><br /> *vValue* DBPROP 멤버에는 개수에 관계없이 유형을 얼마든지 지정할 수 있습니다. *vValue.vt* 멤버에는 열 데이터 형식과 호환되는 유형을 지정해야 합니다. 예를 들어 DBTYPE_WSTR로 정의된 열의 기본값으로 BSTR N/A를 정의하는 것은 서로 호환되므로 가능합니다. DBTYPE_R8으로 정의 된 열에 대해 동일한 기본값을 정의 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 서버에 테이블을 만들려고 할 때 오류가 발생 합니다.|  
|DBPROP_COL_DESCRIPTION|R/W: 읽기/쓰기<br /><br /> Default: None<br /><br /> 설명: DBPROP_COL_DESCRIPTION 열 속성이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 의해 구현 되지 않았습니다.<br /><br /> 소비자가 속성 값을 쓰려고 하면 DBPROP 구조의 *dwStatus* 멤버가 DBPROPSTATUS_NOTSUPPORTED를 반환합니다.<br /><br /> 이 속성을 설정 해도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 대해 심각한 오류가 발생 하지는 않습니다. 다른 매개 변수 값이 모두 올바르기만 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이 생성됩니다.|  
|DBPROP_COL_FIXEDLENGTH|R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE<br /><br /> 설명: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 소비자가 DBCOLUMNDESC의 *wtype* 멤버를 사용 하 여 열의 데이터 형식을 정의 하는 경우 DBPROP_COL_FIXEDLENGTH를 사용 하 여 데이터 형식 매핑을 결정 합니다. 자세한 내용은 [ITableDefinition의 데이터 형식 매핑](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)을 참조하세요.|  
|DBPROP_COL_NULLABLE|R/W: 읽기/쓰기<br /><br /> Default: None<br /><br /> 설명: 테이블을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 속성이 설정 된 경우 열이 null 값을 허용 해야 하는지 여부를 나타냅니다. 해당 속성이 설정되어 있지 않으면 열의 NULL 값 허용 여부가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 기본 데이터베이스 옵션을 통해 확인됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 ISO 호환 공급자입니다. 연결된 세션에서는 ISO 동작을 따르므로 소비자가 DBPROP_COL_NULLABLE을 설정하지 않은 경우 열은 null 값을 허용합니다.|  
|DBPROP_COL_PRIMARYKEY|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: VARIANT_TRUE 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 PRIMARY KEY 제약 조건이 있는 열을 만듭니다.<br /><br /> 열 속성으로 정의된 경우 단일 열만 이 제약 조건을 확인할 수 있습니다. 단일 열에 대 한 속성 VARIANT_TRUE 설정 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 테이블을 만들려고 할 때 오류가 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 됩니다.<br /><br /> 참고: 소비자는 **IIndexDefinition::CreateIndex** 를 사용하여 둘 이상의 열에 대해 PRIMARY KEY 제약 조건을 만들 수 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 DBPROP_COL_PRIMARYKEY와 DBPROP_COL_UNIQUE 모두 VARIANT_TRUE이 고 DBPROP_COL_UNIQUE의 *dwoption* 이 DBPROPOPTIONS_REQUIRED 되지 않은 경우 DB_S_ERRORSOCCURRED을 반환 합니다.<br /><br /> DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE이고 DBPROP_COL_UNIQUE의 *dwOption* 이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_PRIMARYKEY *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_NULLABLE 모두 VARIANT_TRUE 이면 Native Client OLE DB 공급자가 오류를 반환 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 잘못 된 데이터 형식의 열에 대 한 PRIMARY KEY 제약 조건을 만들려고 하면 Native Client OLE DB 공급자가에서 오류를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **bit**, **text**, **ntext**, **image** 등의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 사용하여 만든 열에 대해서는 PRIMARY KEY 제약 조건을 정의할 수 없습니다.|  
|DBPROP_COL_UNIQUE|R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE 설명: 열에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UNIQUE 제약 조건을 적용합니다.<br /><br /> 열 속성으로 정의된 경우 이 제약 조건은 단일 열에만 적용됩니다. 소비자는 **IIndexDefinition::CreateIndex** 를 사용하여 둘 이상의 결합된 열 값에 대해 UNIQUE 제약 조건을 적용할 수 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE 모두 VARIANT_TRUE이 고 *dwoption* 이 DBPROPOPTIONS_REQUIRED 되지 않는 경우 Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환 합니다.<br /><br /> DBPROP_COL_PRIMARYKEY 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE이고 *dwOption* 이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_PRIMARYKEY *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_COL_NULLABLE 및 DBPROP_COL_UNIQUE 모두 VARIANT_TRUE이 고 *dwoption* 이 DBPROPOPTIONS_REQUIRED 되지 않는 경우 Native Client OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환 합니다.<br /><br /> DBPROP_COL_NULLABLE 및 DBPROP_COL_UNIQUE가 모두 VARIANT_TRUE이고 *dwOption* 이 DBPROPOPTIONS_REQUIRED이면 DB_E_ERRORSOCCURRED가 반환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID 속성을 사용하여 열이 정의되고 DBPROP_COL_NULLABLE *dwStatus* 멤버가 DBPROPSTATUS_CONFLICTING으로 설정됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 잘못 된 데이터 형식의 열에 UNIQUE 제약 조건을 만들려고 하면 Native Client OLE DB 공급자가에서 오류를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** 데이터 형식을 사용하여 만든 열에 대해서는 UNIQUE 제약 조건을 정의할 수 없습니다.|  
  
 소비자가 **Itabledefinition:: CreateTable** 를 호출 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 테이블 속성을 다음과 같이 해석 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE 설명: 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 소비자가 명명 한 테이블을 만듭니다. VARIANT_TRUE 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 소비자에 대 한 임시 테이블 이름을 생성 합니다. 소비자는 **CreateTable** 의 *pTableID* 매개 변수를 NULL로 설정합니다. *ppTableID* 매개 변수는 올바른 포인터를 포함해야 합니다.|  
  
 소비자가 성공적으로 만든 테이블에서 행 집합을 열도록 요청 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 커서 지원 행 집합을 엽니다. 행 집합 속성은 전달하는 속성 집합에서 표시할 수 있습니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 인덱스](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
