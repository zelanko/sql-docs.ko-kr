---
title: 테이블 반환 매개 변수 형식 검색 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ab8d837e4ddf74256e4bae70f772557ec8ff67f7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933254"
---
# <a name="table-valued-parameter-type-discovery"></a>테이블 반환 매개 변수 형식 검색
  소비자 즉, Native Client OLE DB 공급자를 사용 하는 클라이언트 응용 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령 텍스트가 OLE DB 공급자에 지정 된 경우 각 명령 매개 변수의 형식을 검색할 수 있습니다. 테이블 반환 매개 변수의 형식이 확인되면 소비자가 테이블 반환 매개 변수의 개별 열에 대한 메타데이터 정보를 검색할 수 있습니다.  
  
 프로시저 매개 변수의 형식 정보는 대부분의 매개 변수 형식에서 ICommandWithParameters::GetParameterInfo를 통해 지원됩니다. 부터 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 사용자 정의 형식 및 데이터 형식이 도입 됨에 따라 `xml` GetParameterInfo 메서드는 ICommandWithParameters를 통해 사용자 정의 형식 정보 (이름, 스키마 및 카탈로그)를 제공할 수 없기 때문에이 용도로 충분 하지 않습니다. 따라서 확장된 형식 정보를 제공하기 위해 새로운 인터페이스인 ISSCommandWithParameters가 정의되었습니다.  
  
 테이블 반환 매개 변수의 경우 ISSCommandWithParameters 인터페이스를 사용하여 자세한 정보를 검색할 수도 있습니다. 명령 개체를 준비하고 나면 클라이언트가 ISSCommandWithParameters::GetParameterInfo를 호출합니다. 테이블 반환 매개 변수의 경우 공급자에 의해 DBPARAMINFO 구조의 *wType* 멤버가 DBTYPE_TABLE로 설정됩니다. DBPARAMINFO 구조의 *ulParamSize* 필드 값은 ~0입니다.  
  
 그런 다음, 소비자는 ISSCommandWithParameters::GetParameterProperties를 사용하여 추가 속성(테이블 반환 매개 변수 형식 카탈로그 이름, 테이블 반환 매개 변수 형식 스키마 이름, 테이블 반환 매개 변수 형식 이름, 열 순서 및 기본 열)을 요청합니다.  
  
 형식 이름이 확인되면 소비자는 IOpenRowset::OpenRowsetor를 호출하거나 테이블 반환 매개 변수 형식 이름을 테이블 이름으로 지정하여 DBSCHEMA_TABLE_TYPE_COLUMNS 행 집합을 가져옴으로써 개별 열 정보를 검색해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 반환 매개 변수 OLE DB &#40;&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
