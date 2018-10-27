---
title: 명령 취소 (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: babdafaaa1c507a609760b02895f9438baf21581
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145019"
---
# <a name="canceling-commands-xmla"></a>명령 취소(XMLA)
  명령을 실행 하는 사용자의 관리 권한에 따라 합니다 [취소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) Analysis (XMLA) 세션, 세션, 연결, 서버 프로세스 또는 연관된 된 세션이 명령을 취소할 수에 대 한 xml에서 명령 또는 연결입니다.  
  
## <a name="canceling-commands"></a>명령 취소  
 사용자는 보내어 현재 명시적 세션의 컨텍스트 내에서 현재 실행 중인 명령을 취소할 수 있습니다는 **취소** 명령에 지정 된 속성이 없습니다.  
  
> [!NOTE]  
>  암시적 세션에서 실행 중인 명령은 사용자가 취소할 수 없습니다.  
  
### <a name="canceling-batch-commands"></a>Batch 명령 취소  
 사용자가 취소를 **일괄 처리** 명령을 선택한 다음 내에서 아직 실행 되는 나머지 모든 명령 합니다 **일괄 처리** 명령이 취소 됩니다. 경우는 **일괄 처리** 명령이 트랜잭션인 경우 전에 실행 된 모든 명령은 합니다 **취소** 명령 실행 롤백됩니다.  
  
## <a name="canceling-sessions"></a>세션 취소  
 명시적 세션의 세션 식별자를 지정 하 여는 [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) 의 속성을 **취소** 데이터베이스 관리자나 서버 관리자가 세션을 취소할 수 있습니다를 포함 하 여는 현재 실행 중인 명령입니다. 데이터베이스 관리자는 자신이 관리 권한을 가지고 있는 데이터베이스에 대한 세션만을 취소할 수 있습니다.  
  
 데이터베이스 관리자는 DISCOVER_SESSIONS 스키마 행 집합을 검색하여 지정된 데이터베이스의 활성 세션을 검색할 수 있습니다. DISCOVER_SESSIONS 스키마 행 집합을 검색 하려면 데이터베이스 관리자는 XMLA **Discover** 메서드는 SESSION_CURRENT_DATABASE제한열에대한적절한데이터베이스식별자를지정하고[제한 사항](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) 의 속성을 **Discover** 메서드.  
  
## <a name="canceling-connections"></a>연결 취소  
 연결 식별자를 지정 하 여 합니다 [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) 의 속성을 **취소** 모두를 포함 하 여 지정된 된 연결에 연관 된 세션의 모든 서버 관리자를 취소할 수 있습니다 명령을 실행 하 고 연결을 취소 합니다.  
  
> [!NOTE]  
>  경우 인스턴스의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 찾아 인스턴스 연결을 취소할 수 없습니다 데이터 펌프가 여러 세션 HTTP 연결이 제공 하는 동안 때와 같은 연결을 사용 하 여 연결 된 세션을 취소할 수 없습니다. 실행 하는 동안이 이런 경우가 발생 하는 경우는 **취소** 명령에 오류가 발생 합니다.  
  
 서버 관리자에 대 한 활성 연결을 검색할 수는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XMLA를 사용 하 여 DISCOVER_CONNECTIONS 스키마 행 집합을 검색 하 여 인스턴스 **Discover** 메서드.  
  
## <a name="canceling-server-processes"></a>서버 프로세스 취소  
 에 SPID (서버 프로세스 식별자)를 지정 하 여 합니다 [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) 의 속성을 **취소** 서버 관리자에 지정된 된 SPID에 연관 된 명령을 취소할 수 있습니다.  
  
## <a name="canceling-associated-sessions-and-connections"></a>연관된 세션 및 연결 취소  
 설정할 수 있습니다는 [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) 속성을 true로 연결, 세션 및 연결, 세션 또는에 지정 된 SPID에 연관 된 명령을 취소 하는 **취소** 명령입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Discover 메서드 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
