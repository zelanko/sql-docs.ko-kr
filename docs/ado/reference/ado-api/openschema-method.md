---
title: OpenSchema 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2080145e00c658288f9d34e3fa42ed335e0c1d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931869"
---
# <a name="openschema-method"></a>OpenSchema 메서드
공급자에서 데이터베이스 스키마 정보를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Return Value  
 스키마 정보를 포함 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 반환 합니다. **레코드 집합** 은 읽기 전용 정적 커서로 열립니다. *QueryType* 는 **레코드 집합**에 표시 되는 열을 결정 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *QueryType*  
 실행할 스키마 쿼리의 유형을 나타내는 [Schemaenum](../../../ado/reference/ado-api/schemaenum.md) 값입니다.  
  
 *조건*  
 (선택 사항) [Schemaenum](../../../ado/reference/ado-api/schemaenum.md)에 나열 된 각 *QueryType* 옵션에 대 한 쿼리 제약 조건의 배열입니다.  
  
 *SchemaID*  
 OLE DB 사양에서 정의 하지 않은 공급자 스키마 쿼리의 GUID입니다. 이 매개 변수는 *QueryType* 이 **adschemaproviderspecific**로 설정 된 경우에 필요 합니다. 그렇지 않은 경우에는 사용 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 **OpenSchema** 메서드는 데이터 원본에 있는 테이블, 테이블의 열, 지원 되는 데이터 형식과 같은 데이터 원본에 대 한 자체 설명 정보를 반환 합니다.  
  
 *QueryType* 인수는 반환 되는 열 (스키마)을 나타내는 GUID입니다. OLE DB 사양에는 전체 스키마 목록이 있습니다.  
  
 *조건* 인수는 스키마 쿼리 결과를 제한 합니다. *조건* 결과 **레코드 집합**에서 제약 조건 열 이라고 하는 열의 해당 하위 집합에서 발생 해야 하는 값의 배열을 지정 합니다.  
  
 상수 **Adschemaproviderspecific** 는 공급자가 위에 나열 된 것과 다른 외부 스키마 쿼리를 정의 하는 경우 *QueryType* 인수에 사용 됩니다. 이 상수를 사용 하는 경우 실행할 스키마 쿼리의 GUID를 전달 하려면 *Schemaid* 인수가 필요 합니다. *QueryType* 가 **Adschemaproviderspecific** 으로 설정 되었지만 *schemaid* 가 제공 되지 않으면 오류가 발생 합니다.  
  
 공급자는 모든 OLE DB 표준 스키마 쿼리를 지 원하는 데 필요 하지 않습니다. 특히 OLE DB 지정에는 **adSchemaTables**, **AdSchemaColumns**및 **adschemaprovidertypes** 만 필요 합니다. 그러나 공급자는 이러한 스키마 쿼리에 대해 앞에 나열 된 *조건* 제약 조건을 지원할 필요가 없습니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에서는 **OpenSchema** 메서드를 사용할 수 없습니다.  
  
> [!NOTE]
>  Visual Basic에서 **연결** 개체의 **OpenSchema** 메서드에서 반환 된 **레코드 집합** 에 4 바이트 부호 없는 정수 (DBTYPE UI4)가 있는 열은 다른 변수와 비교할 수 없습니다. OLE DB 데이터 형식에 대 한 자세한 내용은 Microsoft OLE DB 프로그래머 참조의 데이터 형식 [OLE DB (OLE DB)](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a) 및 [부록 a: 데이터 형식](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) (영문)을 참조 하세요.  
  
> [!NOTE]
>  **Visual C/c + + 사용자** 클라이언트 쪽 커서를 사용 하지 않는 경우 ADO에서 열 스키마의 "ORDINAL_POSITION"를 검색 하면 mdac 2.7, MDAC 2.8 및 windows DAC (Windows Data Access Components) 6.0에 VT_R8 형식의 변형이 반환 되지만 MDAC 2.6에서 사용 되는 유형은 VT_I4 됩니다. Mdac 2.6 용으로 작성 된 프로그램은 MDAC 2.7, MDAC 2.8 및 Windows DAC 6.0 (수정 하지 않음)에서 실행 되는 경우 모든 서 수에 대해 0을 사용 하 여 VT_I4 형식으로 반환 된 variant만 찾습니다. 이 변경 작업은 OLE DB 반환 하는 데이터 형식이 DBTYPE_UI4 되 고, 서명 된 VT_I4 형식에 잘림이 발생 하지 않고 가능한 모든 값을 포함할 공간이 부족 하 여 데이터가 손실 될 수 있기 때문에 수행 되었습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [OpenSchema 메서드 예제 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema 메서드 예제 (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
