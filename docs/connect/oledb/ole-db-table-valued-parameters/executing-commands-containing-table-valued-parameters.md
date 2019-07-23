---
title: 테이블 반환 매개 변수가 포함된 명령 실행 | Microsoft Docs
description: 테이블 반환 매개 변수가 포함된 명령 실행
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 320a66b84c6a5b904e98941251801c7ee5927087
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994147"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>테이블 반환 매개 변수가 포함된 명령 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  테이블 반환 매개 변수를 사용하여 명령을 실행하려면 두 단계가 필요합니다.  
  
1.  매개 변수 유형을 지정합니다.  
  
2.  매개 변수 데이터를 바인딩합니다.  
  
## <a name="table-valued-parameter-specification"></a>테이블 반환 매개 변수 사양  
 소비자는 테이블 반환 매개 변수의 유형을 지정할 수 있습니다. 이 정보에는 테이블 반환 매개 변수 유형 이름이 포함됩니다. 연결의 현재 기본 스키마에 테이블 반환 매개 변수의 사용자 정의 테이블 형식이 없는 경우에는 스키마 이름도 포함됩니다. 서버에서 지원하는 경우 소비자는 열의 순서와 같은 선택적인 메타데이터 정보를 지정할 수 있으며 특정 열의 모든 행이 기본값을 가지도록 지정할 수 있습니다.  
  
 소비자는 테이블 반환 매개 변수를 지정 하기 위해 ISSCommandWithParameter:: SetParameterInfo를 호출 하 고 필요에 따라 ISSCommandWithParameters:: SetParameterProperties를 호출 합니다. 테이블 반환 매개 변수에서 DBPARAMBINDINFO 구조의 *pwszDataSourceType* 필드는 DBTYPE_TABLE 값을 갖습니다. *ulParamSize* 필드는 길이를 알 수 없음을 나타내기 위해 ~0으로 설정됩니다. 스키마 이름, 유형 이름, 열 순서 및 기본 열과 같은 테이블 반환 매개 변수의 특정 속성은 ISSCommandWithParameters:: SetParameterProperties를 통해 설정할 수 있습니다.  
  
## <a name="table-valued-parameter-binding"></a>테이블 반환 매개 변수 바인딩  
 테이블 반환 매개 변수는 모든 행 집합 개체가 될 수 있습니다. 공급자는 실행 중에 서버로 테이블 반환 매개 변수를 보내는 동안 이 개체를 읽어 들입니다.  
  
 테이블 반환 매개 변수를 바인딩하기 위해 소비자는 IAccessor:: CreateAccessor를 호출 합니다. 테이블 반환 매개 변수의 DBBINDING 구조에 있는 *wType* 필드는 DBTYPE_TABLE로 설정됩니다. DBBINDING 구조의 *pObject* 멤버는 NULL이 아니며 *pObject*의 *iid* 멤버는 IID_IRowset 또는 다른 테이블 반환 매개 변수 행 집합 개체 인터페이스로 설정됩니다. DBBINDING 구조의 나머지 필드는 스트림된 BLOB에 설정할 때와 같은 방법으로 설정되어야 합니다.  
  
 테이블 반환 매개 변수에 대한 바인딩과 테이블 반환 매개 변수와 연결된 행 집합 개체에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   테이블 반환 매개 변수 행 집합 열 데이터에는 DBSTATUS_S_ISNULL 및 DBSTATUS_S_OK 상태 값만 지원됩니다. DBSTATUS_S_DEFAULT를 사용하면 오류가 발생하며 바인딩된 상태 값은 DBSTATUS_E_BADSTATUS로 설정됩니다.  
  
-   테이블 반환 매개 변수를 DBSTATUS_S_DEFAULT 상태로 표시할 수 있습니다. 유효한 값은 DBSTATUS_S_DEFAULT 및 DBSTATUS_S_OK뿐입니다. 상태를 DBSTATUS_S_DEFAULT로 설정하면 테이블 반환 매개 변수의 값이 빈 테이블과 같게 됩니다.  
  
-   테이블 반환 매개 변수의 읽기 전용 열(ID 열 또는 계산 열)은 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 속성을 사용하여 기본값으로 표시해야 합니다. 기본값을 가지는 열 역시 특정 테이블 반환 매개 변수의 열 데이터 값에 이 기본값이 사용될 수 있도록 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 속성을 통해 기본값으로 표시해야 합니다. 공급자는 기본값으로 표시된 열에 바인딩된 데이터 값을 무시합니다.  
  
-   SSPROP_PARAM_TABLE_DEFAULT를 함께 설정하지 않으면 DBPROP_COL_AUTOINCREMENT 또는 SSPROP_COL_COMPUTED가 포함된 열의 데이터가 서버로 전송됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
