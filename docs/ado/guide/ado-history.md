---
title: "ADO 기록 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e76e56b9d1840d4e6e1f42acd10b3b9226a61d4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="ado-features-for-each-release"></a>각 릴리스에 대 한 ADO 기능
이 항목에서는 ADO, ADO MD 및 ADOX의 각 버전에서 도입 된 새로운 기능을 나열 합니다.

## <a name="ado-60"></a>ADO 6.0
 ADO 6.0 Windows Vista, Windows Data Access Components (Windows DAC) 6.0의 일부로 포함 됩니다. ADO 6.0 ADO 2.8 기능적으로 같습니다.

## <a name="ado-28"></a>ADO 2.8
 Windows XP 및 Windows Server 2003의 Microsoft 데이터 액세스 구성 요소 (MDAC) 2.8 일부로 ADO 2.8 포함 되었습니다. MDAC 2.8 재배포 가능 버전도 있습니다. 참고가 재배포 가능 버전 Windows 2000에만 설치 해야 합니다. ADO 2.8 몇 가지 보안 관련 문제를 해결합니다.

 *신뢰할 수 있는 영역 외부 하드 드라이브 액세스가 허용 되지 않습니다.*
도메인 간 스크립팅 관련 된 트러스트 되지 않은 사이트에서 다음 작업이 비활성화 됩니다: **Stream.SaveToFile**, **Stream.LoadFromFile**, **Recordset.Save**, 및 **Recordset.Open**와 함께에서 사용 되는 **adCmdFile** 플래그 또는 공급자와 함께 Microsoft OLE DB 지 속성 (MSPersist).

 **Recordset.Open** *,***Recordset.Save** *,***Stream.SaveToFile** *, 및* **Stream.LoadFromFile***만 실제 파일에서 작동 합니다.* 
이러한 메서드는 이제 파일 핸들이 물리적 파일에만 해당를 가리키는지 확인 합니다.

 **Recordset.ActiveCommand***HTML/ASP 페이지에서 호출 될 때 오류를 반환 합니다.* 
이렇게 하면는 **명령** 의 부적절 한 개체입니다.

 *수가***레코드 집합***중첩 된 반환한***셰이프***명령에 상한 값입니다.* 
중첩 된 shape 명령에는 이제 최대 512의 반환 **레코드 집합**합니다. 즉, 한 **셰이프** 명령을 모든 수준에서 더 이상 중첩 될 수 없습니다. 대신, 최대 수준 깊이로 512로, 각 명령 (자식)는 단일 결과가 같은 경우 **레코드 집합**합니다. 모든 수준에서 if는 **셰이프** 명령은 여러 반환 **레코드 집합**의 최대 수준을 512 보다 작은 수 있습니다.

## <a name="ado-27"></a>ADO 2.7
 *64 비트 플랫폼 지원* ADO 2.7 64 비트 프로세서에 대 한 지원이 도입 되었습니다.

## <a name="ado-26"></a>ADO 2.6
 **CubDef.GetSchemaObject***메서드* ADO 2.6 부터는 ADO MD 개체를 검색할 수에 지정 된 대로 고유한 이름을 사용 하 여 [UniqueName 속성 ADO MD](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)합니다. 부모 개체의 이름을 알면 됩니다 필요 없고 부모 컬렉션 스키마 개체를 가져와 채울 필요는 없습니다. 참조 [GetSchemaObject 메서드 ADO MD](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)합니다.

 *스트림을 명령* 는 **명령** 개체가 스트림 형태로 표시 명령을 사용 하는 대신 지원는 **CommandText** 속성입니다. [CommandStream 속성 (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) 는 XML 서식 파일 또는 updategram으로 지정 하는 데 사용할 수는 **명령** SQL Server 용 Microsoft OLE DB 공급자와 함께 입력 합니다.

 **언어***속성* [언어](../../ado/reference/ado-api/dialect-property.md) 구문을 정의 하는 새 속성 및 공급자 문자열 또는 스트림에 구문 분석을 사용 하 여 일반 규칙입니다.

 **Command.Execute***메서드* 는 [Execute 메서드](../../ado/reference/ado-api/execute-method-ado-command.md) ADO의 **명령** 개체 입력 및 출력 스트림을 사용 하도록 향상 되었습니다.

 *Statusvalues 필드* 사용자 수정 하는 경우에 DB_E_ERRORSOCCURRED 오류가 발생할 경우 한 **필드** 의 **레코드 집합**, ADO를 채울 이제는 **Field.Status**적절 한 상태 정보를 사용 하 여 속성 함으로써 사용자가을 갖도록 무엇이 잘못 되었는지에 대 한 자세한 정보. 참조 [Status 속성 (ADO 필드)](../../ado/reference/ado-api/status-property-ado-field.md)합니다.

 **NamedParameters***속성* [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md) 는의 새로운 속성은 **명령** 공급자 사용 해야 함을 나타내는 개체의 이름은 매개 변수입니다.

 *스트림에서 Resultsets* ADO에 있는 데이터 원본의 결과 집합을 반환할 수 있습니다는 **스트림**, 아닌 **레코드 집합** 개체입니다. 최신 버전의 Microsoft OLE DB Provider for SQL Server를 사용 하는 "XML" 쿼리를 실행 하 여 공급자에서 XML 결과 얻을 수 있습니다. A **스트림** 결과 집합을 받는 소스로 "XML" 명령을 사용 하 여 열 수 있습니다. 참조 [스트림으로 결과 집합 검색](../../ado/guide/data/retrieving-resultsets-into-streams.md)합니다.

 *단일 행 결과 집합* The ADO **레코드** 명령 문자열에서 이제 개체를 열 수 또는 **명령** 공급자에서 데이터의 한 행을 반환 하는 개체입니다. 이 인해 MDAC 2.6 공급자와 함께 성능 향상된. 참조 [Open 메서드 (ADO 레코드)](../../ado/reference/ado-api/open-method-ado-record.md)합니다.

## <a name="ado-25"></a>ADO 2.5
 **레코드** *개체* ADO 2.5 소개는 **레코드** 나타내고에서 행을 관리 하는 개체는 **레코드 집합** 데이터 공급자 또는 개체 예: 파일 또는 디렉터리의 반 구조화 된 데이터를 캡슐화 합니다.

 **스트림** *개체* ADO 2.5도 소개 합니다.는 **스트림** 이진 또는 텍스트 데이터 스트림을 나타내는 개체를 합니다.

 *URL 바인딩을* ADO 2.5 URL 사용 하는 연결 문자열 및 명령 텍스트를 데이터 저장소 개체 이름에 대 한 대안을 소개 합니다. URL을 사용 하 여 기존 **연결** 및 **레코드 집합** 개체도 새와 마찬가지로 **레코드** 및 **스트림** 개체입니다.

 *URL 바인딩을 지 원하는 데이터 공급자* ADO 2.5 URL 스키마를 인식 하는 OLE DB 공급자를 지원 합니다. 여기에 OLE DB Provider for Internet Publishing, Windows 2000 파일 시스템에 액세스 하 고 기존 HTTP 체계 인식입니다.
