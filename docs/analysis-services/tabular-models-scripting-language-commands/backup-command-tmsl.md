---
title: 백업 명령 (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3edffe1a6a54677d3d08d0f87bc48dc718f538c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="backup-command-tmsl"></a>백업 명령을 TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  .Abf 백업 파일을 Analysis Services 데이터베이스를 백업 합니다.  
  
## <a name="request"></a>요청  
  
```  
    {  
        "backup": {  
            "description": "Parameters of Backup command of Analysis Services JSON API",  
            "properties": {  
            "database": {  
                "type": "string"  
            },  
            "file": {  
                "type": "string"  
            },  
            "password": {  
                "type": "string"  
            },  
            "allowOverwrite": {  
                "type": "boolean"  
            },  
            "applyCompression": {  
                "type": "boolean"  
            }  
            },  
. . .   
```  
  
 **백업** 에 몇 가지 속성이 있습니다.  
  
||||  
|-|-|-|  
|**속성**|**Default**|**설명**|  
|데이터베이스|[필수]|백업할 데이터베이스 개체의 이름입니다.|  
|파일|[필수]|백업 파일 이름/경로입니다.|  
|password|비어 있음|백업 파일 암호화에 사용할 암호입니다.|  
|allowOverwrite|False|True 이면 나타내고 백업 파일이 이미 존재 하는 Boolean 덮어쓰게 됩니다. 그렇지 않으면 false입니다.|  
|applyCompression|True|True 인 경우 백업 파일은 압축; 의미 하는 Boolean 그렇지 않으면 false입니다.|  
  
## <a name="response"></a>응답  
 명령이 성공 하는 경우 빈 결과 반환 합니다. 그렇지 않은 경우 XMLA 예외가 반환 됩니다.  
  
## <a name="examples"></a>예  
 **예제 1** -기본 백업 폴더에 파일을 백업 합니다.  
  
```  
{   
   "backup": {   
      "database":"AS_AdventureWorksDW2014",  
      "file":"AS_AdventureWorksDW2014.abf",  
      "password":"secret"  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>사용 현황 (끝점)  
 Command 요소에이의 문에 사용 되는 [메서드 실행 &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통해 호출 합니다.  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   에 대 한 입력 파일로 **호출 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 나 SQL Server 에이전트 작업에 대 한 입력으로  
  
 SSMS에서 데이터베이스 백업 대화 상자에서 스크립트 단추를 클릭 하 여이 명령에 대 한 기본으로 제공 되는 스크립트를 생성할 수 있습니다.  
  
 [ \[MS-SSAS-T\]: QL Server Analysis Services 테이블 (SQL Server 기술 프로토콜)](http://go.microsoft.com/fwlink/p/?LinkId=784855) JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2 문서를 포함 합니다. 현재 문서에서는 명령과 기능은 아직 구현 되지 않은 TMSL 스크립트에서 다룹니다. 항목을 참조 [테이블 형식 모델 스크립팅 언어 &#40;TMSL&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) 지원 되는 기능에 대 한 설명은  

## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 데이터베이스 백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
