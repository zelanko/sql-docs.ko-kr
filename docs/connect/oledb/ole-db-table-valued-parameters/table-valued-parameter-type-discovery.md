---
title: 테이블 반환 매개 변수 형식 검색 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 테이블 반환 매개 변수 형식 검색
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: c45b5f6b00c15dee35d263447f5b95c8e31b986f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801104"
---
# <a name="table-valued-parameter-type-discovery"></a>테이블 반환 매개 변수 형식 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  소비자(SQL Server용 OLE DB 드라이버를 사용하는 클라이언트 애플리케이션)는 OLE DB 공급자에 명령 텍스트가 지정되어 있는 경우 각 명령 매개 변수의 형식을 검색할 수 있습니다. 테이블 반환 매개 변수의 형식이 확인되면 소비자가 테이블 반환 매개 변수의 개별 열에 대한 메타데이터 정보를 검색할 수 있습니다.  
  
 프로시저 매개 변수의 형식 정보를 대부분의 매개 변수 형식에 대 한 icommandwithparameters:: Getparameterinfo에서 지원 됩니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터 사용자 정의 형식과 **xml** 데이터 형식이 도입되면서 GetParameterInfo 메서드는 ICommandWithParameters를 통해 사용자 정의 형식 정보(이름, 스키마 및 카탈로그)를 제공할 수 없으므로 이러한 용도에 적합하지 않게 되었습니다. ISSCommandWithParameters를 새 인터페이스를 확장된 유형 정보를 제공 하도록 정의 되었습니다.  
  
 테이블 반환 매개 변수에 대 한도 세부 정보를 검색할 ISSCommandWithParameters 인터페이스를 사용 합니다. 클라이언트는 명령 개체를 준비한 후 ISSCommandWithParameters::GetParameterInfo를 호출 합니다. 테이블 반환 매개 변수의 경우 공급자에 의해 DBPARAMINFO 구조의 *wType* 멤버가 DBTYPE_TABLE로 설정됩니다. DBPARAMINFO 구조의 *ulParamSize* 필드 값은 ~0입니다.  
  
 그런 다음, 소비자는 ISSCommandWithParameters::GetParameterProperties를 사용하여 추가 속성(테이블 반환 매개 변수 형식 카탈로그 이름, 테이블 반환 매개 변수 형식 스키마 이름, 테이블 반환 매개 변수 형식 이름, 열 순서 및 기본 열)을 요청합니다.  
  
 형식 이름이 확인되면 소비자는 IOpenRowset::OpenRowsetor를 호출하거나 테이블 반환 매개 변수 형식 이름을 테이블 이름으로 지정하여 DBSCHEMA_TABLE_TYPE_COLUMNS 행 집합을 가져옴으로써 개별 열 정보를 검색해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
