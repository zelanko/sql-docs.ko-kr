---
description: Microsoft Active Directory 서비스용 microsoft OLE DB 공급자
title: Microsoft Active Directory 서비스용 microsoft OLE DB 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: rothja
ms.author: jroth
ms.openlocfilehash: 08d945b101ac91300793920e3e01ea0a9619b372
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991054"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft Active Directory 서비스용 microsoft OLE DB 공급자
ADSI (Active Directory 서비스 인터페이스) 공급자를 사용 하면 ADO에서 ADSI를 통해 다른 유형의 디렉터리 서비스에 연결할 수 있습니다. 이를 통해 ADO 응용 프로그램은 LDAP 규격 디렉터리 서비스와 Novell 디렉터리 서비스 외에 Microsoft Windows NT 4.0 및 Microsoft Windows 2000 디렉터리 서비스에 대 한 읽기 전용 액세스를 제공 합니다. ADSI 자체는 공급자 모델을 기반으로 하므로 다른 디렉터리에 대 한 액세스 권한을 부여 하는 새 공급자가 있는 경우 ADO 응용 프로그램에서이를 원활 하 게 액세스할 수 있습니다. ADSI 공급자는 자유 스레드된 및 유니코드를 사용할 수 있습니다.  
  
## <a name="connection-string-parameters"></a>연결 문자열 매개 변수  
 이 공급자에 연결 하려면 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) 속성의 **공급자** 인수를 다음과 같이 설정 합니다.  
  
```vb
ADSDSOObject  
```  
  
 [공급자](../../reference/ado-api/provider-property-ado.md) 속성을 읽으면이 문자열도 반환 됩니다.  
  
## <a name="typical-connection-string"></a>일반 연결 문자열  
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 문자열은 다음 키워드로 구성 됩니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|**공급 기업**|Active Directory 서비스에 대 한 OLE DB 공급자를 지정 합니다.|  
|**사용자 ID**|사용자 이름을 지정합니다. 이 키워드를 생략 하면 현재 로그온이 사용 됩니다.|  
|**암호**|사용자 암호를 지정 합니다. 이 키워드를 생략 하면입니다. 그런 다음 현재 로그온이 사용 됩니다.|  
  
> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.  
  
## <a name="command-text"></a>명령 텍스트  
 다음 구문에서는 네 부분으로 구성 된 명령 텍스트 문자열이 공급자에 의해 인식 됩니다.  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|값|설명|  
|-----------|-----------------|  
|*루트가*|검색을 시작할 **ADsPath** 개체 (즉, 검색의 루트)를 나타냅니다.|  
|*Filter*|RFC 1960 형식의 검색 필터를 나타냅니다.|  
|*특성*|반환할 특성의 쉼표로 구분 된 목록을 나타냅니다.|  
|*범위*|선택 사항입니다. 검색 범위를 지정 하는 **문자열** 입니다. 다음 중 하나일 수 있습니다.<br /><br /> -Base-기준 개체 (검색의 루트)만 검색 합니다.<br />-OneLevel-한 수준만 검색 합니다.<br />-하위 트리-전체 하위 트리를 검색 합니다.|  
  
 예를 들어:  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 공급자는 명령 텍스트에 대해 SQL SELECT도 지원 합니다. 다음은 그 예입니다.  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>설명  
 공급자는 저장 프로시저 호출 또는 간단한 테이블 이름을 허용 하지 않습니다. 예를 들어, [CommandType](../../reference/ado-api/commandtype-property-ado.md) 속성은 항상 **adcmdtext**입니다. 명령 텍스트 요소에 대 한 자세한 설명은 Active Directory 서비스 인터페이스 설명서를 참조 하세요.  
  
## <a name="recordset-behavior"></a>레코드 집합 동작  
 다음 표에서는이 공급자를 사용 하 여 연 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체에 사용할 수 있는 기능을 나열 합니다. 정적 커서 유형 (**Adopenstatic**)만 사용할 수 있습니다.  
  
 공급자 구성의 **레코드 집합** 동작에 대 한 자세한 내용을 보려면 [Supports](../../reference/ado-api/supports-method.md) 메서드를 실행 하 고 **레코드 집합** 의 [속성](../../reference/ado-api/properties-collection-ado.md) 컬렉션을 열거 하 여 공급자별 동적 속성이 있는지 여부를 확인 합니다.  
  
 **표준 ADO 레코드 집합 속성의 가용성:**  
  
|속성|가용성|  
|--------------|------------------|  
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|읽기/쓰기|  
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|읽기/쓰기|  
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|읽기 전용|  
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|  
|[책갈피](../../reference/ado-api/bookmark-property-ado.md)|읽기/쓰기|  
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|읽기/쓰기|  
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|항상 **Aduseserver**|  
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|항상 **Adopenstatic**|  
|[EditMode](../../reference/ado-api/editmode-property.md)|항상 **adEditNone**|  
|[객체](../../reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|  
|[Filter](../../reference/ado-api/filter-property.md)|읽기/쓰기|  
|[LockType](../../reference/ado-api/locktype-property-ado.md)|읽기/쓰기|  
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|사용할 수 없음|  
|[Records](../../reference/ado-api/maxrecords-property-ado.md)|읽기/쓰기|  
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|읽기 전용|  
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|읽기/쓰기|  
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|읽기 전용|  
|[원본](../../reference/ado-api/source-property-ado-recordset.md)|읽기/쓰기|  
|[State](../../reference/ado-api/state-property-ado.md)|읽기 전용|  
|[상태](../../reference/ado-api/status-property-ado-recordset.md)|읽기 전용|  
  
 **표준 ADO 레코드 집합 메서드의 가용성:**  
  
|방법|사용 가능 여부|  
|------------|----------------|  
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|아니요|  
|[취소](../../reference/ado-api/cancel-method-ado.md)|아니요|  
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|아니요|  
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|아니요|  
|[복제](../../reference/ado-api/clone-method-ado.md)|예|  
|[닫기](../../reference/ado-api/close-method-ado.md)|예|  
|[Delete](../../reference/ado-api/delete-method-ado-recordset.md)|아니요|  
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|예|  
|[이동](../../reference/ado-api/move-method-ado.md)|예|  
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[MoveLast](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)|예|  
|[열기](../../reference/ado-api/open-method-ado-recordset.md)|예|  
|[매크로](../../reference/ado-api/requery-method.md)|예|  
|[다시 동기화](../../reference/ado-api/resync-method.md)|예|  
|[지원](../../reference/ado-api/supports-method.md)|예|  
|[Update](../../reference/ado-api/update-method.md)|아니요|  
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|아니요|  
  
 ADSI 및 공급자의 세부 사항에 대 한 자세한 내용은 Active Directory 서비스 인터페이스 설명서를 참조 하거나 ADSI 웹 페이지를 방문 하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [CommandType 속성 (ADO)](../../reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString 속성 (ADO)](../../reference/ado-api/connectionstring-property-ado.md)   
 [Properties 컬렉션 (ADO)](../../reference/ado-api/properties-collection-ado.md)   
 [Provider 속성 (ADO)](../../reference/ado-api/provider-property-ado.md)   
 [레코드 집합 개체 (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [Supports 메서드](../../reference/ado-api/supports-method.md)