---
title: CREATE ACTION 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b723a706521b24c9aa216c46f617d8ff94997137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098548"
---
# <a name="mdx-data-definition---create-action"></a>MDX 데이터 정의 - CREATE ACTION


  큐브, 차원, 계층 또는 종속 개체와 연관될 수 있는 동작을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열입니다.  
  
 *Action_ 이름*  
 만들 동작의 이름을 지정하는 유효한 문자열입니다.  
  
 *Hierarchy_ 이름*  
 계층 이름을 지정하는 유효한 문자열입니다.  
  
 *Level_ 이름*  
 수준 이름을 지정하는 유효한 문자열입니다.  
  
 *Member_ 이름*  
 멤버 이름이나 멤버 키를 지정하는 유효한 문자열입니다.  
  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
 *String_Expression*  
 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 클라이언트 애플리케이션에서 안전하지 않은 동작을 만들고 실행하거나 안전하지 않은 기능을 사용할 수도 있습니다. 이러한 상황을 방지 하려면 사용 합니다 **Safety** 속성입니다. 자세한 내용은 보안 옵션 속성을 참조하십시오.  
  
> [!NOTE]  
>  이 문은 이전 버전과의 호환성을 위해 포함되었습니다. 새로운 동작은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 드릴스루 또는 보고서 동작과 같은 지원 되지 않습니다.  
  
## <a name="action-types"></a>동작 유형  
 다음 표에서 다양 한 유형의 작업에서 사용할 수 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다.  
  
|동작 유형|설명|  
|-----------------|-----------------|  
|**URL**|인터넷 브라우저를 사용하여 열 수 있는 URL이 동작 문자열로 반환됩니다.<br /><br /> 참고: 이 작업을 사용 하 여 시작 되지 않으면 `https://` 또는 `https://`, 동작을 브라우저에 사용할 수 없게 됩니다 경우가 아니면 **SafetyOptions** 로 설정 되어 **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**합니다.|  
|**HTML**|HTML 스크립트가 동작 문자열로 반환됩니다. 이 문자열은 파일로 저장되며, 인터넷 브라우저를 사용하여 파일을 렌더링해야 합니다. 이 경우 생성된 HTML의 일부로 전체 스크립트가 실행될 수 있습니다.|  
|**문**|설정 하 여 실행 해야 하는 문인 동작 문자열로 반환된 합니다 **ICommand::SetText** 문자열 및 호출 명령 개체의 메서드는 **icommand:: Execute**메서드. 명령이 성공하지 않으면 오류가 반환됩니다.|  
|**데이터 집합**|동작 문자열로 반환된은 설정 하 여 실행 해야 하는 MDX 문을 합니다 **ICommand::SetText** 문자열과 호출 명령 개체의 메서드는 **icommand:: Execute** 메서드. 요청된 된 인터페이스 ID (IID) 이어야 합니다 **IDataset**합니다. 데이터 집합이 생성된 경우 명령이 성공한 것입니다. 클라이언트 애플리케이션에서는 사용자가 반환된 데이터 세트을 검색할 수 있어야 합니다.|  
|**ROWSET**|비슷합니다 **데이터 집합**의 IID를 요청 하는 대신 **IDataset**, 클라이언트 응용 프로그램의 IID를 요청 해야 **IRowset**합니다. 행 집합이 생성된 경우 명령이 성공한 것입니다. 클라이언트 애플리케이션에서는 사용자가 반환된 행 집합을 검색할 수 있어야 합니다.|  
|**명령줄**|클라이언트 애플리케이션에서 동작 문자열을 실행합니다. 이 문자열은 명령 줄입니다.|  
|**소유**|애플리케이션에 특정 동작에 대한 특수한 사용자 지정 지식이 없으면 클라이언트 애플리케이션에서 동작이 표시되거나 실행되지 않습니다. 클라이언트 응용 프로그램에 적절 한 제한을 설정 하 여 이러한 항목에 대해 명시적으로 요청 하지 않으면 소유 동작이 클라이언트 응용 프로그램에 반환 되지 않습니다 합니다 **APPLICATION_NAME**합니다.|  
  
## <a name="invocation-types"></a>호출 유형  
 다음 표에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 사용할 수 있는 여러 유형의 호출에 대해 설명합니다. 호출 유형은 클라이언트 애플리케이션에서 동작 호출 시기를 결정하기 위해서만 사용됩니다. 호출 유형은 작업의 호출 동작을 결정하지 않습니다.  
  
|호출 유형|설명|  
|---------------------|-----------------|  
|**대화형**|클라이언트 애플리케이션에서 사용자 상호 작용을 통해 동작이 호출됩니다.|  
|**ON_OPEN**|대상 개체가 열려 있을 때 클라이언트 애플리케이션에서 동작이 호출됩니다. 이 호출 유형은 현재 구현되어 있지 않습니다.|  
|**BATCH**|클라이언트 애플리케이션의 결정에 따라 대상 작업이 일괄 처리 작업에 포함된 경우 클라이언트 애플리케이션에서 동작이 호출됩니다. 이 호출 유형은 현재 구현되어 있지 않습니다.|  
  
### <a name="scope"></a>Scope  
 각 동작은 특정 큐브에 대해 정의되며 해당 큐브에서 고유한 이름을 가집니다. 동작은 다음 표에 나열된 범위 중 하나를 포함할 수 있습니다.  
  
 큐브 범위  
 특정 차원, 멤버 또는 셀과 독립적인 동작에 대 한 예를 들어: "AS에 대 한 터미널 에뮬레이션 실행 / 400 프로덕션 시스템"입니다.  
  
 차원 범위  
 특정 차원에 적용되는 동작을 위한 범위입니다. 이러한 동작은 특정 수준 또는 멤버 선택에 종속되지 않습니다.  
  
 수준 범위  
 특정 차원 수준에 적용되는 동작을 위한 범위입니다. 이러한 동작은 해당 차원의 특정 멤버 선택에 종속되지 않습니다.  
  
 멤버 범위  
 특정 멤버에 적용되는 동작을 위한 범위입니다.  
  
 셀 범위  
 특정 셀에만 적용되는 동작을 위한 범위입니다.  
  
 집합 범위  
 집합에만 적용되는 동작을 위한 범위입니다. 이름으로 **ActionParameterSet**, 동작의 식 내에서 응용 프로그램에서 사용 하도록 예약 되어 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
