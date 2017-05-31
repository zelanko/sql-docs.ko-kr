---
title: "열 속성(일반 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.columnproperties.general.f1
ms.assetid: a745890b-994e-4c23-8028-5c83751e60c4
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 478dc0e10767f9e4e10c5c3ede74aec5ddaddef4
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="column-properties-general-page"></a>열 속성(일반 페이지)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  이 페이지를 사용하여 선택한 열의 속성을 볼 수 있습니다.  
  
 이 페이지의 정보는 읽기 전용입니다. 열을 수정하려면 **열 속성** 대화 상자를 닫고, 개체 탐색기에서 테이블과 열을 확장하고, 열을 마우스 오른쪽 단추로 클릭한 다음 **디자인**을 클릭합니다.  
  
## <a name="options"></a>옵션  
 **이름**  
 열 이름입니다.  
  
 **데이터 형식**  
 열에서 보유할 수 있는 데이터 형식입니다. 데이터 형식이 사용자 정의 데이터 형식인 경우 해당 형식이 표시됩니다. 사용자 정의 데이터 형식이 아닌 경우에는 시스템 데이터 형식이 표시됩니다. 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.  
  
 **시스템 유형**  
 열에서 보유할 수 있는 데이터 형식입니다. 데이터 형식이 시스템 데이터 형식인 경우 해당 형식이 표시됩니다. 사용자 정의 데이터 형식인 경우에는 해당 사용자 정의 데이터 형식을 구성하는 시스템 데이터 형식이 표시됩니다.  
  
 **기본 키**  
 열이 기본 키인지 여부를 나타냅니다. 가능한 값은 **True**및 **False**입니다.  
  
 **Null 허용**  
 열에 Null 값을 사용할 수 있는지 여부를 나타냅니다. 가능한 값은 **True** 및 **False**입니다.  
  
 **계산 여부**  
 열 값이 계산 식의 결과 값인지 여부를 나타냅니다.  
  
 **계산된 텍스트**  
 열 텍스트 계산에 사용된 문을 나타냅니다. 자세한 내용은 [Specify Computed Columns in a Table](../../relational-databases/tables/specify-computed-columns-in-a-table.md)을 참조하십시오.  
  
 **ID**  
 테이블에 대한 ID 열인지 여부를 나타냅니다. 가능한 값은 **True** 및 **False**입니다.  
  
 **ID 초기값**  
 ID 열의 초기 행 값을 나타냅니다.  
  
 **ID 증가값**  
 **ID 증분** 속성은 새로 삽입되는 행의 ID 값을 생성할 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 기존의 가장 큰 행 ID 값에 추가하는 값을 지정합니다.  
  
 **기본 바인딩**  
 열에 바인딩된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본값입니다. 기본값이 바인딩되지 않은 경우에 이 옵션은 공백입니다.  
  
 **기본 스키마**  
 참조된 열에 바인딩된 기본값을 소유하는 데이터베이스 스키마를 나타냅니다. 기본값이 바인딩되지 않은 경우에 이 옵션은 공백입니다.  
  
 **규칙**  
 열에 바인딩된 데이터 무결성 제약 조건을 나타냅니다. 규칙이 바인딩되지 않은 경우에 이 옵션은 공백입니다.  
  
 **규칙 스키마**  
 참조된 열에 바인딩된 규칙을 소유하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 스키마를 나타냅니다. 규칙이 바인딩되지 않은 경우에 이 옵션은 공백입니다.  
  
 **길이**  
 열에 허용되는 최대 문자 또는 바이트 수를 나타냅니다.  
  
 **데이터 정렬**  
 열에 지정되어 있는 데이터 정렬을 표시합니다. 이 옵션이 공백인 경우 개체의 데이터 정렬 속성이 상속됩니다.  
  
 **전체 자릿수**  
 고정 전체 자릿수의 숫자 데이터 형식에서 최대 자릿수를 나타냅니다.  
  
 **소수 자릿수**  
 고정 전체 자릿수의 숫자 데이터 형식에서 소수점 이하 자릿수를 나타냅니다.  
  
 **XML 스키마 네임스페이스**  
 XSD(XML 스키마 정의) 언어 유효성 검사를 통해 XML 열의 형식을 정의합니다.  
  
 **XML 스키마 네임스페이스 스키마**  
 XML 스키마 네임스페이스를 소유하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마입니다.  
  
> [!NOTE]  
>  스키마는 일반적인 용어지만 몇 가지 다른 의미를 가지고 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 스키마는 데이터베이스 개체를 구성하는 데 사용됩니다. 소유권과 비슷한 개념이라 할 수 있습니다. XML에서는 XML 정보 구성을 일련의 네임스페이스로 정의하는 데 스키마가 사용됩니다. 즉, 스키마를 통해 관련된 XML 코드가 그룹화됩니다.  
  
 **스파스 여부**  
 열이 스파스 열인지 여부를 나타냅니다. 가능한 값은 **True** 및 **False**입니다. 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.  
  
 **열 집합 여부**  
 열이 열 집합인지 여부를 나타냅니다. 가능한 값은 **True** 및 **False**입니다. 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
 **ANSI 패딩 상태**  
 ANSI 패딩의 설정 여부를 나타냅니다. 자세한 내용은 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.  
  
 **전체 텍스트**  
 열이 전체 텍스트 쿼리에 참여하는지 여부를 나타냅니다.  
  
 **통계 의미 체계**  
 열에 대해 통계 의미 체계 검색을 사용하도록 설정할지 여부를 나타냅니다. 자세한 내용은 [의미 체계 검색&#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)을 참조하세요.  
  
 **복제용 아님**  
 열을 복제할 수 있는지 여부를 나타냅니다. 가능한 값은 **True** 및 **False**입니다.  
  
  
