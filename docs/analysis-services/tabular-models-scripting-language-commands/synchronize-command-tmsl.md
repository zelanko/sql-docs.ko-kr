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
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040079"
---
# <a name="synchronize-command-tmsl"></a>Synchronize 명령 TMSL)
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
|데이터베이스||동기화 할 데이터베이스 개체의 이름입니다.|  
|원본(source)||원본 서버에 연결 하는 데 연결 문자열입니다.|  
|synchronizeSecurity|skipMembership|역할 및 사용 권한이 포함 되는 보안 정의 복원 하는 방법을 지정 하는 열거형 값입니다. CopyAll, skipMembership, ignoreSecurity 유효한 값에 포함 되어 있습니다.|  
|applyCompression|True|True 이면 나타내고; 동기화 작업을 하는 동안 압축을 적용할 하는 Boolean 그렇지 않으면 false입니다.|  
  
## <a name="response"></a>응답  
 명령이 성공 하는 경우 빈 결과 반환 합니다. 그렇지 않은 경우 XMLA 예외가 반환 됩니다.  
  
## <a name="usage-endpoints"></a>사용 현황 (끝점)  
 Command 요소에이의 문에 사용 되는 [메서드 실행 &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통해 호출 합니다.  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   에 대 한 입력 파일로 **호출 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 나 SQL Server 에이전트 작업에 대 한 입력으로  
  
 SSMS에서 데이터베이스 동기화 대화 상자에서 스크립트 단추를 클릭 하 여이 명령에 대 한 기본으로 제공 되는 스크립트를 생성할 수 있습니다.  
  
 [ \[MS-SSAS-T\]: QL Server Analysis Services 테이블 (SQL Server 기술 프로토콜)](http://go.microsoft.com/fwlink/p/?LinkId=784855) JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2 문서를 포함 합니다. 현재 문서에서는 명령과 기능은 아직 구현 되지 않은 TMSL 스크립트에서 다룹니다. 항목을 참조 [테이블 형식 모델 스크립팅 언어 &#40;TMSL&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) 지원 되는 기능에 대 한 설명은  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
