---
title: ADO 변경 이력 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
manager: craigg
ms.openlocfilehash: e00a1ff652e3f1463d37e2cd5457965968b4ba4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709561"
---
# <a name="ado-features-for-each-release"></a>버전별 ADO 기능
이 항목에서는 ADO와 ADO MD, ADOX의 각 버전에서 도입된 새 기능을 나열합니다.

## <a name="ado-60"></a>ADO 6.0
 ADO 6.0은 Windows Vista에서 Windows Data Access Components (Windows DAC) 6.0의 일부로 포함됩니다. ADO 6.0은 ADO 2.8과 기능적으로 동일합니다.

## <a name="ado-28"></a>ADO 2.8
 Windows XP 및 Windows Server 2003의 Microsoft 데이터 액세스 구성 요소 (MDAC) 2.8 일부로 ADO 2.8 포함 되었습니다. MDAC 2.8 재배포 가능 패키지 버전은 사용할 수 있습니다; 또한 Windows 2000에만이 재배포 가능 패키지 버전을 설치 해야 하는 참고 합니다. ADO 2.8 몇 가지 보안 관련 문제를 해결 합니다.

 *신뢰할 수 있는 영역 외부 하드 드라이브 액세스가 허용 되지 않습니다.*
도메인 간 트러스트와 관련 된 사이트 스크립팅에서 다음 작업은 사용 하지 않도록 설정: **Stream.SaveToFile**를 **Stream.LoadFromFile**하십시오 **Recordset.Save**, 및 **Recordset.Open**와 함께에서 사용 합니다 **adCmdFile** 플래그 또는 Microsoft OLE DB 지 속성 공급자 (MSPersist).

 **Recordset.Open** *를***Recordset.Save** *하십시오***Stream.SaveToFile** *, 및* **Stream.LoadFromFile***물리적 파일에만 작동 합니다.* 
이러한 메서드는 이제 파일 핸들 실제 파일만를 가리키는지 확인 합니다.

 **Recordset.ActiveCommand***HTML/ASP 페이지에서 호출 될 때 오류를 반환 합니다.* 
그래야 합니다 **명령** 막을 개체입니다.

 *수가***레코드 집합***중첩 된 반환한***셰이프***명령에 상한 값입니다.* 
중첩 된 shape 명령에는 이제 최대 512 반환 **레코드 집합**합니다. 즉를 **셰이프** 명령을 모든 수준에서 더 이상 중첩 될 수 없습니다. 각 명령 (자식)는 단일 결과 경우 최대 수준 512을가 하는 대신 **레코드 집합**합니다. 모든 수준에서의 경우는 **셰이프** 명령을 여러 개 반환 합니다 **레코드 집합**, 최대 깊이 수준은 512 보다 작은 됩니다.

## <a name="ado-27"></a>ADO 2.7
 *64비트 플랫폼 지원* ADO 2.7부터 64비트 프로세서를 지원하기 시작했습니다.

## <a name="ado-26"></a>ADO 2.6
 **CubDef.GetSchemaObject***메서드* ADO 2.6부터 ADO MD 개체를 검색할 수 있습니다에 지정 된 대로 고유 이름을 사용 하 여 [UniqueName 속성 (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)합니다.   부모 개체의 이름을 알 수 하지 않아도 및 부모 컬렉션 스키마 개체를 검색 하려면 채울 필요가 없습니다. 참조 [GetSchemaObject 메서드 (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)합니다.

 *명령 스트림을* 는 **명령** 개체가 사용 하는 대신 명령 스트림 형식에서 지원 합니다 **CommandText** 속성입니다. 합니다 [CommandStream 속성 (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) XML 템플릿 또는 updategram으로 지정할 수는 **명령** SQL Server 용 Microsoft OLE DB Provider를 사용 하 여 입력 합니다.

 **Dialect***속성* [언어](../../ado/reference/ado-api/dialect-property.md) 구문을 정의 하는 새 속성 이며 일반 공급자 문자열 또는 스트림에 구문 분석 하는 규칙입니다.  

 **Command.Execute***메서드* 는 [Execute 메서드](../../ado/reference/ado-api/execute-method-ado-command.md) ADO의 **명령** 개체는 입력 및 출력 스트림을 사용 하도록 향상 되었습니다.  

 *Statusvalues 필드* 수정 하는 경우 사용자가 DB_E_ERRORSOCCURRED 오류를 발견할 경우는 **필드** 의 **레코드 집합**, ADO를 채울 이제는 **Field.Status**적절 한 상태 정보를 사용 하 여 속성을 갖도록 사용자는 무엇이 잘못 되었는지에 대 한 자세한 내용은 합니다. 참조 [Status 속성 (ADO 필드)](../../ado/reference/ado-api/status-property-ado-field.md)합니다.

 **NamedParameters***속성* [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md) 는의 새로운 속성을 **명령** 공급자를 사용 해야 함을 나타내는 개체의 이름은 매개 변수입니다.  

 *스트림에서 Resultsets* ADO의 데이터 소스에서 결과 집합을 반환할 수 있습니다를 **Stream**, 대신 **레코드 집합** 개체입니다. 최신 버전의 Microsoft OLE DB Provider for SQL Server를 사용 하는 "XML" 쿼리를 실행 하 여 공급자 로부터 XML 결과 가져올 수 있습니다. A **Stream** 결과 집합을 수신 하는 원본으로 "XML" 명령을 사용 하 여 열 수 있습니다. 참조 [스트림으로 결과 집합 검색](../../ado/guide/data/retrieving-resultsets-into-streams.md)합니다.

 *단일 행 결과 집합* ADO **레코드** 명령 문자열에서 이제 개체를 열 수 나 **명령** 공급자에서 데이터 행 하나를 반환 하는 개체입니다. 그러면 MDAC 2.6 공급자를 사용 하 여 성능이 향상 됩니다. 참조 [Open 메서드 (ADO 레코드)](../../ado/reference/ado-api/open-method-ado-record.md)합니다.

## <a name="ado-25"></a>ADO 2.5
 **레코드** *개체* 2.5 ADO 소개 합니다 **레코드** 나타내고에서 행을 관리 하는 개체를 **레코드 집합** 데이터 공급자 또는 캡슐화 하는 개체를 파일 또는 디렉터리와 같은 반 구조화 된 데이터입니다.

 **Stream** *개체* ADO 2.5 폴더도 **Stream** 이진 또는 텍스트 데이터 스트림을 나타내는 개체입니다.

 *URL 바인딩을* 2.5 ADO 연결 문자열 및 명령 텍스트, 데이터 저장소 개체 이름으로 하는 대신 URL 사용 방법을 소개 합니다. URL을 사용 하 여 기존 **연결** 하 고 **레코드 집합** 개체에도 새와 마찬가지로 **레코드** 및 **Stream** 개체입니다.

 *URL 바인딩을 지 원하는 데이터 공급자* ADO 2.5 URL 스키마를 인식 하는 OLE DB 공급자를 지원 합니다. 여기에 OLE DB Provider for Internet Publishing, Windows 2000 파일 시스템에 액세스 하 고 기존 HTTP 체계를 인식 합니다.
