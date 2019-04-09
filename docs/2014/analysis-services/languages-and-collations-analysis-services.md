---
title: 언어 및 데이터 정렬 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Windows collations [Analysis Services]
- default collations
- languages [Analysis Services]
- sort orders [Analysis Services]
- language identifiers [Analysis Services]
- default languages
- collations [Analysis Services]
ms.assetid: 666cf8a7-223b-4be5-86c0-7fe2bcca0d09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6300606195ea435a0290d828109b821d0d6702c
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241831"
---
# <a name="languages-and-collations-analysis-services"></a>언어 및 데이터 정렬(Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 운영 체제에서 제공하는 언어 및 데이터 정렬을 지원합니다. `Language` 및 `Collation` 속성 설치 하는 동안 처음에 인스턴스 수준에서 설정 되었지만 개체 계층 구조의 여러 수준에서 나중에 변경할 수 있습니다.  
  
 다차원 모델 (전용)의 데이터베이스나 큐브에서 이러한 속성을 설정할 수 있습니다-큐브 내 개체에 대해 만드는 번역에 설정할 수 있습니다.  
  
 `Language` 및 `Collation` 설정 시 처리 및 쿼리 실행 중 데이터 모델에서 사용되는 설정을 지정하거나, (다차원 모델에만 해당) 외국어 사용자가 모국어로 모델을 사용할 수 있도록 다양한 언어로 번역된 모델을 제공합니다. 개체(데이터베이스, 모델 또는 큐브)에 대한 `Language` 및 `Collation` 속성을 명시적으로 설정하는 것은 개발 환경 및 프로덕션 서버가 다양한 로캘용으로 구성되고 언어 및 데이터 정렬이 의도한 대상 환경의 언어 및 데이터 정렬과 일치해야 하는 경우를 위한 것입니다.  
  
 이 항목에는 다음의 섹션이 포함됩니다.  
  
-   [언어 및 데이터 정렬 속성을 지원하는 개체](#bkmk_object)  
  
-   [Analysis Services의 언어 지원](#bkmk_lang)  
  
-   [Analysis Services에서의 데이터 정렬 지원](#bkmk_collations)  
  
-   [인스턴스에서의 기본 언어 또는 데이터 정렬 변경](#bkmk_defaultLang)  
  
-   [큐브에서의 언어 또는 데이터 정렬 변경](#bkmk_cube)  
  
-   [XMLA를 사용하여 데이터 모델 내에서 언어와 데이터 정렬 변경](#bkmk_XMLA)  
  
-   [EnableFast1033Locale을 통해 영어 로캘에 대한 성능 향상](#bkmk_enablefast1033)  
  
-   [Analysis Services에서의 GB18030 지원](#bkmk_gb18030)  
  
##  <a name="bkmk_object"></a> 언어 및 데이터 정렬 속성을 지원하는 개체  
 `Language` 및 `Collation` 속성은 종종 함께 표시 설정할 수 있습니다 `Language`를 설정할 수도 있습니다 `Collation`합니다.  
  
 다음 개체들에서 `Language`와 `Collation`을 설정할 수 있습니다.  
  
-   **인스턴스**. 인스턴스에 배포하는 모든 프로젝트는 언어와 데이터 정렬이 정의되어 있지 않다고 가정하고 인스턴스의 언어와 데이터 정렬을 채택하게 됩니다. 기본적으로 다차원 모델은 언어 및 데이터 정렬을 비워 둡니다. 프로젝트가 배포되면 결과 데이터베이스와 큐브는 인스턴스의 언어와 데이터 정렬을 가져옵니다.  
  
     처음에는 설치 중에 언어와 데이터 정렬 속성이 정해지지만 관리자가 Management Studio에서 이것을 재정의할 수 있습니다. 자세한 내용은 [인스턴스에서의 기본 언어 또는 데이터 정렬 변경](#bkmk_defaultLang) 를 참조하세요.  
  
-   **데이터베이스**. 상속을 중단하기 위해 데이터베이스에 포함된 모든 큐브에 의해 사용되는 프로젝트 수준에서 언어 및 데이터 정렬을 명시적으로 설정할 수 있습니다. 달리 명시하지 않는 한 데이터베이스에 있는 모든 큐브는 이 수준에서 지정하는 언어와 데이터 정렬을 가져오게 됩니다. 정기적으로 코드를 하고 서로 다른 로캘에 배포하는 경우(예를 들어 중국어 컴퓨터에서 솔루션을 개발하지만 프랑스어 자회사가 소유한 서버에 배포하는 경우) 데이터베이스 수준에서 언어와 데이터 정렬을 설정하는 것은 솔루션이 대상 환경에서 작동하도록 하는 첫 번째이자 가장 중요한 단계입니다. 이러한 속성을 설정하는 가장 좋은 곳은 프로젝트 내부입니다(프로젝트에서 **데이터베이스 편집** 명령을 통해).  
  
-   **데이터베이스 차원**. 디자이너가 데이터베이스 차원의 `Language` 및 `Collation` 속성을 노출하더라도 이 개체의 속성을 설정하는 것은 유용하지 않습니다. 데이터베이스 차원은 독립 실행형 개체로 사용되지 않으므로 사용자가 정의하는 속성을 사용하는 것은 불가능하지 않다면 어려울 수 있습니다. 차원은 큐브에 있으면 항상 큐브 부모로부터 `Language`와 `Collation`를 상속받습니다. 독립 실행형 데이터베이스 차원 개체에 설정했을 수 있는 모든 값은 무시됩니다.  
  
-   **큐브**. 기본 쿼리 구조로서 큐브 수준에서 언어와 데이터 정렬을 설정할 수 있습니다. 예를 들어, 동일한 프로젝트 내에서 영어 및 중국어 버전과 같이 여러 언어로 된 큐브 버전을 만들 수 있습니다. 여기서 각 큐브에는 자체 언어 및 데이터 정렬이 있습니다.  
  
     설정한 언어와 데이터 정렬이 무엇이든 간에 큐브는 큐브에 포함된 모든 측정값 및 차원에 의해 사용됩니다. 데이터 정렬 속성을 더욱 상세한 수준으로 설정하는 유일한 방법은 차원 특성에서 번역을 만드는 경우입니다. 그렇지 않고 특성 수준에서 번역이 없는 것으로 가정하면 큐브당 하나의 데이터 정렬이 존재하게 됩니다.  
  
 또한 설정할 수 있습니다 `Language`, 자체로는 **번역** 개체입니다.  
  
 번역 개체는 큐브나 차원에 번역을 추가할 때 생성됩니다. `Language` 번역 정의의 일부가입니다. `Collation`다른 한편으로 큐브의 이상으로 설정 되며 모든 번역에서 공유 합니다. 이것은 여러 언어 속성(각 번역에 대해 하나)과 오직 한 데이터 정렬이 표시되는 번역이 포함된 큐브의 XMLA에서 명백히 나타납니다. 차원 특성 번역에 대한 한 가지 예외가 있습니다. 이 예외에서는 원본 열과 일치하는 특성 데이터 정렬을 지정하기 위해 큐브 데이터 정렬을 재정의합니다. (데이터베이스 엔진에서는 개별 열에 대한 데이터 정렬 설정을 지원하며, 다른 원본 열에서 멤버 데이터를 가져오도록 개별 번역을 구성하는 것은 일반적입니다.) 하지만 그렇지 않으면 다른 모든 번역에 대해 `Language`에 상관없이 `Collation`가 단독으로 사용됩니다. 자세한 내용은 [번역&#40;Analysis Services&#41;](translations-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_lang"></a> Analysis Services의 언어 지원  
 `Language` 속성에서는 쿼리 처리 중 사용된 개체의 로캘을 설정하고 `Captions` 및 `Translations`을 사용하여 다국어 시나리오를 지원합니다. 로캘은 영어와 같은 언어 식별자와 미국이나 오스트레일리아와 같이 날짜와 시간 표현을 더 구체적으로 정의하는 지역을 기반으로 합니다.  
  
 인스턴스 수준에서 속성은 Windows Server 운영 체제의 언어(37개 언어 중 하나)를 기반으로 설치 중에 설정됩니다(언어 팩 하나가 설치되어 있다고 가정). 설치 프로그램에서는 언어를 변경할 수 없습니다.  
  
 설치 후 Management Studio의 서버 속성 페이지를 사용하거나 msmdsrv.ini 구성 파일에서 `Language`를 재정의할 수 있습니다. Windows 클라이언트에서 지원하는 모든 언어를 포함하여 보다 많은 언어 중에서 선택할 수 있습니다. 서버에서는 인스턴스 수준에서 설정되는 경우 `Language`가 이후에 배포되는 모든 데이터베이스의 로캘을 결정합니다. 예를 들어 `Language`를 독일어로 설정하는 경우 인스턴스에 배포되는 모든 데이터베이스에는 독일어용 LCID인 언어 속성 1031이 생깁니다.  
  
###  <a name="bkmk_lcid"></a> 언어 속성의 값이 LCID(로캘 식별자)입니다.  
 유효한 값에는 드롭다운 목록에 표시되는 LCID가 포함됩니다. Management Studio 및 SQL Server Data Tools에서는 LCID가 해당 문자열로 표시됩니다. `Language` 속성이 노출되는 곳에는 도구에 관계없이 같은 언어가 표시됩니다. 동일한 언어 목록이 있으면 모델 전체에서 일관되게 번역을 구현 및 테스트할 수 있습니다.  
  
 Analysis Services에 언어가 이름별로 나열되더라도 속성에 대해 저장된 실제 값은 LCID입니다. 언어 속성을 프로그래밍 방식이나 msmdsrv.ini 파일을 통해 설정할 때에는 [LCID(로캘 식별자)](http://en.wikipedia.org/wiki/Locale) 를 값으로 사용하세요. LCID는 언어 ID, 정렬 ID 및 특정 언어를 식별하는 예약된 비트로 구성된 32비트 값입니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 LCID를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 및 개체에 대해 선택할 언어를 지정합니다.  
  
 16진수나 10진수 형식을 사용하여 LCID를 설정할 수 있습니다. 유효한 값에 대 한 몇 가지 예는 `Language` 속성 포함:  
  
-   0x0409 또는 1033 - **영어(미국)**  
  
-   0x0411 또는 1041 - **일본어**  
  
-   0x0407 또는 1031 - **독일(독일어)**  
  
-   0x0416 또는 1046 - **포르투갈어(브라질)**.  
  
 긴 목록을 보려면 [Microsoft에서 할당한 로캘 ID](https://msdn.microsoft.com/goglobal/bb964664.aspx)(영문)를 참조하세요. 자세한 배경 정보를 참조 하세요 [코드 페이지](/windows/desktop/Intl/code-pages)합니다.  
  
> [!NOTE]  
>  `Language` 속성은 시스템 메시지 표시용 언어나 사용자 인터페이스에 표시할 문자열을 결정하지 않습니다. 오류, 경고 및 메시지는 Office와 Office 365에서 지원하는 모든 언어로 지역화되어 있으며, 지원되는 로캘 중 하나를 클라이언트 연결이 지정하면 자동으로 사용됩니다.  
  
##  <a name="bkmk_collations"></a> Analysis Services에서의 데이터 정렬 지원  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서는 Windows 및 이진 데이터 정렬을 배타적으로 사용합니다. 레거시 SQL Server 데이터 정렬은 사용하지 않습니다. 큐브 내에서 단일 데이터 정렬은 특성 수준의 번역을 제외하고, 전체에서 사용됩니다. 특성 번역을 정의하는 방법에 대한 자세한 내용은 [번역&#40;Analysis Services&#41;](translations-analysis-services.md)을 참조하세요.  
  
 데이터 정렬은 개체 식별자를 제외하고 bicameral 언어 스크립트에서 모든 문자열의 대/소문자 구분을 제어합니다. 개체 식별자에서 대문자와 소문자를 모두 사용하는 경우 개체 식별자의 대/소문자 구분은 데이터 정렬이 아니라 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 따라 결정됩니다. 영어 스크립트에 구성된 개체 식별자의 경우, 개체 식별자는 데이터 정렬에 관계없이 항상 대/소문자를 구분합니다. 키릴자모 및 기타 bicameral 언어에서는 반대로 수행합니다(항상 대/소문자 구분). 자세한 내용은 [세계화 팁과 모범 사례&#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) 를 참조하세요.  
  
 Analysis Services의 데이터 정렬은 각 서비스에 대해 선택한 정렬 옵션에서 패리티를 유지 관리하는 것으로 가정하여 SQL Server 관계형 데이터베이스 엔진의 데이터 정렬과 호환합니다. 예를 들어, 관계형 데이터베이스에서 악센트를 구분하는 경우에는 큐브를 동일한 방식으로 구성해야 합니다. 데이터 정렬 설정이 달라지면 문제가 발생할 수 있습니다. 예와 해결 방법이 필요하면 [유니코드 문자열의 공백에 데이터 정렬을 기반으로 한 서로 다른 처리 결과가 있는 경우](https://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)(영문)를 참조하세요. 데이터 정렬 및 데이터베이스 엔진에 대해 알려면 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
###  <a name="bkmk_collationtype"></a> 데이터 정렬 유형  
 Analysis Services에서는 두 가지 데이터 정렬 유형을 지원합니다.  
  
-   **Windows 데이터 정렬**  
  
     Windows 데이터 정렬은 언어의 언어적 및 문화적 특징을 기반으로 문자를 정렬합니다. Windows에서 데이터 정렬은 공통 알파벳을 공유하는 많은 언어와 문자 정렬 및 비교 규칙들로 인해 함께 사용하는 로캘(또는 언어) 보다 월등히 많습니다. 예를 들어 모든 포르투갈어 및 영어 Windows 로캘을 포함한 33개의 Windows 로캘은 Latin1 코드 페이지(1252)를 사용하고 문자 정렬 및 비교 시 공용 규칙 집합을 따릅니다.  
  
-   **이진 데이터 정렬(BIN 또는 BIN2)**  
  
     이진 데이터 정렬에서는 언어 값이 아니라 유니코드 코드 포인트로 정렬합니다. 예를 들어 Latin_1_General_BIN과 Japanese_BIN은 유니코드 데이터에서 사용할 때 동일한 정렬 결과를 생성합니다. 모든 대문자의 코드 포인트가 소문자의 코드 포인트보다 높으므로 이진 정렬은 ABCDabcd인 반면 언어적 정렬은 aAbBcCdD와 같은 결과를 산출할 수 있습니다.  
  
###  <a name="bkmk_sortorder"></a> 정렬 순서 옵션  
 정렬 옵션은 대/소문자, 악센트, 가나 및 전자/반자 구분을 기준으로 정렬 및 비교 규칙을 세분화하는 데 사용됩니다.  예를 들어 `Collation`의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 구성 속성 기본값이 Latin1_General_AS_CS이면 Latin1_General 데이터 정렬에 악센트 구분, 대/소문자 구분 정렬 순서를 사용하도록 지정됩니다.   
  
 BIN 및 BIN2는 다른 정렬 옵션과 함께 사용할 수 없으며, BIN 또는 BIN2를 사용하려면 악센트 구분용 정렬 옵션의 선택을 취소합니다. 마찬가지로 BIN2를 선택하면 대/소문자 구분, 대/소문자 구분 안 함, 악센트 구분, 악센트 구분 안 함, 일본어 가나 구분 및 전자/반자 구분 옵션을 사용할 수 없습니다.  
  
 다음 표에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 대한 Windows 데이터 정렬 순서 옵션 및 관련 접미사를 설명합니다.  
  
|정렬 순서(접미사)|정렬 순서 설명|  
|---------------------------|----------------------------|  
|이진(_BIN) 또는 BIN2(_BIN2)|SQL Server에는 두 가지 유형의 이진 데이터 정렬 즉, 이전 BIN 데이터 정렬과 최신 BIN2 데이터 정렬이 있습니다. BIN2 데이터 정렬에서 모든 문자는 코드 포인트에 따라 정렬됩니다. BIN 데이터 정렬에서 첫 번째 문자만 코드 포인트에 따라 정렬되며 나머지 문자는 바이트 값에 따라 정렬됩니다. Intel 플랫폼은 little endian 아키텍처이므로, 유니코드 문자는 항상 바이트 스왑 상태로 저장됩니다.<br /><br /> 유니코드 데이터 형식에서의 이진 데이터 정렬의 경우 데이터 정렬 시 로캘은 고려되지 않습니다. 예를 들어 Latin_1_General_BIN과 Japanese_BIN은 유니코드 데이터에서 사용할 때 동일한 정렬 결과를 생성합니다.<br /><br /> 이진 정렬 순서는 대/소문자와 악센트를 구분합니다. 이진은 가장 빠른 정렬 순서입니다.|  
|대/소문자 구분(_CS)|대/소문자를 구분합니다. 이 정렬 순서를 선택하면 소문자가 대문자보다 먼저 정렬됩니다. _CI를 지정하여 대/소문자를 구분하지 않도록 명시적으로 설정할 수 있습니다. 데이터 정렬 관련 대/소문자 설정은 차원, 큐브 및 기타 개체의 ID와 같은 개체 식별자에 적용되지 않습니다. 자세한 내용은 [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) 를 참조하세요.|  
|악센트 구분(_AS)|악센트가 있는 문자와 악센트가 없는 문자를 구분합니다. 예를 들어 'a'와 'ấ'는 같지 않습니다. 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 정렬할 때 악센트가 있는 문자와 악센트가 없는 문자가 동일한 것으로 간주합니다. _AI를 지정하여 악센트를 구분하지 않도록 명시적으로 설정할 수 있습니다.|  
|일본어 가나 구분(_KS)|일본어 가나 문자의 두 가지 유형인 히라가나와 가타가나를 구분합니다. 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 정렬할 때 히라가나 문자와 가타가나 문자가 동일한 것으로 간주합니다. 가나를 구분하지 않고 정렬할 때는 정렬 순서 접미사가 없습니다.|  
|전자/반자 구분(_WS)|같은 문자라도 싱글바이트 문자와 더블바이트 문자를 구분합니다. 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 정렬할 때 싱글바이트와 더블바이트로 표시된 같은 문자를 동일한 것으로 간주합니다. 전자/반자를 구분하지 않고 정렬할 때는 정렬 순서 접미사가 없습니다.|  
  
##  <a name="bkmk_defaultLang"></a> 인스턴스에서의 기본 언어 또는 데이터 정렬 변경  
 기본 언어와 데이터 정렬은 설치 중 정해지지만 설치 후 구성의 일부로서 변경할 수 있습니다. 인스턴스 수준에서 데이터 정렬을 변경하는 것은 특수한 경우로서, 다음의 요구 사항이 동반됩니다.  
  
-   서비스 다시 시작.  
  
-   기존 개체의 데이터 정렬 설정 업데이트. 데이터 정렬 설정은 개체가 만들어질 때 한 번 상속됩니다. 데이터 정렬에 대한 이후의 변경은 수동으로 수행해야 합니다. 자세한 내용은 [XMLA를 사용하여 데이터 모델 내에서 언어와 데이터 정렬 변경](#bkmk_XMLA) 을 참조하세요.  
  
-   데이터 정렬이 업데이트된 후에는 파티션 및 차원은 다시 처리합니다.  
  
 SQL Server Management Studio나 AMO PowerShell을 사용하면 서버 수준에서 기본 언어나 데이터 정렬을 변경할 수 있습니다. 수정할 수 있습니다 합니다  **\<언어 >** 하 고  **\<CollationName >** 언어의 LCID를 지정 하 여 msmdsrv.ini 파일에서 설정 합니다.  
  
1.  Management Studio에서 서버 이름 | **속성** | **언어/데이터 정렬**을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  정렬 옵션을 선택합니다. **이진** 와 **이진 2**중 하나를 선택하려면 우선 **악센트 구분**확인란의 선택을 취소하세요.  
  
     데이터 정렬 및 언어는 완전히 독립적인 설정입니다. 하나를 변경해도 다른 하나의 값은 공통 조합을 표시하도록 필터링되지 않습니다.  
  
3.  새 데이터 정렬을 사용하도록 데이터 모델을 업데이트합니다(다음 섹션 참조).  
  
4.  서비스를 다시 시작합니다.  
  
##  <a name="bkmk_cube"></a> 큐브에서의 언어 또는 데이터 정렬 변경  
  
1.  솔루션 탐색기에서 큐브를 두 번 클릭하여 큐브 디자이너에서 엽니다.  
  
2.  측정값 또는 차원 창에서 최상위 노드를 선택합니다. 두 창 중 하나에 대한 최상위 개체는 큐브입니다.  
  
3.  속성에서 `Language`와 `Collation`을 설정합니다. 선택한 값은 큐브 차원 및 측정값을 포함하여 모든 큐브 개체에 의해 사용되며, 처리 및 쿼리 작업에 영향을 줍니다.  
  
     큐브 내에 개체에 대한 대체 언어 및 데이터 정렬 속성을 포함하는 유일한 방법은 번역을 통한 것입니다. 자세한 내용은 [번역&#40;Analysis Services&#41;](translations-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_XMLA"></a> XMLA를 사용하여 데이터 모델 내에서 언어와 데이터 정렬 변경  
 개체가 만들어질 때 언어와 데이터 정렬 설정이 한 번 상속됩니다. 이 속성들에 대한 이후의 변경은 수동으로 수행해야 합니다. 여러 개체에서 데이터 정렬을 신속하게 변경하는 한 가지 방법을 XMLA 스크립트에서 ALTER 명령을 사용하는 것입니다.  
  
 기본적으로 데이터 정렬은 데이터베이스 수준에서 한번 설정됩니다. 개체 계층 구조의 나머지 부분에서는 상속되는 것으로 간주됩니다. 큐브 내 개체에서 `Collation`을 명시적으로 설정하는 경우 개별 차원 특성에서 이 작업이 허용되면 XMLA 정의에 표시됩니다. 그러지 않으면 최상위 데이터 정렬 속성만 존재합니다.  
  
 XMLA를 사용하여 기존 데이터베이스를 수정하기 전에 데이터베이스와 데이터베이스 빌드에 사용되는 원본 파일 간에 불일치가 생기지 않도록 확인합니다. 예를 들어 개념 증명 테스트를 위해 XMLA를 사용하여 언어나 데이터 정렬을 신속하게 변경한 후에 원본 파일을 변경하여( [큐브에서의 언어 또는 데이터 정렬 변경](#bkmk_cube)참조) 이미 마련된 기존 운영 절차를 사용하여 솔루션을 다시 배포할 수 있습니다.  
  
1.  Management Studio에서 데이터베이스 | **데이터베이스 스크립팅** | **ALTER** | **새 쿼리 편집기 창**을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  기존 언어 또는 데이터 정렬을 검색하고 대체 값으로 바꿉니다.  
  
3.  F5 키를 눌러 스크립트를 실행합니다.  
  
4.  큐브를 다시 처리합니다.  
  
##  <a name="bkmk_enablefast1033"></a> EnableFast1033Locale을 통해 영어 로캘에 대한 성능 향상  
  영어(미국) 식별자(0x0409 또는 1033)를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스의 기본 언어로 사용하는 경우 이 언어 식별자에만 사용 가능한 고급 구성 속성인 `EnableFast1033Locale` 구성 속성을 설정하여 성능상 이점을 추가로 얻을 수 있습니다.  이 속성의 값을 **true** 로 설정하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 가 문자열 해시 및 비교에 보다 빠른 알고리즘을 사용할 수 있습니다. 구성 속성을 설정하는 방법에 대한 자세한 내용은 [Analysis Services에서 서버 속성 구성](server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_gb18030"></a> Analysis Services에서의 GB18030 지원  
 GB18030은 중국에서 사용하는 별개의 중국어 인코딩 표준입니다. GB18030에서 문자 길이는 1바이트, 2바이트 또는 4바이트일 수 있습니다. Analysis Services에는 외부 원본의 데이터를 처리할 때 데이터 변환이 이루어지지 않습니다. 데이터는 유니코드로 간단히 저장됩니다. 쿼리 시 클라이언트 운영 체제 설정에 따라 쿼리 결과에 텍스트 데이터가 반환되면 Analysis Services 클라이언트 라이브러리를 통해 GB18030 변환이 수행됩니다(특히, MSOLAP.dll OLE DB 공급자). 데이터베이스 엔진은 GB18030도 지원합니다. 자세한 내용은 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 다차원에 대한 세계화 시나리오](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [세계화 팁과 모범 사례&#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)   
 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)  
  
  
