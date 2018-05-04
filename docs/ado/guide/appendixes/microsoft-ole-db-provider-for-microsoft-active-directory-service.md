---
title: Microsoft Active Directory 서비스에 대 한 Microsoft OLE DB Provider | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c38caaead8d2eb1fa24a4b7a38aebfdc19cbcec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft Active Directory 서비스에 대 한 Microsoft OLE DB Provider
서비스 인터페이스 ADSI (Active Directory) 공급자 ADO를 ADSI 통해 유형이 다른 디렉터리 서비스에 연결할 수 있습니다. 그러면 ADO 응용 프로그램에서는 읽기 전용 액세스할 모든 LDAP 호환 디렉터리 서비스 및 Novell 디렉터리 서비스 외에 Microsoft Windows NT 4.0 및 Microsoft Windows 2000 디렉터리 서비스에 있습니다. ADO 응용 프로그램 원활 하 게 액세스할 수 없는 경우 다른 디렉터리에 새 공급자 주어진 액세스, 있도록 ADSI 자체 공급자 모델에 기반 합니다. ADSI 공급자는 자유 스레드 및 유니코드를 사용할 수 있습니다.  
  
## <a name="connection-string-parameters"></a>연결 문자열 매개 변수  
 이 공급자에 연결할 설정는 **공급자** 의 인수는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을 다음:  
  
```  
ADSDSOObject  
```  
  
 읽기는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성은이 문자열을 반환 합니다.  
  
## <a name="typical-connection-string"></a>일반적인 연결 문자열  
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.  
  
```  
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 다음 키워드 중 문자열 구성 됩니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|**공급자**|Active Directory 서비스에 대 한 OLE DB Provider를 지정합니다.|  
|**사용자 ID**|사용자 이름을 지정합니다. 이 키워드를 생략 하면 현재 로그온이 사용 됩니다.|  
|**암호**|사용자 암호를 지정합니다. 이 키워드를 생략 합니다. 현재 로그온이 사용 됩니다.|  
  
> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 또는 **통합 보안 = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.  
  
## <a name="command-text"></a>명령 텍스트  
 다음 구문에 대 한 공급자가 네 부분으로 된 명령 텍스트 문자열을 인식 합니다.  
  
```  
"Root; Filter; Attributes[; Scope]"  
```  
  
|Value|Description|  
|-----------|-----------------|  
|*Root*|나타냅니다는 **ADsPath** 개체 (즉, 검색의 루트) 검색을 시작할입니다.|  
|*필터*|RFC 1960 형식에서 검색 필터를 나타냅니다.|  
|*특성*|쉼표로 구분 된 목록이 반환 될 특성을 나타냅니다.|  
|*범위*|(선택 사항) A **문자열** 검색 범위를 지정 하는 합니다. 다음 중 하나일 수 있습니다.<br /><br /> 밑수가-기준 개체 (검색의 루트)를 검색 합니다.<br />-기준 개체를 검색 한 수준입니다.<br />-하위 트리-전체 하위 트리를 검색 합니다.|  
  
 예를 들어:  
  
```  
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 공급자도 지원 SQL SELECT 명령 텍스트에 대 한 합니다. 예를 들어:  
  
```  
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>주의  
 저장된 프로시저 호출 또는 간단한 테이블 이름을 공급자 허용 하지 않습니다 (예를 들어는 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성은 항상 **adCmdText**). 명령 텍스트 요소에 대 한 보다 철저 한 설명 Active Directory 서비스 인터페이스 설명서를 참조 하십시오.  
  
## <a name="recordset-behavior"></a>레코드 집합 동작  
 다음 표에서에서 사용할 수 있는 기능을 나열는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가이 공급자를 사용 하 여 열립니다. 정적 커서 유형만 (**adOpenStatic**)를 사용할 수 있습니다.  
  
 에 대 한 자세한 내용은 **레코드 집합** 실행 공급자 구성에 대 한 동작의 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드 열거는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 는 의컬렉션 **레코드 집합** 공급자별 동적 속성은 있는지 여부를 확인 하려면.  
  
 **사용 가능한 표준 ADO 레코드 집합 속성:**  
  
|속성|가용성|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|읽기/쓰기|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|읽기/쓰기|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|읽기 전용|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|  
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)|읽기/쓰기|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|읽기/쓰기|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|always **adUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|always **adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|  
|[필터](../../../ado/reference/ado-api/filter-property.md)|읽기/쓰기|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|읽기/쓰기|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|사용할 수 없음|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|읽기/쓰기|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|읽기 전용|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|읽기/쓰기|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|읽기 전용|  
|[원본](../../../ado/reference/ado-api/source-property-ado-recordset.md)|읽기/쓰기|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|읽기 전용|  
|[상태](../../../ado/reference/ado-api/status-property-ado-recordset.md)|읽기 전용|  
  
 **표준 ADO 레코드 집합 메서드 사용 가능성:**  
  
|메서드|사용 가능 여부|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|아니요|  
|[취소](../../../ado/reference/ado-api/cancel-method-ado.md)|아니요|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|아니요|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|아니요|  
|[복제](../../../ado/reference/ado-api/clone-method-ado.md)|예|  
|[닫기](../../../ado/reference/ado-api/close-method-ado.md)|예|  
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|아니요|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|예|  
|[이동](../../../ado/reference/ado-api/move-method-ado.md)|예|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|예|  
|[열기](../../../ado/reference/ado-api/open-method-ado-recordset.md)|예|  
|[다시 쿼리](../../../ado/reference/ado-api/requery-method.md)|예|  
|[다시 동기화](../../../ado/reference/ado-api/resync-method.md)|예|  
|[지원](../../../ado/reference/ado-api/supports-method.md)|예|  
|[업데이트](../../../ado/reference/ado-api/update-method.md)|아니요|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|아니요|  
  
 ADSI 및 공급자의 세부 사항에 대 한 자세한 내용은 Active Directory 서비스 인터페이스 설명서를 참조 하거나 ADSI 웹 페이지를 방문 하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [CommandType 속성 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString 속성 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [공급자 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
