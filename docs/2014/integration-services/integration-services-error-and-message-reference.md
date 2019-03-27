---
title: Integration Services 오류 및 메시지 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ec7f81ec412a2ed597f8cd282b637fc5adf73ebf
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394591"
---
# <a name="integration-services-error-and-message-reference"></a>Integration Services 오류 및 메시지 참조
  다음 표에서는 각 범주별로 미리 정의된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류, 경고 및 정보 메시지를 숫자 코드 및 심볼 이름과 함께 오름차순으로 나열합니다. 이러한 각 오류는 <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> 네임스페이스에 있는 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스의 필드로 정의됩니다.  
  
 이 목록은 아무런 설명 없이 오류가 발생할 경우 유용할 수 있습니다. 이 목록에는 현재 문제 해결 정보는 들어 있지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 작업할 때 볼 수 있는 오류 메시지 중 상당수가 다른 구성 요소의 메시지입니다. 이 항목에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 구성 요소에서 발생하는 모든 오류가 나와 있습니다. 이 목록에 없는 오류는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]가 아닌 다른 구성 요소에서 발생한 것입니다. 여기에는 OLE DB 공급자, 다른 데이터베이스 구성 요소(예: [!INCLUDE[ssDE](../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ) 또는 다른 서비스나 구성 요소(예: 파일 시스템, SMTP 서버 또는 MSMQ라고도 하는 Message Queuing)가 포함됩니다. 이러한 외부 오류 메시지에 대한 자세한 내용은 해당 구성 요소의 설명서를 참조하십시오.  
  
 이 목록에는 다음과 같은 메시지 그룹이 포함되어 있습니다.  
  
-   [오류 메시지(DTS_E_*)](#msgError)  
  
-   [경고 메시지(DTS_W_*)](#msgWarning)  
  
-   [정보 메시지(DTS_I_*)](#msgInfo)  
  
-   [일반 및 이벤트 메시지(DTS_MSG_*)](#msgGeneral)  
  
-   [성공 메시지(DTS_S_*)](#msgSuccess)  
  
-   [데이터 흐름 구성 요소 오류 메시지(DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> 오류 메시지  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 메시지의 심볼 이름은 `DTS_E_`로 시작합니다.  
  
|16진수 코드|10진수 코드|심볼 이름|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|대상에서 저장 프로시저 "%1"을(를) 덮어쓰고 있습니다.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|"%2" 열의 데이터 형식 "%1"이(가) %3에 대해 지원되지 않습니다. 이 열은 DT_NTEXT로 변환됩니다.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|XML 스키마에서 테이블 %2의 열 %1에 외부 메타데이터 열에 대한 매핑이 없습니다.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|내부 개체 또는 변수가 초기화되지 않았습니다. 이것은 제품 내부 오류입니다.  이 오류는 변수의 값이 올바르지 않은 경우에 반환됩니다.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services 평가 기간이 만료되었습니다.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|이 속성에는 음수 값을 할당할 수 없습니다. 이 오류는 COUNT 속성과 같이 양수 값만 포함할 수 있는 속성에 음수 값이 할당될 때 발생합니다.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|인덱스는 음수일 수 없습니다. 이 오류는 음수 값이 컬렉션에 대한 인덱스로 사용될 때 발생합니다.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|서버 이름 "%1"이(가) 잘못되었습니다. SSIS 서비스는 다중 인스턴스를 지원하지 않습니다. "server name\instance" 대신에 서버 이름만 사용하십시오.|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Visual Tools for Applications 디자이너 지원이 부족하여 VSA 스크립트에 대한 마이그레이션 작업을 64비트 플랫폼에서 수행할 수 없습니다. 64비트 플랫폼에서 WOW64를 통해 마이그레이션을 실행하십시오.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|명령 실행으로 인해 오류가 발생했습니다.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 외부에서 SSIS 패키지를 실행하려면 Integration Services를 %1 이상 설치해야 합니다.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|변수를 찾을 수 없습니다. 이 오류는 패키지를 실행하는 동안 컨테이너의 Variables 컬렉션에서 검색하는 변수가 없는 경우에 발생합니다. 변수 이름이 변경되었거나 변수가 생성되지 않았을 수 있습니다.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|변수 "%1"은(는) 읽기 전용 변수이므로 쓸 수 없습니다.|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|태스크 및 데이터 흐름 태스크 구성 요소를 포함하는 디렉터리를 찾을 수 없습니다. 올바르게 설치되었는지 확인하십시오.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|패키지 이름이 너무 깁니다. 제한 길이는 128자입니다. 패키지 이름을 줄이십시오.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|패키지 설명이 너무 깁니다. 제한 길이는 1024자입니다. 패키지 설명을 줄이십시오.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments 속성이 너무 깁니다. 제한 길이는 1024자입니다. VersionComments를 줄이십시오.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|컬렉션에서 요소를 찾을 수 없습니다. 이 오류는 패키지 실행 도중에 컨테이너의 컬렉션에서 검색하는 요소가 없는 경우에 발생합니다.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|SQL Server 데이터베이스에서 지정한 패키지를 로드할 수 없습니다.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|변수 값 할당이 잘못되었습니다. 이 오류는 클라이언트나 태스크가 런타임 개체를 변수 값에 할당할 때 발생합니다.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|네임스페이스를 변수에 할당하는 동안 오류가 발생했습니다. 네임스페이스 "System"은 시스템용으로 예약되어 있습니다. 이 오류는 구성 요소나 태스크가 네임스페이스가 "System"인 변수를 만들려고 할 때 발생합니다.|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|연결 "%1"을(를) 찾을 수 없습니다. 이 오류는 특정 연결 요소를 찾을 수 없을 때 Connections 컬렉션에 의해 발생합니다.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|변수 "%1"은(는) 이 운영 체제에서 지원되지 않는 64비트 정수 변수입니다. 이 변수는 32비트 정수로 다시 캐스팅되었습니다.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|변수 "%1"의 읽기 전용 특성을 변경하려고 했습니다. 이 오류는 변수의 읽기 전용 특성을 런타임에 변경하려고 할 때 발생합니다. 읽기 전용 특성은 디자인 타임에만 변경할 수 있습니다.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|변수를 컨테이너 참조로 설정하려고 했습니다.  변수는 컨테이너를 참조할 수 없습니다.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|잘못된 값이나 개체를 변수 "%1"에 할당하려고 했습니다. 이 오류는 값이 변수에 적합하지 않을 때 발생합니다.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|하나 이상의 오류가 발생했습니다. 이 오류에 앞서 보다 자세한 설명이 포함된 구체적인 오류가 발생합니다. 이 메시지는 오류가 발생한 함수에서의 반환 값으로 사용됩니다.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|배열 값을 가져오거나 설정하는 동안 오류가 발생했습니다. "%1" 유형은 허용되지 않습니다. 이 오류는 배열을 변수에 로드할 때 발생합니다.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|배열에 지원되지 않는 유형이 있습니다. 이 오류는 지원되지 않는 유형의 배열을 변수에 저장할 때 발생합니다.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|값 "%1"을(를) 노드 "%2"에서 로드하는 동안 오류가 발생했습니다.|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|노드 "%1"이(가) 올바른 노드가 아닙니다. 이 오류는 저장이 실패할 때 발생합니다.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|유형 "%2"의 태스크 "%1"을(를) 로드하지 못했습니다. 이 태스크의 연락처 정보는 "%3"입니다.|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|요소 "%1"이(가) 컬렉션 "%2"에 없습니다.|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|ObjectData 요소가 호스팅된 개체의 XML 블록에 없습니다. 이 오류는 XML 파서가 검색하는 개체의 데이터 요소가 없는 경우에 발생합니다.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|변수 "%1"을(를) 찾을 수 없습니다. 이 오류는 패키지 실행 도중에 컨테이너의 Variables 컬렉션에서 검색하는 변수가 없는 경우에 발생합니다.  변수 이름이 변경되었거나 변수가 생성되지 않았을 수 있습니다.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|패키지에 로드하지 못한 태스크가 포함되어 있기 때문에 패키지를 실행할 수 없습니다.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|태스크를 로드하지 못했습니다. 이 태스크의 연락처 정보는 "%1"입니다.|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|태스크 "%1"을(를) 로드하는 동안 오류가 발생했습니다.|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|태스크를 로드하는 동안 오류가 발생했습니다. 이 오류는 XML에서 태스크를 로드하지 못할 때 발생합니다.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|캐시에 %2을(를) 이미 썼으므로 %1을(를) 캐시에 쓸 수 없습니다.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|새 데이터에 대한 캐시를 준비하지 못했습니다.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|캐시를 데이터로 채워진 것으로 표시하지 못했습니다.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|캐시가 초기화되지 않았으므로 %1에서 읽을 수 없습니다.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|데이터를 제공하기 위해 캐시를 준비하지 못했습니다.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|캐시를 %1에서 쓰고 있으므로 %2에서 읽을 수 없습니다.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|캐시를 %1에서 읽고 있으므로 %2에서 쓸 수 없습니다.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|런타임 개체를 지정한 XML 노드에서 로드할 수 없습니다.  이 오류는 올바른 유형이 아닌 XML 노드(예: 비-SSIS XML 노드)에서 패키지나 다른 개체를 로드하려고 할 때 발생합니다.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|오류 0x%2!8.8X! "%3"(으)로 인해 패키지 파일 "%1"을(를) 열지 못했습니다.  이 오류는 패키지를 로드하면서 파일을 열 수 없거나 XML 문서로 올바르게 로드할 수 없을 때 발생합니다. 이 오류는 LoadPackage를 호출할 때 잘못된 파일 이름을 지정했거나 잘못된 형식의 XML 파일을 지정했기 때문에 발생할 수 있습니다.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|오류 0x%1!8.8X! "%2"(으)로 인해 XML을 로드하지 "%2"입니다. 이 오류는 패키지를 로드할 때 파일을 열 수 없거나 XML 문서로 올바르게 로드할 수 없는 경우에 발생합니다.  이 오류는 잘못된 파일 이름을 LoadPackage 메서드에 제공했거나 잘못된 형식의 XML 파일을 지정했기 때문에 발생할 수 있습니다.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|오류 0x%2!8.8X! "%3"(으)로 인해 패키지 파일 "%1"에서 XML을 로드하지 못했습니다.  이 오류는 패키지를 로드할 때 파일을 열 수 없거나 XML 문서로 올바르게 로드할 수 없는 경우에 발생합니다. 이 오류는 잘못된 파일 이름을 LoadPackage 메서드에 제공했거나 잘못된 형식의 XML 파일을 지정했기 때문에 발생할 수 있습니다.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|패키지 파일을 열지 못했습니다. 이 오류는 패키지를 로드할 때 파일을 열 수 없거나 XML 문서로 올바르게 로드할 수 없는 경우에 발생합니다. 이 오류는 잘못된 파일 이름을 LoadPackage 메서드에 제공했거나 잘못된 형식의 XML 파일을 지정했기 때문에 발생할 수 있습니다.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|패키지에서 이진 형식을 디코딩할 수 없습니다.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|패키지에 유효한 XML 형식이 없기 때문에 패키지를 XML로 로드할 수 없습니다. 특정 XML 파서 오류가 게시됩니다.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|XML에서 로드하는 동안 오류가 발생했습니다. 자세한 오류 정보를 저장할 수 있는 Events 개체가 전달되지 않았으므로 이 문제에 대한 자세한 추가 오류 정보를 지정할 수 없습니다.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|XML 문서 개체 모델의 인스턴스를 만들 수 없습니다. MSXML이 등록되지 않았을 수 있습니다.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|패키지를 로드할 수 없습니다. 이 오류는 이전 버전의 패키지를 로드하려고 하거나 패키지 파일이 참조하는 구조화된 개체가 잘못되었을 때 발생합니다.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|패키지 파일을 저장하지 못했습니다.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|오류 0x%2!8.8X! "%3"(으)로 인해 패키지 파일 "%1"을(를) 저장하지 못했습니다.|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|개체가 IDTSName100에서 상속되어야 합니다.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|구성 항목 "%1"이(가) 패키지 구분 기호로 시작되지 않기 때문에 형식이 잘못되었습니다. "\package" 구분 기호가 없습니다.|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|구성 항목 "%1"의 형식이 잘못되었습니다. 이 오류는 구분 기호가 없거나 잘못된 배열 구분 기호 등의 형식 오류가 있을 때 발생할 수 있습니다.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|구성 파일을 내보내는 동안 오류가 발생했습니다.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|속성 컬렉션을 수정할 수 없습니다.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|구성 파일을 저장할 수 없습니다. 파일이 읽기 전용일 수 있습니다.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure 속성은 패키지 컨테이너에 적용할 수 없습니다.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|태스크 "%1"은(는) 설치된 Integration Services %2에서 실행할 수 없습니다. %3 이상이 필요합니다.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|xml을 "%1"에 저장할 수 없습니다. 파일이 읽기 전용일 수 있습니다.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|패키지 경로 "%2"에 대한 구성 "%1"에서 유형을 변환하지 못했습니다.  이 오류는 문자열에서 적절한 대상 유형으로 구성 값을 변환할 수 없을 때 발생합니다. 구성 값을 검사하여 대상 속성 또는 변수의 유형으로 변환할 수 있는지 확인하십시오.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|구성 오류입니다. 이것은 모든 구성 유형에 대한 일반 경고입니다. 이 경고 이전의 다른 경고를 통해 자세한 정보를 확인할 수 있습니다.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|패키지가 ExecutePackage 태스크의 유효성을 검사하지 못했습니다. 패키지를 실행할 수 없습니다.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|오류 0x%2!8.8X!(으)로 인해 뮤텍스 "%1"을(를) 만들지 못했습니다.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|뮤텍스 "%1"이(가) 이미 있으며 다른 사용자가 소유하고 있습니다.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|오류 0x%2!8.8X!(으)로 인해 뮤텍스 "%1"을(를) 가져오지 못했습니다.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|오류 0x%2!8.8X!(으)로 인해 뮤텍스 "%1"을(를) 해제하지 못했습니다.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|래퍼 태스크 포인터가 잘못되었습니다. 태스크에 대한 래퍼 포인터가 잘못되었습니다.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|실행 파일이 다른 컨테이너의 Executables 컬렉션에 추가되었습니다. 이 오류는 클라이언트가 실행 파일을 둘 이상의 Executables 컬렉션에 추가하려고 할 때 발생합니다. 실행 파일을 추가하기 전에 현재의 Executables 컬렉션에서 실행 파일을 제거해야 합니다.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|연결 관리자 "%2"에 지정된 연결 형식 "%1"이(가) 올바른 연결 관리자 유형으로 인식되지 않습니다. 이 오류는 알 수 없는 연결 형식에 대한 연결 관리자를 만들려고 할 때 반환됩니다. 연결 형식 이름의 철자를 확인하십시오.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|개체를 만들었지만 개체를 컬렉션에 추가하지 못했습니다. 이 오류는 메모리 부족 상태로 인해 발생할 수 있습니다.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|ODBC(Open Database Connectivity) 환경을 만드는 동안 오류가 발생했습니다.|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|ODBC(Open Database Connectivity) 데이터베이스 연결을 만드는 동안 오류가 발생했습니다.|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|데이터베이스 서버와의 ODBC(Open Database Connectivity) 연결을 만드는 동안 오류가 발생했습니다.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|이 연결 관리자 인스턴스에 한정자가 이미 설정되었습니다. 한정자는 인스턴스당 하나만 설정할 수 있습니다.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|이 연결 관리자 인스턴스에 한정자가 설정되지 않았습니다. 초기화를 완료하려면 한정자를 설정해야 합니다.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|이 연결 관리자는 한정자 지정을 지원하지 않습니다.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|연결 관리자 "0x%1"을(를) Out-of-process 실행을 위해 복제할 수 없습니다.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|SQL Server Profiler의 로그 공급자가 pfclnt.dll을 로드할 수 없습니다. SQL Server Profiler가 설치되었는지 확인하십시오.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|SSIS 로깅 인프라가 실패했습니다(오류 코드 0x%1!8.8X!). 이 오류는 이 로깅 오류의 원인을 특정 로그 공급자에서 찾을 수 없다는 것을 나타냅니다.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|SSIS 로깅 공급자 "%1"이(가) (%3).  이것은 로깅 오류의 원인을 지정된 로그 공급자에서 찾을 수 있다는 것을 나타냅니다.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|SaveToSQLServer 메서드에서 OLE DB 오류 코드 0x%1!8.8X!(%2)이(가) 0x%1!8.8X!(%2)).  실행된 SQL 문이 실패했습니다.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|LoadFromSQLServer 메서드에서 OLE DB 오류 코드 0x%1!8.8X!(%2)이(가) 0x%1!8.8X!(%2)).  실행된 SQL 문이 실패했습니다.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|RemoveFromSQLServer 메서드에서 OLE DB 오류 코드 0x%1!8.8X!(%2)이(가) 발생했습니다. 실행된 SQL 문이 실패했습니다.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|ExistsOnSQLServer 메서드에서 OLE DB 오류 코드 0x%1!8.8X!(%2)이(가) 0x%1!8.8X!(%2)). 실행된 SQL 문이 실패했습니다.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|제공된 연결 문자열을 사용하여 OLE DB가 데이터베이스 연결을 설정하지 못했습니다.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|선행 제약 조건을 추가할 때 이 컨테이너의 자식이 아닌 From 실행 파일이 지정되었습니다.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|선행 제약 조건을 추가할 때 이 컨테이너의 자식이 아닌 To 실행 파일이 지정되었습니다.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|ODBC 연결을 트랜잭션에 참여시키려는 동안 오류가 발생했습니다. SQLSetConnectAttr이 SQL_ATTR_ENLIST_IN_DTC 특성을 설정하지 못했습니다.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|패키지 OfflineMode 속성이 TRUE이므로 연결 관리자 "%1"이(가) 연결을 설정하지 않습니다. OfflineMode가 TRUE이면 연결을 설정할 수 없습니다.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|오류 0x%1!8.8X! "%2"(으)로 인해 SSIS 런타임이 분산 트랜잭션을 시작하지 "%2"입니다. DTS 트랜잭션을 시작하지 못했습니다. 이 오류는 MSDTC 서비스가 실행되지 않는 경우에 발생할 수 있습니다.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|패키지 실행 중에 연결 관리자에서 SetQualifier 메서드를 호출할 수 없습니다. 이 메서드는 디자인 타임에만 사용됩니다.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|SQL Server에 패키지를 저장 또는 수정하려면 SSIS 런타임과 데이터베이스가 같은 버전이어야 합니다. 이전 버전에서는 패키지를 저장하는 것이 지원되지 않습니다.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|연결 "%1"에서 유효성을 검사하지 못했습니다.|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|연결에 지정된 파일 이름 "%1"이(가) 잘못되었습니다.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Retain 속성이 TRUE이면 연결에서 여러 파일 이름을 지정할 수 없습니다. 연결 문자열에서 여러 파일 이름을 지정할 때 사용되는 세로 막대가 발견되었으며, Retain 속성도 TRUE입니다.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|ODBC 오류 %1!d!이(가) 발생했습니다.|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|"%1" 및 "%2" 사이의 선행 제약 조건에 오류가 있습니다.|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|ForEachEnumeratorInfos 컬렉션을 네이티브 ForEachEnumerators로 채우지 못했습니다. 오류 코드: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|오류 0x%1!8.8X! "%2"(으)로 인해 ForEach 열거자의 GetEnumerator 메서드가 "%2"입니다. 이 오류는 ForEach 열거자가 항목을 열거할 수 없을 때 발생합니다.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|원시 인증서 데이터를 제공된 인증서 개체에서 가져올 수 없습니다(오류: %1). 이 오류는 CPackage::put_CertificateObject가 ManagedHelper 개체를 인스턴스화할 수 없을 경우, ManagedHelper 개체가 실패할 경우 또는 ManagedHelper 개체가 잘못된 형식의 배열을 반환할 경우 발생합니다.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|인증서 컨텍스트를 만들지 못했습니다(오류: %1). 이 오류는 해당 CryptoAPI 함수가 실패할 때 CPackage::put_CertificateObject 또는 CPackage::LoadFromXML에서 발생합니다.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|오류 "%1"(으)로 인해 내 인증서 저장소를 열지 못했습니다. 이 오류는 CPackage::LoadUserCertificateByName 및 CPackage::LoadUserCertificateByHash에서 발생합니다.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|이름으로 지정된 인증서를 내 저장소에서 찾을 수 없습니다(오류: %1). 이 오류는 CPackage::LoadUserCertificateByName에서 발생합니다.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|해시로 지정된 인증서를 "내" 저장소에서 찾을 수 없습니다(오류: %1). 이 오류는 CPackage::LoadUserCertificateByHash에서 발생합니다.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|해시 값이 1차원 바이트 배열이 아닙니다(오류: %1). 이 오류는 CPackage::LoadUserCertificateByHash에서 발생합니다.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|배열의 데이터에 액세스할 수 없습니다(오류: %1). 이 오류는 GetDataFromSafeArray가 호출될 때마다 발생할 수 있습니다.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|오류 0x%1!8.8X! "%2"(으)로 인해 관리되는 SSIS 도우미 개체를 만들지 "%2"입니다. 이 오류는 CoCreateInstance CLSID_DTSManagedHelper가 실패할 때마다 발생할 수 있습니다.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|오류 0x%1!8.8X! "%2"(으)로 인해 SSIS 런타임이 OLE DB 연결을 분산 트랜잭션에 참여시키지 못했습니다.|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|오류 0x%1!8.8X! "%2"(으)로 인해 패키지를 서명하지 "%2"입니다. 이 오류는 ManagedHelper.SignDocument 메서드가 실패할 때 발생합니다.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|오류 0x%1!8.8X! "%2"(으)로 인해 패키지 XML에서 XML 서명 봉투를 확인하지 "%2"입니다. 이 오류는 CPackage::LoadFromXML에서 발생합니다.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|오류 0x%1!8.8X! "%2"(으)로 인해 XML DOM 개체에서 XML 원본을 가져오지 "%2"입니다. 이 오류는 IXMLDOMDocument::get_xml이 실패할 때 발생합니다.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|오류 0x%1!8.8X! "%2"(으)로 인해 패키지의 암호화 서명을 확인하지 "%2"입니다. 이 오류는 서명 확인 작업이 실패할 때 발생합니다.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|오류 0x%1!8.8X! "%2"(으)로 인해 지정된 인증서와 연결된 암호화 키 쌍을 얻지 "%2"입니다. 발급된 인증서에 대한 키 쌍이 있는지 확인하십시오. 이 오류는 일반적으로 개인 키가 없는 인증서를 사용하여 문서에 서명하려고 할 때 발생합니다.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|디지털 서명이 잘못되었습니다. 패키지 내용이 수정되었습니다.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|디지털 서명이 유효하지만 서명자를 신뢰할 수 없으므로 신뢰성을 보증할 수 없습니다.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|연결이 분산 트랜잭션 참여를 지원하지 않습니다.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|오류 0x%1!8.8X! "%2"(으)로 인해 패키지 보호를 적용하지 "%2"입니다. 이 오류는 XML에 저장할 때 발생합니다.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|오류 0x%1!8.8X! "%2"(으)로 인해 패키지 보호를 제거하지 "%2"입니다. 이 오류는 CPackage::LoadFromXML 메서드에서 발생합니다.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|패키지가 암호로 암호화되어 있습니다. 암호가 지정되지 않았거나 올바르지 않습니다.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|지정된 실행 파일 사이에 선행 제약 조건이 이미 있습니다. 둘 이상의 선행 제약 조건은 허용되지 않습니다.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|오류 0x%1!8.8X! "%2"(으)로 인해 패키지를 로드하지 "%2"입니다. 이 오류는 CPackage::LoadFromXML이 실패할 때 발생합니다.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|오류 0x%1!8.8X! "%2"(으)로 인해 서명된 XML 봉투에서 패키지 개체를 찾지 "%2"입니다. 이 오류는 서명된 XML에 SSIS 패키지가 포함되지 않을 때 발생합니다.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|매개 변수 이름, 유형 및 설명 배열의 길이가 다릅니다. 이러한 길이는 동일해야 합니다. 이 오류는 배열의 길이가 일치하지 않을 때 발생합니다. 각 배열에는 매개 변수당 하나의 항목이 있어야 합니다.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|패키지를 열거하는 동안 OLE DB 오류 0x%1!8.8X!(%2)이(가) 발생했습니다. 실행된 SQL 문이 실패했습니다.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|로그 공급자 "%2"에 지정된 로그 공급자 유형 "%1"이(가) 유효한 로그 공급자 유형으로 인식되지 않습니다. 이 오류는 알 수 없는 로그 공급자 유형에 대한 로그 공급자를 만들려고 할 때 발생합니다. 로그 공급자 유형 이름의 철자를 확인하십시오.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|로그 공급자 유형이 유효한 로그 공급자 유형으로 인식되지 않습니다. 이 오류는 알 수 없는 로그 공급자 유형에 대한 로그 공급자를 만들려고 할 때 발생합니다. 로그 공급자 유형 이름의 철자를 확인하십시오.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|연결 관리자에 지정된 연결 형식이 올바른 연결 관리자 유형이 아닙니다. 이 오류는 알 수 없는 연결 형식에 대한 연결 관리자를 만들려고 할 때 발생합니다. 연결 형식 이름의 철자를 확인하십시오.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|SQL Server에서 패키지 "%1"을(를) 제거하려는 동안 오류가 발생했습니다.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|SQL Server에서 폴더 "%1"에 "%2"(이)라는 폴더를 만들려는 동안 오류가 발생했습니다.|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|CreateFolderOnSQLServer 메서드에서 OLE DB 오류 코드 0x%1!8.8X!(%2)이(가) 발생했습니다. 실행된 SQL 문이 실패했습니다.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|SQL Server에서 폴더 "%1\\\\%2"의 이름을 "%1\\\\%3"(으)로 바꾸는 동안 오류가 발생했습니다.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|RenameFolderOnSQLServer 메서드에서 OLE DB 오류 코드 0x%1!8.8X!(%2)이(가) 0x%1!8.8X!(%2)). 실행된 SQL 문이 실패했습니다.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|SQL Server 폴더 "%1"을(를) 삭제하는 동안 오류가 발생했습니다.|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|RemoveFolderOnSQLServer 메서드에서 OLE DB 오류 코드 0x%1!8.8X!(%2)이(가) 0x%1!8.8X!(%2)). 실행된 SQL 문이 실패했습니다.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|지정한 패키지 경로에 패키지 이름이 없습니다. 이 오류는 적어도 하나 이상의 백슬래시 또는 슬래시가 경로에 없을 때 발생합니다.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|폴더 "%1"을(를) 찾을 수 없습니다.|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|SQL에서 폴더를 찾으려는 동안 OLE DB 오류가 0x%1!8.8X!(%2)).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|SSIS 로깅 공급자가 로그를 열지 못했습니다. 오류 코드: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|오류 0x%1!8.8X! "%2"(으)로 인해 ConnectionInfos 컬렉션을 가져오지 "%2"입니다. 이 오류는 IDTSApplication100:get_ConnectionInfos를 호출하지 못하는 경우에 발생합니다.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|변수를 잠그려는 동안 교착 상태가 발견되었습니다. 16번 시도했지만 잠그지 못했습니다. 잠금 시간이 초과되었습니다.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|Variables 컬렉션이 VariableDispenser에서 반환되지 않았습니다. 분배된 컬렉션에서만 허용되는 작업이 시도되었습니다.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|이 Variables 컬렉션은 이미 잠금 해제되었습니다. Unlock 메서드는 디스펜스된 Variables 컬렉션에서 한 번만 호출됩니다.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|하나 이상의 변수를 잠금 해제하지 못했습니다.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|Variables 컬렉션이 VariableDispenser에서 반환되었으며 수정할 수 없습니다. 분배된 컬렉션에서 항목을 추가하거나 제거할 수 없습니다.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|변수 "%1"이(가) 이미 읽기 목록에 있습니다. 변수는 읽기 잠금 목록이나 쓰기 잠금 목록에 한 번만 추가할 수 있습니다.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|변수 "%1"이(가) 이미 쓰기 목록에 있습니다. 변수는 읽기 잠금 목록이나 쓰기 잠금 목록에 한 번만 추가할 수 있습니다.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|오류 0x%2!8.8X! "%3"(으)로 인해 변수 "%1"을(를) 읽기용으로 잠그지 못했습니다.|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|오류 0x%2!8.8X! "%3"(으)로 인해 변수 "%1"을(를) 읽기/쓰기용으로 잠그지 못했습니다.|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|사용자 지정 이벤트 "%1"은(는) 이미 다른 매개 변수 목록을 사용하여 선언되었습니다. 다른 매개 변수 목록을 사용하여 이미 다른 태스크에 의해 선언된 사용자 지정 이벤트를 선언하려고 했습니다.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|사용자 지정 이벤트 "%1" 제공 태스크는 패키지에서 이 이벤트의 처리를 허용하지 않습니다. 이 사용자 지정 이벤트는 AllowEventHandlers = FALSE로 선언되었습니다.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|VariableDispenser에서 안전하지 않은 Variables 컬렉션을 받았습니다. 이 작업을 반복할 수 없습니다.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath가 ForEachEnumerator에서 호출되었지만 ForEachLoop 패키지 경로가 지정되지 않았습니다.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|변수 "%1"을(를) 읽기용으로 잠그려는 동안 교착 상태가 발견되었습니다. 16번 시도했지만 잠그지 못했습니다. 잠금 시간이 초과되었습니다.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|변수 "%1"을(를) 읽기/쓰기용으로 잠그려는 동안 교착 상태가 발견되었습니다. 16번 시도했지만 잠그지 못했습니다. 잠금 시간이 초과되었습니다.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|변수 "%1"을(를) 읽기용으로 잠그고 변수 "%2"을(를) 읽기/쓰기용으로 잠그려는 동안 교착 상태가 발견되었습니다. 16번 시도했지만 잠그지 못했습니다. 잠금 시간이 초과되었습니다.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|패키지 보호 수준에 암호가 필요하지만 PackagePassword 속성이 비어 있습니다.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|암호가 지정되지 않았거나 올바르지 않기 때문에 암호화된 XML 노드를 해독하지 못했습니다. 암호화된 정보 없이 패키지 로드가 계속 시도됩니다.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|사용자 키를 사용하여 암호화된 패키지를 해독하지 못했습니다. 현재 사용자가 이 패키지를 암호화한 사용자가 아니거나 사용 중인 컴퓨터가 이 패키지를 저장하는 데 사용된 컴퓨터가 아닙니다.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|이 대상에 저장할 때 보호 수준 ServerStorage를 사용할 수 없습니다. 시스템에서 대상이 보안 스토리지 기능을 지원하는지 확인하지 못했습니다.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer 메서드가 실패했습니다.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|디지털 서명의 상태가 서명 정책을 위반하므로 패키지를 로드할 수 없습니다. 오류 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|패키지가 서명되지 않았습니다.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|pfclnt.dll은 32비트 시스템에서만 지원되므로 SQL Server Profiler용 로그 공급자가 pfclnt.dll을 로드하지 못했습니다.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|같은 이름의 다른 개체가 이미 컬렉션에 존재하기 때문에 개체를 추가할 수 없습니다. 이 오류를 해결하려면 다른 이름을 사용하십시오.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|컬렉션의 다른 개체가 이미 해당 이름을 사용하고 있기 때문에 개체 이름을 "%1"에서 "%2"(으)로 변경할 수 없습니다. 이 오류를 해결하려면 다른 이름을 사용하십시오.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|패키지 종속성을 열거하는 동안 오류가 발생했습니다. 자세한 내용은 다른 메시지를 참조하십시오.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|현재 패키지 설정은 지원되지 않습니다.  SaveCheckpoints 속성 또는 TransactionOption 속성을 변경하십시오.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|연결 관리자를 트랜잭션에서 제거하지 못했습니다.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|지정된 중단점 ID가 이미 있습니다. 이 오류는 동일한 ID를 사용하여 CreateBreakpoint를 여러 번 호출할 때 발생합니다. 두 번째 중단점을 만들기 전에 첫 번째 중단점에서 RemoveBreakpoint를 호출하면 동일한 ID를 사용하여 중단점을 여러 번 만들 수 있습니다.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|지정된 중단점 ID가 없습니다. 이 오류는 존재하지 않는 중단점을 태스크가 참조할 때 발생합니다.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|파일 "%1"을(를) 쓰기용으로 열 수 없습니다. 이 파일이 읽기 전용이거나 사용자에게 올바른 권한이 없습니다.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|이 쿼리 실행과 연결된 결과 행 집합이 없습니다. 결과가 올바르게 지정되지 않았습니다.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|디버그 덤프 파일이 잘못 생성되었습니다. hresult는 0x%1!8.8X!입니다.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|지정된 URL이 잘못되었습니다. 이 오류는 서버 또는 프록시 URL이 Null이거나 잘못된 형식일 때 발생할 수 있습니다. 유효한 URL 형식은 http://ServerName:Port/ResourcePath 또는 https://ServerName:Port/ResourcePath 형식입니다.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|URL %1이 잘못되었습니다. 이 오류는 http 또는 https가 아닌 스키마가 지정되었거나 URL의 형식이 잘못되었을 때 발생할 수 있습니다. 유효한 URL 형식은 http://ServerName:Port/ResourcePath 또는 https://ServerName:Port/ResourcePath 형식입니다.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|서버 %1에 연결을 설정할 수 없습니다. 이 오류는 서버가 없거나 프록시 설정이 올바르지 않을 때 발생할 수 있습니다.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|서버와의 연결이 재설정되었거나 종료되었습니다. 나중에 다시 시도하십시오.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|"%1"에 로그인하지 못했습니다. 이 오류는 제공된 로그인 자격 증명이 올바르지 않을 때 발생합니다. 로그인 자격 증명을 확인하십시오.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|URL %1에 지정된 서버 이름을 확인할 수 없습니다.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|프록시 인증에 실패했습니다. 이 오류는 로그인 자격 증명이 제공되지 않았거나 자격 증명이 올바르지 않을 때 발생합니다.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|서버에서 얻은 SSL 인증서 응답이 잘못되었습니다. 요청을 처리할 수 없습니다.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|요청 시간이 초과되었습니다. 이 오류는 지정된 제한 시간이 너무 짧거나 서버 또는 프록시에 대한 연결을 설정할 수 없을 때 발생할 수 있습니다. 서버 및 프록시 URL이 올바른지 확인하십시오.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|클라이언트 인증서가 없습니다. 이 오류는 SSL 클라이언트 인증서가 서버에 필요하지만 사용자가 잘못된 인증서를 제공하거나 인증서를 제공하지 않을 때 발생합니다. 이 연결에 대한 클라이언트 인증서를 구성해야 합니다.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|지정된 서버 URL %1에 리디렉션이 있지만 리디렉션을 요청하지 못했습니다.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|서버 인증에 실패했습니다. 이 오류는 로그인 자격 증명이 제공되지 않았거나 자격 증명이 올바르지 않을 때 발생합니다.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|요청을 처리할 수 없습니다. 나중에 다시 시도하십시오.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|서버에서 상태 코드가 반환되었습니다 - %1!u! : %2. 이 오류는 서버에 문제가 있을 때 발생합니다.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|이 플랫폼은 WinHttp 서비스에서 지원하지 않습니다.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|제한 시간 값이 잘못되었습니다. 제한 시간 범위는 %1!d!에서 %2!d!(초) %2!d!(으)로 합니다.|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|청크 크기가 잘못되었습니다. ChunkSize 속성 범위는 %1!d!에서 %2!d!(KB) %2!d!(으)로 합니다.|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|클라이언트 인증서를 처리하는 동안 오류가 발생했습니다. 이 오류는 제공된 클라이언트 인증서가 개인 인증서 저장소에 없는 경우에 발생할 수 있습니다. 클라이언트 인증서가 유효한지 확인하십시오.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|서버에서 "403 - 사용할 수 없음" 오류 코드를 반환했습니다. 이 오류는 지정된 리소스에 "https" 액세스가 필요하지만 인증서 유효 기간이 만료되었거나 인증서가 요청된 사용에 적합하지 않거나 인증서가 해지된 경우 또는 해지를 확인할 수 없는 경우에 발생할 수 있습니다.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|프록시 "%1"을(를) 사용하여 HTTP 세션을 초기화하는 동안 오류가 발생했습니다. 이 오류는 잘못된 프록시가 지정되었을 때 발생할 수 있습니다. HTTP 연결 관리자는 CERN 유형 프록시만 지원합니다.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|인증서 저장소를 여는 동안 오류가 발생했습니다.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|오류 0x%2!8.8X! "%3"(으)로 인해 보호된 XML 노드 "%1"을(를) 해독하지 못했습니다. 이 정보에 액세스할 수 있는 권한이 없을 수 있습니다. 이 오류는 암호화 오류가 있을 때 발생합니다. 사용할 수 있는 올바른 키를 확인하십시오.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|오류 0x%2!8.8X! "%3"(으)로 인해 서버 "%1"에 대한 보호된 연결 문자열을 해독하지 못했습니다. 이 정보에 액세스할 수 있는 권한이 없을 수 있습니다. 이 오류는 암호화 오류가 있을 때 발생합니다. 사용할 수 있는 올바른 키를 확인하십시오.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|버전 번호는 음수일 수 없습니다. 이 오류는 패키지의 VersionMajor, VersionMinor 또는 VersionBuild 속성이 음수 값으로 설정되었을 때 발생합니다.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|로드하는 중에 패키지가 이후 버전으로 마이그레이션되었습니다. 프로세스를 완료하려면 패키지를 다시 로드해야 합니다. 이것은 내부 오류 코드입니다.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|오류 0x%3!8.8X! "%4"(으)로 인해 버전 %1!d!에서 버전 %2!d!(으)로 패키지를 마이그레이션하지 못했습니다.|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|패키지 마이그레이션 모듈을 로드하지 못했습니다.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|패키지 마이그레이션 모듈이 실패했습니다.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|기본 지속성을 사용하여 개체를 지속할 수 없습니다. 이 오류는 기본 지속성이 호스팅된 개체에 있는 개체를 확인할 수 없을 때 발생합니다.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|런타임 모드에서는 패키지에서 요소를 추가하거나 제거할 수 없습니다. 이 오류는 패키지가 실행되는 동안에 컬렉션에서 개체를 추가하거나 제거하려고 할 때 발생합니다.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|사용자 지정 기본 지속성에서 "%1" 노드를 찾을 수 없습니다. 이 오류는 확장 가능한 개체의 저장된 기본 XML이 변경되어 저장된 개체를 더 이상 찾을 수 없는 경우나 확장 가능한 개체 자체가 변경된 경우에 발생합니다.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|패키지 유효성 검사 또는 실행 중에 이 컬렉션을 수정할 수 없습니다.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|패키지 유효성 검사 또는 실행 중 "%1" 컬렉션을 수정할 수 없습니다. "%2"을(를) 컬렉션에 추가할 수 없습니다.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|FTP 서버와의 연결이 설정되지 않았습니다.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|요청된 FTP 작업에서 오류가 발생했습니다. 자세한 오류 설명: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|재시도 횟수가 잘못되었습니다. 재시도 횟수는 %1!d!에서 %2!d! 사이여야 합니다.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|FTP 연결 관리자를 사용하려면 다음 DLL이 작동해야 합니다: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|연결 문자열에 지정된 포트가 잘못되었습니다. ConnectionString 형식은 ServerName:Port입니다. 포트는 %1!d!에서 %2!d! 사이의 정수 값이어야 합니다.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|폴더 "%1"을(를) 만드는 중 ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|폴더 "%1"을(를) 삭제하는 중 ... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|현재 디렉터리를 "%1"(으)로 변경하고 있습니다. %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|전송할 파일이 없습니다. 이 오류는 전송 또는 수신 작업을 수행할 때 전송하도록 지정된 파일이 없는 경우에 발생할 수 있습니다.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|지정한 로컬 경로가 잘못되었습니다. 올바른 로컬 경로를 지정하십시오. 이 오류는 지정한 로컬 경로가 Null일 때 발생할 수 있습니다.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|삭제하도록 지정한 파일이 없습니다.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|인증서를 로드하는 동안 내부 오류가 발생했습니다. 이 오류는 인증서 데이터가 잘못되었을 때 발생할 수 있습니다.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|인증서 데이터를 저장하는 동안 내부 오류가 발생했습니다.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|검사점 파일 "%1"이(가) 이 패키지와 일치하지 않습니다. 패키지의 ID와 검사점 파일의 ID가 일치하지 않습니다.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|기존 검사점 파일에서 이 패키지에 적합하지 않은 것으로 보이는 내용이 발견되었기 때문에 새 검사점 저장을 시작하도록 파일을 덮어쓸 수 없습니다. 기존 검사점 파일을 제거하고 다시 시도하십시오. 이 오류는 검사점 파일이 있고 패키지가 검사점 파일을 사용하지 않도록 설정되었지만 검사점을 저장하도록 설정되었을 때 발생합니다. 기존 검사점 파일을 덮어쓰지 않습니다.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|검사점 파일 "%1"이(가) 다른 프로세스에 의해 잠겼습니다. 이 오류는 이 패키지의 다른 인스턴스가 현재 실행 중일 때 발생할 수 있습니다.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|오류 0x%2!8.8X! "%3"(으)로 인해 검사점 파일 "%1"을(를) 열지 못했습니다.|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|오류 0x%2!8.8X! "%3"(으)로 인해 검사점 파일 "%1"을(를) 만들지 못했습니다.|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|FTP 포트에 잘못된 값이 있습니다. FTP 포트 값은%1!d!에서 %2!d! 사이의 정수여야 합니다.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|컴퓨터 "%1"에서 SSIS 서비스에 연결하지 못했습니다:<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|Variable 개체에서는 Expression 속성이 지원되지 않습니다. EvaluateAsExpression 속성을 대신 사용하십시오.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|속성 "%1"의 식 "%2"을(를) 계산할 수 없습니다. 식을 올바르게 수정하십시오.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|속성 "%1"의 식 "%2"에 대한 결과를 속성에 쓸 수 없습니다. 식이 계산되었지만 속성에 설정할 수 없습니다.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|루프에 대한 계산 식이 잘못되었습니다. 식을 수정해야 합니다. 추가 오류 메시지가 있습니다.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|식 "%1"은(는) True 또는 False로 계산되어야 합니다. 부울 값으로 계산되도록 식을 변경하십시오.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|계산할 루프 식이 없습니다. 이 오류는 For Loop에 대한 식이 비어 있을 때 발생합니다. 식을 추가하십시오.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|루프에 대한 대입 식이 잘못되었으며 수정해야 합니다. 추가 오류 메시지가 있습니다.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|루프에 대한 초기화 식이 잘못되었으며 수정해야 합니다. 추가 오류 메시지가 있습니다.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|패키지의 버전 번호가 잘못되었습니다. 버전 번호는 현재 버전 번호보다 클 수 없습니다.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|패키지의 버전 번호가 잘못되었습니다. 버전 번호가 음수입니다.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|패키지의 버전이 오래된 형식인데 자동 패키지 형식 업그레이드 기능이 비활성화되어 있습니다.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|식을 계산하는 동안 잘림이 발생했습니다.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|래퍼가 ExecutionValueVariable 속성에 지정된 변수의 값을 설정할 수 없습니다.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|변수 "%1"에 대한 식을 계산하지 못했습니다. 식에 오류가 있습니다.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|이 데이터베이스 버전에서는 시도한 작업이 지원되지 않습니다.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|보유된 연결이 사용되면 트랜잭션을 지정할 수 없습니다. 이 오류는 연결 관리자에서 Retain이 TRUE로 설정되었지만 Null이 아닌 트랜잭션 매개 변수와 함께 AcquireConnection이 호출되었을 때 발생합니다.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|보유된 연결에 호환되지 않는 트랜잭션 컨텍스트가 지정되었습니다. 이 연결은 다른 트랜잭션 컨텍스트에서 설정되었습니다. 보유된 연결은 정확하게 하나의 트랜잭션 컨텍스트에서만 사용할 수 있습니다.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|패키지가 일시 중지되지 않았기 때문에 Resume 호출에 실패했습니다. 이 오류는 클라이언트가 Resume을 호출하지만 패키지가 일시 중지되지 않았을 때 발생합니다.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|실행 파일이 이미 실행 중이므로 Execute를 호출하지 못했습니다. 이 오류는 마지막 Execute 호출부터 계속 실행 중인 컨테이너에서 클라이언트가 Execute를 호출할 때 발생합니다.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|실행 파일이 실행 중이 아니거나 최상위 실행 파일이 아니기 때문에 Suspend 또는 Resume을 호출하지 못했습니다. 이 오류는 현재 Execute 호출을 처리하고 있지 않는 실행 파일에서 클라이언트가 Suspend 또는 Resume을 호출할 때 발생합니다.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|For Each File 열거자에 지정된 파일이 잘못되었습니다. For Each File 열거자에 지정된 파일이 존재하는지 확인하십시오.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|값 인덱스가 정수가 아닙니다. ForEach 변수 번호 %1!d!을(를) 변수 "%2"(으)로 매핑하고 있습니다.|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|값 인덱스가 음수입니다. ForEach 변수 번호 %1!d!을(를) 변수 "%2"(으)로 매핑하고 있습니다.|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|ForEach 변수 번호 %1!d!의 변수 "%2"에 대한 매핑을 적용할 수 없습니다.|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|ForEachLoop 컨테이너의 직계 자식이 아닌 ForEachPropertyMapping에 개체를 추가하는 동안 오류가 발생했습니다.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|시스템 변수를 제거하지 못했습니다. 이 오류는 필수 변수를 제거할 때 발생합니다.  필수 변수는 태스크 및 런타임 간의 통신을 위해 런타임에 생성되는 변수입니다.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|변수가 시스템 변수이므로 변수의 속성을 변경하지 못했습니다. 시스템 변수는 읽기 전용입니다.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|변수가 시스템 변수이므로 변수의 이름을 변경하지 못했습니다. 시스템 변수는 읽기 전용입니다.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|변수가 시스템 변수이므로 변수의 네임스페이스를 변경하지 못했습니다. 시스템 변수는 읽기 전용입니다.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|이벤트 처리기 이름을 변경하지 못했습니다. 이벤트 처리기 이름은 읽기 전용입니다.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|개체의 경로를 검색할 수 없습니다. 시스템 오류입니다.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|변수 "%1"에 할당되는 값의 유형이 현재 변수 유형과 다릅니다. 실행 도중에는 변수의 유형을 변경할 수 없습니다. Object 유형의 변수를 제외한 모든 변수 유형은 엄격하게 유지됩니다.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|문자열에 잘못된 문자가 있습니다. "%1". 이 오류는 속성 값에 제공된 문자열에 인쇄할 수 없는 문자가 있을 때 발생합니다.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS 개체 이름이 잘못되었습니다. 정확한 명명 문제를 설명하는 더 구체적인 오류가 발생했을 수 있습니다.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|속성 "%1"이(가) 읽기 전용입니다. 이 오류는 읽기 전용 속성을 변경하려고 할 때 발생합니다.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|개체가 유형 정보를 지원하지 않습니다. 이 오류는 런타임에 Properties 컬렉션을 채우기 위해 개체에서 유형 정보를 가져오려고 할 때 발생합니다.  개체는 유형 정보를 지원해야 합니다.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|속성 "%1"의 값을 검색하는 동안 오류가 발생했습니다. 오류 코드는 0x%2!8.8X!입니다.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|속성 "%1"의 값을 검색하는 동안 오류가 발생했습니다. 오류 코드는 0x%2!8.8X! 못했습니다.|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|속성 "%1"의 값을 설정하는 동안 오류가 발생했습니다. 반환된 오류는 0x%2!8.8X!입니다.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|속성 "%1"의 값을 설정하는 동안 오류가 발생했습니다. 반환된 오류는 0x%2!8.8X! 못했습니다.|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|속성 "%1"은(는) 쓰기 전용입니다. 이 오류는 쓰기 전용 속성에 속성 개체를 통해 값을 검색하려고 할 때 발생합니다.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|개체가 IDispatch를 구현하지 않습니다. 이 오류는 속성 개체나 속성 컬렉션이 개체의 IDispatch 인터페이스에 액세스하려고 할 때 발생합니다.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|개체의 형식 라이브러리를 검색할 수 없습니다. 이 오류는 Properties 컬렉션이 해당 IDispatch 인터페이스를 통해 개체에 대한 형식 라이브러리를 검색하려고 할 때 발생합니다.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|0x%3!8.8X! " %4!s!" 오류로 인해 " %1!s!" 태스크, " %2!s!" 유형에 대해 태스크 개체를 초기화하지 없습니다.|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|XML 문서 "%1"을(를) 만들지 못했습니다.|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|변수에서 유형이 다른 속성으로의 속성 매핑이 수행되기 때문에 오류가 발생했습니다. 속성 유형은 변수 유형과 일치해야 합니다.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|속성 매핑의 대상을 지원되지 않는 개체 유형으로 설정하려고 했습니다. 이 오류는 지원되지 않는 개체 유형을 속성 매핑에 전달할 때 발생합니다.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|패키지 "%1"의 개체에 대한 패키지 경로를 확인할 수 없습니다.  패키지 경로가 올바른지 확인하십시오.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|속성 맵의 대상 속성이 비어 있습니다. 대상 속성 이름을 설정하십시오.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|패키지가 적어도 하나 이상의 속성 매핑을 복원하지 못했습니다.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|이 이름을 가진 여러 변수가 다른 네임스페이스에 존재하므로 변수 이름이 모호합니다. 모호하지 않게 하려면 네임스페이스로 한정된 이름을 지정하십시오.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|속성 매핑의 대상 개체에 부모가 없습니다. 대상 개체가 시퀀스 컨테이너의 자식이 아닙니다. 패키지에서 제거되었을 수 있습니다.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|속성 매핑이 잘못되었습니다. 매핑이 무시됩니다.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|대상이 제거됨을 알리는 속성 매핑 경고 시 오류가 발생했습니다.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|For Each 루프에서 잘못된 속성 매핑이 발견되었습니다. 이 오류는 ForEach 속성 매핑을 복원하지 못할 때 발생합니다.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|대상 속성이 잘못된 속성 매핑에서 지정되었습니다. 이 오류는 대상 개체에서 찾을 수 없는 속성을 해당 개체에서 지정할 때 발생합니다.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|XML에서 태스크를 만들 수 없습니다. 이 오류는 런타임에 태스크를 만들기 위한 이름을 확인하지 못할 때 발생합니다. 이름이 올바른지 확인하십시오.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|기존 검사점 파일을 업데이트된 검사점 파일로 바꿀 수 없습니다. 임시 파일에서 검사점이 생성되었지만 기존 파일을 새 파일로 덮어쓰지 못했습니다.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|패키지가 항상 검사점에서 다시 시작되도록 구성되었지만 검사점 파일이 지정되지 않았습니다.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|오류 0x%2!8.8X! "%3"(으)로 인해 XML 검사점 파일 "%1"을(를) 로드하지 못했습니다. 지정된 파일 이름이 올바른지, 그리고 파일이 존재하는지 확인하십시오.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|검사점 파일을 로드할 수 없기 때문에 실행 중에 패키지가 실패했습니다. 패키지를 계속 실행하려면 검사점 파일이 필요합니다. 이 오류는 일반적으로 CheckpointUsage 속성이 ALWAYS로 설정되어 패키지가 항상 다시 시작되도록 지정된 경우에 발생합니다.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|For Loop "%1"에서 계산 조건 식이 비어 있습니다. For Loop에는 부울 계산 식이 있어야 합니다.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|대입 식 "%1"의 결과를 할당된 변수와 호환되는 유형으로 변환할 수 없습니다.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|대입 식에서 읽기 전용 변수 "%1"을(를) 사용하는 동안 오류가 발생했습니다. 변수가 읽기 전용이므로 식 결과를 변수에 할당할 수 없습니다. 쓸 수 있는 변수를 선택하거나 이 변수에서 식을 제거하십시오.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|변수 "%1"이(가) 없거나 쓰기용으로 액세스할 수 없기 때문에 식 "%2"을(를) 계산할 수 없습니다. 변수를 찾을 수 없거나 쓰기용으로 잠글 수 없기 때문에 식 결과를 변수에 할당할 수 없습니다.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|식 "%1"의 결과 유형이 "%2"이며 이 유형을 지원되는 유형으로 변환할 수 없습니다.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|"%1" 식의 결과를 "%2" 유형에서 지원되는 유형으로 변환하지 못했습니다(오류 코드 0x%3!8.8X!). 유형 변환이 지원되지만 식 결과를 런타임 엔진이 지원하는 유형으로 변환하려는 동안 오류가 발생했습니다.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|개체 이름이 잘못되었습니다. 이름을 NULL로 설정할 수 없습니다.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|개체 이름이 잘못되었습니다. 이름을 비워 둘 수 없습니다.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|개체 이름 "%1"이(가) 잘못되었습니다. 이름에는 / \ : [ ] . 문자를 사용할 수 없습니다. =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|개체 이름 "%1"이(가) 잘못되었습니다. 인쇄가 불가능한 제어 문자를 이름에 사용할 수 없습니다.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|개체 이름 "%1"이(가) 잘못되었습니다. 이름은 공백으로 시작할 수 없습니다.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|개체 이름 "%1"이(가) 잘못되었습니다. 이름은 공백으로 끝낼 수 없습니다.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|개체 이름 "%1"이(가) 잘못되었습니다. 이름은 알파벳 문자로 시작해야 합니다.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|개체 이름 "%1"이(가) 잘못되었습니다. 이름은 알파벳 문자나 밑줄("_")로 시작해야 합니다.|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|개체 이름 "%1"이(가) 잘못되었습니다. 이름에는 영숫자나 밑줄("_")만 포함되어야 합니다.|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|개체 이름 "%1"이(가) 잘못되었습니다. 이름에는 / \ : ? 문자를 사용할 수 없습니다. " \< > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|기본 지속성을 사용하여 값 속성 "%1"을(를) 로드하지 못했습니다.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|연결 관리자 "%1"이(가) "%2" 유형이 아닙니다.|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1"이(가) 비어 있습니다.|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|nodelist 열거자 섹션의 데이터 노드가 잘못되었습니다.|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|열거자를 만들 수 없습니다.|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|캐시가 사용 중이므로 작업이 실패했습니다.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|속성을 수정할 수 없습니다.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|패키지를 업그레이드하지 못했습니다.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|오류 0x%1!8.8X! 발생했습니다. %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|패키지를 지정하지 않았습니다.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|연결을 지정하지 않았습니다.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|"%2" 유형의 연결 관리자 "%1"은(는) 지원되지 않습니다. "FILE" 및 "OLEDB" 연결 관리자만 지원됩니다.|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|오류 0x%1!8.8X! 발생했습니다. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|오류 0x%1!8.8X! 발생했습니다. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|태스크에서 Validate 메서드가 실패했으며 오류 코드 0x%1!8.8X!(%2)이(가) 0x%1!8.8X!(%2)). Validate 메서드는 성공해야 하며 "out" 매개 변수를 사용하여 결과를 나타내야 합니다.|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|태스크에서 Execute 메서드가 오류 코드 0x%1!8.8X!(%2)을(를) 0x%1!8.8X!(%2)). Execute 메서드는 성공해야 하며 "out" 매개 변수를 사용하여 결과를 나타내야 합니다.|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|종속성을 검색하는 동안 태스크 "%1": 0x%2!8.8X! 에서 오류가 발생했습니다. 런타임에 태스크의 종속성 컬렉션에서 종속성을 검색하는 동안 오류가 발생했습니다. 종속성 인터페이스 중 하나를 태스크에서 잘못 구현했을 수 있습니다.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|태스크의 유효성 검사 중에 오류가 발생했습니다.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|연결 문자열 형식이 잘못되었습니다. 연결 문자열은 X=Y 형태의 구성 요소가 세미콜론으로 구분되어 하나 이상 구성되어야 합니다. 이 오류는 구성 요소가 없는 연결 문자열이 데이터베이스 연결 관리자에 설정될 때 발생합니다.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|연결 문자열 구성 요소는 따옴표가 없는 세미콜론을 포함할 수 없습니다. 값에 세미콜론을 사용해야 할 경우 전체 값을 따옴표로 묶어야 합니다. 이 오류는 InitialCatalog 속성과 같이 연결 문자열의 값에 따옴표가 없는 세미콜론이 있을 때 발생합니다.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|하나 이상의 로그 공급자에 대한 유효성을 검사하지 못했습니다. 패키지를 실행할 수 없습니다. 로그 공급자의 유효성을 검사하지 못하면 패키지가 실행되지 않습니다.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|배열의 값이 잘못되었습니다.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|ForEach 열거자에서 반환한 열거자 요소가 IEnumerator를 구현하지 않습니다. ForEach 열거자의 CollectionEnumerator 속성과 일치하지 않습니다.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|열거자가 인덱스 "%1!d!"의 요소를 검색하지 못했습니다.|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|함수를 찾을 수 없습니다.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|함수를 찾을 수 없습니다.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|ActiveX 스크립트 태스크가 잘못된 XML 요소로 시작되었습니다.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|처리기를 찾을 수 없습니다.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|시스템에 설치된 스크립트 언어를 검색하는 동안 오류가 발생했습니다.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|ActiveX 스크립트 호스트를 만드는 동안 오류가 발생했습니다. 스크립트 호스트를 올바르게 설치했는지 확인하십시오.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|선택한 언어에 대한 스크립트 호스트를 인스턴스화하는 동안 오류가 발생했습니다. 선택한 스크립트 언어가 시스템에 설치되었는지 확인하십시오.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|SSIS 변수를 스크립트 호스트 네임스페이스에 추가하는 동안 오류가 발생했습니다. 이로 인해서 스크립트의 SSIS 변수를 태스크에서 사용하지 못할 수 있습니다.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|스크립트 텍스트를 구문 분석하는 동안 오류가 발생했습니다. 선택한 언어에 대한 스크립트 엔진이 제대로 설치되었는지 확인하십시오.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|입력한 함수 이름이 잘못되었습니다. 올바른 함수 이름이 지정되어 있는지 확인하십시오.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|스크립트를 실행하는 동안 오류가 발생했습니다. 선택한 언어에 대한 스크립트 엔진이 올바르게 설치되었는지 확인하십시오.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|관리되는 형식 라이브러리를 스크립트 호스트에 추가하는 동안 오류가 발생했습니다. DTS 2000 런타임이 설치되었는지 확인하십시오.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|대량 삽입 태스크가 잘못된 XML 요소로 시작되었습니다.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|데이터 파일 이름을 지정하지 않았습니다.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|처리기를 찾을 수 없습니다.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|지정한 연결을 설정하지 못했습니다: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|연결 관리자를 가져오지 못했습니다.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|연결이 잘못되었습니다.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|연결이 Null입니다.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|실행하지 못했습니다.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|데이터베이스에서 테이블을 검색하는 동안 오류가 발생했습니다.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|테이블의 열을 검색하는 동안 오류가 발생했습니다.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|데이터베이스 작업에서 오류가 발생했습니다.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|지정한 연결 "%1"이(가) 잘못되었거나 잘못된 개체를 가리킵니다. 계속하려면 올바른 연결을 지정하십시오.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|지정한 대상 연결이 잘못되었습니다. 계속하려면 올바른 연결을 지정하십시오.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|계속하려면 테이블 이름을 지정해야 합니다.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|태그 "%1"의 LoadFromXML에서 오류가 발생했습니다.|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|태그 "%1"의 SaveToXML에서 오류가 발생했습니다.|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|연결이 잘못되었습니다.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|실행하지 못했습니다.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|데이터베이스에서 테이블을 검색하는 동안 오류가 발생했습니다.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|테이블의 열을 검색하는 동안 오류가 발생했습니다.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|데이터 파일을 여는 동안 오류가 발생했습니다.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|입력 OEM 파일을 지정된 형식으로 변환할 수 없습니다.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|데이터베이스 작업에 오류가 발생했습니다.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|지정된 연결 관리자가 없습니다.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|연결 "%1"이(가) Analysis Services 연결이 아닙니다.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|연결 "%1"을(를) 찾을 수 없습니다.|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services DDL 실행 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services 처리 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|DDL이 잘못되었습니다.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|ProcessingCommands에서 찾은 DDL이 잘못되었습니다.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|실행 결과를 읽기 전용 변수에 저장할 수 없습니다.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|변수 "%1"이(가) 정의되지 않았습니다.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|연결 관리자 "%1"이(가) 정의되지 않았습니다.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|연결 관리자 "%1"이(가) 파일 연결 관리자가 아닙니다.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|역직렬화하는 동안 "%1"을(를) 찾지 못했습니다.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|예외로 인해 추적이 중지되었습니다.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|DDL을 실행하지 못했습니다.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|연결 "%1"에 연결된 파일이 없습니다.|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|변수 "%1"이(가) 정의되지 않았습니다.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|파일 연결 "%1"이(가) 정의되지 않았습니다.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|DTS 2000 패키지 실행 태스크가 잘못된 XML 요소로 시작되었습니다.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|처리기를 찾을 수 없습니다.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|패키지 이름을 지정하지 않았습니다.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|패키지 ID를 지정하지 않았습니다.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|패키지 버전 GUID를 지정하지 않았습니다.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server를 지정하지 않았습니다.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|SQL Server 사용자 이름을 지정하지 않았습니다.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|스토리지 파일 이름을 지정하지 않았습니다.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|DTS 2000 패키지 속성이 비어 있습니다.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|DTS 2000 패키지를 실행하는 동안 오류가 발생했습니다.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|네트워크에서 사용 가능한 SQL Server를 로드할 수 없습니다. 네트워크 연결을 확인합니다.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|데이터 형식은 Null일 수 없습니다. 값의 유효성 검사에 사용할 올바른 데이터 형식을 지정하십시오.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|데이터 형식에 대해 Null의 유효성을 검사할 수 없습니다.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|필수 인수가 Null입니다.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|DTS 2000 패키지 태스크를 실행하려면 SQL Server 설치 프로그램을 시작하고 [설치할 구성 요소] 페이지에서 [고급] 단추를 사용하여 [레거시 구성 요소]를 선택하십시오.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1"이(가) 값 유형이 아닙니다.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|"%1"을(를) "%2"(으)로 변환할 수 없습니다.|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|"%2"에 대해 "%1"의 유효성을 검사할 수 없습니다.|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|태그 "%1"의 LoadFromXML에서 오류가 발생했습니다.|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|태그 "%1"의 SaveToXML에서 오류가 발생했습니다.|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|제공된 제한 시간 값이 잘못되었습니다. 태스크에서 프로세스 실행을 허용하는 시간(초)을 지정하십시오. 최소 제한 시간은 0이며, 이 경우 제한 시간 값이 사용되지 않으므로 프로세스가 완료되거나 오류가 발생할 때까지 실행됩니다. 최대 제한 시간은 2147483(((2^31) - 1)/1000)입니다.|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|프로세스가 태스크의 유효 기간 이후에도 계속 실행되는 경우 스트림을 리디렉션할 수 없습니다.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|프로세스 시간이 초과되었습니다.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|실행 파일을 지정하지 않았습니다.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|표준 출력 변수는 읽기 전용입니다.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|표준 오류 변수는 읽기 전용입니다.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|프로세스 실행 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|"%1"에서 "%2" "%3"을(를) 실행하면서 필요한 프로세스 종료 코드는 "%4"이었으나 사용된 코드는 "%5"입니다.|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|디렉터리 "%1"이(가) 없습니다.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|파일/프로세스 "%1"이(가) 디렉터리 "%2"에 없습니다.|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|파일/프로세스 "%1"이(가) 경로에 없습니다.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|작업 디렉터리 "%1"이(가) 없습니다.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|프로세스가 종료될 때 코드 "%1"이(가) 반환되었습니다. 필요한 코드는 "%2"입니다.|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|동기화 개체가 실패했습니다.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|파일 시스템 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|디렉터리가 이미 있습니다.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1"이(가) 작업 유형 "%2"에서 잘못되었습니다.|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|작업 "%1"의 대상 속성이 설정되지 않았습니다.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|작업 "%1"의 원본 속성이 설정되지 않았습니다.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|연결 "%1"의 유형이 파일이 아닙니다.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|변수 "%1"이(가) 없습니다.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|변수 "%1"이(가) 문자열이 아닙니다.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|연결 "%2"이(가) 나타내는 파일 또는 디렉터리 "%1"이(가) 없습니다.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|대상 파일 연결 관리자 "%1"의 사용 유형이 잘못되었습니다: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|원본 파일 연결 관리자 "%1"의 사용 유형 "%2"이(가) 잘못되었습니다.|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|파일 시스템 작업에 대한 정보를 제공합니다.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|파일 시스템 태스크|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|파일 복사 및 삭제 같은 파일 시스템 작업을 수행합니다.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|동기화 개체가 실패했습니다.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|파일 목록을 가져올 수 없습니다.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|로컬 경로가 비어 있습니다.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|원격 경로가 비어 있습니다.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|지역 변수가 비어 있습니다.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|원격 변수가 비어 있습니다.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|FTP 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|연결이 비어 있습니다. 올바른 FTP 연결이 제공되었는지 확인하십시오.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|지정한 연결이 FTP 연결이 아닙니다. 올바른 FTP 연결이 제공되었는지 확인하십시오.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Null XML 요소로 태스크를 초기화할 수 없습니다.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Null XML 문서에 태스크를 저장할 수 없습니다.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|태그 "%1"의 LoadFromXML에서 오류가 발생했습니다.|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|"%1"에 파일이 없습니다.|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|변수 "%1"이(가) 비어 있습니다.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|변수 "%1"이(가) 비어 있습니다.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|파일 "%1"에 파일 경로가 없습니다.|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|변수 "%1"에 파일 경로가 없습니다.|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|변수 "%1"이(가) 문자열이 아닙니다.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|변수 "%1"이(가) 없습니다.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|작업 "%1"의 경로가 잘못되었습니다.|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1"이(가) 이미 있습니다.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|연결 "%1"의 유형이 파일이 아닙니다.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|"%1"이(가) 나타내는 파일이 없습니다.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|디렉터리가 변수 "%1"에 지정되어 있지 않습니다.|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|파일이 "%1"에 없습니다.|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|디렉터리가 파일 연결 관리자 "%1"에 지정되어 있지 않습니다.|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|로컬 파일 "%1"을(를) 삭제할 수 없습니다.|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|로컬 디렉터리 "%1"을(를) 제거할 수 없습니다.|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|로컬 디렉터리 "%1"을(를) 만들 수 없습니다.|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|"%1"을(를) 사용하여 파일을 받을 수 없습니다.|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|"%1"을(를) 사용하여 파일을 보낼 수 없습니다.|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|"%1"을(를) 사용하여 원격 디렉터리를 만들 수 없습니다.|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|"%1"을(를) 사용하여 원격 디렉터리를 제거할 수 없습니다.|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|"%1"을(를) 사용하여 원격 파일을 삭제할 수 없습니다.|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|"%1"을(를) 사용하여 FTP 서버에 연결할 수 없습니다.|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|변수 "%1"이(가) "/" 문자로 시작하지 않습니다.|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|원격 경로 "%1"이(가) "/" 문자로 시작하지 않습니다.|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|FTP 연결을 설정하는 동안 오류가 발생했습니다. 올바른 연결 형식 "%1"이(가) 지정되어 있는지 확인하십시오.|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|인증서 저장소를 열지 못했습니다.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|인증서의 표시 이름을 검색하는 동안 오류가 발생했습니다.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|인증서의 발급자 이름을 검색하는 동안 오류가 발생했습니다.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|인증서의 이름을 검색하는 동안 오류가 발생했습니다.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|MSMQ 연결 이름이 설정되지 않았습니다.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|태스크가 잘못된 XML 요소로 초기화되었습니다.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|데이터 파일 이름이 비어 있습니다.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|저장할 데이터 파일에 지정된 이름이 비어 있습니다.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|파일 크기는 4MB보다 작아야 합니다.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|데이터 파일을 저장하지 못했습니다.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|문자열 필터 값이 비어 있습니다.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|큐 경로가 잘못되었습니다.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|메시지 큐 태스크가 분산 트랜잭션 참여를 지원하지 않습니다.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|메시지 유형이 잘못되었습니다.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|메시지 큐 시간이 초과되었습니다. 메시지를 받지 못했습니다.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|지정된 속성이 잘못되었습니다. 인수 유형이 올바른지 확인하십시오.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|메시지가 인증되지 않았습니다.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|잘못된 개체로 암호화 알고리즘 값을 설정하려고 합니다.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|문자열 메시지를 받는 변수가 비어 있습니다.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|변수 메시지를 받는 변수가 비어 있습니다.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|연결 "%1"이(가) MSMQ 유형이 아닙니다.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|데이터 파일 "%1"이(가) 지정한 위치에 이미 있습니다. 덮어쓰기 옵션이 False로 설정되어 있으므로 파일을 덮어쓸 수 없습니다.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|문자열 메시지를 받기 위해 지정한 변수 "%1"이(가) 패키지 변수 컬렉션에 없습니다.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|연결 관리자 "%1"이(가) 비어 있습니다.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|연결 관리자 "%1"이(가) 없습니다.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|오류 "%1": "%2"\r\n줄 "%3"   열 "%4"-"%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|스크립트를 컴파일하는 동안 오류가 발생했습니다: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|오류 "%1": "%2"\r\n줄 "%3" 열 "%4"-"%5"\r\n줄 텍스트: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|사용자 스크립트에서 오류 결과를 반환했습니다.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|사용자 스크립트 파일을 로드하지 못했습니다.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|사용자 스크립트에서 예외가 발생했습니다. "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|진입점 클래스 "%1"의 인스턴스를 만들 수 없습니다.|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|XML에서 스크립트 태스크를 로드하는 동안 예외가 발생했습니다: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|원본 항목 "%1"이(가) 패키지에 없습니다.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|이진 항목 "%1"이(가) 패키지에 없습니다.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1"은(는) 유효한 스크립트 언어가 아닙니다.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|스크립트 이름이 잘못되었습니다. 공백, 슬래시 또는 특수 문자를 사용하거나 숫자로 시작할 수 없습니다.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|지정된 스크립트 언어가 잘못되었습니다.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Null 태스크로 초기화할 수 없습니다.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|스크립트 태스크 사용자 인터페이스는 스크립트 태스크로 초기화해야 합니다.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|스크립트 태스크 사용자 인터페이스가 초기화되지 않았습니다.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|이름을 비워 둘 수 없습니다.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|프로젝트 이름이 잘못되었습니다. 공백, 슬래시 또는 특수 문자를 사용하거나 숫자로 시작할 수 없습니다.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|지정된 스크립트 언어가 잘못되었습니다.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|진입점을 찾을 수 없습니다.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|스크립트 언어를 지정하지 않았습니다. 올바른 스크립트 언어가 지정되어 있는지 확인하십시오.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|사용자 인터페이스 초기화: 태스크가 Null입니다.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|스크립트 태스크 사용자 인터페이스가 잘못된 태스크로 초기화되었습니다.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|받는 사람을 지정하지 않았습니다.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|SMTP(Simple Mail Transfer Protocol) 서버를 지정하지 않았습니다. SMTP 서버의 올바른 이름이나 IP 주소를 지정하십시오.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|메일 보내기 태스크가 잘못된 XML 요소로 시작되었습니다.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|파일 "%1"이(가) 없거나 파일에 액세스할 수 있는 권한이 없습니다.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|지정된 SMTP(Simple Mail Transfer Protocol) 서버가 올바른지 확인하십시오.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|연결 "%1"이(가) File 유형이 아닙니다.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|작업 "%1"에 파일 "%2"이(가) 없습니다.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|변수 "%1"이(가) 문자열 유형이 아닙니다.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|연결 "%1"이(가) SMTP 유형이 아닙니다.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|연결 "%1"이(가) 비어 있습니다.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|지정한 연결 "%1"이(가) 없습니다.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|Transact-SQL 문을 지정하지 않았습니다.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|연결이 XML 결과 집합을 지원하지 않습니다.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|지정한 연결 형식의 처리기를 찾을 수 없습니다.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|지정된 연결 관리자가 없습니다.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|연결 관리자에서 연결을 가져올 수 없습니다.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Null 매개 변수 이름을 가질 수 없습니다.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|매개 변수 이름이 잘못되었습니다.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|유효한 매개 변수 이름은 Int 또는 문자열 유형입니다.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|변수 "%1"이(가) 읽기 전용이므로 결과 바인딩에 사용할 수 없습니다.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|이 컬렉션에는 색인이 할당되지 않았습니다.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|변수 "%1"이(가) 읽기 전용이므로 매개 변수 바인딩에서 "out" 매개 변수나 반환 값으로 사용할 수 없습니다.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|이 컬렉션에 해당 개체가 없습니다.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|관리되는 연결을 설정할 수 없습니다.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|단일 행 결과 유형에 대한 결과 열을 채울 수 없습니다. 쿼리가 빈 결과 집합을 반환했습니다.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|ResultSetType에 대해 반환된 결과 바인딩 수가 잘못되었습니다: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|전체 결과 집합 및 XML 결과에 대해 결과 바인딩 이름을 0으로 설정해야 합니다.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|매개 변수 방향 플래그가 잘못되었습니다.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|XML 조각에 SQL 태스크 데이터가 없습니다.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|반환 값 유형의 매개 변수가 첫 번째 매개 변수가 아니거나 반환 값 유형의 매개 변수가 여러 개 있습니다.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|연결 "%1"이(가) 파일 연결 관리자가 아닙니다.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|"%1"이(가) 나타내는 파일이 없습니다.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|변수 "%1"의 유형이 문자열이 아닙니다.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|변수 "%1"이(가) 없거나 잠글 수 없습니다.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|연결 관리자 "%1"이(가) 없습니다.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|연결 "%1"을(를) 설정하지 못했습니다. 연결이 제대로 구성되지 않았거나 이 연결에 대한 올바른 권한이 없는 것 같습니다.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|이름 "%1"별 결과 바인딩은 이 연결 형식에 대해 지원되지 않습니다.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|단일 행의 결과 집합 유형을 지정했지만 행이 반환되지 않았습니다.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|Transact-SQL 문에 사용할 수 있는 연결이 끊긴 레코드 집합이 없습니다.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|지원되지 않는 유형입니다.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|알 수 없는 유형입니다.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|매개 변수 바인딩 \\"%s\\"에 지원되지 않는 데이터 형식이 있습니다.|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|매개 변수 이름에서는 서수와 명명된 형식을 혼합하여 사용할 수 없습니다.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|매개 변수 바인딩 \\"%s\\"에서 매개 변수 방향이 잘못되었습니다.|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|결과 집합 바인딩 \\"%s\\"에서 데이터 형식이 지원되지 않습니다.|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|결과 열 인덱스 %d이(가) 잘못되었습니다.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|결과 집합에서 열 \\"%s\\"을(를) 찾을 수 없습니다.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|이 쿼리 실행과 연결된 결과 행 집합이 없습니다.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|ODBC 연결에서 연결이 끊긴 레코드 집합을 사용할 수 없습니다.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|결과 집합인 열 %hd에서 데이터 형식이 지원되지 않습니다.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|쿼리 결과가 포함된 XML을 로드할 수 없습니다.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|패키지에 대한 연결 이름 또는 변수 이름을 지정해야 합니다.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|패키지를 만들지 못했습니다.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|TableMetaDataNode가 XMLNode가 아닙니다.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|파이프라인을 만들지 못했습니다.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|변수의 유형이 잘못되었습니다.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|지정한 연결 관리자가 파일 연결 관리자가 아닙니다.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|연결 관리자 "%1"에 지정한 파일 이름이 잘못되었습니다.|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|연결이 비어 있습니다. 올바른 HTTP 연결이 지정되어 있는지 확인하십시오.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|연결이 없습니다. 올바른 기존 HTTP 연결이 지정되어 있는지 확인하십시오.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|지정한 연결이 HTTP 연결이 아닙니다. 올바른 HTTP 연결이 지정되어 있는지 확인하십시오.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|웹 서비스 이름이 비어 있습니다. 올바른 웹 서비스 이름이 지정되어 있는지 확인하십시오.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|웹 메서드 이름이 비어 있습니다. 올바른 웹 메서드가 지정되어 있는지 확인하십시오.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|웹 메서드가 비어 있거나 없을 수 있습니다. 지정할 기존 웹 메서드가 있는지 확인하십시오.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|출력 위치가 비어 있습니다. 기존 파일 연결이나 변수가 지정되어 있는지 확인하십시오.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|변수를 찾을 수 없습니다. 변수가 패키지에 있는지 확인하십시오.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|결과를 저장할 수 없습니다. 변수가 읽기 전용이 아닌지 확인하십시오.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|태그 "%1"의 LoadFromXML에서 오류가 발생했습니다.|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|태그 "%1"의 SaveToXML에서 오류가 발생했습니다.|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Null XML 문서에 태스크를 저장할 수 없습니다.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Null XML 요소로 태스크를 초기화할 수 없습니다.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|웹 서비스 태스크가 잘못된 XML 요소로 시작되었습니다.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|예기치 않은 XML 요소를 발견했습니다.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|HTTP 연결을 설정하는 동안 오류가 발생했습니다. 올바른 연결 형식이 지정되어 있는지 확인하십시오.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|결과를 저장할 수 없습니다. 기존 파일 연결이 있는지 확인하십시오.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|결과를 저장할 수 없습니다. 파일이 있는지 확인하십시오.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|결과를 저장할 수 없습니다. 파일 이름이 비어 있거나 다른 프로세스에서 파일을 사용 중입니다.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|파일 연결을 설정하는 동안 오류가 발생했습니다. 올바른 파일 연결이 지정되어 있는지 확인하십시오.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Primitive 값을 가진 Complex 유형, 즉 Primitive Array 및 Enumeration만 지원됩니다.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Primitive, Enum, Complex, PrimitiveArray 및 ComplexArray 유형만 지원됩니다.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|이 버전의 WSDL은 지원되지 않습니다.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|잘못된 XML 요소로 초기화되었습니다.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|필수 특성을 찾을 수 없습니다.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|열거형 "%1"에 값이 없습니다. WSDL이 손상되었습니다.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|연결을 찾을 수 없습니다.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|이름이 같은 연결이 이미 있습니다.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|연결은 Null이거나 비워 둘 수 없습니다.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|지정한 연결이 HTTP 연결이 아닙니다. 올바른 HTTP 연결이 지정되어 있는지 확인하십시오.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|지정한 URI(Uniform Resource Identifier)에 올바른 WSDL이 없습니다.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|WSDL 파일을 읽을 수 없습니다. 입력 WSDL 파일이 잘못되었습니다. 판독기에서 다음 오류가 발생했습니다: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|서비스 설명은 Null일 수 없습니다.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|서비스 이름은 Null일 수 없습니다.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL은 Null일 수 없습니다.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|서비스를 현재 사용할 수 없습니다.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|SOAP 포트에서 서비스를 사용할 수 없습니다.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|WSDL(Web Services Description Language)을 구문 분석하지 못했습니다. SOAP 포트에 해당하는 바인딩을 찾을 수 없습니다.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|WSDL(Web Services Description Language)을 구문 분석하지 못했습니다. SOAP 포트에 해당하는 PortType을 찾을 수 없습니다.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|지정한 메서드에 해당하는 메시지를 찾을 수 없습니다.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|지정된 웹 서비스에 대한 프록시를 생성할 수 없습니다. 프록시 "%1"을(를) 생성하는 동안 다음 오류가 발생했습니다.|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|지정된 웹 서비스에 대한 프록시를 로드할 수 없습니다. 정확한 오류는 다음과 같습니다: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|지정한 서비스를 찾을 수 없습니다. 정확한 오류는 다음과 같습니다: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|메서드 실행 중에 웹 서비스에서 다음 오류가 발생했습니다: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|웹 메서드를 실행할 수 없습니다. 정확한 오류는 다음과 같습니다: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo는 Null일 수 없습니다.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|지정한 WebMethodInfo가 잘못되었습니다. 지정한 ParamValue가 ParamType과 일치하지 않습니다. DTSParamValue가 PrimitiveValue 유형이 아닙니다.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|지정한 WebMethodInfo가 잘못되었습니다. 지정한 ParamValue가 ParamType과 일치하지 않습니다. 검색된 DTSParamValue가 EnumValue 유형이 아닙니다.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|지정한 WebMethodInfo가 잘못되었습니다. 지정한 ParamValue가 ParamType과 일치하지 않습니다. 검색된 DTSParamValue가 ComplexValue 유형이 아닙니다.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|지정한 WebMethodInfo가 잘못되었습니다. 지정한 ParamValue가 ParamType과 일치하지 않습니다. 검색된 DTSParamValue가 ArrayValue 유형이 아닙니다.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|지정한 WebMethodInfo가 잘못되었습니다. "%1"이(가) Primitive 유형이 아닙니다.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|ArrayValue의 형식이 잘못되었습니다. 배열에 적어도 하나 이상의 요소가 있어야 합니다.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|열거의 값은 Null일 수 없습니다. 열거의 기본값을 선택하십시오.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|데이터 형식에 대해 Null의 유효성을 검사할 수 없습니다.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|열거 값이 잘못되었습니다.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|지정한 클래스에 이름이 "%1"인 공용 속성이 없습니다.|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|"%1"을(를) "%2"(으)로 변환할 수 없습니다.|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|정리하지 못했습니다. 웹 서비스에 대해 생성된 프록시가 삭제되지 않았을 수 있습니다.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|"%1" 유형의 개체를 만들 수 없습니다. 기본 생성자가 있는지 확인하십시오.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1"이(가) 값 유형이 아닙니다.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|"%1"의 유효성을 "%1"에 대해 검사할 수 없습니다.|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|데이터 형식은 Null일 수 없습니다. 유효성을 검사할 데이터 형식의 값을 지정하십시오.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|이 지점에서 ParamValue를 삽입할 수 없습니다. 지정한 인덱스가 0보다 작거나 정해진 길이보다 긴 것 같습니다.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|입력 WSDL 파일이 잘못되었습니다.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|동기화 개체가 실패했습니다.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|WQL 쿼리가 없습니다.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|대상을 설정해야 합니다.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|WMI 연결이 설정되지 않았습니다.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI 데이터 판독기 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|태스크의 유효성을 검사하지 못했습니다.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|파일 "%1"이(가) 없습니다.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|연결 관리자 "%1"이(가) 없습니다.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|변수 "%1"이(가) 문자열 또는 개체 유형이 아닙니다.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|연결 "%1"이(가) "FILE" 유형이 아닙니다.|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|연결 "%1"이(가) "WMI" 유형이 아닙니다.|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|파일 "%1"이(가) 이미 있습니다.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|연결 관리자 "%1"이(가) 비어 있습니다.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|변수 "%1"은(는) 데이터 테이블에 할당할 개체 유형이어야 합니다.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|잘못된 WMI 쿼리로 인해 태스크가 실패했습니다. "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|원래 값을 유지하도록 설정되었기 때문에 변수 "%1"에 쓸 수 없습니다.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|동기화 개체가 실패했습니다.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|WQL 쿼리가 없습니다.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|WMI 연결이 없습니다.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|WMI 쿼리를 실행하지 못했습니다.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|WMI 이벤트 감시자 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|연결 관리자 "%1"이(가) 없습니다.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|파일 "%1"이(가) 없습니다.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|변수 "%1"이(가) 문자열 유형이 아닙니다.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|연결 "%1"이(가) "FILE" 유형이 아닙니다.|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|연결 "%1"이(가) "WMI" 유형이 아닙니다.|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|파일 "%1"이(가) 이미 있습니다.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|연결 관리자 "%1"이(가) 비어 있습니다.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|"%2"이(가) 나타내는 이벤트가 발생하기 전에 "%1"초의 제한 시간이 초과되었습니다.|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Wql 쿼리를 감시하는 중 다음 시스템 예외가 발생했습니다: "%1". 쿼리에서 오류를 확인하거나 WMI 연결의 액세스 권한 및 사용 권한을 확인하십시오.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|지정한 작업이 정의되지 않았습니다.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|연결 형식이 FILE이 아닙니다.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|원본 XML 문서에서 XmlReader를 가져올 수 없습니다.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|변경된 XML 문서에서 XmlReader를 가져올 수 없습니다.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|XDL diffgram XML에서 XDL diffgram 판독기를 가져올 수 없습니다.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|노드 목록이 비어 있습니다.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|요소를 찾을 수 없습니다.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|지정한 작업이 정의되지 않았습니다.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|XPathNavigator에 예기치 않은 내용 항목이 있습니다.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|유효성 검사를 적용하기 위한 스키마를 찾을 수 없습니다.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|인스턴스 문서의 유효성을 검사하는 동안 유효성 검사 오류가 발생했습니다.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|동기화 개체가 실패했습니다.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|루트 노드가 일치하지 않습니다.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|최종 편집 스크립트의 편집 스크립트 작업 유형이 잘못되었습니다.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|DiffgramAddSubtrees 클래스와 함께 CDATA 노드를 추가해야 합니다.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|DiffgramAddSubtrees 클래스와 함께 설명 노드를 추가해야 합니다.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|DiffgramAddSubtrees 클래스와 함께 텍스트 노드를 추가해야 합니다.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|DiffgramAddSubtrees 클래스와 함께 의미 있는 공백 노드를 추가해야 합니다.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|OperationCost 배열이 XmlDiffOperation 열거를 반영하도록 수정하십시오.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|태스크에 작업이 없습니다.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|문서에 이미 데이터가 있으며 다시 사용할 수 없습니다.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|노드 유형이 잘못되었습니다.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|XML 태스크에서 잘못된 태스크 데이터 노드를 받았습니다.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|변수 데이터 형식이 문자열이 아닙니다.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|XML에서 인코딩을 가져올 수 없습니다.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|원본이 지정되지 않았습니다.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|두 번째 피연산자가 지정되지 않았습니다.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|XDL diffgram이 잘못되었습니다. "%1"은(는) 잘못된 경로 설명자입니다.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|XDL diffgram이 잘못되었습니다. 경로 설명자 "%1"과(와) 일치하는 노드가 없습니다.|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|XDL diffgram이 잘못되었습니다. 네임스페이스 URI가 "%1"인 루트 요소로 xd:xmldiff가 필요합니다.|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|XDL diffgram이 잘못되었습니다. xd:xmldiff 요소에 srcDocHash 특성이 없습니다.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|XDL diffgram이 잘못되었습니다. xd:xmldiff 요소에 옵션 특성이 없습니다.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|XDL diffgram이 잘못되었습니다. srcDocHash 특성에 잘못된 값이 있습니다.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|XDL diffgram이 잘못되었습니다. 옵션 특성에 잘못된 값이 있습니다.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|XDL diffgram은 이 XML 문서에 적용할 수 없습니다. rcDocHash 값이 일치하지 않습니다.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|XDL diffgram이 잘못되었습니다. 둘 이상의 노드가 xd:node 또는 xd:change 요소의 "%1" 경로 설명자와 일치합니다.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|XDL diffgram은 이 XML 문서에 적용할 수 없습니다. 새 XML 선언을 추가할 수 없습니다.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|내부 오류입니다. XmlDiffPathSingleNodeList는 하나의 노드만 포함할 수 있습니다.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|내부 오류입니다. 패치 후 "%1"개의 노드가 남았는데 1개만 필요합니다.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|XSLT에 의해 생성된 파일/텍스트가 유효한 XmlDocument가 아닙니다. 이 결과는 작업의 결과로 설정할 수 없습니다. "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|연결 "%1"에 연결된 파일이 없습니다.|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|속성 "%1"에 원본 XML 텍스트가 없습니다. XML 텍스트가 잘못되었거나 Null이거나 빈 문자열입니다.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|파일 "%1"이(가) 이미 있습니다.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|원본 연결을 지정해야 합니다.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|대상 연결을 지정해야 합니다.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|패키지에서 연결 "%1"을(를) 찾을 수 없습니다.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|연결 "%1"에 지정된 SQL Server 인스턴스의 버전은 전송 작업에 지원되지 않습니다.  버전 7, 2000 및 2005만 지원됩니다.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|원본 연결 "%1"에는 대상 연결 "%2"보다 이전 버전 또는 같은 버전의 SQL Server 인스턴스를 지정해야 합니다.|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|원본 데이터베이스를 지정해야 합니다.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|원본 서버에 원본 데이터베이스 "%1"이(가) 있어야 합니다.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|대상 데이터베이스를 지정해야 합니다.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|원본 데이터베이스와 대상 데이터베이스는 달라야 합니다.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|전송 파일 정보 %1에 파일 이름이 없습니다.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|전송 파일 정보 %1에 폴더 부분이 없습니다.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|전송 파일 정보 %1에 네트워크 공유 부분이 없습니다.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|원본 전송 파일 수와 대상 전송 파일 수가 같아야 합니다.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|트랜잭션 참여는 지원되지 않습니다.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|오프라인 데이터베이스 전송 중 다음 예외가 발생했습니다: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|네트워크 공유 "%1"을(를) 찾을 수 없습니다.|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|네트워크 공유 "%1에 액세스할 수 없습니다.  오류는 %2입니다.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|온라인 데이터베이스 전송을 수행하려면 사용자 "%1"이(가) DBO 또는 "%2"의 sysadmin이어야 합니다.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|오프라인 데이터베이스 전송을 수행하려면 사용자 "%1"이(가) "%2"의 sysadmin이어야 합니다.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|두 SQL Server 2005 서버 간에 오프라인 데이터베이스 전송을 수행하는 경우 전체 텍스트 카탈로그만 포함할 수 있습니다.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|데이터베이스 "%1"이(가) 대상 서버 "%2"에 이미 있습니다.|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|적어도 하나의 원본 파일을 지정해야 합니다.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|원본 데이터베이스 "%2"에서 파일 "%1"을(를) 찾을 수 없습니다.|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|U.S. FIPS 140-2와 호환되는 시스템에서는 요청한 작업을 수행할 수 없습니다.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|다음 오류로 인해 쿼리 "%1"을(를) 실행하지 못했습니다. "%2". 가능한 실패 원인: 쿼리에 문제가 있거나 "ResultSet" 속성, 매개 변수 또는 연결을 올바르게 설정하지 않았을 수 있습니다.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|XML 파일에서 저장 프로시저 이름을 읽는 중 오류가 발생했습니다.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|저장 프로시저 전송 태스크에 대한 데이터 노드가 잘못되었습니다.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|연결 "%1"이(가) "SMOServer" 유형이 아닙니다.|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|오류 "%1"(으)로 인해 실행하지 못했습니다.|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|다음 오류 메시지와 함께 오류가 발생했습니다: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|대량 삽입 실행이 실패했습니다.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|대상 경로가 잘못되었습니다.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|디렉터리를 만들 수 없습니다. 디렉터리가 있을 경우 태스크가 실패하도록 지정했습니다.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|태스크의 트랜잭션 옵션이 "Required"이고 연결 "%1"이(가) "ODBC" 유형입니다. ODBC 연결은 트랜잭션을 지원하지 않습니다.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|값을 변수 "%1"에 할당하는 동안 오류가 발생했습니다: "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|원본이 비어 있습니다.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|대상이 비어 있습니다.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|파일 또는 디렉터리 "%1"이(가) 없습니다.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|"%1"이(가) 원본 또는 대상으로 사용되며 비어 있습니다.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|파일 또는 디렉터리 "%1"이(가) 삭제되었습니다.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|디렉터리 "%1"이(가) 삭제되었습니다.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|변수 "%1"은(는) 데이터 테이블에 할당할 개체 유형이어야 합니다.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|변수 "%1"이(가) 문자열 데이터 형식이 아닙니다.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|FTP 연결을 설정하는 동안 오류가 발생했습니다. "%1"에 올바른 연결 형식이 지정되어 있는지 확인하십시오.|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|FTP 연결 관리자 "%1"을(를) 찾을 수 없습니다.|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|연결 "%1"의 파일 사용법 유형은 작업 "%3"에 대해 "%2"이(가) 되어야 합니다.|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|원본 서버와 대상 서버는 달라야 합니다.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|전송할 오류 메시지가 없습니다.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|오류 메시지와 해당 언어 목록의 크기가 다릅니다.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|오류 메시지 ID "%1"은(는) 허용되는 사용자 정의 오류 메시지 범위를 벗어났습니다. 사용자 정의 오류 메시지 ID는 50000에서 2147483647 사이여야 합니다.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|이 태스크는 트랜잭션에 참여할 수 없습니다.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|오류 메시지 전체 또는 일부를 전송하지 못했습니다.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|오류 메시지 "%1"이(가) 대상 서버에 이미 있습니다.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|원본 서버에서 오류 메시지 "%1"을(를) 찾을 수 없습니다.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|다음 오류로 인해 실행하지 못했습니다. "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|작업을 전송하지 못했습니다.|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|전송할 작업이 없습니다.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|작업 "%1"이(가) 대상 서버에 이미 있습니다.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|원본 서버에서 작업 "%1"을(를) 찾을 수 없습니다.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|전송할 "로그인" 목록이 비어 있습니다.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|원본 서버에서 "로그인" 목록을 가져올 수 없습니다.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|로그인 "%1"이(가) 대상 서버에 이미 있습니다.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|로그인 "%1"이(가) 원본에 없습니다.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|로그인 전체 또는 일부를 전송하지 못했습니다.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|저장 프로시저를 전송하지 못했습니다. 자세한 정보를 제공하는 오류가 이전에 발생했을 것입니다.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|저장 프로시저 "%1"을(를) 원본에서 찾을 수 없습니다.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|저장 프로시저 "%1"이(가) 대상 서버에 이미 있습니다.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|전송할 저장 프로시저가 없습니다.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|개체를 전송하지 못했습니다.|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|전송할 "개체" 목록이 비어 있습니다.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|저장 프로시저 "%1"이(가) 원본에 없습니다.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|저장 프로시저 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|전송할 저장 프로시저 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|규칙 "%1"이(가) 원본에 없습니다.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|규칙 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|전송할 규칙 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|테이블 "%1"이(가) 원본에 없습니다.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|테이블 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|전송할 테이블 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|뷰 "%1"이(가) 원본에 없습니다.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|뷰 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|전송할 뷰 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|사용자 정의 함수 "%1"이(가) 원본에 없습니다.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|사용자 정의 함수 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|전송할 사용자 정의 함수 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|기본값 "%1"이(가) 원본에 없습니다.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|기본값 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|전송할 기본값 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|사용자 정의 데이터 형식 "%1"이(가) 원본에 없습니다.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|사용자 정의 데이터 형식 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|전송할 사용자 정의 데이터 형식 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|파티션 함수 "%1"이(가) 원본에 없습니다.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|파티션 함수 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|전송할 파티션 함수 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|파티션 구성표 "%1"이(가) 원본에 없습니다.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|파티션 구성표 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|전송할 파티션 구성표 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|스키마 "%1"이(가) 원본에 없습니다.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|스키마 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|전송할 스키마 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|SqlAssembly "%1"이(가) 원본에 없습니다.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|전송할 SqlAssemblies 목록을 가져와서 설정하는 동안 오류가 발생했습니다. "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|사용자 정의 집계 "%1"이(가) 원본에 없습니다.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|사용자 정의 집계 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|전송할 사용자 정의 집계 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|사용자 정의 형식 "%1"이(가) 원본에 없습니다.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|사용자 정의 형식 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|전송할 사용자 정의 형식 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1"|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|XmlSchemaCollection "%1"이(가) 원본에 없습니다.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|전송할 XmlSchemaCollections 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|SQL Server 2005 이상의 서버 간에는 "%1" 유형의 개체만 지원됩니다.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|데이터베이스 목록이 비어 있습니다.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|로그인 "%1"이(가) 원본에 없습니다.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|로그인 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|전송할 로그인 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|사용자 "%1"이(가) 원본에 없습니다.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|사용자 "%1"이(가) 대상에 이미 있습니다.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|전송할 사용자 목록을 가져와서 설정하는 동안 오류가 발생했습니다: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|태스크가 트랜잭션에 연결 관리자를 보유할 수 없습니다.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|공급자가 OUTPUTENCODING 속성을 지원하지 않으므로 SQL Server에서 유니코드의 XML 데이터를 가져올 수 없습니다.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|FTP 작업 "%1"에 필요한 파일 연결 관리자 "%2"을(를) 찾을 수 없습니다.|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"로그인"은 서버 수준 개체이며 원본 및 대상이 같은 서버이므로 먼저 삭제할 수 없습니다. 개체를 먼저 삭제하면 원본에서 로그인도 제거됩니다.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|매개 변수 "%1"은(는) 음수일 수 없습니다. (-1)이 기본값으로 사용됩니다.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|데이터 흐름 개체를 로드할 수 없습니다. Microsoft.SqlServer.PipelineXml.dll이 제대로 등록되었는지 확인하십시오.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|데이터 흐름 개체를 저장할 수 없습니다. Microsoft.SqlServer.PipelineXml.dll이 제대로 등록되었는지 확인하십시오.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|데이터 흐름 개체를 저장하지 못했습니다.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|데이터 흐름 개체를 로드하지 못했습니다.|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|데이터 흐름 개체를 저장하지 못했습니다. 지정된 형식은 지원되지 않습니다.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|데이터 흐름 개체를 로드하지 못했습니다. 지정된 형식은 지원되지 않습니다.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|데이터 흐름 개체의 XML 지속성 이벤트 속성을 설정하지 못했습니다.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|데이터 흐름 개체의 지속성 XML DOM 속성을 설정하지 못했습니다.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|데이터 흐름 개체의 지속성 XML ELEMENT 속성을 설정하지 못했습니다.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|데이터 흐름 개체의 XML 지속성 속성을 설정하지 못했습니다.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|데이터 흐름 구성 요소의 사용자 지정 속성 컬렉션을 가져오지 못했습니다.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|실행 트리에 주기가 포함되어 있습니다.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|%1 개체 "%2"(%3!d!)이(가) 레이아웃에서 연결이 끊어졌습니다.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|레이아웃 개체에 대한 ID가 잘못되었습니다.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|필수 입력 개체가 경로 개체에 연결되지 않았습니다.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1에 잘못된 동기 입력 ID %2!d!이(가) 있습니다.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1에 계보 ID %2!d!이(가) 있지만 %3!d!이(가) 필요합니다.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|패키지에 중복된 이름의 두 개체, "%1" 및 "%2"이(가) 있습니다.|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|"%1" 및 "%2"은(는) 동일한 제외 그룹에 있지만 동기 입력이 다릅니다.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|동일 컬렉션의 두 개체, %2 및 %3에 중복된 계보 ID %1!d!이(가) 있습니다.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|레이아웃의 유효성을 검사하지 못했습니다.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|하나 이상의 구성 요소에 대한 유효성을 검사하지 못했습니다.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|레이아웃과 하나 이상의 구성 요소에 대한 유효성을 검사하지 못했습니다.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|하나 이상의 필수 스레드를 만들 수 없기 때문에 데이터 흐름 태스크 엔진이 시작되지 못했습니다.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|스레드가 초기화 시에 뮤텍스를 만들지 못했습니다.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|스레드가 초기화 시에 세마포를 만들지 못했습니다.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|시스템에서 %1!d!퍼센트의 메모리 로드를 보고합니다. 실제 메모리는 %2바이트이고 그 중에서 %3바이트를 사용할 수 있습니다. 가상 메모리는 %4바이트이고 그 중에서 %5바이트를 사용할 수 있습니다. 페이징 파일은 %6바이트이고 그 중에서 %7바이트를 사용할 수 있습니다.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|%1!d!바이트를 할당하는 동안 버퍼에 오류가 바이트입니다.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|버퍼 관리자를 만들 수 없습니다.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|버퍼 유형 %1!d!의 %2!I64d! 바이트입니다.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1이(가) 현수로 표시되었지만 경로가 연결되어 있습니다.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1의 유효성을 검사하지 못했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1이(가) 실행 후 단계에서 실패했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1이(가) 준비 단계에서 실패했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1이(가) 실행 전 단계에서 실패했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1이(가) 정리 단계에서 실패했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1에는 이전에 데이터 흐름 태스크에 사용되지 않았던 계보 ID %2!d!이(가) 있습니다.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|주기가 생성되기 때문에 %1을(를) %2에 연결할 수 없습니다.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|데이터 형식 "%1"을(를) 비교할 수 없습니다. 해당 데이터 형식의 비교가 지원되지 않으므로 정렬하거나 키로 사용할 수 없습니다.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|이 스레드는 종료되었으며 입력을 위한 버퍼를 허용하지 않습니다.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS 오류 코드 DTS_E_THREADFAILED.  스레드 "%1"이(가) 종료되었습니다(오류 코드 0x%2!8.8X!).  스레드가 종료된 이유에 대한 자세한 정보와 함께 이 오류 메시지보다 먼저 게시된 오류 메시지가 있을 수도 있습니다.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS 오류 코드 DTS_E_PROCESSINPUTFAILED.  입력 "%4"(%5!d!)을(를) 처리하는 동안 구성 요소 "%1"(%2!d!)에서 ProcessInput 메서드가 실패했습니다(오류 코드 0x%3!8.8X!). 식별된 구성 요소가 ProcessInput 메서드에서 오류를 반환했습니다. 이 오류는 해당 구성 요소와 관련되어 있지만 데이터 흐름 태스크의 실행을 중지할 수도 있는 오류입니다.  오류에 대한 자세한 정보와 함께 이 오류 메시지보다 먼저 게시된 오류 메시지가 있을 수도 있습니다.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|가상 버퍼 집합을 인식할 수 없습니다.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|이 파이프라인에 필요한 스레드 수는 시스템 한도인 %2!d!개보다 많은 %1!d!개입니다. 파이프라인에 필요한 스레드 수가 너무 많게 구성되었습니다. 비동기 출력이 너무 많거나 EngineThreads 속성이 너무 높게 설정되었습니다. 파이프라인을 여러 패키지로 분할하거나 EngineThreads 속성 값을 줄이십시오.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|데이터 흐름 엔진 스케줄러가 레이아웃의 원본 수를 가져올 수 없습니다.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|데이터 흐름 엔진 스케줄러가 레이아웃의 대상 수를 가져올 수 없습니다.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|구성 요소 뷰를 사용할 수 없습니다. 구성 요소 뷰가 생성되었는지 확인하십시오.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|구성 요소 뷰 ID가 잘못되었습니다. 구성 요소 뷰가 동기화되지 않았을 수 있습니다. 구성 요소 뷰를 해제하고 다시 만드십시오.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|이 버퍼는 잠기지 않았으므로 조작할 수 없습니다.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|데이터 흐름 태스크가 버퍼 정의 작성을 위해 메모리를 할당할 수 없습니다. 버퍼 정의에 %1!d!개의 열이 있습니다.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|데이터 흐름 태스크가 버퍼 유형을 등록할 수 없습니다. 이 유형은 %1!d!개의 열을 가지며 실행 트리 %2!d!용입니다.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|UsesDispositions 속성을 초기 값에서 변경할 수 없습니다. 이 오류는 XML을 편집하고 UsesDispositions 값을 수정할 때 발생합니다. 이 값은 패키지에 추가될 때 구성 요소에 의해 설정되며 변경할 수 없습니다.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|데이터 흐름 태스크가 필수 스레드를 초기화하지 못했으며 실행을 시작할 수 없습니다. 이 스레드에서 이전에 특정 오류가 보고되었습니다.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|데이터 흐름 태스크가 필수 스레드를 만들지 못했으며 실행을 시작할 수 없습니다. 이 오류는 일반적으로 메모리가 부족할 때 발생합니다.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|순환이 생성되기 때문에 "%2"의 동기 입력을 "%1"(으)로 설정할 수 없습니다.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|해당 이름의 스톡 속성이 있기 때문에 "%1"(이)라는 사용자 지정 속성이 잘못되었습니다. 사용자 지정 속성의 이름은 동일한 개체에 있는 스톡 속성의 이름과 같을 수 없습니다.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|버퍼의 잠금이 이미 해제되었습니다.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1을(를) 초기화하지 못했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1을(를) 종료하는 동안 오류가 발생했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다. 구성 요소가 해당 인터페이스를 해제하지 못했습니다.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS 오류 코드 DTS_E_PRIMEOUTPUTFAILED.  %1에서 PrimeOutput 메서드가 오류 코드 0x%2!8.8X!을(를) 반환했습니다.  파이프라인 엔진이 PrimeOutput()을 호출할 때 이 구성 요소가 오류 코드를 반환했습니다. 이 오류 코드의 의미는 구성 요소에 따라 다르지만 파이프라인의 실행을 중지할 수도 있는 오류입니다.  오류에 대한 자세한 정보와 함께 이 오류 메시지보다 먼저 게시된 오류 메시지가 있을 수도 있습니다.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS 오류 코드 DTS_E_THREADCANCELLED.  스레드 "%1"이(가) 종료 신호를 받았으며 종료 중입니다. 사용자가 종료를 요청했거나 다른 스레드의 오류로 인해 파이프라인을 종료합니다.  스레드가 취소된 이유에 대한 자세한 정보와 함께 이 오류 메시지보다 먼저 게시된 오류 메시지가 있을 수도 있습니다.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|오류 0x%8.8X(으)로 인해 스레드 "%1"의 배포자가 구성 요소 "%3"에서 속성 "%2"을(를) 초기화하지 못했습니다. 배포자가 구성 요소의 속성을 초기화할 수 없으며 계속 실행될 수 없습니다.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|데이터 흐름 태스크가 뷰 버퍼 유형을 등록할 수 없습니다. 이 유형은 %1!d!개의 열을 가지며 입력 ID %2!d!용입니다.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|메모리가 부족하여 실행 트리를 만들 수 없습니다.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|메모리가 부족하여 개체를 해시 테이블에 삽입할 수 없습니다.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|개체가 해시 테이블에 없습니다.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|다른 구성 요소 뷰가 이미 있기 때문에 구성 요소 뷰를 만들 수 없습니다. 한 번에 하나의 구성 요소 뷰만 존재할 수 있습니다.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|입력 "%1"(%2!d!)에서 가상 입력 열 컬렉션은 계보 ID가 %3!d!인 가상 입력 열을 포함하지 않습니다.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|요청된 개체에 잘못된 개체 유형이 있습니다.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|버퍼 관리자가 BufferTempStoragePath 속성의 임의 경로에서 임시 스토리지 파일을 만들 수 없습니다. 파일 이름이 잘못되었거나 권한이 없거나 경로가 꽉 찼습니다.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|버퍼 관리자가 파일 "%2"에서 오프셋 %1!d!을(를) 찾을 수 없습니다. 파일이 손상되었습니다.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|버퍼 관리자가 파일 "%1"의 길이를 %2!lu!바이트로 바이트입니다.  디스크 공간이 부족합니다.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|버퍼 관리자가 파일 "%2"에 %1!d!바이트를 쓸 수 없습니다. 디스크 공간이나 할당량이 부족합니다.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|버퍼 관리자가 파일 "%2"에서 %1!d!바이트를 읽을 수 도달했습니다. 파일이 손상되었습니다.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|버퍼 ID %1!d!은(는) 다른 가상 버퍼를 지원하며 순차 모드로 사용될 수 없습니다. 가상 버퍼를 지원하는 버퍼에서 IDTSBuffer100.SetSequentialMode가 호출되었습니다.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|버퍼가 읽기 전용 모드에 있기 때문에 이 작업을 수행할 수 없습니다. 읽기 전용 버퍼는 수정할 수 없습니다.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|순환이 생성되기 때문에 ID %1을(를) %2!d!(으)로 설정할 수 없습니다.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|버퍼 관리자가 버퍼 유형의 테이블을 확장하는 동안 메모리 부족 오류가 발생했습니다. 이 오류는 메모리 부족 상태로 인해 발생합니다.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|버퍼 관리자가 새 버퍼 유형을 만들지 못했습니다.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|데이터 흐름 엔진 스케줄러가 인덱스 %1!d!의 실행 트리를 레이아웃에서 검색하지 못했습니다. 이 스케줄러는 실제로 존재하는 것보다 많은 실행 트리가 포함된 개수를 받았습니다.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|데이터 흐름 태스크가 구성 요소 "%1"(%2!d!)에서 출력 "%3"(%4!d!)에 대한 PrimeOutput을 호출하기 위해 버퍼를 만들지 못했습니다. 이 오류는 일반적으로 메모리 부족 상태로 인해 발생합니다.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|메모리가 부족하기 때문에 데이터 흐름 엔진 스케줄러가 스레드 개체를 만들지 못했습니다. 이 오류는 메모리 부족 상태로 인해 발생합니다.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|데이터 흐름 엔진 스케줄러가 ID가 %1!d!인 개체를 레이아웃에서 검색하지 못했습니다. 데이터 흐름 엔진 스케줄러가 이전에 찾은 개체는 더 이상 사용할 수 없습니다.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|데이터 흐름 태스크가 출력 "%1"(%2!d!)에서 시작하는 실행 트리 노드를 위해 버퍼를 준비하지 못했습니다.|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|데이터 흐름 태스크가 실행을 준비하기 위해 가상 버퍼를 만들 수 없습니다.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|최대 ID 수에 도달했습니다. 개체에 할당할 수 있는 ID가 더 이상 없습니다.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|%1이(가) 이미 연결되어 있어 다시 연결할 수 없습니다.  분리한 후 다시 시도하십시오.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|출력 "%2"의 열 이름 "%1"은(는) 동기 입력 "%3"에 있는 동일한 이름의 열과 충돌하기 때문에 사용할 수 없습니다.|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|데이터 흐름 태스크가 행 집합의 끝을 표시하기 위해 버퍼를 만들 수 없습니다.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|관리되는 사용자 구성 요소에서 예외 "%1"이(가) 발생했습니다.|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|데이터 흐름 엔진 스케줄러가 실행 구조에 필요한 메모리를 할당할 수 없습니다. 시스템에 메모리가 부족하여 실행을 시작할 수 없습니다.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|메모리 부족 상태로 인해 버퍼 개체를 만들 수 없습니다.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|메모리 부족 상태로 인해 버퍼의 계보 ID를 DTP_HCOL 인덱스로 매핑할 수 없습니다.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|"%1!s!"이(가) Variables 컬렉션을 캐시할 수 없으며 오류 코드 0x%2!8.8X이(가) 반환되었습니다.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|"%1"이(가) 구성 요소 메타데이터 개체를 캐시하지 못했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1"에 0이 아닌 SortKeyPosition이 있지만 해당 값(%2!ld!)이 너무 큽니다. 이 값은 열 수보다 작거나 같아야 합니다.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|%1의 IsSorted 속성이 TRUE로 설정되었지만 0이 아닌 출력 열 SortKeyPositions의 절대값은 1에서 시작하는 단조 증가 형식이 아닙니다.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1"의 유효성을 검사하지 못했으며 유효성 검사 상태 "%2"이(가) 반환되었습니다.|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|구성 요소 " %1!s!"을(를) 만들 수 없으며 오류 코드 0x%2!8.8X! "%3!s!"이(가) 반환되었습니다 구성 요소가 제대로 등록되었는지 확인하십시오.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|"%1"을(를) 포함하는 모듈이 올바르게 등록 또는 설치되지 않았습니다.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|"%1"을(를) 포함하는 모듈이 등록되었지만 찾을 수 없습니다.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|스크립트를 선컴파일하도록 스크립트 구성 요소가 구성되어 있지만 이진 코드가 없습니다. 이진 코드를 생성하는 [스크립트 디자인] 단추를 클릭하여 스크립트 구성 요소 편집기에서 IDE를 실행하십시오.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|버퍼 관리자가 BLOBTempStoragePath 속성에 명명된 디렉터리에서 Long 개체를 스풀링하기 위해 파일을 만들 수 없습니다.  잘못된 파일 이름이 지정되었거나 권한이 없거나 경로가 꽉 찼습니다.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|"%1"의 SynchronousInputID 속성이 %2!d!이지만 %3!d!이(가) 필요합니다.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|ID가 %1!d!인 개체가 없습니다.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|오류 코드 0x%2!8.8X!(으)로 인해 ID가 %1!d!인 개체를 찾을 수 없습니다.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|출력 열 "%2"(%3!d!)에 지정된 코드 페이지 %1!d!이(가) 잘못되었습니다. 출력 열 "%2"에 대한 다른 코드 페이지를 선택하십시오.|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|EventInfos 컬렉션을 "%1"이(가) 캐시할 수 없으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|"%1"의 이름이 중복됩니다.  모든 이름은 고유해야 합니다.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|입력 열 "%1"(%2!d!)에 연결된 출력 열이 없습니다.|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1"에 루트 원본에서 확장하는 가상 버퍼가 있습니다. 동기 입력 0이 포함된 0이 아닌 제외 그룹이 존재합니다.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|오류 출력을 비독점 동기 출력에 포함할 수 없으므로 "%1"은(는) 오류 출력이 될 수 없습니다.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|0으로 나누기 오류가 발생했습니다. 식 "%1"에서 오른쪽 피연산자는 0으로 계산됩니다.|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|리터럴 "%1"이(가) 너무 커서 %2 유형에 적합하지 않습니다. 이 리터럴의 크기가 해당 유형을 오버플로합니다.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|데이터 형식 %2 및 %3에서 이항 연산 "%1"의 결과가 숫자 유형에 대한 최대 크기를 초과합니다. 피연산자 유형이 숫자(DT_NUMERIC) 결과로 암시적으로 캐스팅될 때는 전체 자릿수 또는 소수 자릿수가 항상 손실됩니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|이항 연산 "%1"의 결과가 결과 데이터 형식 "%2"에 대한 최대 크기를 초과합니다. 연산 결과의 크기가 결과의 유형을 오버플로합니다.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|함수 호출 "%1"의 결과가 너무 커서 "%2" 유형에 적합하지 않습니다. 함수 호출 결과의 크기가 피연산자의 유형을 오버플로합니다. 더 큰 유형으로 명시적으로 캐스팅해야 할 수 있습니다.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|이항 연산자 "%3"에서 "%1" 및 "%2" 데이터 형식이 호환되지 않습니다. 피연산자 유형을 이 연산에 호환되는 유형으로 암시적으로 캐스팅할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|데이터 형식 "%1"은(는) 이항 연산자 "%2"과(와) 함께 사용할 수 없습니다. 하나 또는 두 개의 피연산자의 유형이 연산에 지원되지 않습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|"%2" 연산의 비트 이항 연산자 "%1"에서 부호가 일치하지 않습니다. 이 연산자의 두 피연산자는 모두 양수이거나 음수여야 합니다.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|이항 연산 "%1"이(가) 실패했습니다(오류 코드 0x%2!8.8X!). 내부 오류가 발생했거나 메모리가 부족합니다.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|이항 연산 "%1"의 결과 유형을 설정하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|"%2"을(를) 문자열 "%1"과(와) 비교하지 못했습니다.|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|데이터 형식 "%1"을(를) 단항 연산자 "%2"과(와) 함께 사용할 수 없습니다. 이 피연산자 유형은 연산에 지원되지 않습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|단항 연산 "%1"이(가) 실패했습니다(오류 코드 0x%2!8.8X!). 내부 오류가 발생했거나 메모리가 부족합니다.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|단항 연산 "%1"의 결과 유형을 설정하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|함수 "%1"은(는) 매개 변수 번호 %3!d!에 대한 데이터 형식 "%2"을(를) 지원하지 않습니다. 매개 변수의 유형을 이 함수와 호환되는 유형으로 암시적으로 캐스팅할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|함수 "%1"이(가) 인식되지 않습니다. 함수 이름이 잘못되었거나 없습니다.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|길이 %1!d!이(가) 함수 "%2"에 적합하지 않습니다. 길이 매개 변수는 음수일 수 없습니다. 길이 매개 변수를 0이나 양수 값으로 변경하십시오.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|시작 인덱스 %1!d!이(가) 함수 "%2"에 적합하지 않습니다. 시작 인덱스 값은 0보다 큰 정수여야 합니다. 시작 인덱스는 0이 아닌 1부터 시작합니다.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|함수 "%1"이(가) 문자열 "%2"에서 문자 매핑을 수행할 수 없습니다.|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1"이(가) 함수 "%2"의 유효한 날짜 부분이 아닙니다.|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|데이터 형식이 "%2"인 함수 NULL의 매개 변수 번호 %1!d!이(가) 정수가 잘못되었습니다. NULL()의 매개 변수는 정적이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|데이터 형식이 "%2"인 함수 NULL의 매개 변수 번호 %1!d!이(가) 정수가 아닙니다. NULL()의 매개 변수는 정수이거나 정수로 변환할 수 있는 유형이어야 합니다.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|데이터 형식이 "%2"인 함수 NULL의 매개 변수 번호 %1!d!이(가) 정수가 아닙니다. 이 매개 변수는 정적이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|데이터 형식이 "%2"인 함수 NULL의 매개 변수 번호 %1!d!이(가) 정수가 잘못되었습니다. 캐스트 연산자의 매개 변수는 정적이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|데이터 형식이 "%2"인 함수 NULL의 매개 변수 번호 %1!d!이(가) 정수가 아닙니다. 캐스트 연산자의 매개 변수는 정수이거나 정수로 변환할 수 있는 유형이어야 합니다.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|식 "%1"을(를) 데이터 형식 "%2"에서 데이터 형식 "%3"(으)로 캐스팅할 수 없습니다. 요청된 캐스트가 지원되지 않습니다.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|식 "%1"을(를) 구문 분석하지 못했습니다.  줄 번호 "%3", 문자 번호 "%4"의 토큰 "%2"이(가) 인식되지 않았습니다. 이 식은 지정된 위치에 잘못된 요소를 포함하므로 구문 분석할 수 없습니다.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|식 "%1"을(를) 구문 분석하는 동안 오류가 발생했습니다. 알 수 없는 이유로 인해 이 식을 구문 분석하지 못했습니다.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|식 "%1"을(를) 구문 분석하지 못했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다. 이 식은 구문 분석할 수 없습니다. 이 식은 잘못된 요소를 포함하거나 형식이 잘못되었을 수 있습니다. 또한 메모리가 부족할 수도 있습니다.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|식 "%1"이(가) 잘못되었으며 구문 분석할 수 없습니다. 식에 잘못된 요소가 있거나 식의 형식이 잘못되었을 수 있습니다.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|컴퓨팅할 식이 없습니다. 빈 식의 문자열을 컴퓨팅하거나 가져오려고 했습니다.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|식 "%1"을(를) 컴퓨팅하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|식의 문자열 표현을 생성하지 못했습니다(오류 코드 0x%1!8.8X!). 식을 나타내는 표시 가능한 문자열을 생성하는 동안 오류가 발생했습니다.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|식 결과 데이터 형식 "%1"을(를) 열 데이터 형식 "%2"(으)로 변환할 수 없습니다. 식 결과를 입/출력 열에 기록해야 하지만 식의 데이터 형식을 열의 데이터 형식으로 변환할 수 없습니다.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|조건부 연산자의 조건 식 "%1"에 잘못된 데이터 형식 "%2"이(가) 있습니다. 조건부 연산자의 조건 식은 DT_BOOL 유형의 부울을 반환해야 합니다.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|데이터 형식 "%1" 및 "%2"은(는) 조건부 연산자와 호환되지 않습니다. 피연산자 유형을 이 조건부 연산에 호환되는 유형으로 암시적으로 캐스팅할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|조건부 연산 "%1"의 결과 유형을 설정하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|이 버퍼는 분리되었습니다. 처리 중인 버퍼를 그대로 둔 상태에서 버퍼 관리자가 종료되었으며 해당 버퍼에 대한 정리가 수행되지 않습니다. 메모리 손실이나 기타 문제가 존재할 수 있습니다.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|"%1"(이)라는 입력 열을 찾지 못했습니다(오류 코드 0x%2!8.8X!). 지정한 입력 열을 입력 열 컬렉션에서 찾을 수 없습니다.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|계보 ID가 %1!d!인 입력 열을 찾지 못했습니다(오류 코드 0x%2!8.8X!). 해당 입력 열을 입력 열 컬렉션에서 찾을 수 없습니다.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|인식할 수 없는 토큰 "%1"이(가) 식에 포함되어 있습니다. "%1"이(가) 변수인 경우 "\@%1"(으)로 표현해야 합니다. 지정한 토큰이 잘못되었습니다. 토큰을 변수 이름으로 사용하려면 \@ 기호가 접두사로 와야 합니다.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|인식할 수 없는 토큰 "#%1!d!"이(가) 식에 포함되어 있습니다.|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|변수 "%1"을(를) Variables 컬렉션에서 찾을 수 없습니다. 이 변수가 범위를 벗어났을 수 있습니다.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|식 "%1"을(를) 구문 분석하지 못했습니다. 이 식은 잘못된 토큰, 불완전한 토큰 또는 잘못된 요소가 있거나 형식이 잘못되었거나 괄호 같은 필수 요소의 일부가 없을 수 있습니다.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|"%1"의 이름이 비어 있습니다. 이름은 비워둘 수 없습니다.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|"%1"에서 HasSideEffects 속성이 TRUE로 설정되어 있으나 "%1"은(는) 동기화되었으며 다른 작업을 할 수 없습니다. HasSideEffects 속성을 FALSE로 설정하십시오.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|데이터 형식 "%2"(으)로 캐스팅하는 코드 페이지 매개 변수에 지정한 값 %1!d!이(가) 잘못되었습니다. 코드 페이지가 시스템에 설치되지 않았습니다.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 잘못되었습니다. 전체 자릿수가 %3!d!에서 %4!d! 사이의 범위 내에 있어야 하는데 전체 자릿수 값이 형식 캐스팅의 범위를 벗어났습니다.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 잘못되었습니다. 소수 자릿수가 %3!d!에서 %4!d! 사이의 범위 내에 있어야 하는데 소수 자릿수 값이 형식 캐스팅의 범위를 벗어났습니다. 소수 자릿수는 전체 자릿수를 초과할 수 없으며 양수여야 합니다.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|"%1"의 IsSorted 속성이 false이지만 해당 출력 열의 SortKeyPositions의 %2!lu!이(가) 0이 아닙니다.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|%2 유형에 대한 조건부 연산 "%1"의 피연산자에 대해 코드 페이지가 일치해야 합니다. 왼쪽 피연산자의 코드 페이지가 오른쪽 피연산자의 코드 페이지와 일치하지 않습니다. 지정한 유형에 대한 조건부 연산자의 경우 코드 페이지가 동일해야 합니다.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|입력 "%1"(%2!d!)이(가) 입력 "%3"(%4!d!)을(를) 참조하지만 두 입력의 열 수가 동일하지 않습니다. 입력 %5!d!에는 %6!d!개의 열이 있고 입력 %7!d!에는 %8!d!개의 열이 있습니다.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|계보 ID가 %1!d!인 개체가 없습니다.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|파일 이름에 대한 출력 열을 찾을 수 없습니다.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|파일 이름에 대한 출력 열이 Null로 끝나는 유니코드 문자열(DT_WSTR)이 아닙니다.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|오류 0x%2!8.8X!(으)로 인해 배포자가 버퍼를 스레드 "%1"에 제공하지 못했습니다. 대상 스레드가 종료 중인 것 같습니다.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|LocaleID %1!ld!이(가) 이 시스템에 설치되지 않았습니다.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|문자열 리터럴 "%1"에 잘못된 16진수 이스케이프 시퀀스 "\x%2"이(가) 있습니다. 이 이스케이프 시퀀스는 식 계산기의 문자열 리터럴에서 지원되지 않습니다. 16진수 이스케이프 시퀀스의 형식은 \xhhhh여야 하며, 여기서 h는 유효한 16진수 숫자입니다.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|문자열 리터럴 "%1"에 잘못된 이스케이프 시퀀스 "\\%2!c!"이(가) 있습니다. 이 이스케이프 시퀀스는 식 계산기의 문자열 리터럴에서 지원되지 않습니다. 문자열에 백슬래시가 필요한 경우 이중 백슬래시 "\\\\"를 사용하세요.|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1"에 출력 열이 없습니다. 비동기 출력은 출력 열을 포함해야 합니다.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|"%1"에 지원되지 않는 Long 개체 데이터 형식인 DT_TEXT, DT_NTEXT 또는 DT_IMAGE가 있습니다.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|출력 ID %1!d!에 여러 오류 출력 구성이 제공되었습니다. 첫 번째는 %2!d! 및 %3!d!이며 그 다음은 %4!d!입니다. %5!d!입니다.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|"%1"에 대한 데이터 형식 변환 확인 중에 OLE DB 공급자가 실패했습니다.|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|이 버퍼는 행 집합의 끝을 나타내며 행 수를 변경할 수 없습니다.  행 집합 플래그의 끝을 포함하는 버퍼에서 AddRow 또는 RemoveRow를 호출하려고 했습니다.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|데이터 형식 "%1"은(는) 식에서 지원되지 않습니다. 지정한 형식이 지원되지 않거나 잘못되었습니다.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|"%1"의 PrimeOutput 메서드가 성공을 반환했지만 행 집합의 끝을 보고하지 않았습니다. 구성 요소에 오류가 있습니다. 행 끝이 보고되었어야 합니다. 예기치 않은 결과를 방지하기 위해 파이프라인이 실행을 종료합니다.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|데이터 형식 "%1"에서 데이터 형식 "%2"(으)로 변환하는 동안 오버플로가 발생했습니다. 원본 유형이 너무 커서 대상 유형에 적합하지 않습니다.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|데이터 형식 "%1"에서 데이터 형식 "%2"(으)로의 변환이 지원되지 않습니다. 원본 유형을 대상 유형으로 변환할 수 없습니다.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|데이터 형식 %2에서 데이터 형식 %3(으)로 변환하려는 동안 오류 코드 0x%1!8.8X!이(가) 발생했습니다.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|조건부 연산 "%1"이(가) 실패했습니다(오류 코드 0x%2!8.8X!). 내부 오류나 메모리 부족 오류가 있습니다.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|데이터 형식 "%2"에서 데이터 형식 "%3"(으)로 식 "%1"을(를) 캐스팅하지 못했습니다(오류 코드 0x%4!8.8X!).|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|함수 "%1"을(를) 계산하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|데이터 형식이 "%2"인 함수 NULL의 매개 변수 번호 %1!d!이(가) 정수가 없습니다.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|빠른 로드 옵션이 설정되었고 최대 삽입 커밋 크기가 0으로 설정된 경우 행을 리디렉션하도록 "%1"에서 오류 행 처리를 설정할 수 없습니다.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|"%2" 유형에 대한 이항 연산자 "%1"의 피연산자에 대해 코드 페이지가 일치해야 합니다. 현재 왼쪽 피연산자의 코드 페이지가 오른쪽 피연산자의 코드 페이지와 일치하지 않습니다. 지정한 유형에 대한 지정한 이항 연산자의 경우 코드 페이지가 동일해야 합니다.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|변수 "%1"의 값을 검색하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|변수 "%1"의 데이터 형식이 식에서 지원되지 않습니다.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|캐스팅 중인 값의 코드 페이지(%4!d!)가 요청된 결과 코드 페이지(%5!d!)와 일치하지 않으므로 식 "%1"을(를) 데이터 형식 "%2"에서 데이터 형식 "%3"(으)로 캐스팅할 수 없습니다. 원본의 코드 페이지는 대상에 대해 요청된 코드 페이지와 일치해야 합니다.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|기본 버퍼 크기는 %1!d!에서 메타데이터가 바이트입니다. DefaultBufferSize 속성을 너무 작거나 너무 큰 값으로 설정하려고 했습니다.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|기본 버퍼 최대 행 수는 %1!d!개보다 많아야 캐시했습니다. DefaultBufferMaxRows 속성을 너무 작은 값으로 설정하려고 했습니다.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|%1의 코드 페이지가 %2!d!이지만 %3!d!이어야 합니다.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|데이터 흐름 태스크의 EngineThreads 속성에 %3!d!을(를) 할당하지 못했습니다. 값은 %1!d!에서 합니다.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|식 "%1"을(를) 구문 분석하지 못했습니다. 줄 번호 "%2", 문자 번호 "%3"에는 작은따옴표를 사용할 수 없습니다.|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|식 "%1"을(를) 구문 분석하지 못했습니다. 줄 번호 "%2", 문자 번호 "%3"에는 등호(=)를 사용할 수 없습니다. 지정한 위치에 이중 등호(==)가 필요할 수 있습니다.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|구성 요소 "%1"이(가) 런타임 개체 참조 추적 장치 컬렉션을 캐시하지 못했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|이름이 "%1"인 여러 입력 열이 있습니다. 원하는 입력 열을 [Component Name].[%2]\(으)로 고유하게 지정하거나 계보 ID로 참조해야 합니다. 현재 지정한 입력 열이 둘 이상의 구성 요소에 있습니다.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|"[%1].[%2]"이라는 입력 열을 찾지 못했습니다(오류 코드 0x%3!8.8X!). 해당 입력 열을 입력 열 컬렉션에서 찾을 수 없습니다.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|이름이 "%1"인 여러 변수가 있습니다. 원하는 변수를 \@[Namespace::%2]\(으)로 고유하게 지정해야 합니다. 해당 변수가 둘 이상의 네임스페이스에 있습니다.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|데이터 흐름 엔진 스케줄러가 파이프라인에 대한 실행 계획을 줄이지 못했습니다. OptimizedMode 속성을 false로 설정하십시오.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|SQRT 함수에는 음수 값을 사용할 수 없지만 음수 값이 SQRT 함수에 전달되었습니다.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|LN 함수에는 0 또는 음수 값을 사용할 수 없지만 0 또는 음수 값이 LN 함수에 전달되었습니다.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|LOG 함수에는 0 또는 음수 값을 사용할 수 없지만 0 또는 음수 값이 LOG 함수에 전달되었습니다.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|POWER 함수에 전달된 매개 변수를 계산할 수 없으며 생성 결과를 알 수 없습니다.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|오류 0x%1!8.8X!(으)로 인해 런타임에서 취소 이벤트를 제공할 수 없습니다.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|파이프라인에서 취소 요청을 받았으며 종료하고 있습니다.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|단항 마이너스(부정) 연산 "%1"의 결과가 결과 데이터 형식 "%2"의 최대 크기를 초과합니다. 연산 결과의 크기가 결과의 유형을 오버플로합니다.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|자리 표시자 "%1"이(가) 식에서 발견되었습니다. 이 자리 표시자를 실제 매개 변수나 피연산자로 바꾸어야 합니다.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|길이 %1!d!이(가) 함수 "%2"에 적합하지 잘못되었습니다. 길이 매개 변수는 음수일 수 없습니다.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|반복 횟수 %1!d!이(가) 음수이므로 함수 "%2"에 적합하지 않습니다. 반복 횟수 매개 변수는 양수여야 합니다.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|변수 "%1"을(를) 읽지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|이항 연산의 피연산자의 경우 입력 열과 캐스트 연산에 대해서만 데이터 형식 DT_STR이 지원됩니다. 식 "%1"은(는) 입력 열 또는 캐스트 결과가 아닌 DT_STR 피연산자가 있으므로 이항 연산에 사용할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|조건부 연산자의 피연산자의 경우 입력 열과 캐스트 연산에 대해서만 데이터 형식 DT_STR이 지원됩니다. 식 "%1"은(는) 입력 열 또는 캐스트 결과가 아닌 DT_STR 피연산자가 있으므로 조건부 연산에 사용할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|발생 횟수 %1!d!이(가) 함수 "%2"에 적합하지 않습니다. 이 매개 변수는 0보다 커야 합니다.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1"이(가) LogEntryInfos 컬렉션을 캐시하지 못했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|함수 "%1"에 지정한 날짜 부분 매개 변수가 잘못되었습니다. 이 매개 변수는 정적 문자열이어야 합니다.  날짜 부분 매개 변수는 입력 열 같은 동적 요소를 포함할 수 없으며 DT_WSTR 유형이어야 합니다.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 잘못되었습니다. 길이는 양수여야 합니다.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 잘못되었습니다. 코드 페이지가 컴퓨터에 설치되지 않았습니다.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 벗어났습니다. 전체 자릿수가 %3!d!에서 %4!d! 사이의 범위 내에 있어야 합니다.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 벗어났습니다. 소수 자릿수는 %3!d!에서 %4!d! 사이의 범위 내에 있어야 합니다. 소수 자릿수는 전체 자릿수를 초과할 수 없으며 음수가 아니어야 합니다.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 잘못되었습니다. 길이는 양수여야 합니다.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|%1에 음수 값을 할당할 수 없습니다.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|"%2"에 대한 "%1" 사용자 지정 속성을 true로 설정할 수 없습니다.  열 데이터 형식은  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2 또는 DT_FILETIME 중 하나여야 합니다.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|"%1"을(를) 다시 연결할 수 없습니다. 경로를 삭제하고 새로 추가한 다음 연결하십시오.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|함수 "%1"에는 %3!d!개의 매개 변수가 아니라 %2!d!개의 매개 변수가 필요합니다. 함수 이름이 인식되었지만 매개 변수 수가 잘못되었습니다.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|함수 "%1"에는 %3!d!개의 매개 변수가 아니라 %2!d!개의 매개 변수가 필요합니다. 함수 이름이 인식되었지만 매개 변수 수가 잘못되었습니다.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|함수 "%1"에는 %3!d!개의 매개 변수가 아니라 %2!d!개의 매개 변수가 필요합니다. 함수 이름이 인식되었지만 매개 변수 수가 잘못되었습니다.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|메모리가 부족하여 식 "%1"을(를) 구문 분석하지 못했습니다.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1에서 필요한 제품 수준 검사를 수행하지 못했으며 오류 코드 0x%2!8.8X!이(가) 반환되었습니다.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS 오류 코드 DTS_E_PRODUCTLEVELTOLOW.  설치된 Integration Services %2에서 %1을(를) 실행할 수 없습니다. %3 이상이 필요합니다.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|식에 있는 문자열 리터럴이 최대 허용 길이인 %1!d!자를 초과합니다. 구성됩니다.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|변수 %1에 있는 문자열이 최대 허용 길이인 %2!d!자를 초과합니다. 구성됩니다.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|필요한 Integration Services 인터페이스(IDTSRuntimeComponent100)를 지원하지 않는 %1이(가) 발견되었습니다.  구성 요소 공급자로부터 이 구성 요소의 업데이트된 버전을 얻으십시오.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|레지스트리 키 "%1"을(를) 열 수 없습니다.|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|CLSID가 "%1"인 구성 요소의 파일 이름을 가져올 수 없습니다. 구성 요소가 올바르게 등록되었는지 또는 제공된 CLSID가 올바른지 확인하십시오.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|구성 요소 중 하나에 대한 CLSID가 잘못되었습니다. 파이프라인의 모든 구성 요소에 유효한 CLSID가 있는지 확인하십시오.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|ID가 %1!d!인 구성 요소 중 하나에 대한 CLSID가 잘못되었습니다.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|인덱스가 잘못되었습니다.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|애플리케이션 개체를 액세스할 수 없습니다. SSIS가 올바르게 설치되었는지 확인하십시오.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|구성 요소에 대한 파일 이름을 검색하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|ID가 %2!d!인 구성 요소에서 속성 "%1"을(를) 검색할 수 없습니다.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|데이터 흐름 태스크에서 ID %1!d!을(를) 두 번 이상 사용하려고 합니다.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|열이 없는 컬렉션에서 계보 ID로 항목을 검색할 수 없습니다.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|오류 코드 0x%2!8.8X!(으)로 인해 연결 관리자 컬렉션에서 ID가 "%1"인 연결 관리자를 찾을 수 없습니다. "%4"의 연결 관리자 컬렉션에서 "%3"에 이 연결 관리자가 필요합니다. 연결 관리자 컬렉션 Connections에서 해당 ID를 사용하여 연결 관리자가 생성되었는지 확인하십시오.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|스레드 "%1"이(가) 입력 %2!d!에 대한 버퍼를 받았지만 이 스레드는 해당 입력을 처리하지 않습니다. 오류가 발생하여 데이터 흐름 엔진 스케줄러가 잘못된 실행 계획을 작성했습니다.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|구성 요소 "%1"(%2!d!)이(가) IDTSRuntimeComponent100 인터페이스를 제공할 수 없습니다.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|데이터 흐름 태스크 엔진이 다른 스레드를 할당하기 위해 버퍼를 복사하려고 했지만 실패했습니다.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|데이터 흐름 태스크 엔진이 버퍼 %3!d에 대해 %2!d! 유형 대신에 %1!d! 유형의 뷰 버퍼를 만들지 못했습니다.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|버퍼 관리자가 경로 "%1"에서 임시 파일을 만들 수 없습니다. 이 경로는 임시 스토리지용으로 다시 사용되지 않습니다.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|버퍼 관리자가 오류 출력으로 등록되지 않은 출력에 오류 행을 밀어넣으려고 했습니다. IsErrorOut 속성이 TRUE로 설정되지 않은 출력에서 DirectErrorRow가 호출되었습니다.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|전용 버퍼에서 버퍼 메서드가 호출되었지만 전용 버퍼는 이 작업을 지원하지 않습니다.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|전용 모드 버퍼는 이 작업을 지원하지 않습니다.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|PrimeOutput에 전달된 버퍼에서 이 작업을 호출할 수 없습니다. PrimeOutput 중에 버퍼 메서드가 호출되었지만 PrimeOutput 중에는 이 호출이 허용되지 않습니다.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|ProcessInput에 전달된 버퍼에서 이 작업을 호출할 수 없습니다. ProcessInput 중에 버퍼 메서드가 호출되었지만 ProcessInput 중에는 이 호출이 허용되지 않습니다.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|버퍼 관리자가 임시 파일 이름을 가져올 수 없습니다.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|코드에서 너무 넓은 열이 발견되었습니다.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|오류 코드 0x%3!8.8X!(으)로 인해 "%2"의 연결 관리자 컬렉션 Connections에서 "%1"(으)로 지정한 런타임 연결 관리자의 ID를 가져올 수 없습니다. 런타임 연결 개체의 ConnectionManager.ID 속성이 해당 구성 요소에 대해 설정되었는지 확인하십시오.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|"%2"의 연결 관리자 컬렉션 Connections에 있는 "%1"에 ID 속성에 대한 값이 없습니다. 런타임 연결 개체의 ConnectionManagerID 속성이 해당 구성 요소에 대해 설정되었는지 확인하십시오.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|실행 중에 메타데이터를 변경할 수 없습니다.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|"%1"의 구성 요소 메타데이터를 최신 버전의 구성 요소로 업그레이드할 수 없습니다. PerformUpgrade 메서드가 실패했습니다.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|%1의 버전이 이 버전의 DataFlow와 호환되지 않습니다.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|구성 요소가 없거나 등록되지 않았거나 업그레이드할 수 없거나 필수 인터페이스가 없습니다. 이 구성 요소에 대한 연락처 정보는 "%1"입니다.|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|잘못된 버퍼에서 메서드가 호출되었습니다. 구성 요소 출력에 사용되지 않는 버퍼는 이 작업을 지원하지 않습니다.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|식을 계산하는 동안 오류가 발생했습니다.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|식에 0으로 나누기 오류가 있습니다.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|리터럴 값의 크기가 너무 커서 요청된 유형에 적합하지 않습니다.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|이항 연산의 결과가 너무 커서 숫자 유형의 최대 크기에 적합하지 않습니다. 피연산자 유형이 숫자(DT_NUMERIC) 결과로 암시적으로 캐스팅될 때는 전체 자릿수 또는 소수 자릿수가 항상 손실됩니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|이항 연산 결과의 크기가 결과 데이터 형식의 최대 크기를 오버플로합니다.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|함수 호출 결과의 크기가 너무 커서 결과 유형에 적합하지 않으며 피연산자의 유형을 오버플로했습니다. 더 큰 유형으로 명시적으로 캐스팅해야 할 수 있습니다.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|호환되지 않는 데이터 형식이 이항 연산자에 사용되었습니다. 피연산자 유형을 이 연산에 호환되는 유형으로 암시적으로 캐스팅할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|지원되지 않는 데이터 형식이 이항 연산자에서 사용되었습니다. 하나 또는 두 개의 피연산자의 유형이 연산에 지원되지 않습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|비트 이항 연산자에서 부호가 일치하지 않습니다. 이 연산자의 두 피연산자는 모두 양수이거나 음수여야 합니다.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|이항 연산이 실패했습니다. 메모리가 부족하거나 내부 오류가 발생했습니다.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|이항 연산의 결과 유형을 설정하지 못했습니다.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|두 문자열을 비교할 수 없습니다.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|지원되지 않는 데이터 형식이 단항 연산자에서 사용되었습니다. 이 피연산자 유형은 연산에 지원되지 않습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|단항 연산이 실패했습니다. 메모리가 부족하거나 내부 오류가 있습니다.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|단항 연산의 결과 유형을 설정하지 못했습니다.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|함수에 데이터 형식이 지원되지 않는 매개 변수가 있습니다. 매개 변수의 유형을 이 함수에 호환되는 유형으로 암시적으로 캐스팅할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|잘못된 함수 이름이 식에 표시되었습니다. 함수 이름이 있는지, 그리고 올바른지 확인하십시오.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|길이 매개 변수가 함수 SUBSTRING에 적합하지 않습니다. 길이 매개 변수는 음수일 수 없습니다.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|시작 인덱스가 함수 SUBSTRING에 적합하지 않습니다. 시작 인덱스 값은 0보다 큰 정수여야 합니다. 즉, 시작 인덱스는 0이 아닌 1부터 시작합니다.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|잘못된 수의 매개 변수가 함수에 제공되었습니다. 함수 이름이 인식되었지만 매개 변수 수가 잘못되었습니다.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|문자 매핑 함수가 실패했습니다.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|인식할 수 없는 날짜 부분 매개 변수가 날짜 함수에 지정되었습니다.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|잘못된 매개 변수가 함수 NULL에 제공되었습니다. NULL의 매개 변수는 정적이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|잘못된 매개 변수가 함수 NULL에 제공되었습니다. NULL의 매개 변수는 정수이거나 정수로 변환할 수 있는 유형이어야 합니다.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|잘못된 매개 변수가 함수에 제공되었습니다. 이 매개 변수는 정적이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|잘못된 매개 변수가 캐스트 연산에 제공되었습니다. 캐스트 연산자의 매개 변수는 정적이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|잘못된 매개 변수가 캐스트 연산에 제공되었습니다. 캐스트 연산자의 매개 변수는 정수이거나 정수로 변환할 수 있는 유형이어야 합니다.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|지원되지 않는 유형 캐스트가 식에 있습니다.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|인식되지 않는 토큰이 식에 있습니다. 잘못된 요소가 있기 때문에 식을 구문 분석할 수 없습니다.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|식이 잘못되었으며 구문 분석할 수 없습니다. 식에 잘못된 요소가 있거나 식의 형식이 잘못되었을 수 있습니다.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|단항 마이너스(부정) 연산의 결과가 결과 데이터 형식의 최대 크기를 오버플로합니다. 연산 결과의 크기가 결과의 유형을 오버플로합니다.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|식을 컴퓨팅하지 못했습니다.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|식의 문자열 표현을 생성하지 못했습니다.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|식 결과 데이터 형식을 열 데이터 형식으로 변환할 수 없습니다. 식 결과를 입/출력 열에 기록해야 하지만 식의 데이터 형식을 열의 데이터 형식으로 변환할 수 없습니다.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|조건부 연산자의 조건 식에 잘못된 데이터 형식이 있습니다. 조건 식은 DT_BOOL 유형이어야 합니다.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|조건부 연산자에서 피연산자의 데이터 형식이 서로 호환되지 않습니다. 피연산자 유형을 이 조건부 연산에 호환되는 유형으로 암시적으로 캐스팅할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 하나 또는 두 개의 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|조건부 연산의 결과 유형을 설정하지 못했습니다.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|지정한 입력 열을 입력 열 컬렉션에서 찾을 수 없습니다.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|계보 ID로 입력 열을 찾지 못했습니다. 해당 입력 열을 입력 열 컬렉션에서 찾을 수 없습니다.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|입력 열 참조로 표시되는 인식할 수 없는 토큰이 식에 있지만 입력 열을 처리하는 데 사용할 수 있는 입력 열 컬렉션이 없습니다. 입력 열 컬렉션이 식 계산기에 제공되지 않았지만 입력 열이 식에 포함되어 있습니다.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|지정한 변수를 컬렉션에서 찾을 수 없습니다. 이 변수가 범위를 벗어났을 수 있습니다. 변수가 있는지, 그리고 범위가 올바른지 확인하십시오.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|식을 구문 분석하지 못했습니다. 식에 잘못되었거나 호환되지 않는 토큰이 있습니다. 이 식에 잘못된 요소가 있거나 닫는 괄호 같은 필수 요소의 일부가 없거나 형식이 잘못되었을 수 있습니다.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|데이터 형식 DT_STR 또는 DT_TEXT로 캐스팅되는 코드 페이지 매개 변수에 지정한 값이 잘못되었습니다. 지정한 코드 페이지가 컴퓨터에 설치되지 않았습니다.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|캐스트 연산의 전체 자릿수 매개 변수에 지정한 값이 유형 캐스트에 대한 범위를 벗어났습니다.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|캐스트 연산의 소수 자릿수 매개 변수에 지정한 값이 유형 캐스트에 대한 범위를 벗어났습니다. 소수 자릿수는 전체 자릿수를 초과할 수 없으며 음수가 아니어야 합니다.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|조건부 연산에서 코드 페이지가 일치하지 않습니다. 왼쪽 피연산자의 코드 페이지가 오른쪽 피연산자의 코드 페이지와 일치하지 않습니다. 해당 유형에 대한 조건부 연산자의 경우 코드 페이지가 동일해야 합니다.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|문자열 리터럴에 잘못된 16진수 이스케이프 시퀀스가 있습니다. 이 이스케이프 시퀀스는 식 계산기의 문자열 리터럴에서 지원되지 않습니다. 16진수 이스케이프 시퀀스의 형식은 \xhhhh여야 하며, 여기서 h는 유효한 16진수 숫자입니다.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|문자열 리터럴에 잘못된 이스케이프 시퀀스가 있습니다. 이 이스케이프 시퀀스는 식 계산기의 문자열 리터럴에서 지원되지 않습니다. 이 이스케이프 시퀀스는 식 계산기의 문자열 리터럴에서 지원되지 않습니다. 문자열에 백슬래시가 필요한 경우 이중 백슬래시 "\\\\"서식을 적용하세요.|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|지원되지 않거나 인식되지 않는 데이터 형식이 식에 사용되었습니다.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|데이터 형식 간에 변환하는 동안 오버플로가 발생했습니다. 원본 유형이 너무 커서 대상 유형에 맞지 않습니다.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|지원되지 않는 데이터 형식 변환이 식에 포함되어 있습니다. 원본 유형을 대상 유형으로 변환할 수 없습니다.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|데이터 변환을 수행하는 동안 오류가 발생했습니다. 원본 유형을 대상 유형으로 변환할 수 없습니다.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|조건부 연산이 실패했습니다.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|유형 캐스트를 수행하는 동안 오류가 발생했습니다.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|"%1"을(를) DT_STR 유형에서 DT_WSTR 유형으로 변환하지 못했습니다(오류 코드 0x%2!8.8X!). 입력 열에서 암시적 변환을 수행하는 동안 오류가 발생했습니다.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|입력 열을 DT_STR 유형에서 DT_WSTR 유형으로 변환하지 못했습니다. 입력 열에서 암시적 변환을 수행하는 동안 오류가 발생했습니다.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|함수를 계산하는 동안 오류가 발생했습니다.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|함수 매개 변수를 정적 값으로 변환할 수 없습니다. 이 매개 변수는 정적이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|길이 매개 변수가 함수 RIGHT에 적합하지 않습니다. 길이 매개 변수는 음수일 수 없습니다.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|반복 횟수 매개 변수가 함수 REPLICATE에 적합하지 않습니다. 이 매개 변수는 음수일 수 없습니다.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|이항 연산에서 코드 페이지가 일치하지 않습니다. 왼쪽 피연산자의 코드 페이지가 오른쪽 피연산자의 코드 페이지와 일치하지 않습니다. 이항 연산의 경우 코드 페이지가 동일해야 합니다.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|변수에 대한 값을 검색하지 못했습니다.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|데이터 형식이 지원되지 않는 변수가 식에 있습니다.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|캐스팅 중인 값의 코드 페이지가 요청된 결과 코드 페이지와 일치하지 않으므로 식을 캐스팅할 수 없습니다. 원본의 코드 페이지는 대상에 대해 요청된 코드 페이지와 일치해야 합니다.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|예기치 않은 작은따옴표가 식에 있습니다. 큰따옴표가 필요할 수 있습니다.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|예기치 않은 등호(=)가 식에 있습니다. 이 오류는 일반적으로 이중 등호(==)가 필요할 때 발생합니다.|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|모호한 입력 열 이름이 지정되었습니다.  열은 [Component Name].[Column Name]으로 한정하거나 계보 ID로 참조해야 합니다. 이 오류는 입력 열이 둘 이상의 구성 요소에 있을 때 발생합니다. 이 경우에는 구성 요소 이름을 추가하거나 계보 ID를 사용하여 이러한 구성 요소를 구별해야 합니다.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|식에 자리 표시자 함수 매개 변수 또는 피연산자가 있습니다. 실제 매개 변수나 피연산자로 바꿔야 합니다.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|모호한 변수 이름이 지정되었습니다. 원하는 변수를 \@[Namespace::Variable]로 한정해야 합니다. 이 오류는 변수가 둘 이상의 네임스페이스에 있을 때 발생합니다.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|이항 연산의 피연산자의 경우 데이터 형식 DT_STR은 입력 열 및 캐스트 연산에만 지원됩니다. 입력 열 또는 유형 캐스트의 결과가 아닌 DT_STR 피연산자는 이항 연산에서 사용할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|조건부 연산자의 피연산자의 경우 데이터 형식 DT_STR은 입력 열 및 캐스트 연산에만 지원됩니다. 입력 열 또는 캐스트의 결과가 아닌 DT_STR 피연산자는 조건부 연산에서 사용할 수 없습니다. 이 연산을 수행하려면 캐스트 연산자를 사용하여 피연산자를 명시적으로 캐스팅해야 합니다.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|발생 횟수 매개 변수가 함수 FINDSTRING에 적합하지 않습니다. 이 매개 변수는 0보다 커야 합니다.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|날짜 함수에 지정한 "날짜 부분" 매개 변수가 잘못되었습니다. "날짜 부분" 매개 변수는 정적 문자열이어야 하며 입력 열과 같은 동적 요소를 포함할 수 없습니다. DT_WSTR 유형이어야 합니다.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|캐스트 연산의 길이 매개 변수에 지정한 값이 잘못되었습니다. 길이는 양수여야 합니다. 유형 캐스트에 지정한 길이가 음수입니다. 양수 값으로 변경하십시오.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|NULL 함수의 길이 매개 변수에 지정한 값이 잘못되었습니다. 길이는 양수여야 합니다. NULL 함수에 지정한 길이가 음수입니다. 양수 값으로 변경하십시오.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|데이터 형식이 DT_STR 또는 DT_TEXT인 NULL 함수의 코드 페이지 매개 변수에 지정한 값이 잘못되었습니다. 지정한 코드 페이지가 컴퓨터에 설치되지 않았습니다. 지정한 코드 페이지를 변경하거나 코드 페이지를 컴퓨터에 설치하십시오.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|NULL 함수의 전체 자릿수 매개 변수에 지정한 값이 잘못되었습니다. 지정한 전체 자릿수가 NULL 함수의 범위를 벗어났습니다.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|NULL 함수의 소수 자릿수 매개 변수에 지정한 값이 잘못되었습니다. 지정한 소수 자릿수가 NULL 함수의 범위를 벗어났습니다. 소수 자릿수는 전체 자릿수를 초과할 수 없으며 양수여야 합니다.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|%1이(가) %3의 %2에 데이터를 쓰지 못했습니다. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|조회 변환이 사용자로부터 취소 요청을 받았습니다.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|4GB 한도에 도달하여 문자 또는 BLOB(Binary Large Object) 데이터 처리가 중지되었습니다.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|관리되는 파이프라인 구성 요소 "%1"을(를) 로드할 수 없습니다.  예외: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS 오류 코드 DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: OLE DB 공급자를 사용할 수 없으므로 64비트 버전의 SSIS에서 Excel 연결 관리자를 지원하지 않습니다.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|캐시 파일이 손상되었거나 캐시 연결 관리자를 사용하여 파일을 만들지 않았습니다.  올바른 캐시 파일을 지정하십시오.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|SQL 명령이 올바르게 설정되지 않았습니다. SQLCommand 속성을 확인하십시오.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|COM 오류 개체 정보를 사용할 수 있습니다.  원본: "%1" 오류 코드: 0x%2!8.8X!  설명: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|설정한 연결에 액세스할 수 없습니다.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|열 수가 잘못되었습니다.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|열 "%1"을(를) 데이터 원본에서 찾을 수 없습니다.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|"OLE DB 레코드를 사용할 수 있습니다.  원본: "%1" Hresult: 0x%2!8.8X!  설명: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS 오류 코드 DTS_E_OLEDBERROR.  OLE DB 오류가 발생했습니다. 오류 코드: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|구성 요소가 이미 연결되었습니다. 연결을 시도하기 전에 구성 요소의 연결을 끊어야 합니다.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|속성 "%1"의 값이 잘못되었습니다.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|데이터 파일 "%1"을(를) 열 수 없습니다.|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|대상 플랫 파일 이름을 지정하지 않았습니다. 플랫 파일 연결 관리자가 연결 문자열로 구성되었는지 확인하십시오. 플랫 파일 연결 관리자가 여러 구성 요소에 사용될 경우 연결 문자열에 충분한 파일 이름이 있는지 확인하십시오.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|열 "%1"에 대한 텍스트 한정자를 찾을 수 없습니다.|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|"%1"에서 "%2"(으)로의 변환이 지원되지 않습니다.|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|%2에서 %3(으)로의 유형 변환에 대한 유효성을 검사하는 동안 오류 코드 0x%1!8.8X!이(가) 반환되었습니다.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|"%2"에 필요한 계보 ID가 "%1!d!"인 입력 열을 찾을 수 없습니다. 출력 열의 SourceInputColumnLineageID 사용자 지정 속성을 확인하십시오.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|출력 수가 잘못되었습니다. 적어도 %1!d!개 이상의 출력이 있어야 합니다.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|출력 수가 잘못되었습니다. 정확하게 %1!d!개의 출력이 있어야 합니다.|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|문자열이 너무 길어서 변환할 수 없습니다.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|입력 수가 잘못되었습니다. 정확하게 %1!d!개의 출력이 있어야 합니다.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|%1의 입력 열 수는 0일 수 없습니다.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|이 구성 요소에 %1!d!개의 입력이 합니다.  이 구성 요소에서는 입력이 허용되지 않습니다.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|ProcessInput이 잘못된 입력 ID %1!d!(으)로 호출되었습니다.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|사용자 지정 속성 "%1"은(는) %2 유형이어야 합니다.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|버퍼 유형이 잘못되었습니다. 파이프라인 레이아웃 및 모든 구성 요소가 유효성 검사를 통과했는지 확인하십시오.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|사용자 지정 속성 "%1"의 값이 잘못되었습니다.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|연결이 없기 때문에 오류가 발생했습니다. 메타데이터를 요청할 때는 연결이 필요합니다. 오프라인으로 작업하는 경우 SSIS 메뉴에서 [오프라인으로 작업]의 선택을 취소하여 연결을 활성화하십시오.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|사용자 지정 속성 "%1"을(를) 만들 수 없습니다.|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|초기화를 위해 사용자 지정 속성 컬렉션을 검색할 수 없습니다.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|OLE DB 접근자를 만들 수 없습니다. 열 메타데이터가 올바른지 확인하십시오.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|PrimeOutput이 잘못된 출력 ID %1!d!(으)로 호출되었습니다.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|"%2"에서 "%1" 속성 값이 잘못되었습니다.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|데이터를 읽으려면 연결해야 합니다.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|머리글 행을 읽는 동안 오류가 발생했습니다.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|열 이름 "%1"이(가) 중복됩니다.|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|ID가 %1!d!인 열의 이름을 가져올 수 없습니다.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|행을 출력 "%1"(%2!d!)에 전달하지 못했습니다.|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|오류 "%1"(으)로 인해 대량 삽입 스레드를 만들 수 없습니다.|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|SSIS 대량 삽입 태스크에 대한 스레드를 초기화하지 못했습니다.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|SSIS 대량 삽입 태스크에 대한 스레드가 이미 실행 중입니다.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|오류나 경고로 인해 SSIS 대량 삽입 태스크에 대한 스레드가 종료되었습니다.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|"%1"에 대한 빠른 로드 행 집합을 열지 못했습니다. 해당 개체가 데이터베이스에 있는지 확인하십시오.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|연결이 없기 때문에 오류가 발생했습니다. 메타데이터 유효성 검사를 진행하려면 연결이 필요합니다.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|대상 테이블 이름을 지정하지 않았습니다.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|OLE DB 어댑터에 사용되는 OLE DB 공급자가 IConvertType을 지원하지 않습니다. 어댑터의 ValidateColumnMetaData 속성을 FALSE로 설정하십시오.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|OLE DB 어댑터에서 사용하는 OLE DB 공급자가 "%3"에 대해 "%1"과(와) "%2" 유형 간에 변환할 수 없습니다.|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|열 메타데이터의 유효성을 검사하지 못했습니다.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1"은(는) 행 ID 열이며 데이터 삽입 작업에 포함될 수 없습니다.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|행 버전 열 "%1"에 삽입하려고 했습니다. 행 버전 열에 삽입할 수 없습니다.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|읽기 전용 열 "%1"에 삽입하지 못했습니다.|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|데이터 원본에서 열 정보를 검색할 수 없습니다. 데이터베이스에서 대상 테이블을 사용할 수 있는지 확인하십시오.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|버퍼를 잠글 수 없습니다. 시스템에 메모리가 부족하거나 버퍼 관리자가 할당량에 도달했습니다.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|값이 %2!d!인 추가 플래그를 포함하는 ComparisonFlags 속성이 %1에 있습니다.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|열 메타데이터를 유효성 검사에 사용할 수 없습니다.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|데이터 파일에 쓸 수 없습니다.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|열 "%1"에 대한 열 구분 기호를 찾을 수 없습니다.|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|데이터 파일에서 열 "%1"을(를) 구문 분석하지 못했습니다.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|파일 이름이 잘못 지정되었습니다.  원시 파일의 경로와 이름을 FileName 속성에 직접 지정하거나 FileNameVariable 속성에 변수를 지정하여 제공하십시오.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|파일 "%1"을(를) 쓰기용으로 열 수 없습니다. 파일 권한이 없거나 디스크가 꽉 찬 경우 오류가 발생할 수 있습니다.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|출력 파일에 대한 I/O 버퍼를 만들 수 없습니다. 파일 권한이 없거나 디스크가 꽉 찬 경우 오류가 발생할 수 있습니다.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|파일 "%2"에 %1!d!바이트를 쓸 수 없습니다. 자세한 내용은 이전 오류 메시지를 참조하십시오.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|파일 헤더에 잘못된 메타데이터가 있습니다. 파일이 손상되었거나 SSIS가 생성한 원시 데이터 파일이 아닙니다.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|출력 파일이 이미 있으며 WriteOption이 '한 번 만들기'로 설정되어 있으므로 오류가 발생했습니다. WriteOption 속성을 '항상 만들기'로 설정하거나 파일을 삭제하십시오.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|속성 설정이 충돌하여 오류가 발생했습니다. AllowAppend 속성과 ForceTruncate 속성이 모두 TRUE로 설정되어 있습니다. 두 속성을 모두 TRUE로 설정할 수 없습니다. 두 속성 중 하나를 FALSE로 설정하십시오.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|파일에 잘못된 버전 및 플래그 정보가 있습니다. 파일이 손상되었거나 SSIS가 생성한 원시 데이터 파일이 아닙니다.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|출력 파일이 호환되지 않는 버전에 의해 작성되었으므로 추가할 수 없습니다. 파일이 더 이상 사용할 수 없는 오래된 파일 형식일 수 있습니다.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|기존 파일의 열이 입력의 "%1" 열과 일치하지 않으므로 출력 파일을 추가할 수 없습니다. 이전 파일이 메타데이터에서 일치하지 않습니다.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|출력 파일의 열 수가 이 대상의 열 수와 일치하지 않으므로 출력 파일을 추가할 수 없습니다. 이전 파일이 메타데이터에서 일치하지 않습니다.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|열 코드 페이지 정보를 검색하는 동안 오류가 발생했습니다.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|파일 "%2"에서 %1!d!바이트를 읽을 수 도달했습니다. 오류의 원인은 이전에 보고되었습니다.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|파일 "%2"에서 %1!d!바이트를 읽는 동안 예기치 않은 파일의 끝에 도달했습니다. 잘못된 파일 형식으로 인해 파일이 중간에 끝났습니다.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|열 %1을(를) 사용할 수 없습니다. 원시 어댑터는 image, text 또는 ntext 데이터를 지원하지 않습니다.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|어댑터에서 인식할 수 없는 데이터 형식 %1!d!을(를) 발견했습니다. 이 오류는 손상된 입력 파일(원본) 또는 잘못된 버퍼 유형(대상)으로 인해 발생할 수 있습니다.|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|문자열이 너무 깁니다. 어댑터가 %1!d!바이트 길이의 문자열을 읽었지만 오프셋 %3!d!에서 %2!d!바이트보다 짧은 문자열이 필요합니다. 입력 파일이 손상되었을 수 있습니다. 파일에 표시되는 문자열 길이가 너무 커서 버퍼 열에 맞지 않습니다.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|원시 어댑터가 계보 ID가 %3!d!인 참조되지 않은 열 "%2"에 대한 입력 열에서 %1!d!바이트를 건너뛰려고 했지만 오류가 발생했습니다. 운영 체제에서 반환된 오류는 이전에 보고되었습니다.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|원시 어댑터가 계보 ID가 %3!d!인 열 "%2"에 대한 입력 열에서 %1!d!바이트를 읽으려고 했지만 오류가 발생했습니다. 운영 체제에서 반환된 오류는 이전에 보고되었습니다.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|파일 이름 속성이 잘못되었습니다. 파일 이름이 디바이스이거나 잘못된 문자를 포함합니다.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|데이터 삽입을 위해 SSIS 대량 삽입을 준비할 수 없습니다.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|데이터베이스 개체 이름 "%1"이(가) 잘못되었습니다.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|정렬 절이 잘못되었습니다.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|파일 "%1"을(를) 읽기용으로 열 수 없습니다. 권한이 없거나 파일을 찾을 수 없는 경우 오류가 발생할 수 있습니다. 정확한 원인은 이전 오류 메시지에서 보고되었습니다.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator를 만들 수 없습니다.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Microsoft.AnalysisServices.TimeDimGenerator를 구성할 수 없습니다.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|열 %1!d!에 대한 데이터 형식이 지원되지 않습니다.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|Microsoft.AnalysisServices.TimeDimGenerator에서 읽지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|Microsoft.AnalysisServices.TimeDimGenerator에서 열 "%2!d!" 데이터를 읽지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|VariableName 속성이 유효한 변수의 이름으로 설정되지 않았습니다. 쓸 수 있는 런타임 변수 이름이 필요합니다.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|ADODB.Recordset 개체를 만들거나 구성할 수 없습니다.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|ADODB.Recordset 개체에 쓰는 동안 오류가 발생했습니다.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|파일 이름이 잘못되었습니다. 파일 이름이 디바이스이거나 잘못된 문자를 포함합니다.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|파일 이름 "%1"이(가) 잘못되었습니다. 파일 이름이 디바이스이거나 잘못된 문자를 포함합니다.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|SQL 명령의 매개 변수에서 대상 열 설명을 검색할 수 없습니다.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|매개 변수가 바인딩되지 않았습니다. SQL 명령의 모든 매개 변수는 입력 열에 바인딩되어야 합니다.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|입력 열 "%1"(%2!d!)의 PivotUsage 값이 잘못되었습니다.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|너무 많은 피벗 키가 발견되었습니다. 입력 열은 하나만 피벗 키로 사용할 수 있습니다.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|피벗 키를 찾을 수 없습니다. 입력 열 하나는 반드시 피벗 키로 사용해야 합니다.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|둘 이상의 출력 열(예: "%1"(%2!d!))이 입력 열 "%3"(%4!d!)(으)로 매핑되었습니다.|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|출력 열 "%1"(%2!d!)을(를) PivotKey 입력 열로 매핑할 수 없습니다.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|출력 열 "%1"(%2!d!)에 올바른 입력 열 계보 ID가 아닌 SourceColumn %3!d!이(가) 있습니다.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|출력 열 "%1"(%2!d!)이(가) 피벗된 값 입력 열로 매핑되었지만 해당 PivotKeyValue 속성 값이 없습니다.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|출력 열 "%1"(%2!d!)이(가) 피벗된 값 입력 열로 매핑되었지만 해당 PivotKeyValue 속성 값이 고유하지 않습니다.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|입력 열 "%1"(%2!d!)이(가) 어떠한 출력 열에도 매핑되지 않습니다.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|집합 키에 대한 값을 비교하는 동안 오류가 발생했습니다.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|입력 열 "%1"(%2!d!)은(는) Long 데이터를 포함하므로 집합 키, 피벗 키 또는 피벗 값으로 사용할 수 없습니다.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|출력 유형이 잘못되었습니다. 출력 열 "%1"(%2!d!)은(는) 매핑되는 입력 열과 동일한 데이터 형식과 메타데이터를 가져야 합니다.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|원본 레코드를 피벗하는 동안 오류가 발생했습니다.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|피벗 키 값 "%1"이(가) 잘못되었습니다.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|데이터 행을 건너뛰는 동안 오류가 발생했습니다.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|파일 "%1"의 데이터 행 %2!I64d!을(를) 처리하는 동안 오류가 발생했습니다.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|플랫 파일 파서를 초기화하는 동안 오류가 발생했습니다.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|플랫 파일 연결 관리자에서 열 정보를 검색할 수 없습니다.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|열 "%1"에 대한 열 이름을 쓰지 못했습니다.|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|열 "%1"에 대한 열 유형이 잘못되었습니다. 현재 유형은 "%2"입니다. "%3" 또는 "%4"만 가능합니다.|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|%1!d!바이트의 데이터를 디스크 I/O에 쓰지 못했습니다. 디스크 I/O 버퍼의 사용 가능한 공간은 %2!d!바이트입니다.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|파일 헤더를 쓰는 동안 오류가 발생했습니다.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|파일 "%1"에 대한 파일 크기를 가져오는 동안 오류가 발생했습니다.|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|파일 "%1"에 대한 파일 포인터를 설정하는 동안 오류가 발생했습니다.|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|디스크 I/O 버퍼를 설정하는 동안 오류가 발생했습니다.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|열 "%1"의 열 데이터가 디스크 I/O 버퍼를 오버플로했습니다.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|파일을 읽는 동안 디스크 I/O 오류가 발생했습니다.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|파일을 읽는 동안 디스크 I/O 시간 초과가 발생했습니다.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|이 변환에 대한 입력 열에 지정한 사용 유형은 읽기/쓰기일 수 없습니다. 사용 유형을 읽기 전용으로 변경하십시오.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|열 "%1"에 대한 플랫 파일 데이터를 복사하거나 변환할 수 없습니다.|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|데이터를 변환하지 못했습니다. 열 "%1"에 대한 데이터 변환 중에 상태 값 %2!d! 및 상태 텍스트 "%3"이(가) 반환되었습니다.|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|Variables 컬렉션을 사용할 수 없습니다.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|PivotKeyValue가 중복됩니다. 입력 열 "%1"(%2!d!)이(가) 피벗된 값 출력 열로 매핑되었지만 PivotKeyValue가 고유하지 않습니다.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|피벗 해제 대상을 찾을 수 없습니다. 적어도 하나 이상의 입력 열을 PivotKeyValue를 사용하여 출력의 DestinationColumn으로 매핑해야 합니다.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue가 잘못되었습니다. 둘 이상의 피벗 해제되는 DestinationColumn이 있는 UnPivot 변환에서 대상별 PivotKeyValues 집합은 정확하게 일치해야 합니다.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|UnPivot 메타데이터가 잘못되었습니다. UnPivot 변환에서 동일한 DestinationColumn을 가리키는 설정된 PivotKeyValue가 있는 모든 입력 열은 DestinationColumn과 정확하게 일치하는 메타데이터를 가져야 합니다.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|피벗 키 값 "%1"을(를) 피벗 키 열의 데이터 형식으로 변환할 수 없습니다.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|너무 많은 피벗 키를 지정했습니다. 하나의 출력 열만 피벗 키로 사용할 수 있습니다.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|출력 열 "%1"(%2!d!)이(가) 입력 열의 DestinationColumn 속성에 의해 매핑되지 않았습니다.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|PivotKey로 표시된 출력 열이 없습니다.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|입력 열 "%1"(%2!d!)에 유효한 출력 열 LineageID를 참조하지 않는 DestinationColumn 속성 값이 있습니다.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|중복된 대상 오류입니다. 피벗되지 않은 둘 이상의 입력 열이 동일한 대상 출력 열로 매핑되었습니다.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|입력 열을 찾을 수 없습니다. 적어도 하나 이상의 입력 열을 출력 열로 매핑해야 합니다.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|입력 열과 출력 열의 수가 다릅니다. 모든 입력에 있는 입력 열의 총 수는 출력 열의 총 수와 같아야 합니다.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|입력이 정렬되지 않았습니다. "%1"을(를) 정렬해야 합니다.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|%1에 대한 JoinType 사용자 지정 속성에 잘못된 값 %2!ld!이(가) 있습니다. 유효한 값은 0(전체), 1(왼쪽) 또는 2(내부)입니다.|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|NumKeyColumns 값이 잘못되었습니다. %1에서 NumKeyColumns 사용자 지정 속성의 값은 1에서 %2!lu! 사이여야 합니다.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|키 열을 찾을 수 없습니다. %1에는 0이 아닌 SortKeyPosition을 가진 열이 적어도 하나 이상 있어야 합니다.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|키 열이 부족합니다. %1에는 0이 아닌 SortKeyPosition 값을 가진 열이 적어도 %2!ld!개 이상 있어야 합니다.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|데이터 형식 불일치가 발생했습니다. SortKeyPosition 값이 %1!ld!인 열에 대한 데이터 형식이 일치하지 않습니다.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|SortKeyPosition 값이 %1!ld!인 열이 잘못되었습니다. %2!ld!이어야 합니다.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|정렬 방향이 일치하지 않습니다. SortKeyPosition 값이 %1!ld!인 열에 대한 정렬 방향이 일치하지 않습니다.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|열이 없습니다. %1에는 연결된 입력 열이 있어야 합니다.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|입력 열에는 출력 열이 있어야 합니다. 사용 유형이 읽기 전용이며 연결된 출력 열이 없는 입력 열이 있습니다.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|비교 플래그가 0이 아닙니다. 문자열이 아닌 열에 대한 비교 플래그는 0이어야 합니다.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|SortKeyPosition 값이 %1!ld!인 열에 대한 비교 플래그가 일치하지 않습니다.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|인식할 수 없는 피벗 키 값입니다.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|계보 항목 값 %1!ld!이(가) 잘못되었습니다. 유효한 범위는 %2!ld!에서 %3!ld! 사이입니다.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|입력 열이 허용되지 않습니다. 입력 열 수는 0이어야 합니다.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|"%1"의 데이터 형식이 지정된 계보 항목에 적합하지 않습니다.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|"%1"의 길이가 지정된 계보 항목에 적합하지 않습니다.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|"%1"의 메타데이터가 연결된 출력 열의 메타데이터와 일치하지 않습니다.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|연결된 입력 열의 SortKeyPosition과 일치하지 않는 SortKeyPosition 값을 가진 출력 열이 있습니다.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|행을 데이터 흐름 태스크 버퍼에 추가하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|열 "%1"(%2!d!)에서 열 "%3"(%4!d!)(으)로 변환하는 동안 데이터를 변환하지 못했습니다.  변환 중에 상태 값 %5!d! 및 상태 텍스트 "%6"이(가) 반환되었습니다.|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|행 핸들 버퍼를 할당하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|행을 SQL Server로 보내지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|버퍼 상태를 준비하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|버퍼 행의 시작을 검색하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|SSIS 대량 삽입에 대한 스레드가 더 이상 실행 중이 아닙니다.  추가 행을 삽입할 수 없습니다. 대량 삽입 스레드 제한 시간을 늘리십시오.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|원본 파일이 잘못되었습니다. 원본 파일에서 131,072개 이상의 열을 반환합니다. 이 오류는 일반적으로 원본 파일이 원시 파일 대상에 의해 생성되지 않을 때 발생합니다.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|%1은(는) 연결되지 않은 추가 입력이며 제거됩니다.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|%1은(는) 연결되지 않았는데 현수로 표시되지 않았습니다.  현수로 표시되어야 합니다.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|피벗 키 값 "%1"이(가) 중복됩니다.|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|피벗 키 값이 중복됩니다.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|구성 요소 로캘 ID를 검색하는 동안 오류가 발생했습니다. 오류 코드는 0x%1!8.8X!입니다.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|로캘 ID가 일치하지 않습니다. 구성 요소 로캘 ID(%1!d!)가 연결 관리자 로캘 ID(%2!d!)와 일치하지 않습니다.|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|구성 요소 로캘 ID가 설정되지 않았습니다. 플랫 파일 어댑터에는 플랫 파일 연결 관리자 로캘 ID가 설정되어 있어야 합니다.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|이진 필드가 너무 깁니다. 어댑터가 %1!d!바이트 길이의 이진 필드를 읽으려고 했지만 오프셋 %3!d!에서 %2!d!보다 짧은 필드가 필요합니다. 이 오류는 일반적으로 입력 필드가 잘못되었을 때 발생합니다. 파일에 있는 문자열 길이가 너무 커서 버퍼 열에 적합하지 않습니다.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|백분율 %2!ld!이(가) "%1" 속성에 적합하지 않습니다. 0부터 100 사이여야 합니다.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|행 수인 %2!ld!이(가) "%1" 속성에 적합하지 않습니다. 0보다 커야 합니다.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|어댑터가 %1!I64d!바이트 길이의 문자열을 기록하라는 요청을 받았지만 모든 데이터의 길이는 4294967295바이트보다 작아야 합니다.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|입력이 출력으로 매핑되지 않았습니다. "%1"에는 적어도 하나 이상의 입력 열이 출력 열로 매핑되어야 합니다.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|코드 페이지가 %2!d!인 "%1"에서 코드 페이지가 %4!d!인 "%3"(으)로의 변환은 지원되지 않습니다.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|%1에 대한 외부 메타데이터 열 매핑이 잘못되었습니다.  외부 메타데이터 열 ID는 0일 수 없습니다.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|%1이(가) 존재하지 않는 외부 메타데이터 열로 매핑되었습니다.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|열 "%1"에 대해 DT_TEXT, DT_NTEXT 또는 DT_IMAGE 유형의 Long 개체 데이터를 데이터 흐름 태스크 버퍼에 쓰지 못했습니다.|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|"%1"에 대한 행 집합을 열지 못했습니다. 해당 개체가 데이터베이스에 있는지 확인하십시오.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|변수 "%1"에 액세스하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|연결 관리자 "%1"을(를) 찾을 수 없습니다. 구성 요소가 Connections 컬렉션에서 연결 관리자를 찾지 못했습니다.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|버전 "%1"에서 버전 %2!d!(으)로 업그레이드하지 못했습니다.|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|입력 열의 값이 너무 커서 ADODB.Recordset 개체에 저장할 수 없습니다.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|열 "%1" 및 "%2"은(는) 유니코드 또는 비유니코드 문자열 데이터 형식으로 변환할 수 없습니다.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|VariableName 속성으로 지정된 변수 "%1"이(가) 잘못되었습니다. 쓸 수 있는 올바른 변수 이름이 필요합니다.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|VariableName 속성으로 지정된 변수 "%1"이(가) 정수가 아닙니다. 변수를 VT_I4, VT_UI4, VT_I8 또는 VT_UI8 유형으로 변경하십시오.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|파일 내에서 구성 요소를 이동할 수 있는 열이 지정되지 않았습니다.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|"%1"에서 IsSorted가 TRUE로 설정되었지만 모든 출력 열의 SortKeyPosition이 0입니다. IsSorted를 FALSE로 변경하거나 0이 아닌 SortKeyPosition을 포함할 출력 열을 적어도 하나 이상 선택하십시오.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|"%1" 메타데이터가 입력 열의 메타데이터와 일치하지 않습니다.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|지정한 변수의 값을 찾거나 잠그거나 설정할 수 없습니다.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|둘 이상의 코드 페이지(%2!d! 및 %3!d!)가 지정되었기 때문에 열 "%1"을(를) 처리할 수 없습니다.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|%2과(와) %3 유형 간의 변환이 지원되지 않으므로 열 "%1"을(를) 삽입할 수 없습니다.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|열 "%1"을(를) 유니코드 또는 비유니코드 문자열 데이터 형식으로 변환할 수 없습니다.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|%1이(가) LineageID가 %2!ld!인 열을 입력 버퍼에서 찾을 수 없습니다.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|%1이(가) 열 %2!lu!에 대한 열 정보를 입력 버퍼에서 가져올 수 없습니다.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|%1이(가) 열 "%2!lu!"에 대한 열 정보를 해당 복사 버퍼에서 가져올 수 없습니다.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|%1이(가) 해당 복사 버퍼에 대한 버퍼 유형을 등록할 수 없습니다.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|%1이(가) 정렬을 위해 데이터를 복사할 버퍼를 만들 수 없습니다.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader 클라이언트에서 Read를 호출하지 못했거나 DataReader를 닫았습니다.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|SQL 명령이 열 정보를 반환하지 않았습니다.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|%1이(가) SQL 명령에 대해 열 정보를 검색할 수 없습니다. 다음 오류가 발생했습니다. %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|원본 테이블 이름이 지정되지 않았습니다.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|캐시 인덱스 위치 %1!d!이(가) 잘못되었습니다. 인덱스가 아닌 열의 경우 인덱스 위치는 0이어야 합니다. 인덱스 열의 경우 인덱스 위치는 순차적인 양수여야 합니다.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|인덱스 위치 %1!d!이(가) 중복됩니다. 인덱스가 아닌 열의 경우 인덱스 위치는 0이어야 합니다. 인덱스 열의 경우 인덱스 위치는 순차적인 양수여야 합니다.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|캐시 연결 관리자에 대해 하나 이상의 인덱스 열을 지정해야 합니다. 인덱스 열을 지정하려면 캐시 열의 인덱스 위치 속성을 설정하십시오.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|캐시 인덱스 위치는 연속적이어야 합니다. 인덱스가 아닌 열의 경우 인덱스 위치는 0이어야 합니다. 인덱스 열의 경우 인덱스 위치는 순차적인 양수여야 합니다.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|속성 "%1"을(를) "%2"에 설정할 수 없습니다. 설정하려는 속성이 지정한 개체에서 지원되지 않습니다. 속성 이름, 대/소문자 및 철자를 확인하십시오.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|속성 유형을 구성 요소에 의해 설정된 유형에서 변경할 수 없습니다.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|출력 ID %1!d!에 여러 오류 출력 구성이 실패했습니다. 새 출력이 생성되지 않았습니다.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|출력 컬렉션에서 출력 ID %1!d!을(를) 삭제할 수 없습니다.  ID가 잘못되었거나 ID가 기본 또는 오류 출력일 수 있습니다.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|속성 "%1"을(를) "%2"에 설정하지 못했습니다.|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|%1의 유형을 유형: "%2", 길이: %3!d!, 전체 자릿수: %4!d!, 소수 자릿수: %5!d!, 코드 페이지: %6!d!(으)로 설정하지 못했습니다.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|둘 이상의 오류 출력이 구성 요소에서 발견되었습니다. 오류 출력은 하나만 있어야 합니다.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|출력 열에서 속성을 설정할 수 없습니다.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|"%1"에 대한 데이터 형식을 오류 "%2"에서 수정할 수 없습니다.|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|"%1"은(는) 원본 출력이 아니기 때문에 IsSorted 속성을 TRUE로 설정할 수 없습니다. 원본 출력의 SynchronousInputID 값은 0입니다.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|"%1"이(가) 원본 출력이 아니기 때문에 "%2"은(는) SortKeyPosition 속성을 0이 아닌 값으로 설정할 수 없습니다. 출력 열 "colname"(ID)은 해당 출력 "outputname"(ID)이 원본 출력이 아니기 때문에 SortKeyPosition 속성을 0이 아닌 값으로 설정할 수 없습니다.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|"%2"이(가) 원본 출력이 아니기 때문에 "%1"에 대한 ComparisonFlags 속성을 0이 아닌 값으로 설정할 수 없습니다. 출력 열 "colname"(ID)은 해당 출력 "outputname"(ID)이 원본 출력이 아니기 때문에 ComparisonFlags 속성을 0이 아닌 값으로 설정할 수 없습니다.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|해당 유형이 문자열 유형이 아니기 때문에 "%1"에 대한 비교 플래그는 0이어야 합니다. ComparisonFlags는 문자열 유형 열에 대해 0이 아닌 값만 가능합니다.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|해당 SortKeyPosition이 0으로 설정되었기 때문에 "%1"은(는) ComparisonFlags 속성을 0이 아닌 값으로 설정할 수 없습니다. 출력 열의 ComparisonFlags는 해당 SortKeyPosition도 0이 아닌 경우 0이 아닌 값만 가능합니다.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|속성이 읽기 전용입니다.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|%1에 잘못된 데이터 형식 값(%2!ld!)이 설정되어 있습니다.|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|"%1"에는 설정할 코드 페이지가 필요한데 전달된 값이 0입니다.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|"%1"에 잘못된 길이가 있습니다. 길이는 %2!ld!에서 %3!ld! 사이여야 사이입니다.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|"%1"의 소수 자릿수가 잘못되었습니다. 소수 자릿수는 %2!ld!에서 %3!ld! 사이여야 사이입니다.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|"%1"의 전체 자릿수가 잘못되었습니다. 전체 자릿수는 %2!ld!에서 %3!ld! 사이여야 사이입니다.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|"%1"에서 길이, 전체 자릿수, 소수 자릿수 또는 코드 페이지에 대해 0이 아닌 값이 설정되어 있는데, 이 데이터 형식에 필요한 값은 0입니다.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|%1에서는 출력 열 데이터 형식 속성을 설정할 수 없습니다.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|"%1"에 잘못된 데이터 형식이 있습니다. "%1"은(는) 특수한 오류 열이며 DT_I4 데이터 형식만 유효합니다.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|구성 요소에서 오류 코드 설명을 제공하지 않습니다.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|지정한 오류 코드가 이 구성 요소와 연결되어 있지 않습니다.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|잘림으로 인해서 잘림 처리 설정에 따른 행 리디렉션이 발생했습니다.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|계보 ID가 %2!d!인 열에서 해당 사용 유형이 허용되지 않으므로 "%1"은(는) 이 열을 읽기/쓰기로 만들 수 없습니다. 입력 열의 사용 유형을 이 구성 요소에서 지원되지 않는 UT_READWRITE 유형으로 변경하려고 했습니다.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|계보 ID가 %2!d!인 입력 열의 사용 요청이 %1에서 금지되었습니다.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|"%1"은(는) 계보 ID가 %2!d!인 입력 열에 대해 요청된 변경을 수행할 수 없습니다. 오류 코드 0x%3!8.8X!(으)로 인해 요청이 실패했습니다. 입력 열의 사용 유형을 설정하는 동안 지정한 오류가 발생했습니다.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|"%1"에 데이터 형식 속성을 설정하지 못했습니다(오류 코드 0x%2!8.8X!). 출력 열의 데이터 형식 속성 중에서 하나 이상을 설정하는 동안 오류가 발생했습니다.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|"%1"에 대한 메타데이터를 검색할 수 없습니다. 개체 이름이 올바른지, 그리고 개체가 있는지 확인하십시오.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|출력 열을 외부 메타데이터 열로 매핑할 수 없습니다.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|변수 %1은(는) "%2" 유형이어야 합니다.|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|%1에서는 외부 메타데이터 열 데이터 형식 속성을 설정할 수 없습니다.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|ID %1!lu!은(는) 입력 ID 또는 출력 ID가 아닙니다. 지정한 ID는 외부 메타데이터 컬렉션이 연결된 입력 ID 또는 출력 ID여야 합니다.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|"%1"에서 외부 메타데이터 컬렉션이 사용되지 않은 것으로 표시되어 어떠한 작업도 수행할 수 없습니다.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|%1은(는) 동기 출력인데 동기 출력에 필요한 버퍼 유형을 검색할 수 없습니다.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|입력 열 "%1"은(는) 읽기 전용이어야 합니다. 입력 열에 읽기 전용이 아닌 허용되지 않는 사용 유형이 있습니다.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|"%1"에 필수 속성 "%2"이(가) 없습니다. 이 개체에는 지정한 사용자 지정 속성이 있어야 합니다.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|출력 %1에 속성 "%2"을(를) 할당할 수 없지만 현재 이 속성이 할당되어 있습니다.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|%1은(는) 제외 그룹 %2!d!에 있어야 합니다. 모든 출력은 지정한 제외 그룹에 있어야 합니다.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|속성 "%1"이(가) 비어 있습니다. 이 속성은 비워둘 수 없습니다.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|식 "%1"에 대해 메모리를 할당할 수 없습니다. 식을 보유하기 위한 내부 개체를 만드는 동안 메모리 부족 오류가 발생했습니다.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|식 "%1"을(를) 구문 분석할 수 없습니다. 이 식이 잘못되었거나 메모리가 부족합니다.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|식 "%1"을(를) 계산하지 못했습니다(오류 코드 0x%2!8.8X!). 구문 분석 시에 발견할 수 없는 오류(예: 0으로 나누기)가 이 식에 있거나 메모리가 부족합니다.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|Expression 개체에 대해 메모리를 할당할 수 없습니다. Expression 개체 포인터의 배열을 만드는 동안 메모리 부족 오류가 발생했습니다.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|식 관리자를 만드는 동안 %1이(가) 실패했습니다(오류 코드 0x%2!8.8X!).|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|식 "%1"이(가) 부울이 아닙니다. 이 식의 결과 유형은 부울이어야 합니다.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|"%2"의 식 "%1"이(가) 잘못되었습니다.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|열 "%1"(%2!d!)을(를) 입력 파일 열에 대응시킬 수 없습니다. 출력 열 이름 또는 입력 열 이름을 파일에서 찾을 수 없습니다.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|%2에서 식 "%1"의 결과 열을 설정하지 못했습니다(오류 코드 0x%3!8.8X!). 식 결과를 받기 위한 입력 또는 출력 열을 확인할 수 없거나 식 결과를 열 유형으로 캐스팅할 수 없습니다.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|%1이(가) 패키지에서 로캘 ID를 가져오지 못했습니다.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|매개 변수 매핑 문자열의 형식이 잘못되었습니다.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|SQL 명령에는 %1!d!개의 매개 변수가 필요하지만 매개 변수 매핑에 %2!d!개의 매개 변수만 필요합니다.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|SQL 명령에는 "%1"(이)라는 매개 변수가 필요하지만 매개 변수 매핑에서 이 매개 변수를 찾을 수 없습니다.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|이름이 "%1"인 데이터 원본 열이 여러 개 있습니다.  데이터 원본 열 이름은 고유해야 합니다.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|이름이 없는 데이터 원본 열이 있습니다.  각 데이터 원본 열에는 이름이 있어야 합니다.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|레이아웃에서 구성 요소의 연결이 끊어졌습니다.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|레이아웃 구성 요소에 대한 ID가 잘못되었습니다.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|구성 요소에 있는 입력 수가 잘못되었습니다.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|구성 요소에 있는 출력 수가 잘못되었습니다.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|구성 요소에 입력 또는 출력이 없습니다.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|이 구성 요소가 조작하는 열의 목록을 할당하는 데 사용할 수 있는 메모리가 부족합니다.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|출력 열 "%1"(%2!d!)이(가) 계보 ID가 %3!d!인 입력 열을 참조하지만 해당 계보 ID를 가진 입력을 찾을 수 없습니다.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|적어도 하나 이상의 입력 열을 정렬 키로 표시해야 하지만 키를 찾을 수 없습니다.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|열 "%1"(%2!d!) 및 열 "%3"(%4!d!)이(가) 정렬 키 가중치 %5!d!(으)로 표시되었습니다.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|유효성 검사 문제를 수정할 때까지 요청된 메타데이터 변경 내용을 구성 요소에서 수행할 수 없습니다.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|입력을 입력 컬렉션에 추가할 수 없습니다.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|출력을 출력 컬렉션에 추가할 수 없습니다.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|입력을 입력 컬렉션에서 삭제할 수 없습니다.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|출력을 출력 컬렉션에서 제거할 수 없습니다.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|열의 사용 유형을 변경할 수 없습니다.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|%1이(가) 사용자 지정 속성 "%2"을(를) 가지려면 읽기/쓰기여야 합니다. 입력 또는 출력 열에 지정한 사용자 지정 속성이 있지만 읽기/쓰기가 아닙니다. 속성을 제거하거나 열을 읽기/쓰기로 변경하십시오.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|%1은(는) 읽기/쓰기이며 사용자 지정 속성 "%2"이(가) 있어야 합니다. 이 속성을 추가하거나 열에서 읽기/쓰기 특성을 제거하십시오.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|열을 삭제할 수 없습니다. 구성 요소가 이 입력 또는 출력에서의 열 삭제를 허용하지 않습니다.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|구성 요소가 이 입력 또는 출력에 대한 열 추가를 허용하지 않습니다.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|연결 "%1"을(를) 찾을 수 없습니다. 연결 관리자에 해당 이름을 가진 연결이 있는지 확인하십시오.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|ID가 "%1"인 런타임 연결 관리자를 찾을 수 없습니다. 연결 관리자 컬렉션에 해당 ID를 가진 연결 관리자가 있는지 확인하십시오.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS 오류 코드 DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  오류 코드 0x%2!8.8X!(으)로 인해 연결 관리자 "%1"에 대한 AcquireConnection 메서드 호출이 실패했습니다.  AcquireConnection 메서드 호출이 실패한 이유에 대한 자세한 정보와 함께 이 오류 메시지보다 먼저 게시된 오류 메시지가 있을 수도 있습니다.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|연결 관리자 "%1"(으)로부터 설정한 연결이 잘못되었습니다.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|연결 관리자 "%1"의 유형이 잘못되었습니다.  필요한 유형은 "%2"입니다. 구성 요소에 사용할 수 있는 유형은 "%3"입니다.|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|런타임 연결 관리자로부터 관리되는 연결을 설정할 수 없습니다.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|입력 컬렉션을 초기화할 입력을 만들 수 없습니다.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|출력 컬렉션을 초기화할 출력을 만들 수 없습니다.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|파일 "%1"에 쓰지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|연결 관리자 "%1"이(가) AcquireConnection 메서드에서 잘못된 유형의 개체를 반환했습니다.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|입력 열 "%1"(%2!d!)에 필요한 "%3" 속성을 찾을 수 없습니다. 누락된 속성을 추가해야 합니다.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|"%1"이(가) 읽기 전용으로 표시되었지만 다른 열에 참조되지 않습니다. 참조되지 않는 열은 허용되지 않습니다.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|"%1"이(가) 열 ID %2!d!을(를) 참조하지만 해당 열을 입력에서 찾을 수 없습니다. 존재하지 않는 열을 참조가 가리킵니다.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|"%1"에서 "%2"을(를) 참조하지만 해당 열이 BLOB 유형이 아닙니다.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|"%1"이(가) 출력 열 ID %2!d!을(를) 참조하지만 해당 열을 출력에서 찾을 수 없습니다.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|파일 "%1"에서 읽지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|느린 변경 차원 변환의 입력에는 고정, 변경 또는 기록 유형의 열이 적어도 하나 이상 있어야 합니다. 적어도 하나 이상의 열이 FixedAttribute, ChangingAttribute 또는 HistoricalAttribute인지 확인하십시오.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|"%1"의 ColumnType 속성이 잘못되었습니다. 현재 값이 허용되는 값 범위를 벗어났습니다.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|데이터 형식이 다르기 때문에 입력 열 "%1"을(를) 외부 열 "%2"(으)로 매핑할 수 없습니다. 느린 변경 차원 변환은 DT_STR 및 DT_WSTR을 제외한 다른 형식의 열 사이에서 매핑을 허용하지 않습니다.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|"%1"의 데이터 형식이 ANSI 파일에서 지원되지 않는 DT_NTEXT입니다. DT_TEXT를 대신 사용하고 데이터 변환 구성 요소를 통해 데이터를 DT_NTEXT로 변환하십시오.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|"%1"의 데이터 형식이 유니코드 파일에서 지원되지 않는 DT_TEXT입니다. DT_NTEXT를 대신 사용하고 데이터 변환 구성 요소를 통해 데이터를 DT_TEXT로 변환하십시오.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|"%1"의 데이터 형식이 지원되지 않는 DT_IMAGE입니다. DT_TEXT 또는 DT_NTEXT를 대신 사용하고 데이터 변환 구성 요소를 통해 데이터를 DT_IMAGE로 변환하거나 DT_IMAGE에서 변환하십시오.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|형식 "%1"은(는) 플랫 파일 연결 관리자에서 지원되지 않습니다. 지원되는 형식은 Delimited, FixedWidth, RaggedRight 및 Mixed입니다.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|"%1"이(가) 파일 이름을 포함해야 하는데, 문자열 유형이 아닙니다.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|속성 설정이 충돌하여 오류가 발생했습니다. "%1"에는 TRUE로 설정된 AllowAppend 속성과 ForceTruncate 속성이 있습니다. 두 속성을 모두 TRUE로 설정할 수 없습니다. 두 속성 중 하나를 FALSE로 설정하십시오.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1에서 열 ID %2!d!을 참조하지만 이미 %3이(가) 해당 열을 참조합니다. 해당 열에 대한 두 참조 중 하나를 제거하십시오.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|연결 관리자가 %1에 할당되지 않았습니다.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1에서 ID가 %2!d!인 출력 열을 참조하지만 이미 %3이(가) 해당 열을 참조합니다.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|"%1"을(를) 어떠한 입력 열에서도 참조하지 않습니다. 정확하게 하나의 입력 열에서 각 출력 열을 참조해야 합니다.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|"%1"에서 "%2"을(를) 참조하지만 해당 열의 유형이 잘못되었습니다. DT_TEXT, DT_NTEXT 또는 DT_IMAGE여야 합니다. 참조에서 가리키는 열이 BLOB입니다.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|"%1"에 파일 이름이 있어야 하지만 문자열 유형이 아닙니다.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|%2에 대해 TRUE로 설정된 ExpectBOM 속성이 "%1"에 있지만 이 열은 NT_NTEXT가 아닙니다. ExpectBOM은 열 가져오기 변환의 BOM(바이트 순서 표시) 사용 여부를 지정합니다. ExpectBOM 속성을 false로 설정하거나 출력 열 데이터 형식을 DT_NTEXT로 변경하십시오.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|데이터 출력 열은 DT_TEXT, DT_NTEXT 또는 DT_IMAGE여야 합니다. 데이터 출력 열은 BLOB 유형으로만 설정할 수 있습니다.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|FailOnFixedAttributeChange 속성이 TRUE로 설정된 경우 고정 특성 변경이 검색되면 변환을 실행할 수 없습니다. 행을 고정 특성 출력으로 보내려면 FailOnFixedAttributeChange 속성을 FALSE로 설정하십시오.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|조회 변환에서 행을 검색하지 못했습니다. FailOnLookupFailure가 TRUE로 설정되었고 행이 검색되지 않으면 변환을 실행할 수 없습니다.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|느린 변경 차원 변환의 입력에서는 적어도 하나 이상의 열 유형이 키여야 합니다. 적어도 하나 이상의 열 유형을 키로 설정하십시오.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|이름이 "%1"인 외부 열을 찾을 수 없습니다.|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|유추 지표 열 "%1"은(는) DT_BOOL 유형이어야 합니다.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|%1의 오류 행 처리 값이 RD_NotUsed로 설정되어야 합니다.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|%1의 잘림 행 처리 값이 RD_NotUsed로 설정되어야 합니다.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|ID가 %2!d!인 출력 열에 필요한 계보 ID가 %1!d!인 입력 열을 찾을 수 없습니다.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|출력 열 ID %1!d!에 지정된 집계 유형에 대한 출력 데이터 형식이 잘못되었습니다.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|%2에서 지정된 집계에 사용되는 %1에 대한 입력 데이터 형식이 잘못되었습니다.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|입력 열 계보 ID %1!d! 및 출력 열 ID %2!d!의 데이터 형식이 일치하지 않습니다.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|입력 ID %1!d!에 대한 입력 버퍼 핸들을 가져올 수 없습니다.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|출력 ID %1!d!에 대한 출력 버퍼 핸들을 가져올 수 없습니다.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|출력 버퍼에서 계보 ID가 %1!d!인 열을 찾을 수 없습니다.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|출력 버퍼에서 계보 ID가 %1!d!인 열을 찾을 수 없습니다.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|%1에 대한 출력 열 수는 0일 수 없습니다.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|플랫 파일 연결 관리자의 열 수는 플랫 파일 어댑터의 열 수와 같아야 합니다. 플랫 파일 연결 관리자의 열 수는 %1!d!개이지만 플랫 파일 어댑터의 열 수는 %2!d!개입니다.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|플랫 파일 연결 관리자의 인덱스 %2!d!에 있는 열 "%1"을(를) 플랫 파일 어댑터의 열 컬렉션에 있는 인덱스 %3!d!에서 찾을 수 없습니다.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|ID가 %1!d!인 외부 메타데이터 열이 이미 %2(으)로 매핑되었습니다.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|%1!u!자를 초과하는 키 열이 변환 중에 구성됩니다.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|%1!u!바이트를 초과하는 결과 값이 변환 중에 바이트입니다.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|메모리를 할당할 수 없습니다.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|메모리를 할당할 수 없습니다.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|메모리를 할당할 수 없습니다.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|메모리를 할당할 수 없습니다.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|메모리를 할당할 수 없습니다.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|메모리를 할당할 수 없습니다.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|메모리를 할당할 수 없습니다.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|메모리를 할당할 수 없습니다.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|입력 열 "%1"이(가) 참조되지 않습니다.|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|정렬 변환에서 %1!d!개의 스레드를 가진 스레드 풀을 만들 수 없습니다. 사용 가능한 메모리가 부족합니다.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|정렬 변환에서 작업 항목을 스레드 풀에 대기시킬 수 없습니다. 사용 가능한 메모리가 부족합니다.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|정렬 변환에서 작업자 스레드가 중지되었습니다(오류 코드 0x%1!8.8X!). 버퍼를 정렬하는 동안 치명적인 오류가 발생했습니다.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads가 %1!ld!인데 1에서 %2!ld!(포함) 사이여야 합니다. -1은 CPU 수를 기본값으로 설정합니다.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|XML에서 로드할 수 없습니다.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|XML에 저장할 수 없습니다.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|값 "%1"을(를) 정수로 변환할 수 없습니다.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|값 "%1"을(를) 부울로 변환할 수 없습니다.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|ID가 %1!d!인 개체 근처에서 로드 오류가 발생했습니다.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|값 "%1"은(는) 특성 "%2"에 적합하지 않습니다.|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|값 "%1"은(는) 특성 "%2"에 적합하지 않습니다.|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|값 "%1"은(는) 특성 "%2"에 적합하지 않습니다.|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|%1은(는) 출력 열로 매핑되지 않습니다.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|%1에 잘못된 매핑이 있습니다.  ID가 %2!ld!인 출력 열이 이 구성 요소에 없습니다.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|이 입력에 이미 매핑이 존재하는 출력 열로 %1이(가) 매핑됩니다.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|오류 0x%2!8.8X!(으)로 인해 계보 ID가 %1!ld!인 입력 열을 DT_WSTR로 변환할 수 없습니다.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|ID가 %1!d!인 참조된 개체를 패키지에서 찾을 수 패키지에서 찾을 수 없습니다.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|pipelinexml 모듈에 필요한 지속성 속성을 읽을 수 없습니다. 파이프라인에서 이 속성을 제공하지 않았습니다.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|값 "%1"은(는) 특성 "%2"에 적합하지 않습니다.|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|사용자 지정 속성 "%1"을(를) 검색할 수 없습니다.|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|위치 번호가 %2!d!인 매개 변수를 사용하여 ParameterMap 사용자 지정 속성에 참조된 계보 ID가 %1!d!인 입력 열을 입력 열 컬렉션에서 찾을 수 없습니다.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|참조 열 "%1"을(를) 찾을 수 없습니다.|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 및 "%2"(이)라는 참조 열에 호환되지 않는 데이터 형식이 있습니다.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|매개 변수가 있는 SQL 문이 주 SQL 문과 일치하지 않는 메타데이터를 생성합니다.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|매개 변수가 있는 SQL 문에 잘못된 수의 매개 변수가 있습니다. %1!d!개가 필요한데 %2!d!개가 있습니다.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1에 조인할 수 없는 데이터 형식이 있습니다.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1에 복사할 수 없는 데이터 형식이 있습니다.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|%1에 지원되지 않는 데이터 형식이 있습니다. DT_STR 또는 DT_WSTR이어야 합니다.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|%1에 지원되지 않는 데이터 형식이 있습니다. DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT 또는 DT_IMAGE여야 합니다.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|%1에 지원되지 않는 데이터 형식이 있습니다. DT_STR, DT_WSTR, DT_TEXT 또는 DT_NTEXT여야 합니다.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|정렬 변환에서 작업자 스레드와 통신하기 위한 이벤트를 만들 수 없습니다. 정렬 변환에 사용할 있는 시스템 핸들이 부족합니다.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|정렬 변환에서 작업자 스레드를 만들 수 없습니다. 정렬 변환에 사용할 있는 메모리가 부족합니다.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|정렬 변환에서 버퍼 ID %2!d!에 있는 행 %1!d!을(를) 버퍼 ID %4!d!에 있는 행 %3!d!과(와) 비교하지 못했습니다.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|조회 변환 참조 메타데이터에 너무 적은 열이 있습니다. SQLCommand 속성을 확인하십시오. SELECT 문은 적어도 하나 이상의 열을 반환해야 합니다.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|ColumnInfo 구조의 배열에 대해 메모리를 할당할 수 없습니다.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|ColumnPair 구조의 배열에 대해 메모리를 할당할 수 없습니다.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|주 작업 영역을 만들기 위해 BUFFCOL 구조의 배열에 대해 메모리를 할당할 수 없습니다.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|주 작업 영역 버퍼를 만들 수 없습니다.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|해시 테이블에 대해 메모리를 할당할 수 없습니다.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|해시 노드에 대한 힙을 만들기 위해 메모리를 할당할 수 없습니다.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|해시 노드 힙에 대해 메모리를 할당할 수 없습니다.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|LRU 노드에 대해 힙을 만들 수 없습니다. 메모리가 부족합니다.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|LRU 노드 힙에 대해 메모리를 할당할 수 없습니다. 메모리가 부족합니다.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|열 메타데이터를 로드하는 동안 OLE DB 오류가 발생했습니다. SQLCommand 및 SqlCommandParam 속성을 확인하십시오.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|행 집합을 인출하는 동안 OLE DB 오류가 발생했습니다. SQLCommand 및 SqlCommandParam 속성을 확인하십시오.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|내부 캐시를 채우는 동안 OLE DB 오류가 발생했습니다. SQLCommand 및 SqlCommandParam 속성을 확인하십시오.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|매개 변수를 바인딩하는 동안 OLE DB 오류가 발생했습니다. SQLCommand 및 SqlCommandParam 속성을 확인하십시오.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|바인딩을 만드는 동안 OLE DB 오류가 발생했습니다. SQLCommand 및 SqlCommandParam 속성을 확인하십시오.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|런타임 중에 switch 문에서 잘못된 대/소문자가 발견되었습니다.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|주 작업 영역 버퍼의 새 행에 대해 메모리를 할당할 수 없습니다. 메모리가 부족합니다.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|매개 변수가 있는 행 집합을 인출하는 동안 OLE DB 오류가 발생했습니다. SQLCommand 및 SqlCommandParam 속성을 확인하십시오.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|매개 변수가 있는 행을 인출하는 동안 OLE DB 오류가 발생했습니다. SQLCommand 및 SqlCommandParam 속성을 확인하십시오.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|주 작업 영역 버퍼의 새 행에 대해 메모리를 할당할 수 없습니다. 메모리가 부족합니다.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|주 작업 영역 버퍼를 만들 수 없습니다.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|해시 테이블에 대해 메모리를 할당할 수 없습니다.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|해시 노드에 대한 힙을 만들기 위해 메모리를 할당할 수 없습니다.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|해시 노드 힙에 대해 메모리를 할당할 수 없습니다.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|CountDistinct 노드에 대한 힙을 만들기 위해 메모리를 할당할 수 없습니다.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|CountDistinct 노드 힙에 대해 메모리를 할당할 수 없습니다.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|CountDistinct 체인에 대한 힙을 만들기 위해 메모리를 할당할 수 없습니다.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|CountDistinct 해시 테이블에 대해 메모리를 할당할 수 없습니다.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|CountDistinct 작업 영역 버퍼의 새 행에 대해 메모리를 할당할 수 없습니다.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|CountDistinct 작업 영역 버퍼를 만들 수 없습니다.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|CountDistinct 축소 배열에 대해 메모리를 할당할 수 없습니다.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|CountDistinct 체인에 대해 메모리를 할당할 수 없습니다.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|계보 ID가 %1!d! 및 %2!d!인 열에 일치하지 않는 메타데이터가 있습니다. copymap에 대한 출력 열로 매핑되는 입력 열에 동일한 메타데이터가 없습니다(데이터 형식, 전체 자릿수, 소수 자릿수, 길이 또는 코드 페이지).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|계보 ID가 "%1!d!"인 출력 열이 입력 열에 올바르게 매핑되지 않습니다. 출력 열의 CopyColumnId 속성이 잘못되었습니다.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|열 "%1"에 대한 Long 데이터를 검색하지 못했습니다.|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Long 데이터가 열에 대해 검색되었지만 데이터 흐름 태스크 버퍼에 추가할 수 없습니다.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|출력 "%1"(%2!d!)에 출력 열이 있지만 멀티캐스트 출력에서 열을 선언하지 않습니다. 패키지가 손상되었습니다.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|지역화된 리소스 ID %1!d!을(를) 로드할 수 없습니다. RLL 파일이 있는지 확인하십시오.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|이벤트 인터페이스를 가져올 수 없습니다. XML로 유지하기 위한 데이터 흐름 모듈에 잘못된 이벤트 인터페이스가 전달되었습니다.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|XML 로드 중에 경로 개체를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|XML 로드 중에 입력 개체를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|XML 로드 중에 출력 개체를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|XML 로드 중에 입력 열 개체를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|XML 로드 중에 출력 열 개체를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|XML 로드 중에 속성 개체를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|XML 로드 중에 연결 개체를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|특정 변환 열이 없거나 유형이 잘못되었습니다.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|유사 항목 그룹화 변환에서 필수 테이블과 접근자를 만들지 못했습니다.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|유사 항목 그룹화 변환에서 입력을 복사하지 못했습니다.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|유사 항목 그룹화 변환에서 그룹을 생성하지 못했습니다.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|속성 '%1'의 설정을 적용하는 중에 유사 항목 그룹화에서 오류가 발생했습니다.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|유사 항목 그룹화 변환에서 데이터 표준화에 사용할 데이터 정식 행을 선택하지 못했습니다.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|유사 항목 그룹화에서 IMAGE, TEXT 또는 NTEXT 유형의 입력 열을 지원하지 않습니다.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|DT_STR 또는 DT_WSTR 데이터 형식이 아닌 열 "%1"(%2!d!)에 유사 항목 조회가 지정되었습니다.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|유사 항목 그룹화 변환 파이프라인 오류가 발생했으며 오류 코드 0x%1!8.8X!이(가) 반환되었습니다. "%2"|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|출력 열 "%2"(%3!d!)에 지정된 코드 페이지 %1!d!이(가) 않습니다.  먼저 이 열 앞에 데이터 변환을 삽입하여 변환을 수행할 수 있는 DT_WSTR로 이 열을 변환해야 합니다.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|출력 "%1"(%2!d!)을(를) 제어하는 버퍼에 대한 데이터 끝 플래그를 설정하는 동안 오류가 발생했습니다.|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|입력 버퍼를 복제할 수 없습니다. 메모리가 부족하거나 내부 오류가 있습니다.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|열 "%1"에서 가타카나 및 히라가나 문자를 동시에 생성하도록 요청합니다.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|열 "%1"에서 중국어 간체 및 중국어 번체 문자를 동시에 생성하도록 요청합니다.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|열 "%1"에서 전자 및 반자 문자를 모두 생성하도록 작업을 요청합니다.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|열 "%1"에서 일본어 문자 작업과 중국어 문자 작업을 결합합니다.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|열 "%1"에서 중국어 문자 작업과 대문자 및 소문자 작업을 결합합니다.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|열 "%1"에서 일본어 문자 작업과 대문자 및 소문자 작업을 결합합니다.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|열 "%1"에서 열을 대문자 및 소문자 모두로 매핑합니다.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|열 "%1"에서 대문자 및 소문자가 아닌 플래그를 대/소문자 구분 작업과 결합합니다.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|열 "%1"의 데이터 형식을 지정한 대로 매핑할 수 없습니다.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|기존 일치 인덱스 "%2"의 버전(%1)이 지원되지 않습니다. 필요한 버전은 "%3"입니다. 이 오류는 인덱스 메타데이터에 유지된 버전이 현재 코드가 작성된 버전과 일치하지 않는 경우에 발생합니다. 현재 버전의 코드로 인덱스를 다시 작성하여 오류를 수정하십시오.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|테이블 "%1"이(가) 미리 작성된 올바른 일치 인덱스가 아닌 것 같습니다. 이 오류는 메타데이터 레코드를 지정한 미리 작성된 인덱스에서 로드할 수 없을 때 발생합니다.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|지정한 미리 작성된 일치 인덱스 "%1"을(를) 읽을 수 없습니다.  OLEDB 오류 코드: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|참조 테이블 열에 대한 올바른 조인이 있는 입력 열이 없습니다.  입력 열 속성 JoinToReferenceColumn 및 JoinType을 사용하여 적어도 하나 이상의 조인을 정의해야 합니다.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|지정한 기존 일치 인덱스 "%1"이(가) 원래 열 "%2"에 대한 유사 항목 조회 정보로 작성되지 않았습니다.  이 정보를 포함하도록 이 인덱스를 다시 작성해야 합니다. 이 오류는 유사 항목 조인 열이 아닌 열로 인덱스를 작성했을 때 발생합니다.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|속성 "%2"에 지정된 이름 "%1"이(가) 올바른 SQL 식별자 이름이 아닙니다. 이 오류는 속성의 이름이 올바른 SQL 식별자 이름에 대한 사양을 따르지 않을 때 발생합니다.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|유사 항목 조회 변환에서 MinSimilarity 임계값 속성은 0.0보다 크거나 같고 1.0보다 작은 값이어야 합니다.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|속성 "%2"에 대한 값 "%1"이(가) 잘못되었습니다.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|유사 항목 조인이 DT_STR 및 DT_WSTR 유형의 문자열 열 사이에서만 지원되므로 입력 열 "%1" 및 참조 열 "%2" 사이에 지정된 유사 항목 조회가 잘못되었습니다.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|정확히 조회 열 "%1" 및 "%2"의 데이터 형식이 다르거나 비교할 수 있는 문자열 유형이 아닙니다. 정확히 조인은 동일한 데이터 형식이나 DT_STR 및 DT_WSTR이 조합된 열 사이에서만 지원됩니다.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|복사 열 "%1" 및 "%2"의 데이터 형식이 다르거나 일반적으로 변환할 수 있는 문자열 유형이 아닙니다. 이 오류는 동일한 데이터 형식이나 DT_STR 및 DT_WSTR이 조합된 열 사이에는 참조에서 출력으로의 복사가 지원되지만 다른 유형의 열에서는 지원되지 않기 때문에 발생합니다.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|통과 열 "%1" 및 "%2"의 데이터 형식이 다릅니다. 데이터 형식이 동일한 열만 입력에서 출력으로의 통과 열로 지원됩니다.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|참조 열 "%1"을(를) 찾을 수 없습니다.|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|출력 열에는 정확히 하나의 CopyColumn 또는 PassThruColumn 속성이 지정되어 있어야 합니다. 이 오류는 CopyColumn 및 PassThruColumn 속성이 모두 비어 있지 않은 값으로 설정되지 않았거나 설정되었을 때 발생합니다.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|출력 열 '%3'에서 속성 '%2'에 대해 지정된 원본 계보 ID '%1!d!'을(를) 입력 열 컬렉션에서 찾을 수 없습니다. 이 오류는 출력 열에 통과 열로 지정된 입력 열 ID를 입력 집합에서 찾을 수 없을 때 발생합니다.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|미리 작성된 인덱스 "%2"의 열 "%1"을(를) 참조 테이블/쿼리에서 찾을 수 없습니다. 이 오류는 기존 일치 인덱스가 작성된 후에 참조 테이블의 스키마/쿼리가 변경될 때 발생합니다.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|2147483647자보다 큰 토큰이 구성 요소에서 발견되었습니다.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|출력 파일을 추가할 수 없습니다. 열 "%1"이(가) 이름으로는 일치하지만 파일에 있는 열의 유형은 %2이고 입력 열의 유형은 %3입니다. 열에 대한 메타데이터가 데이터 형식에서 일치하지 않습니다.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|출력 파일을 추가할 수 없습니다. 열 "%1"이(가) 이름으로는 일치하지만 파일 열의 최대 길이는 %2!d!이고 입력 열의 최대 길이는 %3!d!입니다. 열에 대한 메타데이터가 길이에서 일치하지 않습니다.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|출력 파일을 추가할 수 없습니다. 열 "%1"이(가) 이름으로는 일치하지만 파일에 있는 열의 코드 페이지는 %2!d!이고 입력 열의 코드 페이지는 %3!d!입니다. 명명된 열에 대한 메타데이터가 코드 페이지에서 일치하지 않습니다.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|출력 파일을 추가할 수 없습니다. 열 "%1"이(가) 이름으로는 일치하지만 파일에 있는 열의 전체 자릿수는 %2!d!이고 입력 열의 전체 자릿수는 %3!d!입니다. 명명된 열에 대한 메타데이터가 전체 자릿수에서 일치하지 않습니다.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|출력 파일을 추가할 수 없습니다. 열 "%1"이(가) 이름으로는 일치하지만 파일에 있는 열의 소스 자릿수는 %2!d!이고 입력 열의 소스 자릿수는 %3!d!입니다.  명명된 열에 대한 메타데이터가 소수 자릿수에서 일치하지 않습니다.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|"%1"에서 DBMS 이름과 버전을 확인할 수 없습니다. 이 오류는 연결의 IDBProperties가 DBMS 이름과 버전을 확인하는 데 필요한 정보를 반환하지 않았을 때 발생합니다.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|"%1"의 DBMS 유형이나 버전이 지원되지 않습니다.  Microsoft SQL Server 버전 8.0 이상에 대한 연결이 필요합니다. 이 오류는 연결의 IDBProperties가 올바른 버전을 반환하지 않았을 때 발생합니다.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|%1은(는) 특수한 오류 출력 열이므로 삭제할 수 없습니다.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|열 "%1"에 대해 지정된 데이터 형식이 필요한 "%2" 형식이 아닙니다.|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|출력 열 "%3"에서 속성 "%2"이(가) 참조하는 입력 열 계보 ID "%1"을(를) 입력 열 컬렉션에서 찾을 수 없습니다.|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|출력 열 "%3"에서 "%2" 속성이 참조하는 입력 열 "%1"에 속성 ToBeCleaned=True 및 올바른 ExactFuzzy 속성 값이 있어야 합니다.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|속성 'CopyRefTable'이 FALSE로 설정된 경우 있어야 하는 클러스터형 인덱스가 참조 테이블 '%1'의 정수 ID 열에 없습니다. CopyRefTable가 false이면 참조 테이블의 정수 ID 열에 클러스터형 인덱스가 있어야 합니다.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|참조 테이블 '%1'에는 지원되는 않는 정수가 아닌 유형의 ID 열이 있습니다. 열 '%2'이(가) 없는 테이블 뷰를 사용하십시오.  이 오류는 참조 테이블의 복사본을 만들 때 정수 ID 열이 추가되고 각 테이블에서 하나의 ID 열만 허용되기 때문에 발생합니다.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|MatchContribution 및 계층 정보를 동시에 지정할 수 없습니다. 두 속성은 모두 평가 계수를 측정하기 때문에 함께 지정될 수 없습니다.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|계층의 수준은 고유한 숫자여야 합니다. 계층 값의 유효한 수준은 1보다 크거나 같은 정수입니다. 숫자가 작을수록 계층의 열 수준이 낮습니다. 기본값인 0은 열이 계층의 일부가 아니라는 것을 나타냅니다. 열의 겹침이나 간격은 허용되지 않습니다.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|유사 항목 그룹에 대해 정의된 열이 없습니다.  열 속성 ToBeCleaned=true 및 ExactFuzzy=2인 입력 열이 적어도 하나 이상 있어야 합니다.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|알 수 없는 이유로 인해 ID가 '%1!d!'인 열이 잘못되었습니다.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|열 '%1'의 데이터 형식이 지원되지 않습니다.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|출력 열 '%1'의 길이가 원본 열 '%2'의 길이보다 작습니다.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|입력 열이 하나만 있어야 합니다.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|정확하게 두 개의 출력 열이 있어야 합니다.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|입력 열의 데이터 형식은 DT_WSTR 또는 DT_NTEXT만 가능합니다.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|출력 열 [%1!d!]의 데이터 형식은 '%2'만 가능합니다.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|참조 열의 데이터 형식은 DT_STR 또는 DT_WSTR만 가능합니다.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|참조 열 '%1'을(를) 찾는 동안 오류가 발생했습니다.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|변환의 [용어 유형]은 WordOnly, PhraseOnly 또는 WordPhrase만 가능합니다.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|[빈도 임계값]은 '%1!d!'보다 작을 수 없습니다.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|[최대 용어 길이] 값은 '%1!d!'보다 작을 수 없습니다.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|[용어 추출] 참조 메타데이터에 너무 적은 열이 포함되어 있습니다.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|메모리를 할당하는 동안 오류가 발생했습니다.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|작업 영역 버퍼를 만드는 동안 오류가 발생했습니다.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|바인딩을 만드는 동안 OLEDB 오류가 발생했습니다.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|행 집합을 인출하는 동안 OLEDB 오류가 발생했습니다.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|내부 캐시를 채우는 동안 OLEDB 오류가 발생했습니다.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|행 %1!ld!, 열 %2!ld!에서 용어를 추출하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%3!8.8X!입니다. 문제를 해결하려면 입력에서 제거하십시오.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|용어 후보의 수는 4G 한도를 초과할 수 없습니다.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|제외 용어에 사용되는 참조 테이블, 뷰 또는 열이 잘못되었습니다.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|문자열 열 '%1'의 길이가 4000자를 초과합니다.  DT_STR에서 DT_WSTR로 변환 시 문자열이 잘릴 수 있습니다.  열 너비를 줄이거나 DT_WSTR 열 유형만 사용하십시오.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|제외 용어에 사용되는 참조 테이블, 뷰 또는 열이 설정되지 않았습니다.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|용어 조회에 너무 적은 출력 열이 포함되어 있습니다.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|참조 열의 데이터 형식은 DT_STR 또는 DT_WSTR만 가능합니다.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|참조 열 '%1'을(를) 찾는 동안 오류가 발생했습니다.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|용어 조회 참조 메타데이터에 너무 적은 열이 포함되어 있습니다.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|단어를 정규화하는 동안 오류가 발생했습니다.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|작업 영역 버퍼를 만드는 동안 오류가 발생했습니다.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|바인딩을 만드는 동안 OLEDB 오류가 발생했습니다.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|행 집합을 인출하는 동안 OLEDB 오류가 발생했습니다.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|내부 캐시를 채우는 동안 OLEDB 오류가 발생했습니다.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|행 %1!ld!, 열 %2!ld!에서 용어를 조회하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%3!8.8X!입니다. 문제를 해결하려면 입력에서 제거하십시오.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|적어도 하나 이상의 통과 열이 출력 열로 매핑되지 않습니다.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|하나의 참조 열로 매핑되는 정확히 하나의 입력 열이 있어야 합니다.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|참조 열로 매핑되는 입력 열의 데이터 형식은 DT_NTXT 또는 DT_WSTR만 가능합니다.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|참조 테이블 이름 "%1"은(는) 올바른 SQL 식별자가 아닙니다. 이 오류는 입력 문자열에서 테이블 이름을 구문 분석할 수 없을 때 발생합니다. 이름에 따옴표가 없는 공백이 존재할 수 있습니다. 이름을 올바르게 따옴표로 묶었는지 확인하십시오.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|용어 필터에서 반복을 시작하는 동안 오류가 발생했습니다.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|용어 캐시에 사용되는 버퍼를 회수하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|STL 컨테이너에서 std::length_error가 발생했습니다.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|문장 부호 문자가 있는 단어를 저장하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|%1!ld!번째 참조 용어를 처리하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%2!8.8X!입니다. 문제를 해결하려면 참조 테이블에서 참조 용어를 제거하십시오.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|참조 용어를 정렬하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|용어 후보 수를 계산하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|유사 항목 조회에서 Exhaustive 속성을 사용하는 경우 필요한 전체 참조 테이블을 주 메모리에 로드할 수 없습니다.  시스템 메모리가 부족하거나 참조 테이블을 로드하는 데 충분하지 않은 MaxMemoryUsage 한도를 지정했습니다.  MaxMemoryUsage를 0으로 설정하거나 크게 늘리십시오.  또는 Exhaustive를 비활성화하십시오.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|용어 조회의 엔진을 초기화하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|문장을 처리하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|문자열을 내부 버퍼에 추가하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|내부 버퍼에서 음성 부분 태그를 저장하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|용어 후보 수를 계산하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|음성 부분 프로세서를 초기화하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|FSA(Finite State Automata)를 로드하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|용어 추출의 엔진을 초기화하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|문장 내에서 처리하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|음성 부분 프로세서를 초기화하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|문자열을 내부 버퍼에 추가하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|단어를 통계 디코더에 추가하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|문장을 디코딩하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|제외 용어를 설정하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|입력에서 문서를 처리하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|점이 머리 글자어의 일부인지 여부를 테스트하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|참조 용어를 설정하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|입력에서 문서를 처리하는 동안 오류가 발생했습니다. 반환된 오류 코드는 0x%1!8.8X!입니다.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|속성 %1의 값이 허용되지 않는 %2!d!입니다.  값은 %3!d!보다 크거나 같아야 합니다.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|속성 %1의 값이 %2!d!입니다. 값은 속성 %4의 값 %3!d!보다 작거나 같아야 합니다.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|"%1"(이)라는 기존의 유사 항목 조회 인덱스를 삭제하는 동안 오류가 발생했습니다. 이 테이블이 유사 항목 조회(또는 이 버전의 유사 항목 조회)에 의해 생성되지 않았거나, 손상되었거나, 다른 문제가 있을 수 있습니다. "%2"(이)라는 테이블을 수동으로 삭제하거나 MatchIndexName 속성에 다른 이름을 지정하십시오.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|변환의 점수 유형은 빈도 또는 TFIDF만 가능합니다.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|지정한 참조 테이블에 너무 많은 행이 있습니다. 유사 항목 조회는 행 수가 10억개 이하인 참조 테이블에서만 작동합니다. 더 작은 참조 테이블 뷰를 사용해 보십시오.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|참조 테이블 '%1'의 크기를 확인할 수 없습니다.  이 개체가 테이블이 아니라 뷰일 수 있습니다.  유사 항목 조회는 CopyReferentaceTable=false일 경우 뷰를 지원하지 않습니다.  테이블이 있으며 CopyReferenceTable=true인지 확인하십시오.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|%2에서 SSIS 데이터 흐름 태스크의 데이터 형식 "%1"이(가) %3에 대해 지원되지 않습니다.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|ID가 %2!d!인 출력에서 ID가 %1!d!인 출력 열에 대해 데이터 형식 속성을 설정할 수 없습니다. 출력이나 열을 찾을 수 없습니다.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|%2에서 사용자 지정 속성 "%1"의 값을 변경할 수 없습니다.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|오류가 아닌 출력의 %1에 해당하는 출력 열이 오류 출력에 없습니다.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|오류 출력의 %1에 해당하는 출력 열이 오류가 아닌 출력에 없습니다.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|오류 출력의 %1에는 해당 데이터 원본 열의 속성과 일치하지 않는 속성이 있습니다.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|%1에서 DT_WSTR 및 DT_NTEXT 열을 제외한 출력 열의 데이터 형식을 변경할 수 없습니다.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|데이터 형식 "%1"이(가) 원본 열 "%3"의 데이터 형식 "%2"과(와) 일치하지 않습니다.|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|%1은(는) 스키마에 일치하는 원본 열이 없습니다.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|참조 용어에 사용되는 참조 테이블/뷰 또는 열이 잘못되었습니다.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|참조 용어에 사용되는 참조 테이블/뷰 또는 열이 설정되지 않았습니다.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|다른 열에 이미 매핑된 ID %2!ld!의 외부 메타데이터 열에 %1이(가) 매핑되었습니다.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|속성 '%2'에 지정된 SQL 개체 이름 '%1'에 최대 개수보다 많은 접두사가 포함되었습니다.  최대 두 개를 포함할 수 있습니다.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|값이 너무 커서 열에 맞지 않습니다.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|SSIS IDataReader가 닫혀 있습니다.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|SSIS IDataReader가 결과 집합의 끝을 지났습니다.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|열의 서수 위치가 잘못되었습니다.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|%1의 데이터 형식 "%2"을(를) 데이터 형식 "%3"(으)로 변환할 수 없습니다.|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|%1의 코드 페이지 %2!d!은(는) 지원되지 않습니다.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|%1에 XML 스키마에 대한 매핑이 없습니다.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|계보 ID가 %1!d! 및 %2!d!인 열에 일치하지 않는 메타데이터가 있습니다. 출력 열로 매핑되는 입력 열에 동일한 메타데이터가 없습니다(데이터 형식, 전체 자릿수, 소수 자릿수, 길이 또는 코드 페이지).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|SSIS IDataReader가 닫혀 있습니다. 읽기 제한 시간이 만료되었습니다.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|제공된 SQL 명령을 실행하는 동안 오류가 발생했습니다. "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|입력 열 '%1'에 지정한 JoinType 속성이 일치 인덱스를 처음 만들 때 해당 참조 테이블 열에 지정한 JoinType과 다릅니다.  일치 인덱스를 지정된 JoinType으로 다시 작성하거나 일치 인덱스를 만들 때 사용된 유형과 일치하도록 JoinType을 변경하십시오.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|"%2" 열의 데이터 형식 "%1"이(가) %3에 대해 지원되지 않습니다.|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|%2 열의 데이터 형식 "%1"이(가) %3에 대해 지원되지 않습니다.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|%1의 데이터 형식이 %2에 대해 지원되지 않습니다.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|%2을(를) 마이그레이션하는 동안 프로젝트 참조 "%1"을(를) 추가하지 못했습니다. 수동으로 마이그레이션을 완료하십시오.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|%2을(를) 마이그레이션하는 동안 이름이 "%1"인 여러 진입점을 찾았습니다. 수동으로 마이그레이션을 완료하십시오.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|%1을(를) 마이그레이션하는 동안 진입점을 찾지 못했습니다. 수동으로 마이그레이션을 완료하십시오.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|데이터 삽입 중 예외가 발생했습니다. 공급자가 반환한 메시지: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|%1에서 공급자 고정 이름을 검색하지 못했습니다. 이는 ADO.NET 대상 구성 요소에서 현재 지원되지 않습니다.|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|데이터 공급자가 대상에 데이터를 삽입하려고 하는 동안 인수 예외가 발생했습니다. 반환된 메시지: %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|BatchSize 속성은 음의 정수가 아니어야 합니다.|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|대상 데이터 원본에 이 행을 보내는 동안 오류가 발생했습니다.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|tSQL 명령을 실행하는 동안 예외가 발생했습니다. 메시지: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|"%2" 열의 데이터 형식 "%1"이(가) %3에 대해 지원되지 않습니다.|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO.NET 대상 구성 요소가 연결 %1을(를) 설정하지 못했습니다. 연결이 손상되었을 수 있습니다.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|지정한 연결 %1은(는) 관리되지 않는 연결입니다. ADO.NET 대상 구성 요소에 관리되는 연결을 사용하십시오.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|대상 구성 요소에 오류 출력이 없습니다. 손상되었을 수 있습니다.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|외부 열 %2과(와) 연결된 lineageID %1이(가) 런타임에 없습니다.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|%1이(가) 데이터베이스에 없습니다. 제거되었거나 이름이 바뀌었을 수 있습니다.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|외부 열의 속성을 가져오지 못했습니다. 입력한 테이블 이름이 없거나 테이블 개체에 대한 SELECT 권한이 없는 경우 연결을 통해 열 속성을 가져오려고 했지만 실패했습니다. 자세한 오류 메시지: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|입력 열의 오류 처리는 ADO.NET 대상 구성 요소에서 지원하지 않습니다.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|입력 열의 잘림 처리는 ADO.NET 대상 구성 요소에서 지원하지 않습니다.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|입력 열의 잘림 행 처리는 ADO.NET 대상 구성 요소에서 지원하지 않습니다.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|테이블 또는 뷰 이름은 사용할 수 없습니다. \n\t 테이블 이름을 따옴표로 묶는 경우 따옴표로 묶기 위해 선택한 데이터 공급자의 접두사 %1과(와) 접미사 %2을(를) 사용하십시오. \n\t 여러 부분으로 구성된 이름을 사용하는 경우 테이블 이름에 최대 세 개의 부분만 사용하십시오.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|계보 ID가 %2!d!인 열 "%1"을(를) 버퍼에서 찾지 못했습니다. 버퍼 관리자에서 오류 코드 0x%3!8.8X!을(를) 반환했습니다.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|열 "%1"(%2!d!)에 대한 정보를 버퍼에서 가져오지 못했습니다. 반환된 오류 코드는 0x%3!8.8X!입니다.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|"%1"을(를) 집계하는 동안 산술 오버플로가 발생했습니다.|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|행 %1!ld!, 열 %2!ld!에 대한 정보를 버퍼에서 가져오지 못했습니다. 반환된 오류 코드는 0x%3!8.8X!입니다.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|행 %1!ld!, 열 %2!ld!에 대한 정보를 버퍼에 설정하지 못했습니다. 반환된 오류 코드는 0x%3!8.8X!입니다.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|필수 버퍼를 사용할 수 없습니다.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|버퍼 경계 정보를 가져오지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|오류 코드 0x%1!8.8X!(으)로 인해 버퍼에 대한 행 집합의 끝을 설정하지 못했습니다.|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|오류 출력 버퍼에 대한 데이터를 가져오지 못했습니다.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|버퍼에서 행을 제거하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|버퍼 오류 정보를 설정하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|%2의 %1에 오류가 있습니다. 반환된 열 상태는 "%3"입니다.|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|참조 메타데이터를 캐시할 수 없습니다.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|조회 중에 행에서 일치하는 항목을 생성하지 않았습니다.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|%1에 잘못된 오류 또는 잘림 행 처리가 있습니다.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|행을 오류 출력에 전달하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|삽입을 위한 열 상태를 준비하지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|계보 ID가 %2!d!인 %1을(를) 데이터 흐름 태스크 버퍼에서 찾지 못했습니다(오류 코드 0x%3!8.8X!).|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|%1에서 특수하지 않은 오류 열을 찾지 못했습니다.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS 오류 코드 DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  오류 코드 0x%2!8.8X!이(가) 발생했기 때문에 "%1"이(가) 실패했으며 "%3"에서의 오류 행 처리는 오류 발생 시 실패하도록 지정되어 있습니다. 지정된 구성 요소의 해당 개체에서 오류가 발생했습니다.  오류에 대한 자세한 정보와 함께 이 오류 메시지보다 먼저 게시된 오류 메시지가 있을 수도 있습니다.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|잘림이 발생했기 때문에 "%1"이(가) 실패했으며 "%2"에서의 잘림 행 처리는 잘림 발생 시 실패하도록 지정되어 있습니다. 해당 구성 요소의 지정한 개체에서 잘림 오류가 발생했습니다.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|"%2"에서 식 "%1"이(가) NULL로 계산되었으나 "%2"에는 부울 결과가 필요합니다. 출력에서 오류 행 처리를 수정하여 이 결과를 False(오류 무시)로 처리하거나 이 행을 오류 출력으로 리디렉션하십시오(행 리디렉션).  조건부 분할에 대한 식 결과는 부울이어야 합니다.  NULL 식 결과는 오류입니다.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|식이 NULL로 계산되었으나 부울 결과가 필요합니다. 출력에서 오류 행 처리를 수정하여 이 결과를 False(오류 무시)로 처리하거나 이 행을 오류 출력으로 리디렉션하십시오(행 리디렉션). 조건부 분할에 대한 식 결과는 부울이어야 합니다.  NULL 식 결과는 오류입니다.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|UTF-16 Big Endian 파일 형식은 지원되지 않습니다.  UTF-16 Little Endian 형식만 지원됩니다.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|UTF-8 파일 형식은 유니코드로 지원되지 않습니다.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|ID 특성을 읽을 수 없습니다.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|두 개 이상의 조회 입력 열에서 캐시 인덱스 열 %1을(를) 참조합니다.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|조회 시 모든 캐시 연결 관리자 인덱스 열을 참조하는 것은 아닙니다. 조회 시 조인된 열 수: %1!d!. 인덱스 열 수: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 인해 데이터 값을 변환할 수 없습니다.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|데이터 값이 스키마 제약 조건을 위반했습니다.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|데이터가 잘렸습니다.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|데이터 값은 부호가 있고 공급자가 사용한 유형은 부호가 없기 때문에 변환에 실패했습니다.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|데이터 값이 공급자가 사용한 유형을 오버플로했기 때문에 변환에 실패했습니다.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|상태를 사용할 수 없습니다.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|열에 쓸 수 있는 올바른 권한이 사용자에게 없습니다.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|데이터 값이 열에 대한 무결성 제약 조건을 위반했습니다.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|상태를 사용할 수 없습니다.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 인해 데이터 값을 변환할 수 없습니다.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|데이터가 잘렸습니다.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|데이터 값은 부호가 있고 공급자가 사용한 유형은 부호가 없기 때문에 변환에 실패했습니다.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|데이터 값이 공급자가 사용한 유형을 오버플로했기 때문에 변환에 실패했습니다.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|데이터 값이 스키마 제약 조건을 위반했습니다.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 인해 데이터 값을 변환할 수 없습니다.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|데이터가 잘렸습니다.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|데이터 값은 부호가 있고 공급자가 사용한 유형은 부호가 없기 때문에 변환에 실패했습니다.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|데이터 값이 공급자가 사용한 유형을 오버플로했기 때문에 변환에 실패했습니다.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|상태를 사용할 수 없습니다.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|열에 쓸 수 있는 올바른 권한이 사용자에게 없습니다.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|데이터 값이 무결성 제약 조건을 위반했습니다.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 인해 데이터 값을 변환할 수 없습니다.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|데이터가 잘렸습니다.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|데이터 값은 부호가 있고 공급자가 사용한 유형은 부호가 없기 때문에 변환에 실패했습니다.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|데이터 값이 데이터 변환에 사용된 유형을 오버플로했기 때문에 변환에 실패했습니다.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|상태를 사용할 수 없습니다.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 인해 데이터 값을 변환할 수 없습니다.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|데이터가 잘렸습니다.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|데이터 값은 부호가 있고 플랫 파일 원본 어댑터에 사용된 유형은 부호가 없기 때문에 변환에 실패했습니다.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|데이터 값이 플랫 파일 원본 어댑터에 사용된 유형을 오버플로했기 때문에 변환에 실패했습니다.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|상태를 사용할 수 없습니다.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|파일 "%1"을(를) 읽기용으로 열지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|파일을 읽기용으로 열지 못했습니다.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|파일 "%1"을(를) 쓰기용으로 열지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|파일을 쓰기용으로 열지 못했습니다.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|파일에서 읽지 못했습니다.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|파일에 쓰지 못했습니다.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|배열 유형의 속성을 구문 분석할 때 너무 많은 배열 요소가 발견되었습니다. elementCount가 발견된 배열 요소 수보다 작습니다.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|배열 유형의 속성을 구문 분석할 때 너무 적은 배열 요소가 발견되었습니다. elementCount가 발견된 배열 요소 수보다 작습니다.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|파일 "%1"을(를) 쓰기용으로 열지 못했습니다. 파일을 찾을 수 없습니다.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|파일을 쓰기용으로 열지 못했습니다. 파일을 찾을 수 없습니다.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|파일 "%1"을(를) 쓰기용으로 열지 못했습니다. 경로를 찾을 수 없습니다.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|파일을 쓰기용으로 열지 못했습니다. 경로를 찾을 수 없습니다.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|파일 "%1"을(를) 쓰기용으로 열지 못했습니다. 너무 많은 파일이 열려 있습니다.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|파일을 쓰기용으로 열지 못했습니다. 너무 많은 파일이 열려 있습니다.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|파일 "%1"을(를) 쓰기용으로 열지 못했습니다. 올바른 권한이 없습니다.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|파일을 쓰기용으로 열지 못했습니다. 올바른 권한이 없습니다.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|파일 "%1"을(를) 쓰기용으로 열지 못했습니다. 파일이 있지만 덮어쓸 수 없습니다. AllowAppend 속성이 FALSE이고 ForceTruncate 속성이 FALSE이면 파일이 있을 경우에 이 오류가 발생합니다.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|파일을 쓰기용으로 열지 못했습니다. 파일이 이미 있지만 덮어쓸 수 없습니다. AllowAppend 속성과 ForceTruncate 속성이 모두 FALSE로 설정되면 파일이 있을 경우에 이 오류가 발생합니다.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|%2에서 사용자 지정 속성 "%1"의 값이 잘못되었습니다.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|열 "%1" 및 "%2"에 호환되지 않는 메타데이터가 있습니다.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|디스크가 꽉 찼기 때문에 파일 "%1"을(를) 쓰기용으로 열지 못했습니다. 이 파일을 저장하는 데 필요한 디스크 공간이 부족합니다.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|디스크가 꽉 찼기 때문에 파일을 쓰기용으로 열지 못했습니다.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|오류 0x%1!8.8X!(으)로 인해 정렬 키를 생성하지 못했습니다. ComparisonFlags가 활성화되었으며 LCMapString으로 정렬 키를 생성하지 못했습니다.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|변환에서 문자열을 매핑하지 못했으며 오류 0x%1!8.8X!이(가) 반환되었습니다. LCMapString이 실패했습니다.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|파일 "%1"을(를) 읽기용으로 열지 못했습니다. 파일을 찾을 수 없습니다.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|파일을 읽기용으로 열지 못했습니다. 파일을 찾을 수 없습니다.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|파일 "%1"을(를) 읽기용으로 열지 못했습니다. 경로를 찾을 수 없습니다.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|파일을 읽기용으로 열지 못했습니다. 경로를 찾을 수 없습니다.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|파일 "%1"을(를) 읽기용으로 열지 못했습니다. 너무 많은 파일이 열려 있습니다.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|파일을 읽기용으로 열지 못했습니다. 너무 많은 파일이 열려 있습니다.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|파일 "%1"을(를) 읽기용으로 열지 못했습니다. 액세스가 거부되었습니다.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|파일을 읽기용으로 열지 못했습니다. 올바른 권한이 없습니다.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|파일 "%1"에 대한 BOM(바이트 순서 표시) 값이 0x%2!4.4X!인데 필요한 값은 0x%3!4.4X!입니다. 이 파일에 대해 ExpectBOM 속성이 설정되었지만 파일에 BOM 값이 없거나 잘못되었습니다.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|파일에 대한 BOM(바이트 순서 표시) 값이 잘못되었습니다. 이 파일에 대해 ExpectBOM 속성이 설정되었지만 파일에 BOM 값이 없거나 잘못되었습니다.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|%1은(는) 구성 요소에 연결되지 않았습니다.  구성 요소가 연결되어야 합니다.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|사용자 지정 속성 %1의 값이 잘못되었습니다.  %2!d!에서 %3!I64d! 사이의 숫자여야 합니다.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|이 열에 대해 선택한 집계 유형에 사용자 지정 속성 "%1"을(를) 지정할 수 없습니다. 비교 플래그 사용자 지정 속성은 그룹화 및 고유 수 집계 유형에 대해서만 지정할 수 있습니다.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|비교 플래그 사용자 지정 속성 "%1"은(는) 데이터 형식이 DT_STR 또는 DT_WSTR인 열에 대해서만 지정할 수 있습니다.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|%1에서 집계가 실패했습니다(오류 코드 0x%2!8.8X!).|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|매핑을 설정하는 동안 오류가 발생했습니다. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|%1이(가) XML 데이터를 읽을 수 없습니다.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|%1이(가) "%2" 속성에 지정된 변수를 가져올 수 없습니다.|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|%1에 값이 %2이고 스키마의 데이터 테이블을 참조하지 않는 RowsetID가 있습니다.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|속성 %1은(는) 비어 있거나 %2!u!에서 %3!u! 사이의 숫자여야 합니다. Keys 또는 CountDistinctKeys 속성의 값이 잘못되었습니다. 이러한 속성은 0과 ULONG_MAX(포함) 사이의 숫자이거나 설정되지 않아야 합니다.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|집계 구성 요소에서 너무 많은 고유 키 조합이 발견되었습니다. 이 구성 요소는 %1!u!개 이상의 고유 키 값을 수용할 수 없습니다. 주 작업 영역에 ULONG_MAX개 이상의 고유 키 값이 있습니다.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|고유 수 집계를 계산하는 동안 집계 구성 요소에서 너무 많은 고유 값이 발견되었습니다. 이 구성 요소는 %1!u!개 이상의 고유 값을 수용할 수 없습니다. 고유 수 집계를 계산하는 동안 ULONG_MAX개 이상의 고유 값이 발견되었습니다.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|파일 이름 열에 쓰지 못했습니다(오류 코드 0x%1!8.8X!).|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|오류가 발생했지만 오류를 일으킨 열을 확인할 수 없습니다.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|조회 메타데이터를 버전 %1!d!에서 %2!d!(으)로 업그레이드할 수 없습니다. 조회 변환은 PerformUpgrade() 호출에서 메타데이터를 기존 버전 번호로부터 업그레이드하지 못했습니다.|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|문장의 끝 경계를 찾지 못했습니다.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|입력 텍스트의 문장이 너무 길기 때문에 용어 추출 변환에서 입력 텍스트를 처리할 수 없습니다. 문장은 여러 문장으로 조각화됩니다.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|%1이(가) XML 데이터를 읽을 수 없습니다. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|조회 변환 메서드 ReinitializeMetadata를 호출하지 못했습니다.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|조회 변환은 참조 열에 조인되는 입력 열을 적어도 하나 이상 포함해야 하는데 지정된 열이 없습니다. 적어도 하나 이상의 조인 열을 지정해야 합니다.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|관리되는 오류 인프라에 의해 게시되는 메시지 문자열에 잘못된 형식 지정이 있습니다. 이것은 내부 오류입니다.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|관리되는 오류 인프라를 사용하여 메시지 문자열의 형식을 지정하는 동안 형식 지원이 없는 변형 유형이 발견되었습니다. 이것은 내부 오류입니다.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|%1이(가) 데이터를 처리할 수 없습니다. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|%2에서 속성 "%1"이(가) 비어 있습니다.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|이름이 잘못되었기 때문에 경로가 "%2"인 XML 테이블에 대해 이름이 "%1"인 출력을 만들지 못했습니다.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|값이 너무 커서 %1에 맞지 않습니다.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|%1이(가) 데이터를 처리할 수 없습니다.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|잘림이 발생했기 때문에 "%1"이(가) 실패했으며 "%3"의 "%2"에서의 잘림 행 처리는 잘림 발생 시 실패하도록 지정되어 있습니다. 해당 구성 요소의 지정한 개체에서 잘림 오류가 발생했습니다.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|오류 코드 0x%2!8.8X!이(가) 발생했기 때문에 "%1"이(가) 실패했으며 "%3"에서의 오류 행 처리는 오류 발생 시 실패하도록 지정되어 있습니다. 지정된 구성 요소의 해당 개체에서 오류가 발생했습니다.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|SQLCE 대상에서 행에 대한 열 값을 설정할 수 없습니다.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|SQLCE 대상에서 행을 삽입할 수 없습니다.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|열 메타데이터를 로드하는 동안 OLEDB 오류가 발생했습니다.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|조회 참조 메타데이터에 너무 적은 열이 있습니다.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|열 메타데이터를 로드하는 동안 OLEDB 오류가 발생했습니다.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|조회 참조 메타데이터에 너무 적은 열이 있습니다.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|메모리를 할당할 수 없습니다.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|메모리를 할당할 수 없습니다.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|작업 영역 버퍼를 만들 수 없습니다.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|XML DOM 문서를 인스턴스화할 수 없습니다. MSXML 바이너리가 올바르게 설치 및 등록되었는지 확인하십시오.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|처리를 위해 XML 데이터를 로컬 DOM에 로드할 수 없습니다.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|런타임 변수 "%1"의 유형이 잘못되었습니다. 런타임 변수는 개체 유형이어야 합니다.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|XML 원본 어댑터가 XML 데이터를 처리할 수 없습니다. 다중 인라인 스키마는 지원되지 않습니다.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|XML 원본 어댑터가 XML 데이터를 처리할 수 없습니다. 요소 내용을 anyType으로 선언할 수 없습니다.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|XML 원본 어댑터가 XML 데이터를 처리할 수 없습니다. 요소 내용은 그룹에 대한 참조를 포함할 수 없습니다.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|XML 원본 어댑터가 복합 유형에 대해 혼합된 콘텐츠 모델을 지원하지 않습니다.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|XML 원본 어댑터가 XML 데이터를 처리할 수 없습니다. 인라인 스키마는 원본 XML에서 첫 번째 자식 노드여야 합니다.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|XML 원본 어댑터가 XML 데이터를 처리할 수 없습니다. 원본 XML에서 인라인 스키마를 찾을 수 없지만 "UseInlineSchema" 속성이 true로 설정되었습니다.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|빠른 로드 또는 대량 삽입에 대한 트랜잭션의 연결을 유지하는 연결 관리자를 구성 요소에서 사용할 수 없습니다.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|오류 발생 시에 트랜잭션의 연결을 사용하여 리디렉션하도록 %1을(를) 설정할 수 없습니다.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|%1에 해당 입력 열 또는 출력 열이 없습니다.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|파일에 쓸 열을 선택하지 않았습니다.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|%1의 데이터 형식이 잘못되었습니다. 데이터 형식이 DT_IMAGE, DT_TEXT 및 DT_NTEXT인 열을 원시 파일에 쓸 수 없습니다.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|이 구성 요소에서 외부 메타데이터 컬렉션을 잘못 사용했습니다. 구성 요소는 기존 파일을 추가하거나 자를 때 외부 메타데이터를 사용해야 합니다. 그렇지 않을 경우 외부 메타데이터가 필요하지 않습니다.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|id %2!d!의 외부 메타데이터 열에 %1이(가) 매핑됩니다. [쓰기 옵션] 값으로 [항상 만들기]를 선택한 경우에는 입력 열을 외부 메타데이터 열에 매핑하지 말아야 합니다.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|메타데이터를 읽기 위한 파일을 열 수 없습니다. 구성 요소에 이미 정의된 외부 메타데이터가 있는데 해당 파일이 없을 경우 "ValidateExternalMetadata" 속성을 "false"로 설정하면 런타임 시 파일이 생성됩니다.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|데이터 원본 열 "%1"에 대한 데이터 흐름 버퍼에서 LOB 데이터에 액세스하지 못했습니다(오류 코드 0x%2!8.8X!).|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|%1이(가) XML 데이터를 처리할 수 없습니다. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|XML 원본 어댑터가 XML 데이터를 처리할 수 없습니다.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|값 %1!d!이(가) 유효한 액세스 모드로 인식되지 않습니다.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|데이터 원본 열 "%1"에 대한 전체 메타데이터 정보를 사용할 수 없습니다.  데이터 원본에 열이 올바르게 정의되었는지 확인하십시오.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|사용자 이름 열, 패키지 이름 열, 태스크 이름 열 및 컴퓨터 이름 열의 길이만 변경할 수 있습니다.  다른 모든 감사 열 데이터 형식 정보는 읽기 전용입니다.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|OLE DB 공급자가 SQL 명령을 사용한 행 집합을 반환하지 않았습니다.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|커밋할 수 없습니다.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|%2의 사용자 지정 속성 "%1"은(는) ANSI 파일에만 사용할 수 있습니다.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|%2의 사용자 지정 속성 "%1"은(는) DT_BYTES에만 사용할 수 있습니다.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS 오류 코드 DTS_E_OLEDB_NOPROVIDER_ERROR.  요청한 OLE DB 공급자 %2이(가) 등록되지 않았습니다. 오류 코드: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS 오류 코드 DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  요청한 OLE DB 공급자 %2이(가) 등록되지 않았습니다. 64비트 공급자를 사용할 수 없습니다.  오류 코드: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|캐시 열 "%1"이(가) 두 개 이상의 열에 매핑되어 있습니다. 중복된 열 매핑을 제거하십시오.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|%1이(가) 올바른 캐시 열에 매핑되어 있지 않습니다.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|데이터 형식이 일치하지 않아 입력 열 "%1"과(와) 캐시 열 "%2"을(를) 매핑할 수 없습니다.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|입력 열의 수가 캐시 열의 수와 일치하지 않습니다.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|캐시 파일 이름이 제공되지 않았거나 올바르지 않습니다. 올바른 캐시 파일 이름을 제공하십시오.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|열의 인덱스 위치 "%1"이(가) 캐시 연결 관리자 열의 인덱스 위치 "%1"과(와) 다릅니다.|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|파일 "%1"에서 캐시를 로드하지 못했습니다.|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|조회 입력 열 %1이(가) 인덱스가 아닌 캐시 열 %2을(를) 참조합니다.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|연결 문자열을 가져오지 못했습니다.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|하나 이상의 데이터 형식 속성이 일치하지 않아 입력 열 "%1"과(와) 캐시 열 "%2"을(를) 매핑할 수 없습니다.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|캐시 열 "%1"이(가) 캐시에 없습니다.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|%1을(를) 캐시 열에 매핑하지 못했습니다. hresult는 0x%2!8.8X!입니다.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|%1이(가) 파일에서 캐시를 로드했으므로 캐시에 %2을(를) 쓸 수 없습니다.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|캐시가 이미 파일 "%3"에서 로드되었으므로 %1이(가) "%2" 파일에서 캐시를 로드할 수 없습니다.|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|집계 구성 요소의 ID가 %1!d!인 출력을 어느 구성 요소에서도 사용하지 않습니다. 이 출력을 제거하거나 특정 구성 요소의 입력과 연결하십시오.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1이(가) 파일 "%2"에 캐시를 쓰지 못했습니다. hresult는 0x%3!8.8X!입니다.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|요소 "%2"에서 "%1"에 대한 XML 스키마 데이터 형식 정보가 변경되었습니다.  이 구성 요소의 메타데이터를 다시 초기화하고 열 매핑을 검토하십시오.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1이(가) 조인 또는 복사에 사용되지 않았습니다. 입력 열 목록에서 사용하지 않은 열을 제거하십시오.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|들어오는 버퍼를 정렬하는 동안 스택 오버플로로 인해 정렬이 실패했습니다.  데이터 흐름 태스크의 DefaultBufferMaxRows 속성을 줄이십시오.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|연결 문자열에서 PROVIDER를 %1(으)로 변경하거나 https://www.microsoft.com/downloads를 방문하여 %2에 대한 지원을 찾아 설치합니다.|  
|||DTS_E_INITTASKOBJECTFAILED|0x%3!8.8X! "%4!s!" 오류로 인해 태스크 "%1!s!", 유형 "%2!s!"에 대한 태스크 개체를 초기화하지 없습니다.|  
|||DTS_E_GETCATMANAGERFAILED|0x%1!8.8X! "%2!s!" 오류로 인해 COM 구성 요소 범주 관리자를 만들지 못했습니다.|  
|||DTS_E_COMPONENTINITFAILED|0x%2!8.8X! " %3!s!" 오류로 인해 %1!s! 구성 요소를 초기화하지 반환되었습니다|  
  
##  <a name="msgWarning"></a> 경고 메시지  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 경고 메시지의 심볼 이름은 `DTS_W_`로 시작합니다.  
  
|16진수 코드|10진수 코드|심볼 이름|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|평가 기간이 %1!lu!일 남았습니다. 기간이 만료되면 패키지를 실행할 수 없습니다.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|경고가 발생했습니다. 이 경고는 다른 경고에 대한 세부 사항을 설명하며, 이 경고 이전에 더 구체적인 경고가 있습니다.|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|XML 문서 개체 인스턴스를 만들 수 없습니다. MSXML을 올바르게 설치하고 등록했는지 확인하십시오.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|XML 구성 파일을 로드할 수 없습니다. XML 구성 파일이 잘못된 형식이거나 유효하지 않을 수 있습니다.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|구성 파일 이름 "%1"이(가) 잘못되었습니다. 구성 파일 이름을 확인하십시오.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|구성 파일이 로드되었지만 유효하지 않습니다. 파일이 잘못된 형식이거나 요소가 없거나 손상되었을 수 있습니다.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|구성 파일 "%1"을(를) 찾을 수 없습니다. 디렉터리 및 파일 이름을 확인하십시오.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|구성 레지스트리 키 "%1"을(를) 찾을 수 없습니다. 사용할 수 없는 레지스트리 키가 구성 항목에 지정되어 있습니다. 레지스트리를 검사하여 키가 있는지 확인하십시오.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|구성 항목 중 하나에서 구성 유형이 잘못되었습니다. 올바른 유형은 DTSConfigurationType 열거에 나열되어 있습니다.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|패키지 경로에서 참조한 개체 "%1"을(를) 찾을 수 없습니다. 이 오류는 찾을 수 없는 개체에 대한 패키지 경로를 확인하려고 할 때 발생합니다.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|구성 항목 "%1"은(는) 패키지 구분 기호로 시작되지 않기 때문에 형식이 잘못되었습니다. 패키지 경로 앞에 "\package"를 추가하십시오.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|구성 항목 "%1"의 형식이 잘못되었습니다. 이 오류는 구분 기호가 없거나 잘못된 배열 구분 기호 등의 형식 오류가 있을 때 발생할 수 있습니다.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|부모 변수 컬렉션이 없기 때문에 부모 변수 "%1"에서 구성이 발생하지 않았습니다.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|구성 파일을 가져오는 동안 오류가 발생했습니다. "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|부모 변수가 없기 때문에 부모 변수 "%1"에서 구성이 발생하지 않았습니다. 오류 코드: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|구성 파일이 비어 있으며 구성 항목이 포함되지 않았습니다.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|구성 "%1"의 구성 유형이 잘못되었습니다. 이 오류는 구성 개체의 유형 속성을 잘못된 구성 유형으로 설정하려고 할 때 발생할 수 있습니다.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|레지스트리 구성에 대한 구성 유형을 키 "%1"에서 찾을 수 없습니다. ConfigType이라는 값을 레지스트리 키에 추가하고 "Variable", "Property", "ConnectionManager", "LoggingProvider" 또는 "ForEachEnumerator" 문자열 값을 지정하십시오.|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|레지스트리 구성에 대한 구성 값을 키 "%1"에서 찾을 수 없습니다. Value라는 값을 DWORD 또는 String 유형으로 레지스트리 키에 추가하십시오.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|프로세스 구성이 "%1"의 패키지 경로에서 대상을 설정하지 못했습니다. 이 오류는 대상 속성이나 변수를 설정할 수 없을 때 발생합니다. 대상 속성이나 변수를 확인하십시오.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|값을 .ini 파일에서 검색하지 못했습니다. ConfiguredValue 섹션이 비어 있거나 존재하지 않습니다: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|값을 .ini 파일에서 검색하지 못했습니다. ConfiguredType 섹션이 비어 있거나 존재하지 않습니다: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|값을 .ini 파일에서 검색하지 못했습니다. PackagePath 섹션이 비어 있거나 존재하지 않습니다: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|값을 .ini 파일에서 검색하지 못했습니다. ConfiguredValueType 섹션이 비어 있거나 존재하지 않습니다: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|SQL Server에서 구성을 가져오지 못했습니다. "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|필드가 비어 있거나 누락되어 .ini 구성 파일이 유효하지 않습니다.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|테이블 "%1"에 구성을 위한 레코드가 없습니다. 이 오류는 구성을 위한 레코드가 없는 SQL Server 테이블에서 구성을 수행할 때 발생합니다.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|서로 다른 사용자 지정 이벤트에 동일한 이름을 사용하는 오류가 발생했습니다. 사용자 지정 이벤트 "%1"이(가) 이 컨테이너의 다른 자식에 의해 다르게 정의되었습니다. 이벤트 처리기를 실행할 경우 오류가 발생할 수 있습니다.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|구성에서 읽기 전용 변수를 변경하려고 했습니다. 이 변수는 패키지 경로 "%1"에 있습니다.|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|패키지의 ProcessConfiguration을 호출하지 못했습니다. 구성에서 패키지 경로 "%1"의 속성을 변경하려고 했습니다.|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|패키지에 대한 구성 항목을 적어도 하나 이상 로드하지 못했습니다. "%1"에 대한 구성 항목과 이전 경고를 검사하여 실패한 구성에 대한 설명을 확인하십시오.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|구성 파일의 구성 항목 "%1"이(가) 잘못되었거나 변수를 구성하지 못했습니다.  이름은 실패한 항목을 나타냅니다. 일부 경우에는 이름을 사용할 수 없습니다.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|이 태스크 또는 컨테이너가 실패했지만 FailPackageOnFailure 속성이 FALSE이므로 패키지가 계속됩니다. 이 경고는 패키지의 SaveCheckpoints 속성이 TRUE로 설정되고 태스크나 컨테이너가 실패할 경우에 게시됩니다.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|경로가 비어 있습니다.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS 경고 코드 DTS_W_MAXIMUMERRORCOUNTREACHED.  실행 메서드가 성공했지만 발생한 오류 수(%1!d!)가 허용되는 최대값(%2!d!)에 도달했기 때문에 오류가 발생했습니다. 이 오류는 오류 수가 MaximumErrorCount에 지정된 수에 도달할 때 발생합니다. MaximumErrorCount를 변경하거나 오류를 수정하십시오.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|구성 환경 변수를 찾을 수 없습니다.  환경 변수는 "%1"이었습니다. 이 오류는 패키지가 구성 설정에 대한 환경 변수를 지정하지만 해당 변수를 찾을 수 없을 때 발생합니다. 패키지에서 구성 컬렉션을 검사하고 지정된 환경 변수가 사용 가능하고 유효한지 확인하십시오.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|연결 관리자 "%1"의 공급자 이름이 "%2"에서 "%3"(으)로 변경되었습니다.|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|업그레이드 매핑 파일을 읽는 동안 예외가 발생했습니다. 예외는 "%1"입니다.|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|파일 "%1"에 중복 매핑이 있습니다. 태그는 "%2"이고 키는 "%3"입니다.|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|확장 프로그램 "%1"이(가) 암시적으로 "%2"(으)로 업그레이드되었습니다. UpgradeMappings 디렉터리에 이 확장 프로그램에 대한 매핑을 추가하십시오.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|파일 "%1"의 매핑이 잘못되었습니다. 값은 Null이거나 비워 둘 수 없습니다. 태그는 "%2"이고 키는 "%3"이며 값은 "%4"입니다.|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|이전 버전과의 호환성을 위해 ADO 유형 연결 관리자 "%1"의 DataTypeCompatibility 속성이 80으로 설정되었습니다.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|For Each File 열거자가 비어 있습니다. For Each File 열거자가 파일 패턴과 일치하는 파일을 찾을 수 없거나 지정한 디렉터리가 비어 있습니다.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|패키지 "%1"의 개체에 대한 패키지 경로를 확인할 수 없습니다. 패키지 경로가 올바른지 확인하십시오.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|반복 식이 할당 식이 아닙니다: "%1". 이 오류는 일반적으로 ForLoop의 대입 식에 있는 식이 할당 식이 아닐 때 발생합니다.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|초기화 식이 할당 식이 아닙니다: "%1". 이 오류는 일반적으로 ForLoop의 반복 식에 있는 식이 대입 식이 아닐 때 발생합니다.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|실행 파일 "%1"을(를) 붙여 넣었지만 이 실행 파일에 연결된 로그 공급자를 컬렉션 "LogProviders"에서 찾을 수 없습니다.  로그 공급자 정보 없이 실행 파일을 붙여 넣었습니다.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|패키지를 업그레이드했습니다.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|"%1" ProgID는 더 이상 사용되지 않습니다. 대신 이 구성 요소 "%2"의 새 ProgID를 사용해야 합니다.|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|작업 "%1"이(가) 실패했습니다.|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|암호화 알고리즘 "%1"은(는) 약한 암호화를 사용합니다.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|태스크 "%1"을(를) 실행하지 못했습니다.|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|파일/프로세스 "%1"이(가) 경로에 없습니다.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|제목이 비어 있습니다.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|"받는 사람" 줄의 주소 형식이 잘못되었습니다. "\@" 기호가 없거나 잘못되었습니다.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|"보낸 사람" 줄의 주소 형식이 잘못되었습니다. "\@" 기호가 없거나 잘못되었습니다.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|두 XML 문서가 다릅니다.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD 유효성 검사에서는 XML 문서의 DOCTYPE 줄에 정의된 DTD 파일이 사용됩니다. 속성 "%1"에 할당된 문서는 사용되지 않습니다.|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|"%1"의 유효성을 검사하지 못했습니다.|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|전송 동작 값이 잘못되었습니다.  복사로 설정합니다.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|전송 메서드 값이 잘못되었습니다.  온라인 전송으로 설정합니다.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|다음 메시지와 함께 문제가 발생했습니다: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|오류 메시지 "%1"이(가) 대상 서버에 이미 있습니다.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|작업 "%1"이(가) 대상 서버에 이미 있습니다.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|작업 "%1"이(가) 대상에 이미 있으므로 이 작업의 전송을 건너뜁니다.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|대상 서버에서 작업 "%1"을(를) 덮어쓰고 있습니다.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|속성 "FailIfExists"의 지속형 열거 값이 잘못 변경되고 렌더링되었습니다. 기본값으로 다시 설정합니다.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|대상에서 로그인 "%1"을(를) 덮어쓰고 있습니다.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|저장 프로시저 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|규칙 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|테이블 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|뷰 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|사용자 정의 함수 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|기본값 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|사용자 정의 데이터 형식 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|파티션 함수 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|파티션 구성표 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|스키마 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|사용자 정의 집계 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|사용자 정의 형식 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|전송할 요소를 지정하지 않았습니다.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|로그인 "%1"이(가) 대상에 이미 있습니다.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|사용자 "%1"이(가) 대상에 이미 있습니다.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|실행 트리에 주기가 포함되어 있기 때문에 입력 열의 계보 ID에 대한 유효성 검사를 수행할 수 없습니다.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|DataFlow 태스크에 구성 요소가 없습니다. 구성 요소를 추가하거나 이 태스크를 제거하십시오.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|%1의 IsSorted 속성이 TRUE로 설정되어 있지만 출력 열의 모든 SortKeyPositions가 0으로 설정되어 있습니다.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|데이터 흐름 태스크 외부에서 해당 데이터를 볼 수 없으므로 원본 "%1"(%2!d!)을(를) 읽을 수 없습니다.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|출력 "%3"(%4!d!) 및 구성 요소 "%5"(%6!d!)의 출력 열 "%1"(%2!d!)은(는) 이후의 데이터 흐름 태스크에서 사용되지 않습니다. 사용되지 않는 이 출력 열을 제거하면 데이터 흐름 태스크 성능이 향상될 수 있습니다.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|구성 요소 "%1"(%2!d!)은(는) 해당 출력이 사용되지 않으며, 입력에 파생 작업이 없거나 입력이 다른 구성 요소의 출력에 연결되지 않기 때문에 데이터 흐름 태스크에서 제거되었습니다. 이 구성 요소가 필요한 경우에는 적어도 하나 이상의 해당 입력에서 HasSideEffects 속성을 true로 설정하거나 해당 출력을 다른 항목에 연결해야 합니다.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|행이 스레드에 제공되었지만 해당 스레드에 수행할 작업이 없습니다. 레이아웃에 연결이 끊어진 출력이 있습니다. RunInOptimizedMode 속성을 TRUE로 설정한 상태에서 파이프라인을 실행하면 속도가 더 빨라지며 이 경고가 발생하지 않습니다.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|%1에 대한 외부 열이 데이터 원본 열과 동기화되지 않았습니다. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|열 "%1"을(를) 외부 열에 추가해야 합니다.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|외부 열 "%1"을(를) 업데이트해야 합니다.|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|%1을(를) 외부 열에서 제거해야 합니다.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|식 "%1"의 결과 문자열이 최대 길이 %2!d!자를 초과할 경우 문자열이 잘릴 수 구성됩니다. 이 식은 DT_WSTR의 최대 크기를 초과하는 결과 값을 가질 수 있습니다.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|%2의 입력 %1!d!에 대한 ProcessInput 메서드 호출에서 이전에 전달된 버퍼 참조를 유지하고 있습니다. 해당 버퍼에 대한 refcount는 호출 전에는 %3!d!이고 호출이 반환된 후에는 %4!d!입니다.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|"%2"의 "%1"은(는) 사용 유형이 READONLY이지만 식에서 참조하지 않습니다. 사용 가능한 입력 열 목록에서 해당 열을 제거하거나 식에서 참조하십시오.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|구성 요소 %2에 대한 "%1" 값을 찾을 수 없습니다. 이 구성 요소에 대한 CurrentVersion 값을 찾을 수 없습니다. 이 오류는 DTSInfo 섹션에 CurrentVersion 값을 포함하도록 구성 요소가 해당 레지스트리 정보를 설정하지 않을 때 발생합니다. 이 메시지는 특정 구성 요소를 개발 중이거나 구성 요소가 패키지에서 사용될 때, 해당 구성 요소가 올바르게 등록되지 않은 경우에 발생합니다.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|버퍼 관리자가 임시 파일 이름을 가져올 수 없습니다.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|버퍼 관리자가 경로 "%1"에서 임시 파일을 만들 수 없습니다. 이 경로는 임시 스토리지용으로 다시 사용되지 않습니다.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|경고: 성능 DLL로 통신하기 위해 전역 공유 메모리를 열 수 없으므로 데이터 흐름 성능 카운터를 사용할 수 없습니다.  이 문제를 해결하려면 관리자 권한으로 또는 시스템의 콘솔에서 이 패키지를 실행하십시오.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|파일의 끝에 부분 행이 있습니다.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|머리글 행을 읽는 동안 데이터 파일의 끝에 도달했습니다. 머리글 행 구분 기호와 건너뛸 머리글 행 수가 올바른지 확인하십시오.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|OLE DB 공급자에서 열 코드 페이지 정보를 검색할 수 없습니다.  구성 요소가 "%1" 속성을 지원하는 경우 해당 속성의 코드 페이지가 사용됩니다.  현재 문자열 코드 페이지 값이 잘못된 경우 해당 속성의 값을 변경하십시오.  구성 요소가 이 속성을 지원하지 않으면 구성 요소 로캘 ID의 코드 페이지가 사용됩니다.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|데이터가 이미 지정된 대로 정렬되었으므로 변환을 제거할 수 있습니다.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1이(가) 데이터 흐름 태스크의 데이터 형식으로 매핑할 수 없는 외부 데이터 형식을 참조합니다. 데이터 흐름 태스크의 데이터 형식 DT_WSTR이 대신 사용됩니다.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|식 "%1"을(를) 사용하면 항상 데이터가 잘립니다. 이 식에는 정적 잘림(고정 값 잘림)이 포함되어 있습니다.|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|인덱스 %3!d!에서 ID가 %2!d!인 입력 열 "%1"이(가) 매핑되지 않았습니다. 이 열의 계보 ID가 0입니다.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|지정한 구분 기호가 기존의 일치하는 인덱스 "%1"을(를) 작성하는 데 사용되는 구분 기호와 일치하지 않습니다. 이 오류는 필드를 토큰화하는 데 사용되는 구분 기호가 일치하지 않을 때 발생합니다. 이 오류는 일치 동작이나 결과에 알 수 없는 영향을 줄 수 있습니다.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|유사 항목 조회 변환의 MaxOutputMatchesPerInput 속성이 0입니다. 결과가 생성되지 않습니다.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|JoinType 열 속성이 Fuzzy로 설정된 올바른 입력 열이 없습니다.  FuzzyLookup 대신 조회 변환을 사용하여 정확히 조인의 성능을 향상시킬 수 있습니다.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|참조 열 "%1"이(가) SQL 타임스탬프 열일 수 있습니다. 유사 항목 일치 인덱스가 작성되고 참조 테이블 복사본이 생성되면 모든 참조 테이블 타임스탬프는 복사 시점의 현재 테이블 상태를 반영합니다. CopyReferenceTable이 false로 설정된 경우 예기치 않은 동작이 발생할 수 있습니다.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|MatchIndexName에 '%1' 테이블이 이미 지정되었고 DropExistingMatchIndex가 FALSE로 설정되었습니다.  이 테이블을 삭제하지 않거나 다른 이름을 지정하지 않거나 DropExisitingMatchIndex를 TRUE로 설정하지 않으면 변환을 실행할 수 없습니다.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|입력 열 '%1'의 길이가 대응시키려는 참조 열 '%2'의 길이와 다릅니다.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|DT_STR 원본 열 "%1" 및 DT_STR 대상 열 "%2"의 코드 페이지가 일치하지 않습니다.  이로 인해 예기치 않은 결과가 발생할 수 있습니다.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|정확히 일치 조인이 17개 이상이기 때문에 성능이 최적이 아닐 수 있습니다. 성능을 향상시키려면 정확히 일치 조인 수를 줄이십시오. SQL Server에서는 인덱스당 열 수가 16개로 제한되며 반전된 인덱스가 모든 조회에 사용됩니다.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|Exhaustive 옵션을 사용하려면 전체 참조를 주 메모리에 로드해야 합니다.  MaxMemoryUsage 속성에 대해 메모리 제한이 지정되었으므로 전체 참조 테이블이 이 바운드 내에 맞지 않을 수 있으며 런타임 시 일치 작업이 실패할 수 있습니다.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|정확히 일치 조인에 지정된 열의 누적 길이가 인덱스 키에 대한 900바이트 제한을 초과합니다.  유사 항목 조회는 조회 성능을 향상시키기 위해 정확히 일치 열에서 인덱스를 만듭니다. 이 경우 이러한 인덱스 생성은 실패할 가능성이 있으며, 실패할 경우 일치하는 항목을 찾기 위해 더 느린 대체 방법이 조회에 사용됩니다. 성능이 문제일 경우에는 정확히 일치 조인 열을 일부 제거하거나 가변 길이 정확히 일치 열의 최대 길이를 줄이십시오.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|정확히 일치 열에 대한 인덱스를 만들지 못했습니다. 대체 유사 항목 조회 방법으로 되돌리고 있습니다.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|다음과 같은 경고 코드 0x%1!8.8X!의 유사 항목 그룹화 내부 파이프라인 경고가 발생했습니다: "%2"|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|외부 데이터 형식 %2의 %1에 대해 최대 길이가 지정되지 않았습니다. 길이가 %4!d!인 SSIS 데이터 흐름 태스크 데이터 형식 "%3"이(가) 사용됩니다.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|%1이(가) SSIS 데이터 흐름 태스크의 데이터 형식으로 매핑할 수 없는 외부 데이터 형식 %2을(를) 참조합니다.  길이가 %3!d!인 SSIS 데이터 흐름 태스크의 데이터 형식 DT_WSTR이 대신 사용됩니다.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|오류 출력으로 전송된 행이 없습니다. 행을 오류 출력으로 리디렉션하도록 오류 또는 잘림 처리를 구성하거나 오류 출력에 연결된 데이터 흐름 변환 또는 대상을 삭제하십시오.|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|오류 출력으로 전송된 행이 손실됩니다. 오류 행을 받도록 새 데이터 흐름 변환 또는 대상을 추가하거나 오류 출력으로의 행 리디렉션을 중지하도록 구성 요소를 다시 구성하십시오.|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|외부 데이터 형식 %2의 %1에 대해, XML 스키마가 최대 허용 열 길이 %4!d!을(를) 초과하는 %3!d!의 maxLength 제약 조건을 지정합니다. 길이가 %6!d!인 SSIS 데이터 흐름 태스크 데이터 형식 "%5"이(가) 사용됩니다.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|참조 데이터를 캐시할 때 %1에 중복된 참조 키 값이 발생했습니다. 이 오류는 전체 캐시 모드에서만 발생합니다. 중복된 키 값을 제거하거나 캐시 모드를 PARTIAL 또는 NO_CACHE로 변경하십시오.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|길이가 %2!d!인 데이터 흐름 열 "%1"에서 길이가 %4!d!인 데이터베이스 열 "%3"(으)로 데이터를 삽입하기 때문에 데이터가 잘릴 수 있습니다.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|길이가 %2!d!인 데이터베이스 열 "%1"에서 길이가 %4!d!인 데이터 흐름 열 "%3"(으)로 데이터를 가져오기 때문에 데이터가 잘릴 수 있습니다.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|오류 행 처리를 사용하는 경우 현재 배치 모드가 지원되지 않습니다. BatchSize 속성이 1로 설정됩니다.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|대상에 행이 삽입되지 않았습니다. 열 간의 데이터 형식이 일치하지 않거나 ADO.NET 공급자가 지원하지 않는 데이터 형식이 사용되었기 때문일 수 있습니다. 이 구성 요소의 오류 처리가 "구성 요소 실패"가 아니므로 오류 메시지가 여기에 표시되지 않습니다. 오류 메시지를 여기에 표시하려면 오류 처리를 "구성 요소 실패"로 설정하십시오.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|데이터 형식이 "%2"인 입력 열 "%1"에서 데이터 형식이 "%4"인 외부 열 "%3"(으)로 데이터를 삽입하면 데이터가 손실될 수 있습니다. 이 방법 대신 ADO.NET 대상 구성 요소를 실행하기 전에 데이터 변환 구성 요소를 사용하여 변환을 수행할 수 있습니다.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|%1이(가) 데이터베이스 열과 동기화되지 않았습니다.  최신 열에 %2이(가) 있습니다. 필요하면 고급 편집기를 사용하여 사용 가능한 대상 열을 새로 고치십시오.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|%1이(가) 데이터베이스에 없습니다. 제거되었거나 이름이 바뀌었을 수 있습니다. 필요하면 고급 편집기를 사용하여 사용 가능한 대상 열을 새로 고치십시오.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|이름이 %1인 새 열이 외부 데이터베이스 테이블에 추가되었습니다. 필요하면 고급 편집기를 사용하여 사용 가능한 대상 열을 새로 고치십시오.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|불일치 항목 출력으로 보낼 행이 없습니다. 일치하는 항목이 없는 행을 불일치 항목 출력으로 리디렉션하도록 변환을 구성하거나, 불일치 항목 출력에 연결되어 있는 데이터 흐름 변환 또는 대상을 삭제하십시오.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|ADO.Net 공급자를 열거하는 동안 예외가 수신되었습니다. 고정: "%1". 예외 메시지: "%2".|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|매핑되는 입력 열이 %1에 없습니다.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|테이블 "%1"이(가) 변경되었습니다. 이 테이블에 새 열이 추가되었을 수 있습니다.|  
  
##  <a name="msgInfo"></a> 정보 메시지  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 정보 메시지의 심볼 이름은 `DTS_I_`로 시작합니다.  
  
|16진수 코드|10진수 코드|심볼 이름|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|이 컨테이너에 대한 분산 트랜잭션을 시작하고 있습니다.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|이 컨테이너에 의해 시작된 분산 트랜잭션을 커밋하고 있습니다.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|현재 분산 트랜잭션을 중단합니다.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|뮤텍스 "%1"을(를) 가져왔습니다.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|뮤텍스 "%1"을(를) 해제했습니다.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|뮤텍스 "%1"을(를) 만들었습니다.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|모든 오류 이벤트에 대해 디버그 덤프 파일이 생성됩니다.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|다음 이벤트 코드에 대해 디버그 덤프 파일이 생성됩니다. "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|이벤트 코드 0x%1!8.8X!이(가) 폴더 "%2"에 대한 디버그 덤프 파일 생성 작업을 트리거했습니다.|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|SSIS 정보 덤프 파일 "%1"을(를) 만들고 있습니다.|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|디버그 덤프 파일을 만들었습니다.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|패키지 형식을 버전 %1!d!에서 마이그레이션했습니다. 마이그레이션 변경 내용을 유지하려면 패키지를 저장해야 합니다.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|패키지의 스크립트를 마이그레이션했습니다. 마이그레이션 변경 내용을 유지하려면 패키지를 저장해야 합니다.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|파일 "%1"을(를) 받고 있습니다.|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|파일 "%1"을(를) 보내고 있습니다.|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|파일 "%1"이(가) 이미 있습니다.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|내부 오류로 인해 추가 오류 정보를 가져올 수 없습니다.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|파일 "%1"을(를) 삭제하지 못했습니다. 이 오류는 파일이 없거나 파일 이름의 철자가 잘못되었거나 파일을 삭제할 수 있는 권한이 없을 때 발생합니다.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|레지스트리 키 "%1"을(를) 사용하여 레지스트리 항목에서 패키지를 구성하려고 합니다.|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|환경 변수 "%1"에서 패키지를 구성하려고 합니다.|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|.ini 파일 "%1"에서 패키지를 구성하려고 합니다.|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|구성 문자열 "%1"을(를) 사용하여 SQL Server에서 패키지를 구성하려고 합니다.|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|XML 파일 "%1"에서 패키지를 구성하려고 합니다.|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|부모 변수 "%1"에서 패키지를 구성하려고 합니다.|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|SSIS를 버전 "%1"에서 버전"%2"(으)로 업그레이드하려고 합니다. 패키지에서 런타임을 업그레이드하려고 합니다.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|"%1"을(를) 업그레이드하려고 합니다. 패키지에서 확장 가능한 개체를 업그레이드하려고 합니다.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|패키지에서 실행 중에 검사점을 파일 "%1"에 저장합니다. 패키지는 검사점을 저장하도록 구성되었습니다.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|패키지가 검사점 파일 "%1"에서 다시 시작되었습니다. 패키지는 검사점에서 다시 시작되도록 구성되었습니다.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|이 컨테이너의 완료를 기록하기 위해 검사점 파일 "%1"이(가) 업데이트되었습니다.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|패키지를 성공적으로 완료한 후에 검사점 파일 "%1"이(가) 삭제되었습니다.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|검사점 파일 "%1" 업데이트를 시작합니다.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|시스템 구성에 따라 최대 동시 실행 파일 수가 %1!d!개로 설정되었습니다.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|최대 동시 실행 파일 수가 %1!d!개로 설정되었습니다.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|패키지 실행의 시작입니다.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|패키지 실행의 끝입니다.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|디렉터리 "%1"이(가) 삭제되었습니다.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|파일 또는 디렉터리 "%1"이(가) 삭제되었습니다.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|대상 서버 "%2"에서 데이터베이스 "%1"을(를) 덮어쓰고 있습니다.|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|오류 메시지 "%1"이(가) 대상 서버에 이미 있으므로 건너뜁니다.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1"개의 오류 메시지를 전송했습니다.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|"%1"개의 저장 프로시저를 전송했습니다.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|"%1"개의 개체를 전송했습니다.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|전송할 저장 프로시저가 없습니다.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|전송할 규칙이 없습니다.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|전송할 테이블이 없습니다.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|전송할 뷰가 없습니다.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|전송할 사용자 정의 함수가 없습니다.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|전송할 기본값이 없습니다.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|전송할 사용자 정의 데이터 형식이 없습니다.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|전송할 파티션 함수가 없습니다.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|전송할 파티션 구성표가 없습니다.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|전송할 스키마가 없습니다.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|전송할 SqlAssemblies가 없습니다.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|전송할 사용자 정의 집계가 없습니다.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|전송할 사용자 정의 형식이 없습니다.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|전송할 XmlSchemaCollections가 없습니다.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|전송할 로그인이 없습니다.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|전송할 사용자가 없습니다.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|테이블 "%1"을(를) 잘라내는 중|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|실행 준비 단계를 시작하고 있습니다.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|실행 전 단계를 시작하고 있습니다.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|실행 후 단계를 시작하고 있습니다.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|정리 단계를 시작하고 있습니다.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|유효성 검사 단계를 시작하고 있습니다.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1"이(가) %2!ld!개의 행을 캐시했습니다.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|실행 단계를 시작하고 있습니다.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|시스템에 가상 메모리가 부족하지만 어떠한 버퍼도 스왑할 수 없음이 버퍼 관리자에서 확인되었습니다. %1!d!의 버퍼가 고려되었으며 %2!d!개의 버퍼가 잠겼습니다. 설치된 메모리가 부족하기 때문에 파이프라인에 사용할 수 있는 메모리가 부족하거나 다른 프로세스에서 메모리를 사용 중이거나 너무 많은 버퍼가 잠겼습니다.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|버퍼 관리자에서 %3!d!바이트에 대한 메모리 할당을 호출하지 못했지만 메모리 가중을 줄이기 위해 어떠한 버퍼도 스왑하지 못했습니다. %1!d!의 버퍼가 고려되었으며 %2!d!개의 버퍼가 잠겼습니다. 설치된 메모리가 부족하기 때문에 파이프라인에 사용할 수 있는 메모리가 부족하거나 다른 프로세스에서 메모리를 사용 중이거나 너무 많은 버퍼가 잠겼습니다.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|메모리 가중이 검색되고 버퍼를 스왑하려는 시도가 여러 번 실패했지만 버퍼 관리자가 %1!d!바이트를 할당했습니다.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1이(가) %2!d!개의 행을 캐시했습니다.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1이(가) 총 %2!d!개의 행을 캐시했습니다.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|원시 원본 어댑터에서 파일을 열었지만 파일에 열이 없습니다. 어댑터는 데이터를 생성하지 않습니다. 이는 파일이 손상되었거나 0열이 있기 때문에 데이터가 없다는 것을 나타냅니다.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|OLE DB 정보 메시지를 사용할 수 있습니다.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|입력 열 "%1"에서 정확히 조인 FuzzyComparisonFlags를 참조 테이블 열 "%2"에 대한 기본 SQL 데이터 정렬과 일치하도록 설정할 경우 유사 일치 성능이 향상될 수 있습니다.  또한 FuzzyComparisonFlagsEx에서 fold 플래그를 설정하지 않아야 합니다.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|참조 테이블에 지정된 모든 정확히 일치 열에 대한 인덱스를 만들 경우 유사 일치 성능이 향상될 수 있습니다.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|오류 및 잘림 처리를 검토하지 않았습니다. 해당 행을 더 변환하려면 이 구성 요소가 행을 오류 출력으로 리디렉션하도록 구성되었는지 확인하십시오.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|집계 변환에서 %1!d!개의 키 조합이 발견되었습니다. 키 조합 수가 예상보다 많기 때문에 데이터를 다시 해시해야 합니다. Keys, KeyScale 및 AutoExtendFactor 속성을 조정하여 데이터를 다시 해시하지 않도록 구성 요소를 구성할 수 있습니다.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|집계 변환에서 %1!d!개의 키 조합이 발견되었습니다. 고유 값 수가 예상보다 많기 때문에 변환 중에 데이터가 다시 해시됩니다. CountDistinctKeys, CountDistinctKeyScale 및 AutoExtendFactor 속성을 조정하여 데이터를 다시 해시하지 않도록 구성 요소를 구성할 수 있습니다.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|파일 "%1"의 처리를 시작했습니다.|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|파일 "%1"의 처리를 마쳤습니다.|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|파일 "%1"에 대해 처리된 총 데이터 행 수는 %2!I64d!개입니다.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|"%1"에서 데이터 삽입을 위한 마지막 커밋을 시작했습니다.|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|"%1"에서 데이터 삽입을 위한 마지막 커밋을 마쳤습니다.|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|캐시에 행이 %1!u!개 추가되었습니다. 시스템에서 해당 행을 처리하고 있습니다.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|%1이(가) 캐시에서 행 %2!u!개를 처리했습니다. 처리 시간은 %3초이고 캐시에서 사용한 메모리는 %4!I64u!바이트입니다.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|%1이(가) 캐시의 행을 처리하지 못했습니다.  처리 시간은 %2초입니다.|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|%1이(가) 캐시를 준비했습니다. 준비 시간은 %2초입니다.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1에서 다음 작업을 수행했습니다. %2!I64u!행을 처리했고 참조 데이터베이스에 대해 데이터베이스 명령 %3!I64u!개를 실행했으며, 부분 캐시를 사용하여 조회를 %4!I64u!개 수행했습니다.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1에서 다음 작업을 수행했습니다. %2!I64u!행을 처리했고 참조 데이터베이스에 대해 데이터베이스 명령 %3!I64u!개를 실행했으며, 부분 캐시를 사용하여 조회를 %4!I64u!개 수행했고, 초기 조회 시 일치하는 항목이 없는 행에 대해 캐시를 사용하여 조회를 %5!I64u!개 수행했습니다.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1이(가) 파일 "%2"에 캐시를 기록하고 있습니다.|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1이(가) 파일 "%2"에 캐시를 기록했습니다.|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|OLE DB 대상 "%1"의 최대 삽입 커밋 크기 속성이 0으로 설정되어 있습니다. 이 속성 설정으로 인해 실행 중인 패키지의 작동이 중지될 수 있습니다. 자세한 내용은 F1 도움말 항목의 OLE DB 대상 편집기(연결 관리자 페이지)를 참조하십시오.|  
  
##  <a name="msgGeneral"></a> 일반 및 이벤트 메시지  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 메시지의 심볼 이름은 `DTS_MSG_`로 시작합니다.  
  
|16진수 코드|10진수 코드|심볼 이름|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|잘못된 함수입니다.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|시스템에서 지정한 파일을 찾을 수 없습니다.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Microsoft SSIS 서비스를 시작하고 있습니다.<br /><br /> 서버 버전 %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS 서비스가 시작되었습니다.<br /><br /> 서버 버전 %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|대기 작업의 시간이 초과되었습니다.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|사용 가능한 데이터가 더 이상 없습니다.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS 서비스를 시작하지 못했습니다.<br /><br /> 오류: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Microsoft SSIS 서비스를 중지하는 동안 오류가 발생했습니다.<br /><br /> 오류: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS 서비스 구성 파일이 없습니다.<br /><br /> 기본 설정을 사용하여 로드하고 있습니다.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS 서비스 구성 파일이 잘못되었습니다.<br /><br /> 구성 파일을 읽는 동안 오류가 발생했습니다. %1<br /><br /> 기본 설정을 사용하여 서버를 로드하고 있습니다.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS 서비스:<br /><br /> 구성 파일을 지정하는 레지스트리 설정이 없습니다.<br /><br /> 기본 구성 파일을 로드하려고 합니다.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS 서비스: 패키지 실행을 중지하고 있습니다.<br /><br /> 패키지 인스턴스 ID: %1<br /><br /> 패키지 ID: %2<br /><br /> 패키지 이름: %3<br /><br /> 패키지 설명: %4<br /><br /> 패키지 시작자: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|패키지 "%1"이(가) 시작되었습니다.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|패키지 "%1"이(가) 성공적으로 완료되었습니다.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|패키지 "%1"이(가) 취소되었습니다.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|패키지 "%1"이(가) 실패했습니다.|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|오류 %4(으)로 인해 모듈 %1이(가) 진입점 %3을(를) 호출하기 위해 DLL %2을(를) 로드할 수 없습니다. 이 제품을 실행하려면 해당 DLL이 필요하지만 경로에서 DLL을 찾을 수 없습니다.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|모듈 %1이(가) DLL %2을(를) 로드했지만 오류 %4(으)로 인해 진입점 %3을(를) 찾을 수 없습니다. 명명된 DLL을 경로에서 찾을 수 없으며 이 제품을 실행하려면 해당 DLL이 필요합니다.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|이벤트 이름: %1<br /><br /> 메시지: %9<br /><br /> 연산자: %2<br /><br /> 원본 이름: %3<br /><br /> 원본 ID: %4<br /><br /> 실행 ID: %5<br /><br /> 시작 시간: %6<br /><br /> 종료 시간: %7<br /><br /> 데이터 코드: %8|  
  
##  <a name="msgSuccess"></a> Success Messages  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 성공 메시지의 심볼 이름은 `DTS_S_`로 시작합니다.  
  
|16진수 코드|10진수 코드|심볼 이름|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|값이 NULL입니다.|  
|0x40005|262149|DTS_S_TRUNCATED|문자열 값이 잘렸습니다. 너무 길어서 열에 맞지 않는 문자열을 버퍼에서 받았으며 문자열이 버퍼에 의해 잘렸습니다.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|식을 계산하는 동안 잘림이 발생했습니다. 계산 중에 잘림이 발생하면 중간 단계에 임의 지점이 포함될 수 있습니다.|  
  
##  <a name="msgPipeline"></a> 데이터 흐름 구성 요소 오류 메시지  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 메시지의 심볼 이름은 `DTSBC_E_`로 시작합니다. 여기서 "BC"는 대부분의 Microsoft 데이터 흐름 구성 요소가 파생되는 네이티브 기본 클래스를 나타냅니다.  
  
|16진수 코드|10진수 코드|심볼 이름|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|출력 및 오류 출력의 총 수인 %1!lu!이(가) 잘못되었습니다. 정확하게 %2!lu!개가 있어야 합니다.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|인덱스 %1!lu!(으)로 출력을 검색할 수 없습니다.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|오류 출력 수인 %1!lu!이(가) 잘못되었습니다. 정확하게 %2!lu!개가 있어야 합니다.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|유효성 검사 상태 값 "%1!lu!"이(가) "에 지원되지 않는 데이터 형식이 있습니다.  DTSValidationStatus 열거에 있는 값 중 하나여야 합니다.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|입력 "%1!lu!"에 동기 오류 출력이 없습니다.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|입력 "%1!lu!"에 동기 오류 출력이 없습니다.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|HowToProcessInput 값 %1!lu!이(가) 잘못되었습니다. HowToProcessInput 열거에 있는 값 중 하나여야 합니다.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|행 “%1!ld!”, 열 “%2!ld!”에 대한 정보를 버퍼에서 가져오지 못했습니다.  반환된 오류 코드는 0x%3!8.8X!입니다.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|행 “%1!ld!”, 열 “%2!ld!”에 대한 정보를 버퍼에 설정하지 못했습니다.  반환된 오류 코드는 0x%3!8.8X!입니다.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|속성 "%1"이(가) 잘못되었습니다.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|속성 "%1"을(를) 찾을 수 없습니다.|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|값을 읽기 전용 속성 "%1"에 할당하는 동안 오류가 발생했습니다.|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|"%1"에서는 출력 열을 삽입할 수 없습니다.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|출력 열의 메타데이터가 연결된 입력 열의 메타데이터와 일치하지 않습니다.  출력 열의 메타데이터가 업데이트됩니다.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|연결된 출력 열이 없는 입력 열이 있습니다. 출력 열이 추가됩니다.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|연결된 입력 열이 없는 출력 열이 있습니다. 출력 열이 제거됩니다.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|출력 열의 메타데이터가 연결된 입력 열의 메타데이터와 일치하지 않습니다.  입력 열이 매핑 해제됩니다.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|연결된 출력 열이 없는 입력 열이 있습니다. 입력 열이 매핑 해제됩니다.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|출력 열과 연결된 입력 열이 있으며 해당 출력 열은 이미 동일한 입력의 다른 입력 열과 연결되어 있습니다.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|%1에서는 외부 메타데이터 열을 삽입할 수 없습니다.|  
  
  
