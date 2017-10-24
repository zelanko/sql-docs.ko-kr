---
title: "OpenSchema 메서드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e5c547eb8a6c1208bedffb988096f45b4c871d09
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="openschema-method"></a>OpenSchema 메서드
공급자에서 데이터베이스 스키마 정보를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 스키마 정보를 포함 하는 개체입니다. **레코드 집합** 읽기 전용, 정적 커서로 열립니다. *QueryType* 에 표시할 열을 결정는 **레코드 집합**합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *QueryType*  
 모든 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) 스키마 쿼리를 실행 유형을 나타내는 값입니다.  
  
 *조건*  
 (선택 사항) 각각에 대 한 쿼리 제약 조건의 배열을 *QueryType* 에 나열 된 옵션 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)합니다.  
  
 *SchemaID*  
 OLE DB 사양에 정의 되지 않은 공급자 스키마 쿼리에 대 한 GUID입니다. 경우에이 매개 변수는 필수 *QueryType* 로 설정 되어 **adSchemaProviderSpecific**, 그렇지 않으면 사용 되지 않습니다.  
  
## <a name="remarks"></a>주의  
 **OpenSchema** 메서드는 테이블의 열 데이터 원본에 테이블은 같은 데이터 원본에 대 한 정보를 반환 하 고 데이터 형식을 지원 합니다.  
  
 *QueryType* 인수는 반환 되는 열 (스키마)을 나타내는 GUID입니다. OLE DB 사양에 스키마의 전체 목록이 있습니다.  
  
 *조건* 인수 스키마 쿼리의 결과 제한 합니다. *조건* 열리면 제약 조건 열 이라는 열의 해당 하위 집합에서 발생 해야 하는 값의 배열을 지정 **레코드 집합**합니다.  
  
 상수 **adSchemaProviderSpecific** 에 사용 되는 *QueryType* 인수 공급자 외부 하는 것 자체 비표준 스키마 쿼리를 정의 하는 경우 앞에 나열 된 합니다. 이 상수를 사용 하면는 *SchemaID* 실행 스키마 쿼리의 GUID를 전달 하려면 인수가 필요 합니다. 경우 *QueryType* 로 설정 된 **adSchemaProviderSpecific** 하지만 *SchemaID* 를 제공 하지 않으면 오류가 발생 합니다.  
  
 공급자는 모든 OLE DB 표준 스키마 쿼리를 지 원하는 데 필요 하지 않습니다. 특히,만 **adSchemaTables**, **adSchemaColumns**, 및 **adSchemaProviderTypes** OLE DB 사양에서 필요 합니다. 그러나 공급자가 지 원하는 데 필요 하지는 *조건* 제약 조건 앞에 나열 된 해당 스키마 쿼리에 대해 합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 는 **OpenSchema** 메서드는 클라이언트 쪽에서 사용할 수 없습니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
> [!NOTE]
>  Visual Basic의 경우에 4 바이트 부호 없는 정수 (DBTYPE UI4)이 있는 열에는 **레코드 집합** 에서 반환 되는 **OpenSchema** 에서 메서드는 **연결** 개체 수 없습니다 다른 변수 비교 합니다. OLE DB 데이터 형식에 대 한 자세한 내용은 참조 [(OLE DB) OLE db에서 데이터 형식](http://msdn.microsoft.com/en-us/6039292f-74e0-49b2-b133-17bc117ebf6a) 및 [부록 a: 데이터 형식](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6) Microsoft OLE DB 프로그래머 참조에서.  
  
> [!NOTE]
>  **Visual C/c + + 사용자** 클라이언트 쪽 커서를 사용 하지 않을 때 MDAC 2.7, MDAC 2.8 및 유형은 MDAC에 사용 하는 동안 Windows Data Access Components (Windows DAC) 6.0에 VT_R8 유형의 variant를 반환 ADO에 열 스키마의 "ORDINAL_POSITION"를 검색 합니다. 2.6 VT_I4 했습니다. 만 검색 하는 variant MDAC 2.6에 대 한 작성 된 프로그램 VT_I4 수정 하지 않고 MDAC 2.7, MDAC 2.8 및 Windows DAC 6.0에서 실행 되 면 모든 서 수에 대 한 0 대기줄 형식의 반환 합니다. OLE DB 반환 하는 데이터 형식이 DBTYPE_UI4, 이므로이 변경 내용은 및 서명 된 VT_I4 형식에 충분 한 공간이 없을 일어나는 횟수와 데이터의 손실을 초래할 수 있는 잘림 없이 사용 가능한 모든 값을 포함 하도록 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [OpenSchema 메서드 예제 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema 메서드 예제 (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

