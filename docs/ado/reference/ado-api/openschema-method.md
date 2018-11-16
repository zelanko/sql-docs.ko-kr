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
manager: craigg
ms.openlocfilehash: f2b4df18cf783e23792b51fb2c437b82c6a8ec52
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606213"
---
# <a name="openschema-method"></a>OpenSchema 메서드
공급자에서 데이터베이스 스키마 정보를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 스키마 정보가 들어 있는 개체입니다. 합니다 **레코드 집합** 읽기 전용, 정적 커서로 열립니다. 합니다 *QueryType* 에 표시할 열을 결정 합니다 **레코드 집합**합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *QueryType*  
 모든 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) 실행 하려면 스키마 쿼리의 형식을 나타내는 값입니다.  
  
 *조건*  
 선택 사항입니다. 각각에 대 한 쿼리 제약 조건의 배열을 *QueryType* 에 나열 된 옵션 [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)합니다.  
  
 *SchemaID*  
 OLE DB 사양에 정의 되지 않은 공급자 스키마 쿼리에 대 한 GUID입니다. 이 매개 변수는 필요한 경우 *QueryType* 로 설정 된 **adSchemaProviderSpecific**고, 그렇지 않으면 사용 되지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **OpenSchema** 메서드 데이터 원본에 테이블의 열에 있는 테이블 같은 데이터 원본에 대 한 정보를 반환 하 고 데이터 형식을 지원 합니다.  
  
 합니다 *QueryType* 인수가 반환 되는 열 (스키마)를 나타내는 GUID입니다. OLE DB 사양에는 스키마의 전체 목록입니다.  
  
 합니다 *조건을* 인수 스키마 쿼리의 결과 제한 합니다. *기준을* 열, 제약 조건 열을 결과의 해당 하위 집합에서 발생 해야 하는 값의 배열을 지정 **레코드 집합**합니다.  
  
 상수 **adSchemaProviderSpecific** 에 사용 되는 *QueryType* 인수 공급자는 외부 비표준 스키마 쿼리 자체를 정의 하는 경우 앞에 나열 된 합니다. 이 상수를 사용할 경우는 *SchemaID* 실행 스키마 쿼리의 GUID에 전달할 인수가 필요 합니다. 하는 경우 *QueryType* 로 설정 된 **adSchemaProviderSpecific** 되지만 *SchemaID* 제공 되지 않으면 오류가 발생 합니다.  
  
 공급자는 모든 OLE DB 표준 스키마 쿼리를 지원 하기 위해 필요 하지 않습니다. 특히만 **adSchemaTables**를 **adSchemaColumns**, 및 **adSchemaProviderTypes** OLE DB 사양에 필요 합니다. 그러나 공급자가 지 원하는 데 필요한 하지 합니다 *조건을* 제약 조건 앞에 나열 된 이러한 스키마 쿼리에 대 한 합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 는 **OpenSchema** 메서드는 클라이언트 쪽에서 사용할 수 없는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
> [!NOTE]
>  Visual Basic의 경우에 4 바이트 부호 없는 정수 (DBTYPE UI4)이 있는 열에는 **레코드 집합** 에서 반환 된 합니다 **OpenSchema** 메서드를 **연결** 개체 수 없습니다 다른 변수를 비교 합니다. OLE DB 데이터 형식에 대 한 자세한 내용은 참조 하세요. [OLE DB (OLE DB)의 데이터 형식](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a) 하 고 [부록 a: 데이터 형식](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) Microsoft OLE DB 프로그래머 참조에서입니다.  
  
> [!NOTE]
>  **Visual C + + 사용자** 클라이언트 쪽 커서를 사용 하지 않을 경우 MDAC 2.7, MDAC 2.8 및 유형은 MDAC에 사용 하는 동안 Windows Data Access Components (Windows DAC) 6.0 VT_R8 형식의 variant를 반환 ADO에서 열 스키마의 "ORDINAL_POSITION"를 검색 합니다. 2.6 VT_I4 했습니다. 변형만 검색 하는 MDAC 2.6 용으로 작성 된 프로그램 VT_I4 수정 하지 않고 MDAC 2.7, MDAC 2.8 및 Windows DAC 6.0에서 실행 하는 경우 모든 서 수에 대 한 0 얻게 형식의 반환 합니다. OLE DB 반환 하는 데이터 형식, DBTYPE_UI4 이므로 내용을이 변경할 있으며 서명 된 VT_I4 형식에서 발생 하 고 데이터의 손실을 초래할 수 있는 잘림 없이 사용 가능한 모든 값을 포함할 만큼 충분 한 공간이 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [OpenSchema 메서드 예제 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema 메서드 예제 (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
