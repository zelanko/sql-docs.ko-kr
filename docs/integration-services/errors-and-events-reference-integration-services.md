---
title: 오류 및 이벤트 참조(Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- events [Integration Services]
- errors [Integration Services]
- Integration Services, errors
ms.assetid: cf4f0f14-8087-42d7-9b67-e4929228abd6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 64e805e5dd9b334afe252e2c1d43685e9c92b95f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71290619"
---
# <a name="errors-and-events-reference-integration-services"></a>오류 및 이벤트 참조(Integration Services)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  설명서의 이 섹션에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]와 관련된 몇 가지 오류와 이벤트에 대한 정보가 포함되어 있습니다. 또한 오류 메시지의 원인 및 해결 방법 정보도 포함되어 있습니다.  
  
 가장 흔히 발생하는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 목록 및 해당 오류에 대한 설명을 비롯하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 메시지에 대한 자세한 내용은 [Integration Services 오류 및 메시지 참조](../integration-services/integration-services-error-and-message-reference.md)를 참조하세요. 그러나 현재 목록에는 문제 해결 정보가 포함되어 있지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 작업할 때 볼 수 있는 오류 메시지 중 상당수가 다른 구성 요소의 메시지입니다. 여기에는 OLE DB Provider, 다른 데이터베이스 구성 요소(예: [!INCLUDE[ssDE](../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ) 또는 다른 서비스나 구성 요소(예: 파일 시스템, SMTP 서버 또는 Microsoft Message Queueing)가 포함됩니다. 이러한 외부 오류 메시지에 대한 자세한 내용은 해당 구성 요소의 설명서를 참조하십시오.  
  
## <a name="error-messages"></a>오류 메시지  
  
|오류의 심볼 이름|Description|  
|----------------------------|-----------------|  
|DTS_E_CACHELOADEDFROMFILE|캐시 변환이 메모리 내 캐시에 데이터를 쓰려고 하고 있기 때문에 패키지를 실행할 수 없음을 나타냅니다. 그러나 캐시 연결 관리자가 메모리 내 캐시에 캐시 파일을 이미 로드했습니다.|  
|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|지정한 연결이 실패하여 패키지를 실행할 수 없음을 나타냅니다.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|데이터 흐름 구성 요소가 해당 열에 비유니코드 문자열 데이터를 필요로 하는 다른 구성 요소에 유니코드 문자열 데이터를 전달하거나 그 반대 작업을 시도하고 있음을 나타냅니다.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|데이터 흐름 구성 요소가 해당 열에 비유니코드 문자열 데이터를 필요로 하는 다른 구성 요소에 유니코드 문자열 데이터를 전달하거나 그 반대 작업을 시도하고 있음을 나타냅니다.|  
|DTS_E_CANTINSERTCOLUMNTYPE|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 열 데이터 형식과 데이터베이스 열 데이터 형식 간의 변환이 지원되지 않으므로 데이터베이스 테이블에 열을 추가할 수 없음을 나타냅니다.|  
|DTS_E_CONNECTIONNOTFOUND|지정한 연결 관리자를 찾을 수 없어서 패키지를 실행할 수 없음을 나타냅니다.|  
|DTS_E_CONNECTIONREQUIREDFORMETADATA|[!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 원본이나 대상에 대한 새 메타데이터 또는 업데이트된 메타데이터를 검색하기 위해 데이터 원본에 연결해야 하지만 해당 데이터 원본에 연결할 수 없음을 나타냅니다.|  
|DTS_E_MULTIPLECACHEWRITES|캐시 변환이 메모리 내 캐시에 데이터를 쓰려고 하고 있기 때문에 패키지를 실행할 수 없음을 나타냅니다. 그러나 다른 캐시 변환이 메모리 내 캐시에 데이터를 이미 썼습니다.|  
|DTS_E_PRODUCTLEVELTOLOW|적절한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 버전이 설치되어 있지 않으므로 패키지를 실행할 수 없음을 나타냅니다.|  
|DTS_E_READNOTFILLEDCACHE|캐시 변환이 메모리 내 캐시에 데이터를 쓰는 동안 조회 변환이 메모리 내 캐시에서 데이터를 읽으려고 하고 있음을 나타냅니다.|  
|DTS_E_UNPROTECTXMLFAILED|시스템에서 보호된 XML 노드를 해독하지 않았음을 나타냅니다.|  
|DTS_E_WRITEWHILECACHEINUSE|조회 변환이 메모리 내 캐시에서 데이터를 읽는 동안 캐시 변환이 메모리 내 캐시에 데이터를 쓰려고 하고 있음을 나타냅니다.|  
|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|데이터 원본의 열 메타데이터가 데이터 원본에 연결된 원본 또는 대상 구성 요소의 열 메타데이터와 일치하지 않음을 나타냅니다.|  
  
## <a name="events-sqlispackage"></a>이벤트(SQLISPackage)  
 자세한 내용은 [Integration Services 패키지에서 기록하는 이벤트](../integration-services/performance/events-logged-by-an-integration-services-package.md)를 참조하세요.  
  
|행사|Description|  
|-----------|-----------------|  
|SQLISPackage_12288|패키지가 시작되었음을 나타냅니다.|  
|SQLISPackage_12289|패키지가 성공적으로 실행되었음을 나타냅니다.|  
|SQLISPACKAGE_12291|패키지가 실행을 완료하지 못하고 중지되었음을 나타냅니다.|  
|SQLISPackage_12546|패키지의 태스크 또는 기타 실행 파일이 작업을 완료했음을 나타냅니다.|  
|SQLISPackage_12549|패키지에서 경고 메시지가 발생했음을 나타냅니다.|  
|SQLISPackage_12550|패키지에서 오류 메시지가 발생했음을 나타냅니다.|  
|SQLISPackage_12551|패키지가 작업을 완료하지 못하고 중지되었음을 나타냅니다.|  
|SQLISPackage_12557|패키지가 실행되었음을 나타냅니다.|  
  
## <a name="events-sqlisservice"></a>이벤트(SQLISService)  
 자세한 내용은 [Integration Services 서비스에서 기록하는 이벤트](../integration-services/service/events-logged-by-the-integration-services-service.md)를 참조하세요.  
  
|행사|Description|  
|-----------|-----------------|  
|SQLISService_256|시비스가 시작되려고 함을 나타냅니다.|  
|SQLISService_257|시비스가 시작되었음을 나타냅니다.|  
|SQLISService_258|시비스가 중지되려고 함을 나타냅니다.|  
|SQLISService_259|시비스가 중지되었음을 나타냅니다.|  
|SQLISService_260|서비스를 시작하려고 했지만 시작하지 못했음을 나타냅니다.|  
|SQLISService_272|구성 파일이 지정된 위치에 없음을 나타냅니다.|  
|SQLISService_273|구성 파일을 읽을 수 없거나 구성 파일이 유효하지 않음을 나타냅니다.|  
|SQLISService_274|구성 파일의 위치가 포함된 레지스트리 항목이 없거나 비어 있음을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../integration-services/integration-services-error-and-message-reference.md)  
  
  
