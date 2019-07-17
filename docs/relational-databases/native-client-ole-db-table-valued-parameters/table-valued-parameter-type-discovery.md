---
title: 테이블 반환 매개 변수 형식 검색 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d219631203c505ad2e0cac594b629c22032214fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069621"
---
# <a name="table-valued-parameter-type-discovery"></a>테이블 반환 매개 변수 형식 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  소비자-즉, 응용 프로그램 사용 하는 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 있습니다 OLE DB 공급자에 명령 텍스트에 지정 된 경우 각 명령 매개 변수의 형식을 검색 합니다. 테이블 반환 매개 변수의 형식이 확인되면 소비자가 테이블 반환 매개 변수의 개별 열에 대한 메타데이터 정보를 검색할 수 있습니다.  
  
 프로시저 매개 변수의 형식 정보를 대부분의 매개 변수 형식에 대 한 icommandwithparameters:: Getparameterinfo에서 지원 됩니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 사용자 정의 형식과 **xml** 데이터 형식이 도입되면서 GetParameterInfo 메서드는 ICommandWithParameters를 통해 사용자 정의 형식 정보(이름, 스키마 및 카탈로그)를 제공할 수 없으므로 이러한 용도에 적합하지 않게 되었습니다. ISSCommandWithParameters를 새 인터페이스를 확장된 유형 정보를 제공 하도록 정의 되었습니다.  
  
 테이블 반환 매개 변수에 대 한도 세부 정보를 검색할 ISSCommandWithParameters 인터페이스를 사용 합니다. 클라이언트는 명령 개체를 준비한 후 ISSCommandWithParameters::GetParameterInfo를 호출 합니다. 테이블 반환 매개 변수의 경우 공급자에 의해 DBPARAMINFO 구조의 *wType* 멤버가 DBTYPE_TABLE로 설정됩니다. DBPARAMINFO 구조의 *ulParamSize* 필드 값은 ~0입니다.  
  
 그런 다음, 소비자는 ISSCommandWithParameters::GetParameterProperties를 사용하여 추가 속성(테이블 반환 매개 변수 형식 카탈로그 이름, 테이블 반환 매개 변수 형식 스키마 이름, 테이블 반환 매개 변수 형식 이름, 열 순서 및 기본 열)을 요청합니다.  
  
 형식 이름이 확인되면 소비자는 IOpenRowset::OpenRowsetor를 호출하거나 테이블 반환 매개 변수 형식 이름을 테이블 이름으로 지정하여 DBSCHEMA_TABLE_TYPE_COLUMNS 행 집합을 가져옴으로써 개별 열 정보를 검색해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
