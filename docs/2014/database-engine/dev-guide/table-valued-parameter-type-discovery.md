---
title: 테이블 반환 매개 변수 형식 검색 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: eea5d45c4c21b740a3ea91ee27023129b33719b3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082314"
---
# <a name="table-valued-parameter-type-discovery"></a>테이블 반환 매개 변수 형식 검색
  소비자-즉, 응용 프로그램 사용 하는 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자-OLE DB 공급자에 명령 텍스트에 지정 된 경우 각 명령 매개 변수의 형식을 검색할 수 있습니다. 테이블 반환 매개 변수 형식의 알려진 후 소비자는 테이블 반환 매개 변수의 개별 열에 대 한 메타 데이터 정보를 검색할 수 있습니다.  
  
 프로시저 매개 변수의 형식 정보는 대부분 매개 변수 형식에 대 한 icommandwithparameters:: Getparameterinfo에서 지원 됩니다. 부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], 사용자 정의 형식의 도입으로 및 `xml` 데이터 형식을 GetParameterInfo 메서드 충분 하지 않은이 목적을 위해 사용자 정의 형식 정보를 제공할 수 없기 때문에 (이름, 스키마 및 ICommandWithParameters 통해 카탈로그). 확장된 유형 정보를 제공 하는 새로운 인터페이스 ISSCommandWithParameters, 정의 되었습니다.  
  
 테이블 반환 매개 변수에 대 한도 세부 정보를 검색할 ISSCommandWithParameters 인터페이스를 사용 합니다. 클라이언트는 명령 개체를 준비한 후 ISSCommandWithParameters::GetParameterInfo를 호출 합니다. 에 대 한 테이블 반환 매개 변수는 *wType* 공급자에 의해 DBPARAMINFO 구조체의 멤버 DBTYPE_TABLE로 설정 됩니다. *ulParamSize* DBPARAMINFO 구조의 필드 값은 ~ 0입니다.  
  
 소비자는 ISSCommandWithParamters를 사용 하 여 추가 속성 (테이블 반환 매개 변수 형식 카탈로그 이름, 테이블 반환 매개 변수 형식 스키마 이름, 테이블 반환 매개 변수 형식 이름, 열 순서 및 기본 열)을 요청 다음:: GetParameterProperties 합니다.  
  
 형식 이름이 알려져 있으면 후 소비자 호출 해야 하거나 개별 열 정보를 검색할 IOpenRowset::OpenRowsetor 가져올 DBSCHEMA_TABLE_TYPE_COLUMNS 행 집합을 테이블 반환 매개 변수 형식 이름을 테이블 이름으로 지정 하 여.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수를 사용 하 여 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  