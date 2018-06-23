---
title: Excel 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e7d5c7df84ed001aa969f3fb164fa9691670fc3e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082527"
---
# <a name="excel-custom-properties"></a>Excel 사용자 지정 속성
  **원본 사용자 지정 속성**  
  
 Excel 원본에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 Excel 원본의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|정수|데이터베이스에 액세스하는 데 사용되는 모드입니다. 가능한 값은 **행 집합 열기**, **변수에서 행 집합 열기**, `SQL Command`, 및 **변수를 사용한 SQL 명령**합니다. 기본값은 **행 집합 열기**입니다.|  
|CommandTimeout|정수|명령이 종료되기 전의 제한 시간(초)입니다.  값 0은 제한 시간이 없음을 나타냅니다.<br /><br /> **참고** 이 속성은 **Excel 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|OpenRowset|String|행 집합을 여는 데 사용되는 데이터베이스 개체의 이름입니다.|  
|OpenRowsetVariable|String|행 집합을 여는 데 사용되는 데이터베이스 개체의 이름이 포함된 변수입니다.|  
|ParameterMapping|String|SQL 명령의 매개 변수에서 변수로의 매핑입니다.|  
|SqlCommand|String|실행할 SQL 명령입니다.|  
|SqlCommandVariable|String|실행할 SQL 명령이 포함된 변수입니다.|  
  
 Excel 원본의 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Excel Source](excel-source.md)을 참조하세요.  
  
 **대상 사용자 지정 속성**  
  
 Excel 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 Excel 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer(열거형)|대상에서 해당 대상 데이터베이스에 액세스하는 방법을 지정하는 값입니다.<br /><br /> 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> `OpenRowset` (0)-테이블 또는 뷰의 이름을 제공 해야 합니다.<br /><br /> `OpenRowset from Variable` (1)-테이블 또는 뷰의 이름이 포함 된 변수의 이름을 제공 해야 합니다.<br /><br /> `OpenRowset Using Fastload`(3) - 테이블 또는 뷰의 이름을 제공해야 합니다.<br /><br /> `OpenRowset Using Fastload from Variable` (4)-테이블 또는 뷰의 이름이 포함 된 변수의 이름을 제공 해야 합니다.<br /><br /> `SQL Command`(2) - SQL 문을 제공해야 합니다.|  
|CommandTimeout|정수|제한 시간이 초과될 때까지 SQL 명령을 실행할 수 있는 최대 시간(초)입니다. 값 **0** 은 제한 시간이 없음을 의미합니다. 이 속성의 기본값은 **0**입니다.<br /><br /> 참고: 이 속성은 **Excel 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|FastLoadKeepIdentity|Boolean|데이터를 로드할 때 ID 값을 복사할지 여부를 지정하는 값입니다. 이 속성은 빠른 로드 옵션 중 하나를 사용할 경우에만 사용할 수 있습니다. 이 속성의 기본값은 **False**입니다.|  
|FastLoadKeepNulls|Boolean|데이터를 로드할 때 Null 값을 복사할지 여부를 지정하는 값입니다. 이 속성은 빠른 로드 옵션 중 하나와 함께 사용해야 합니다. 이 속성의 기본값은 **False**입니다.|  
|FastLoadMaxInsertCommitSize|정수|Excel 대상에서 빠른 로드 작업을 수행하는 동안 커밋을 시도하는 일괄 처리 크기를 지정하는 값입니다. 기본값은 **2147483647**입니다. **0** 값은 모든 행이 처리된 후의 단일 커밋 작업을 나타냅니다.|  
|FastLoadOptions|String|빠른 로드 옵션 모음입니다. 빠른 로드 옵션에는 테이블 잠금 및 제약 조건 검사가 포함됩니다. 둘 다 또는 둘 중 하나를 지정하거나 아무 것도 지정하지 않을 수 있습니다.<br /><br /> 참고: 이 속성의 일부 옵션은 **Excel 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|OpenRowset|String|AccessMode 다음과 같은 경우 `OpenRowset`를 Excel 대상에서 액세스 하는 뷰나 테이블의 이름입니다.|  
|OpenRowsetVariable|String|AccessMode 다음과 같은 경우 `OpenRowset from Variable`를 Excel 대상에서 액세스 하는 뷰나 테이블의 이름이 포함 된 변수의 이름입니다.|  
|SqlCommand|String|AccessMode 다음과 같은 경우 `SQL Command`를 Excel 대상 사용 하 여 데이터에 대 한 대상 열을 지정 하는 Transact SQL 문입니다.|  
  
 Excel 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Excel Destination](excel-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Common Properties](../common-properties.md)  
  
  