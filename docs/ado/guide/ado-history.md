---
title: ADO 변경 이력 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7fcdee5d45cffb14af2f1e0dc73941689c7fda4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702841"
---
# <a name="ado-features-for-each-release"></a>버전별 ADO 기능

이 항목에서는 ADO와 ADO MD, ADOX의 각 버전에서 도입된 새 기능을 나열합니다.

## <a name="ado-60"></a>ADO 6.0

 ADO 6.0은 Windows Vista에서 Windows Data Access Components (Windows DAC) 6.0의 일부로 포함됩니다. ADO 6.0은 ADO 2.8과 기능적으로 동일합니다.

## <a name="ado-28"></a>ADO 2.8

 ADO 2.8은 Microsoft Data Access Components (MDAC) 2.8의 일부로, Windows XP와 Windows Server 2003에 포함되었습니다. MDAC 2.8 재배포 가능 패키지 역시 사용할 수 있습니다. 이 재배포 가능 패키지는 Windows 2000에서만 설치될 수 있음에 유의하십시오. ADO 2.8은 몇 가지 보안 관련한 문제를 해결합니다.

 *신뢰할 수 있는 영역 외부의 하드 드라이브 액세스가 허용되지 않습니다.*
도메인 간 트러스트 되지 않은 사이트와 관련 된 스크립팅에서 다음 작업을 사용 하는 사용할 수 없습니다. **Stream.SaveToFile**, **Stream.LoadFromFile**, **Recordset.Save**, 및 **Recordset.Open**과 함께에서 사용 되는는 **adCmdFile**  플래그 또는 Microsoft OLE DB 지 속성 공급자 (MSPersist).

 **Recordset.Open** _,_ **Recordset.Save** _,_ **Stream.SaveToFile** _,_ **Stream.LoadFromFile** _은 물리적 파일에서만 동작합니다._
이 메서드들은 파일 핸들이 물리적 파일을 가리키는지 확인합니다.

 **Recordset.ActiveCommand** _는 HTML/ASP 페이지에서 호출될 때 오류를 반환합니다_
이것은 **Command** 개체가 오용되는 것을 방지해 줍니다.

 _중첩된_ **Shape** _명령으로 반환되는_ **Recordsets** _의 수는 일정한 최대값 이상이 될 수 없습니다._
현재 중첩된 shape 명령은 최대 512개의 **Recordsets**를 반환합니다. 이것은 **Shape** 명령을 더 이상 중첩할 수 없다는 뜻입니다. 대신 각 명령에서 단일 (하위) **Recordset**가 발생하면 최대 깊이 수준은 512입니다. 모든 수준에서 **Shape** 명령이 여러 개의 **Recordsets**를 반환하면 최대 깊이 수준은 512 미만이 됩니다.

## <a name="ado-27"></a>ADO 2.7

 *64비트 플랫폼 지원* ADO 2.7부터 64비트 프로세서를 지원하기 시작했습니다.

## <a name="ado-26"></a>ADO 2.6

 **CubDef.GetSchemaObject** _메서드_ ADO 2.6부터 ADO MD 개체는 [UniqueName 속성(ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)으로 지정된 고유한 이름을 사용하여 검색할 수 있습니다. 부모 개체의 이름을 알 필요가 없고, 스키마 오브젝트를 검색하기 위해 상위 컬렉션을 채울 필요가 없습니다. [GetSchemaObject 메서드(ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)를 참조하십시오.

 *Command streams* **Command** 개체는 **CommandText** 속성을 사용하는 대체제로 스트림 형식의 명령을 지원합니다. [CommandStream 속성(ADO)](../../ado/reference/ado-api/commandstream-property-ado.md)을 사용하여 SQL Server용 Microsoft OLE DB 공급자에 대한 **명령**을 입력하여 XML 템플릿 또는 updategram을 지정할 수 있습니다.

 **Dialect** _속성_ [Dialect](../../ado/reference/ado-api/dialect-property.md) 속성은 공급자가 문자열이나 스트림을 구문 분석하는 데 사용하는 구문과 일반 규칙을 정의하는 새로운 속성입니다.

 **Command.Execute** _메서드_ ADO **Command** 개체의 [Execute 메서드](../../ado/reference/ado-api/execute-method-ado-command.md)는 입력 및 출력 스트림을 사용하도록 향상 되었습니다.

 *Field Statusvalues* **Recordset** 개체의 **Field** 를 수정할 때 DB_E_ERRORSOCCURRED 오류가 발생하면 ADO는 **Field.Status** 속성에 적절한 상태 정보를 채웁니다. 그러면 사용자가 잘못된 항목에 대한 자세한 정보를 얻을 수 있습니다. [Status 속성(ADO Field)](../../ado/reference/ado-api/status-property-ado-field.md)을 참조하십시오.

 **NamedParameters** _속성_ [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md)는 공급자가 명명된 매개 변수를 사용해야 함을 나타내는 **Command** 개체의 새 속성입니다.

 *스트림에서의 Resultsets* ADO는 **Recordset** 개체 대신 **Stream** 개체에서 데이터 원본의 결과 집합을 반환할 수 있습니다. SQL Server용 Microsoft OLE DB Provider의 최신 버전을 사용하면 "For XML" 쿼리를 실행하여 공급자로부터 XML 결과를 얻을 수 있습니다. 결과 집합을 받는 **스트림**은 "For XML" 명령을 소스로 사용하여 열 수 있습니다. [스트림으로 결과 집합 검색](../../ado/guide/data/retrieving-resultsets-into-streams.md)을 참고하십시오.

 *단일 행 결과 집합* 이제 ADO **Record** 개체를 공급자로부터 데이터 행 하나를 반환하는 명령 문자열 또는 **Command** 개체에서 열 수 있습니다. 따라서 MDAC 2.6 공급자의 성능이 향상됩니다. [Open 메서드(ADO Record)](../../ado/reference/ado-api/open-method-ado-record.md)를 참고하십시오.

## <a name="ado-25"></a>ADO 2.5

 **레코드** _개체_ ADO 2.5에서는 **Record** 체가 도입되었습니다. 이것은 다음과 같은 데이터를 행으로 나타내거나 관리할 수 있습니다. **Recordset** 개체, 데이터 공급자, 파일이나 디렉터리와 같은 반 구조화된 데이터.

 **Stream** _개체_ ADO 2.5에서는 바이너리/텍스트 데이터의 스트림을 나타내는 **Stream** 개체가 도입되었습니다.

 *URL 바인딩* ADO 2.5에서는 데이터 저장소 개체의 이름을 지정하기 위해 연결 문자열 및 명령 텍스트 대신 URL을 사용합니다. URL은 기존의 **Connection** 및 **Recordset** 개체뿐만 아니라 새로운 **Record** 및 **Stream** 개체와 함께 사용할 수 있습니다.

 *URL 바인딩을 지원하는 데이터 공급자* ADO 2.5는 URL 스키마를 인식하는 OLE DB 공급자를 지원합니다. 여기에는 Windows 2000 파일 시스템에 액세스하고 기존 HTTP 구성표를 인식하는 OLE DB Provider for Internet Publishing이 포함됩니다.
