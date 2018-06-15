---
title: 테이블 반환 매개 변수를 포함 하는 명령 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 169f87c122e1c432c0a008b4e2200d1e19d1f42d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32949698"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>테이블 반환 매개 변수가 포함된 명령 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  테이블 반환 매개 변수가 포함된 명령을 실행하려면 두 단계가 필요합니다.  
  
1.  매개 변수 유형을 지정합니다.  
  
2.  매개 변수 데이터를 바인딩합니다.  
  
## <a name="table-valued-parameter-specification"></a>테이블 반환 매개 변수 사양  
 소비자는 테이블 반환 매개 변수의 유형을 지정할 수 있습니다. 이 정보에는 테이블 반환 매개 변수 유형 이름이 포함됩니다. 연결의 현재 기본 스키마에 테이블 반환 매개 변수의 사용자 정의 테이블 형식이 없는 경우에는 스키마 이름도 포함됩니다. 서버에서 지원하는 경우 소비자는 열의 순서와 같은 선택적인 메타데이터 정보를 지정할 수 있으며 특정 열의 모든 행이 기본값을 가지도록 지정할 수 있습니다.  
  
 테이블 반환 매개 변수를 지정 하려면 소비자 ISSCommandWithParamter::SetParameterInfo를 호출 하 고 필요에 따라 isscommandwithparameters:: Setparameterproperties를 호출 합니다. 테이블 반환 매개 변수는 *pwszDataSourceType* DBPARAMBINDINFO 구조에서 필드는 DBTYPE_TABLE 값이 있습니다. *ulParamSize* 필드가로 설정 된 ~ 0을 해당 길이 알 수 없습니다. Isscommandwithparameters:: Setparameterproperties 통해 스키마 이름, 유형 이름, 열 순서 및 기본 열 같은 테이블 반환 매개 변수에 대 한 특정 속성을 설정할 수 있습니다.  
  
## <a name="table-valued-parameter-binding"></a>테이블 반환 매개 변수 바인딩  
 테이블 반환 매개 변수는 모든 행 집합 개체가 될 수 있습니다. 공급자는 실행 중에 서버로 테이블 반환 매개 변수를 보내는 동안 이 개체를 읽어 들입니다.  
  
 소비자는 테이블 반환 매개 변수를 바인딩하려면 iaccessor:: Createaccessor를 호출 합니다. *wType* 테이블 반환 매개 변수의 DBBINDING 구조체의 필드는 DBTYPE_TABLE로 설정 됩니다. *pObject* DBBINDING 구조체의 멤버는 NULL이 아닌 및 *pObject*의 *iid* 멤버가 IID_IRowset 또는 다른 테이블 반환 매개 변수 행 집합 개체에 설정 된 인터페이스입니다. DBBINDING 구조의 나머지 필드는 스트림된 BLOB에 설정할 때와 같은 방법으로 설정됩니다.  
  
 테이블 반환 매개 변수에 대한 바인딩과 테이블 반환 매개 변수와 연결된 행 집합 개체에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   테이블 반환 매개 변수 행 집합 열 데이터에는 DBSTATUS_S_ISNULL 및 DBSTATUS_S_OK 상태 값만 지원됩니다. DBSTATUS_S_DEFAULT를 사용하면 오류가 발생하며 바인딩된 상태 값은 DBSTATUS_E_BADSTATUS로 설정됩니다.  
  
-   테이블 반환 매개 변수를 DBSTATUS_S_DEFAULT 상태로 표시할 수 있습니다. 유효한 값은 DBSTATUS_S_DEFAULT 및 DBSTATUS_S_OK뿐입니다. 상태를 DBSTATUS_S_DEFAULT로 설정하면 테이블 반환 매개 변수의 값이 빈 테이블과 같게 됩니다.  
  
-   테이블 반환 매개 변수의 읽기 전용 열(ID 열 또는 계산 열)은 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 속성을 사용하여 기본값으로 표시해야 합니다. 기본값을 가지는 열 역시 특정 테이블 반환 매개 변수의 열 데이터 값에 이 기본값이 사용될 수 있도록 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 속성을 통해 기본값으로 표시해야 합니다. 공급자는 기본값으로 표시된 열에 바인딩된 데이터 값을 무시합니다.  
  
-   SSPROP_PARAM_TABLE_DEFAULT를 함께 설정하지 않으면 DBPROP_COL_AUTOINCREMENT 또는 SSPROP_COL_COMPUTED가 포함된 열의 데이터가 서버로 전송됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 반환 매개 변수 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수 사용 & #40; OLE db& #41;를 사용 하 여](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
