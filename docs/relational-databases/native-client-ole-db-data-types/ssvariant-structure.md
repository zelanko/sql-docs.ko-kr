---
title: SSVARIANT 구조 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d87c4a4537683d9dbb9817a0a3c022f23f2b846
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998203"
---
# <a name="ssvariant-structure"></a>SSVARIANT 구조
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Sqlncli에 정의 된 **Ssvariant** 구조는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLEDB 공급자의 DBTYPE_SQLVARIANT 값에 해당 합니다.  
  
 **SSVARIANT**는 판별 공용 구조체입니다. vt 멤버의 값에 따라 소비자는 읽을 멤버를 결정할 수 있습니다. vt 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 해당하므로 **SSVARIANT** 구조는 모든 SQL Server 형식을 보유할 수 있습니다. 표준 OLE DB 형식의 데이터 구조에 대한 자세한 내용은 [형식 표시기](https://go.microsoft.com/fwlink/?LinkId=122171)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 DataTypeCompat==80인 경우, 여러 **SSVARIANT** 하위 유형이 문자열이 됩니다. 예를 들면 다음 vt 값이 **SSVARIANT**에 VT_SS_WVARSTRING으로 나타납니다.  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 DateTypeCompat == 0인 경우, 이러한 유형은 네이티브 형식으로 나타납니다.  
  
 SSPROP_INIT_DATATYPECOMPATIBILITY에 대 한 자세한 내용은 [SQL Server Native Client 연결 문자열 키워드 사용](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조 하세요.  
  
 Sqlncli 파일에는 **ssvariant** 구조의 멤버 유형 역참조를 간소화 하는 변형 액세스 매크로가 포함 되어 있습니다. 예로는 다음과 같이 사용 가능한 V_SS_DATETIMEOFFSET가 있습니다.  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 **Ssvariant** 구조의 각 멤버에 대 한 액세스 매크로의 전체 집합은 sqlncli 파일을 참조 하세요.  
  
 다음 표에서는 **SSVARIANT** 구조의 멤버를 설명합니다.  
  
|멤버|OLE DB 유형 표시기|OLE DB C 데이터 형식|vt 값|주석|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||**SSVARIANT** 구조에 포함된 값 유형을 지정합니다.|  
|bTinyIntVal|DBTYPE_UI1|**바이트만**|**VT_SS_UI1**|에서는 **tinyint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|sShortIntVal|DBTYPE_I2|**간략히**|**VT_SS_I2**|는 **smallint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|lIntVal|DBTYPE_I4|**시간과**|**VT_SS_I4**|는 **int** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|**Bigint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|는 **real** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|**Float** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|**money** 및 **smallmoney**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|는 **bit** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|**Uniqueidentifier** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|**Numeric** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|**Date** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|**smalldatetime**, **datetime** 및 **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|**Time** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *tTime2Val*(**DBTIME2**)<br /><br /> *bScale*(**BYTE**) *tTime2Val* 값의 소수 자릿수를 지정합니다.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|에서는 **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *tsDataTimeVal*(DBTIMESTAMP)<br /><br /> *bScale*(**BYTE**) *tsDataTimeVal* 값의 소수 자릿수를 지정합니다.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|**Datetimeoffset** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원 합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *tsoDateTimeOffsetVal*(**DBTIMESTAMPOFFSET**)<br /><br /> *bScale*(**BYTE**) *tsoDateTimeOffsetVal* 값의 소수 자릿수를 지정합니다.|  
|NCharVal|해당하는 OLE DB 유형 표시기 없음|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|**nchar** 및 **nvarchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *sActualLength*(**SHORT**) *pwchNCharVal*이 가리키는 문자열의 실제 길이를 지정합니다. 이 값은 0으로 끝나지 않습니다.<br /><br /> *sMaxLength*(**SHORT**) *pwchNCharVal*이 가리키는 문자열의 최대 길이를 지정합니다.<br /><br /> *pwchNCharVal*(**WCHAR** \*) 문자열에 대한 포인터입니다.<br /><br /> 사용되지 않는 멤버: *rgbReserved*, *dwReserved* 및 *pwchReserved*.|  
|CharVal|해당하는 OLE DB 유형 표시기 없음|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|**char** 및 **varchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *sActualLength*(**SHORT**) *pchCharVal*이 가리키는 문자열의 실제 길이를 지정합니다. 이 값은 0으로 끝나지 않습니다.<br /><br /> *sMaxLength*(**SHORT**) *pchCharVal*이 가리키는 문자열의 최대 길이를 지정합니다.<br /><br /> *pchCharVal*(**CHAR** \*) 문자열에 대한 포인터입니다.<br /><br /> 사용되지 않은 멤버:<br /><br /> *rgbReserved*, *dwReserved* 및 *pwchReserved*.|  
|BinaryVal|해당하는 OLE DB 유형 표시기 없음|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|**binary** 및 **varbinary**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지원합니다.<br /><br /> 포함되는 멤버는 다음과 같습니다.<br /><br /> *sActualLength*(**SHORT**) *prgbBinaryVal*이 가리키는 문자열의 실제 길이를 지정합니다.<br /><br /> *sMaxLength*(**SHORT**) *prgbBinaryVal*이 가리키는 문자열의 최대 길이를 지정합니다.<br /><br /> *prgbBinaryVal*(**BYTE** \*) 이진 데이터에 대한 포인터입니다.<br /><br /> 사용되지 않는 멤버: *dwReserved*.|  
|UnknownType|UNUSED|UNUSED|UNUSED|UNUSED|  
|BLOBType|UNUSED|UNUSED|UNUSED|UNUSED|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
