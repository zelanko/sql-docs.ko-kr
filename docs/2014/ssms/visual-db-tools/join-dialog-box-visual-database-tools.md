---
title: 조인 대화 상자(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.ppg.joinline
- vdtsql.chm:69638
ms.assetid: 0d9516bb-4ad3-4fcf-bb77-93474dea698f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e266d398debd65a8a03f73d7f8726899c97b7e13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62711141"
---
# <a name="join-dialog-box-visual-database-tools"></a>조인 대화 상자(Visual Database Tools)
  이 대화 상자를 사용하면 테이블을 조인하기 위한 옵션을 지정할 수 있습니다. 이 대화 상자에 액세스하려면 **디자인** 창에서 조인 선을 선택합니다. 그런 다음, **속성** 창에서 **조인 조건 및 형식**을 클릭하고 속성의 오른쪽에 있는 줄임표 **(...)** 를 클릭합니다.  
  
 기본적으로 관련 테이블은 조인 열의 일치하는 정보를 포함하는 행에 기반하여 결과 집합을 만드는 내부 조인을 사용하여 조인됩니다. 
  **조인** 대화 상자에서 옵션을 설정하여 다른 연산자를 기반으로 하는 조인을 지정하거나 외부 조인을 지정할 수 있습니다.  
  
 테이블을 조인하는 방법에 대한 자세한 내용은 [조인을 사용한 쿼리&#40;Visual Database Tools&#41;](visual-database-tools.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
  
|**용어**|**정의**|  
|--------------|--------------------|  
|**테이블**|조인에 관련된 테이블 또는 테이블 반환 개체의 이름입니다. 여기서는 테이블의 이름을 변경할 수 없으며 표시된 정보를 참조만 할 수 있습니다.|  
|**열**|테이블 조인에 사용된 열의 이름입니다. 연산자 목록의 연산자는 열에 있는 데이터 간의 관계를 지정합니다. 여기서는 열의 이름을 변경할 수 없으며 표시된 정보를 참조만 할 수 있습니다.|  
|**연산자**|조인 열과 관련시키는 데 사용되는 연산자를 지정합니다. 등호(=) 이외의 연산자를 지정하려면 목록에서 해당 연산자를 선택하십시오. 속성 페이지를 닫으면 선택한 연산자가 다음 그림과 같이 조인 선의 다이아몬드 모양 안에 나타납니다.<br /><br /> ![Visual Database Tools 아이콘](../../database-engine/media//dv3wbii.gif "Visual Database Tools 아이콘")|  
|**Table1의 \<모든 행>**|오른쪽 테이블에 일치하는 항목이 없는 경우에도 왼쪽 테이블의 모든 행이 출력되도록 지정합니다. 오른쪽 테이블에서 일치하는 데이터가 없는 열은 null로 나타납니다. 이 옵션을 선택하면 SQL 문에 왼쪽 우선 외부 조인을 지정하는 것과 결과가 같습니다.|  
|**Table2의 \<모든 행>**|왼쪽 테이블에 일치하는 항목이 없는 경우에도 오른쪽 테이블의 모든 행이 출력되도록 지정합니다. 왼쪽 테이블에서 일치하는 데이터가 없는 열은 null로 나타납니다. 이 옵션을 선택하면 SQL 문에 RIGHT OUTER JOIN을 지정하는 것과 결과가 같습니다.|  
  
 **Table1>의 \<모든 행** 과 **table2>의 \<모든 행** 을 선택 하는 것은 SQL 문에 FULL OUTER JOIN을 지정 하는 것과 같습니다.  
  
 외부 조인을 만들기 위한 옵션을 선택하면 조인 선의 다이아몬드 모양이 변경되어 왼쪽 우선 외부 조인인지 오른쪽 우선 외부 조인인지 또는 완전 외부 조인인지를 나타냅니다.  
  
> [!NOTE]  
>  "왼쪽"과 "오른쪽"이라는 말이 반드시 다이어그램 창의 테이블 위치를 의미하지는 않습니다. "왼쪽"은 SQL 문에서 JOIN 키워드의 왼쪽에 이름이 나타나는 테이블을 말하고 "오른쪽"은 JOIN 키워드의 오른쪽에 이름이 나타나는 테이블을 말합니다. 
  **다이어그램** 창에서 테이블의 위치를 바꾸어도 여기에서 언급하는 왼쪽과 오른쪽이 바뀌는 것은 아닙니다.  
  
## <a name="see-also"></a>참고 항목  
 [Visual Database Tools를 &#40;조인을 사용 하 여 쿼리&#41;](visual-database-tools.md)   
 [쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
