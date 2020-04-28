---
title: ADO 기록 | Microsoft Docs
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
ms.openlocfilehash: a84ccbb97c26ea92f31212933aac79bde2784b72
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67927164"
---
# <a name="ado-features-for-each-release"></a>각 릴리스에 대 한 ADO 기능

이 항목에서는 ADO, ADO MD 및 ADOX의 각 릴리스에 도입 된 새로운 기능을 나열 합니다.

## <a name="ado-60"></a>ADO 6.0

 Windows Vista에서는 windows DAC (Windows Data Access Components) 6.0의 일부로 ADO 6.0이 포함 되어 있습니다. ADO 6.0는 ADO 2.8와 기능적으로 동일 합니다.

## <a name="ado-28"></a>ADO 2.8

 ADO 2.8는 MDAC (Microsoft Data Access Components) 2.8의 일부로 Windows XP 및 Windows Server 2003에 포함 되었습니다. 재배포 가능 버전의 MDAC 2.8도 사용할 수 있습니다. 이 재배포 가능 버전은 Windows 2000에만 설치 해야 합니다. ADO 2.8은 몇 가지 보안 관련 문제를 해결 합니다.

 *신뢰할 수 있는 영역 외부에서는 하드 드라이브 액세스가 허용 되지 않습니다.*
트러스트 되지 않은 **사이트와 관련**된 도메인 간 스크립팅에는 SaveToFile, LoadFromFile, **Stream.SaveToFile**, **Stream.LoadFromFile** **, 및**작업을 사용할 수 없습니다. **Adcmdfile** 플래그와 함께 사용 되거나 mspersist (Microsoft OLE DB 지 속성 공급자)와 함께 사용 됩니다.

 **Recordset.Open** _,_**Recordset.Save** _,_**SaveToFile** , LoadFromFile _및_**stream**. 열_은 물리적 파일 에서만 작동 합니다_ .        
이러한 메서드는 이제 파일 핸들이 물리적 파일만 가리키도록 확인 합니다.

 **ActiveCommand**는_HTML/ASP 페이지에서 호출 될 때 오류를 반환 합니다._  
이렇게 하면 **명령** 개체가 오용 되지 않습니다.

 중첩 된**Shape**명령에_의해 반환 되_는**레코드 집합** _의 수는__상한이 있습니다._        
이제 중첩 된 shape 명령이 최대 512 개의 **레코드 집합**을 반환 합니다. 이는 **Shape** 명령이 더 이상 중첩 될 수 없음을 의미 합니다. 대신 각 명령이 단일 (자식) **레코드 집합**을 생성 하는 경우 최대 수준 깊이는 512입니다. 어떤 수준에서 나 **Shape** 명령이 여러 **레코드 집합**을 반환 하는 경우 최대 깊이 수준은 512 보다 낮습니다.

## <a name="ado-27"></a>ADO 2.7

 *64 비트 플랫폼 지원* ADO 2.7에는 64 비트 프로세서에 대 한 지원이 도입 되었습니다.

## <a name="ado-26"></a>ADO 2.6

 **CubDef** [UniqueName ADO MD 속성](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)에 지정 된 대로 ADO MD 개체는 ADO_2.6부터 고유_ 이름을 사용 하 여 검색할 수 있습니다.   부모 개체의 이름을 알 필요는 없으며 스키마 개체를 검색 하기 위해 부모 컬렉션을 채울 필요가 없습니다. [Getschemaobject 메서드 (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)를 참조 하세요.

 *명령 스트림* **명령** 개체는 **CommandText** 속성을 사용 하는 대신 스트림 형식의 명령을 지원 합니다. [Commandstream 속성 (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) 은 SQL Server 용 Microsoft OLE DB 공급자를 사용 하 여 XML 템플릿 또는 updategram을 **명령** 입력으로 지정 하는 데 사용할 수 있습니다.

 **언어**  _속성_ [언어](../../ado/reference/ado-api/dialect-property.md) 는 공급자가 문자열 또는 스트림을 구문 분석 하는 데 사용 하는 구문 및 일반 규칙을 정의 하는 새 속성입니다.

 **명령 실행**_메서드_ 입력 및 출력에 대 한 스트림을 사용 하도록 ADO **명령** 개체의 [Execute 메서드가](../../ado/reference/ado-api/execute-method-ado-command.md) 향상 되었습니다.  

 *필드 statusvalues* **레코드 집합**의 **필드** 를 수정할 때 사용자에 게 DB_E_ERRORSOCCURRED 오류가 발생 하면 ADO는 이제 사용자에 게 잘못 된 문제에 대 한 자세한 정보를 제공 하도록 적절 한 상태 정보를 사용 하 여 **status** 속성을 채웁니다. [Status 속성 (ADO 필드)](../../ado/reference/ado-api/status-property-ado-field.md)을 참조 하세요.

 **Namedparameters**  _속성_ [namedparameters](../../ado/reference/ado-api/namedparameters-property-ado.md) 는 공급자가 명명 된 매개 변수를 사용 해야 함을 나타내는 **Command** 개체의 새 속성입니다.

 *스트림의 결과 집합* ADO는 **레코드 집합** 개체가 아닌 **스트림의**데이터 원본에서 결과 집합을 반환할 수 있습니다. 최신 버전의 SQL Server 용 Microsoft OLE DB 공급자를 사용 하 여 "For XML" 쿼리를 실행 하 여 공급자 로부터 XML 결과를 얻을 수 있습니다. Resultset을 받는 **스트림은** "For XML" 명령을 원본으로 사용 하 여 열 수 있습니다. [스트림에 결과 집합 검색](../../ado/guide/data/retrieving-resultsets-into-streams.md)을 참조 하세요.

 *단일 행 resultset* 이제 공급자에서 데이터의 한 행을 반환 하 **는 명령 문자열 또는 명령** 개체에서 ADO **Record** 개체를 열 수 있습니다. 이로 인해 MDAC 2.6 공급자의 성능이 향상 됩니다. [Open 메서드 (ADO 레코드)](../../ado/reference/ado-api/open-method-ado-record.md)를 참조 하세요.

## <a name="ado-25"></a>ADO 2.5

 **Record** _개체_ ADO 2.5는 레코드 **집합이** 나 데이터 공급자의 행을 표시 하 고 관리 하기 위한 **record** 개체 또는 파일이 나 디렉터리와 같은 반 구조화 된 데이터를 캡슐화 하는 개체를 소개 합니다.

 **Stream** _개체_ ADO 2.5는 이진 또는 텍스트 데이터 스트림을 나타내는 **stream** 개체를 도입 합니다.

 *URL 바인딩* ADO 2.5에서는 연결 문자열과 명령 텍스트 대신 URL을 사용 하 여 데이터 저장소 개체의 이름을 사용 하는 방법을 소개 합니다. URL은 기존 **연결** 및 **레코드 집합** 개체 뿐만 아니라 새 **레코드** 및 **스트림** 개체와 함께 사용할 수 있습니다.

 *URL 바인딩을 지 원하는 데이터 공급자* ADO 2.5는 URL 체계를 인식 하는 OLE DB 공급자를 지원 합니다. 여기에는 Windows 2000 파일 시스템에 액세스 하 고 기존 HTTP 체계를 인식 하는 인터넷 게시용 OLE DB 공급자가 포함 됩니다.
