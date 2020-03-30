---
title: 구문 쌍의 자동 일치 기능
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], delimiter highlighting
- IntelliSense [SQL Server], syntax pair matching
ms.assetid: bfc54cda-bfd6-4545-a5b9-f9db2ae13769
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1251b6664266fdd1e4d91519186df95a52e52f35
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74834245"
---
# <a name="automatic-matching-of-syntax-pairs"></a>구문 쌍의 자동 일치 기능
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  구문 쌍 자동 맞추기 기능은 쌍으로 코드를 작성해야 하는 구문 요소가 제대로 쌍을 이루는지 여부에 대한 즉각적인 피드백을 제공합니다. 이를 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서는 구분 기호 짝 맞추기, Analysis Services XMLA 쿼리 편집기에서는 중괄호 짝 맞추기, MDX 및 DMX 편집기에서는 괄호 짝 맞추기라고 합니다.  
  
## <a name="database-engine-query-editor-delimiter-matching"></a>데이터베이스 엔진 쿼리 편집기의 구분 기호 짝 맞추기  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서는 코드 블록의 경계를 식별하는 구분 기호의 짝을 맞춥니다. 짝 맞추기 작업은 다음 두 가지 방법으로 수행됩니다.  
  
-   사용자가 쌍의 두 번째 구분 기호 입력을 완료하면 편집기에서 쌍의 두 구분 기호를 모두 강조 표시합니다.  
  
-   커서가 쌍의 구분 기호 중 하나에 있을 때 Ctrl+] 바로 가기 키를 사용하여 쌍을 이루는 다른 구분 기호로 이동할 수 있습니다.  
  
### <a name="delimiter-pairs"></a>구분 기호 쌍  
 자동 구분 기호 짝 맞추기 기능에서는 다음 구분 기호 집합을 인식합니다.  
  
|여는 구분 기호|닫는 구분 기호|  
|--------------------|-----------------------|  
|**(**|**).**|  
|**BEGIN**|**END**|  
|**BEGIN TRY**|**END TRY**|  
|**BEGIN CATCH**|**END CATCH**|  
  
 구분 기호 쌍 자동 맞추기 기능은 대괄호로 묶은 식별자([ObjectName]) 또는 따옴표 붙은 식별자("ObjectName")의 구분 기호를 인식하지 않습니다. 이미 색 구분을 통해 문자열이 구분 기호로 분리되었는지 여부가 표시되므로 쌍 맞추기 기능이 문자열 리터럴에 대해 작은따옴표 구분 기호('문자열') 쌍을 맞추지는 않습니다.  
  
### <a name="delimiter-highlighting"></a>구분 기호 강조 표시  
 짝 맞추기 기능에서 구분 기호 쌍의 여는 요소와 닫는 요소를 모두 강조 표시합니다. 이를 통해 코드 블록을 시각적으로 식별하고 짝이 맞지 않는 구분 기호 쌍을 검사할 수 있습니다.  
  
 쌍을 완성하는 마지막 문자를 입력하면 구분 기호가 강조 표시됩니다. 예를 들어 BEGIN을 먼저 입력한 다음 END를 입력하는 BEGIN END 쌍의 경우 END의 마지막 문자를 입력할 때 강조 표시 기능이 활성화됩니다. 강조 표시 기능을 활성화하기 위해 반드시 여는 구분 기호와 닫는 구분 기호를 순서대로 입력할 필요는 없습니다. END를 먼저 입력한 다음 스크립트 위로 다시 스크롤하고 BEGIN을 입력할 경우 BEGIN의 마지막 문자를 입력할 때 강조 표시 기능이 활성화됩니다. 또한 마지막에 입력한 문자가 구분 기호의 끝 문자일 필요는 없습니다. 예를 들어 BEGIN을 BEIN으로 잘못 입력한 경우 마지막 G를 삽입할 때 BEGIN END 쌍이 강조 표시됩니다.  
  
 구분 기호 쌍은 커서를 이동할 때까지 강조 표시됩니다. 새 커서 위치가 동일한 구분 기호에 남아 있어도 커서가 이동하면 강조 표시 기능이 비활성화됩니다. 쌍을 이루는 구분 기호의 문자를 삭제한 다음 다시 입력하여 강조 표시 기능을 다시 활성화할 수 있습니다.  
  
## <a name="analysis-services-xmla-query-editor-brace-matching"></a>Analysis Services XMLA 쿼리 편집기의 중괄호 짝 맞추기  
 XMLA 쿼리 편집기의 중괄호 짝 맞추기 기능은 여는 중괄호와 닫는 중괄호를 강조 표시하여 요소를 닫았는지 여부를 보여 줍니다. 또한 Ctrl+] 바로 가기 키를 사용하여 쌍의 한 중괄호에서 다른 중괄호로 이동할 수 있습니다.  
  
 XMLA 쿼리 편집기는 다음 구분 기호와 구문 요소의 중괄호 짝을 맞춥니다.  
  
-   쌍을 이루는 시작 및 끝 태그  
  
-   모든 "\<" 및 ">" 꺾쇠 괄호의 쌍  
  
-   주석의 시작 및 끝  
  
-   처리 명령의 시작 및 끝  
  
-   CDATA 블록의 시작 및 끝  
  
-   DTD 선언의 시작 및 끝  
  
-   특성의 여는 따옴표 및 닫는 따옴표  
  
## <a name="mdx-and-dmx-editor-parenthesis-matching"></a>MDX 및 DMX 편집기의 괄호 짝 맞추기  
 MDX(Multi-Dimensional Expressions) 및 DMX(Data Mining Expressions) 편집기에서는 함수의 괄호 짝을 자동으로 맞춥니다.
