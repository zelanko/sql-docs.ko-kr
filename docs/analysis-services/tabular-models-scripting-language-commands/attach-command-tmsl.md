---
title: "Attach 명령 (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7a12d148-eac9-4e6c-a222-1439e0817c64
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d19093c8030e9faf909168cd4707cf5b3e8759ef
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="attach-command-tmsl"></a>Attach 명령 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Analysis Services 파일 서버에 연결 합니다.  
  
  
## <a name="request"></a>요청  
  
```  
{   
   "attach":{   
      "folder":"C:\\Program Files\\Microsoft SQL Server\\MSAS13.Tabular\\OLAP\\Data\\",  
      "readWriteMode":"readOnly",  
      "password":"secret"  
   }  
}  
```  
  
 Attach 명령 JSON에서 허용 하는 속성은 다음과 같습니다.  
  
||||  
|-|-|-|  
|**속성**|**Default**|**Description**|  
|데이터베이스|[필수]|연결할 데이터베이스 개체의 이름입니다.|  
|폴더|[필수]|연결 된 데이터베이스를 포함 하는 폴더입니다.|  
|password|비어 있음|연결된 된 데이터베이스의 암호를 암호화 하는 데 암호입니다.|  
|readWriteMode|ReadWrite|데이터베이스에 허용 된 액세스 모드를 나타내는 열거형 값입니다.<br /><br /> **열거형 값은 다음과 같습니다.**<br /><br /> readWrite-읽기 / 쓰기 액세스가 허용 됩니다.<br /><br /> 읽기 전용-읽기 전용 권한이 허용 됩니다.<br /><br /> readOnlyExclusive-읽기 전용 단독 액세스가 허용 됩니다.|  
  
## <a name="response"></a>응답  
 명령이 성공 하는 경우 빈 결과 반환 합니다. 그렇지 않은 경우 XMLA 예외가 반환 됩니다.  
  
## <a name="usage-endpoints"></a>사용 현황 (끝점)  
 Command 요소에이의 문에 사용 되는 [메서드 실행 &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통해 호출 합니다.  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   에 대 한 입력 파일로 **호출 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 나 SQL Server 에이전트 작업에 대 한 입력으로  
  
 SSMS에서 데이터베이스 연결 대화 상자에서 스크립트 단추를 클릭 하 여이 명령에 대 한 기본으로 제공 되는 스크립트를 생성할 수 있습니다.  
  
 [ \[MS-SSAS-T\]: QL Server Analysis Services 테이블 (SQL Server 기술 프로토콜)](http://go.microsoft.com/fwlink/p/?LinkId=784855) JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2 문서를 포함 합니다. 현재 문서에서는 명령과 기능은 아직 구현 되지 않은 TMSL 스크립트에서 다룹니다. 항목을 참조 [테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) 지원 되는 기능에 대 한 설명은  

## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 데이터베이스 연결 및 분리](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  

