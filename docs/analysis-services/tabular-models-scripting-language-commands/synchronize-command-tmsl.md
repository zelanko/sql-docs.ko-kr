---
title: Synchronize 명령 (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4265e6fa1e2214fae53cacdb084e152005eb3647
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033276"
---
# <a name="synchronize-command-tmsl"></a>Synchronize 명령 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Analysis Services 데이터베이스를 기존의 다른 데이터베이스와 동기화합니다.  
  
## <a name="request"></a>요청  
 Synchronize 명령 JSON에서 허용 하는 속성은 다음과 같습니다.  
  
```  
{   
   "synchronize":{   
      "database":"AdventureWorksDW_Production",  
      "source":"Provider=MSOLAP.7;Data Source=localhost;Integrated Security=SSPI;Initial Catalog=AdventureWorksDW_Dev",  
      "synchronizeSecurity":"copyAll",  
      "applyCompression":true  
   }  
}  
```  
  
 Synchronize 명령 JSON에서 허용 하는 속성은 다음과 같습니다.  
  
||||  
|-|-|-|  
|**속성**|**Default**|**설명**|  
|database||동기화 할 데이터베이스 개체의 이름입니다.|  
|원본(source)||원본 서버에 연결 하는 데 연결 문자열입니다.|  
|synchronizeSecurity|skipMembership|역할 및 사용 권한을 포함 하 여 보안 정의 복원 하는 방법을 지정 하는 열거형 값입니다. 유효한 값에는 copyAll, skipMembership, ignoreSecurity 포함 됩니다.|  
|applyCompression|True|True 인 경우 동기화 작업을 하는 동안 압축을 적용 됨을 지정 하는 부울 그렇지 않으면 false입니다.|  
  
## <a name="response"></a>응답  
 명령이 성공 하면 빈 결과 반환 합니다. 그렇지 않으면 XMLA 예외가 반환 됩니다.  
  
## <a name="usage-endpoints"></a>사용량 (끝점)  
 이 명령 요소를 사용 하는 문에 [메서드 실행 &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통한 호출:  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   입력 파일로 합니다 **호출할 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 또는 SQL Server 에이전트 작업에 대 한 입력으로  
  
 데이터베이스 동기화 대화 상자에서 스크립트 단추를 클릭 하 여 SSMS에서이 명령에 대 한 바로 사용할 수 있는 스크립트를 생성할 수 있습니다.  
  
 합니다 [ \[MS-SSAS-T\]: QL Server Analysis Services 테이블 형식 (SQL Server 기술 Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) 문서 JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2 포함 되어 있습니다. 현재 문서에서는 명령 및 TMSL 스크립트에서 아직 구현 하는 기능을 설명 합니다. 항목을 참조할 [Tabular Model Scripting Language &#40;TMSL&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) 지원 되는 기능에 대 한 설명에 대 한  
  
## <a name="see-also"></a>관련 항목  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
