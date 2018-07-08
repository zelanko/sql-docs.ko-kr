---
title: 테이블 반환 매개 변수 형식 검색 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 373e2c17254b55ed351695286b9a4a5d03f2d47c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420052"
---
# <a name="table-valued-parameter-type-discovery"></a>테이블 반환 매개 변수 형식 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  소비자-즉, 응용 프로그램 사용 하는 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자, OLE DB 공급자에 명령 텍스트에 지정 된 경우 각 명령 매개 변수의 형식을 검색할 수 있습니다. 테이블 반환 매개 변수의 형식을 알고 있는 경우 후 소비자는 테이블 반환 매개 변수의 개별 열에 대 한 메타 데이터 정보를 검색할 수 있습니다.  
  
 프로시저 매개 변수의 형식 정보를 대부분의 매개 변수 형식에 대 한 icommandwithparameters:: Getparameterinfo에서 지원 됩니다. 부터 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], 사용자 정의 형식의 도입 하며 **xml** 데이터 형식으로 GetParameterInfo 메서드 충분 하지 않은이 목적을 위해 사용자 정의 형식을 제공할 수 없기 때문에 정보 (이름, 스키마 및 카탈로그) ICommandWithParameters 통해입니다. ISSCommandWithParameters를 새 인터페이스를 확장된 유형 정보를 제공 하도록 정의 되었습니다.  
  
 테이블 반환 매개 변수에 대 한도 세부 정보를 검색할 ISSCommandWithParameters 인터페이스를 사용 합니다. 클라이언트는 명령 개체를 준비한 후 ISSCommandWithParameters::GetParameterInfo를 호출 합니다. 에 대 한 테이블 반환 매개 변수를 *wType* DBPARAMINFO 구조체의 멤버는 공급자가 DBTYPE_TABLE로 설정 됩니다. 합니다 *ulParamSize* DBPARAMINFO 구조의 필드의 값이 ~ 0입니다.  
  
 소비자 ISSCommandWithParamters를 사용 하 여 추가 속성 (테이블 반환 매개 변수 형식 카탈로그 이름, 테이블 반환 매개 변수 형식 스키마 이름, 테이블 반환 매개 변수 형식 이름, 열 순서 및 기본 열)를 요청 합니다: GetParameterProperties 합니다.  
  
 형식 이름이 알려져 있으면 후 소비자 중 하나를 호출 해야 하는 개별 열 정보를 검색할 IOpenRowset::OpenRowsetor 가져올 DBSCHEMA_TABLE_TYPE_COLUMNS 행 집합을 테이블 반환 매개 변수 형식 이름을 테이블 이름으로 지정 하 여 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수를 사용 하 여 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
