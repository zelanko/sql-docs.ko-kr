---
title: 테이블 변경 - SQL 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 587d721522503f9b392bb8be7433850fd7449efb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304714"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL 명령
테이블의 구조를 프로그래밍 방식으로 수정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>인수  
 *테이블네임1*  
 구조가 수정된 테이블의 이름을 지정합니다.  
  
 [열] *필드 이름 1* 추가  
 추가할 필드의 이름을 지정합니다.  
  
 [열] *필드 이름 1* 변경  
 수정할 기존 필드의 이름을 지정합니다.  
  
 *필드 타입* *[(n필드 폭* [, *nPrecision]])*  
 새 필드 또는 수정된 필드에 대한 필드 유형, 필드 너비 및 필드 정밀도(소수점 소수점 수)를 지정합니다.  
  
 *FieldType은* 필드의 [데이터 형식을](../../odbc/microsoft/visual-foxpro-field-data-types.md)나타내는 단일 문자입니다. 일부 필드 데이터 형식은 *nFieldWidth* 또는 *nPrecision* 또는 둘 다를 지정해야 합니다.  
  
 *n필드폭* 및 *nPrecision은* D, G, I, L, M, P, T 및 Y 유형에 대해 무시됩니다. 기본적으로 *nPrecision은* b, F 또는 N 형식에 *대해 nPrecision이* 포함되지 않은 경우 0(소수자릿수 없음)입니다.  
  
 NULL &#124; NOT NULL  
 필드의 null 값을 허용하거나 방지합니다.  
  
 NULL 및 NOT NULL을 생략하는 경우 SET NULL의 현재 설정은 필드에서 null 값이 허용되는지 여부를 결정합니다. 그러나 NULL 및 NOT NULL을 생략하고 기본 키 또는 UNIQUE 절을 포함하는 경우 SET NULL의 현재 설정은 무시되고 필드는 기본적으로 NULL이 아닙니다.  
  
 체크 *lExpression1*  
 필드에 대한 유효성 검사 규칙을 지정합니다. *lExpression1은* 논리적 식으로 평가해야 하며 사용자 정의 함수 또는 저장 프로시저일 수 있습니다. 빈 레코드가 추가될 때마다 유효성 검사 규칙이 검사됩니다. 유효성 검사 규칙이 추가된 레코드의 빈 필드 값을 허용하지 않는 경우 오류가 생성됩니다.  
  
 오류 *c메시지텍스트1*  
 필드 유효성 검사 규칙에서 오류를 생성할 때 표시되는 오류 메시지를 지정합니다.  
  
 기본 *eExpression1*  
 필드에 대한 기본값을 지정합니다. *eExpression1의* 데이터 형식은 필드의 데이터 형식과 같아야 합니다.  
  
 PRIMARY KEY  
 기본 인덱스 태그를 만듭니다. 인덱스 태그의 이름은 필드와 같습니다.  
  
 UNIQUE  
 필드와 이름이 같은 후보 인덱스 태그를 만듭니다.  
  
> [!NOTE]  
>  후보 인덱스(ALTER TABLE 또는 CREATE TABLE에서 ANSI 호환성을 위해 제공된 고유 옵션을 포함하여 생성됨)는 INDEX 명령에서 고유 옵션을 사용하여 만든 인덱스와 다릅니다. INDEX 명령에서 UNIQUE를 사용하여 만든 인덱스는 중복 인덱스 키를 허용합니다. 후보 인덱스는 중복 인덱스 키를 허용하지 않습니다.  
  
 Null 값 및 중복 레코드는 기본 또는 후보 인덱스에 사용되는 필드에서 허용되지 않습니다.  
  
 추가 열을 사용 하 여 새 필드를 만드는 경우 Null 값을 지 원하는 필드에 대 한 기본 또는 후보 인덱스를 만드는 경우 Visual FoxPro 오류를 생성 하지 않습니다. 그러나 Visual FoxPro는 기본 또는 후보 인덱스에 사용되는 필드에 null 또는 중복 값을 입력하려고 하면 오류를 생성합니다.  
  
 기존 필드를 수정하고 기본 또는 후보 인덱스 표현식이 테이블의 필드로 구성된 경우 Visual FoxPro는 필드를 검사하여 해당 필드가 null 값또는 중복 레코드를 포함하는지 여부를 확인합니다. 이 경우 Visual FoxPro에서 오류가 발생하고 테이블이 변경되지 않습니다.  
  
 참조 *표Name2* *태그이름1*  
 영구 관계가 설정된 상위 테이블을 지정합니다. 태그 *이름1관계의* 기반이 되는 상위 테이블의 인덱스 태그를 지정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다.  
  
 노CP트랜스  
 문자 및 메모 필드에 대한 다른 코드 페이지로 변환을 방지합니다. 테이블이 다른 코드 페이지로 변환되면 NOCPTRANS가 지정된 필드는 번역되지 않습니다. NOCPTRANS는 문자 및 메모 필드에 대해서만 지정할 수 있습니다.  
  
 다음 예제에서 두 개의 문자 필드와 두 개의 메모 필드를 포함 하는 mytable 라는 테이블을 만듭니다. 두 번째 문자 필드char2 및 두 번째 메모 필드인 memo2에는 번역을 방지하기 위해 NOCPTRANS가 포함됩니다.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 [열] *필드이름2* 변경  
 수정할 기존 필드의 이름을 지정합니다.  
  
 기본 *eExpression2* 설정  
 기존 필드에 대한 새 기본값을 지정합니다. *eExpression2의* 데이터 형식은 필드의 데이터 형식과 같아야 합니다.  
  
 설정 검사 *lExpression2*  
 기존 필드에 대한 새 유효성 검사 규칙을 지정합니다. *lExpression2는* 논리적 식으로 평가해야 하며 사용자 정의 함수 또는 저장 프로시저일 수 있습니다.  
  
 오류 *c메시지텍스트2*  
 필드 유효성 검사 규칙에서 오류를 생성할 때 표시되는 오류 메시지를 지정합니다. 데이터는 찾아보기 또는 편집 창 내에서 변경된 경우에만 메시지가 표시됩니다.  
  
 DROP DEFAULT  
 기존 필드의 기본값을 제거합니다.  
  
 드롭 체크  
 기존 필드에 대한 유효성 검사 규칙을 제거합니다.  
  
 드롭 [열] *필드이름3*  
 테이블에서 제거할 필드를 지정합니다. 테이블에서 필드를 제거하면 필드의 기본값 설정 및 필드 유효성 검사 규칙도 제거됩니다.  
  
 인덱스 키 또는 트리거 식이 필드를 참조하는 경우 필드를 제거할 때 식이 잘못됩니다. 이 경우 필드를 제거할 때 오류가 생성되지 않지만 잘못된 인덱스 키 또는 트리거 식은 런타임에 오류를 생성합니다.  
  
 설정 검사 *lExpression3*  
 테이블 유효성 검사 규칙을 지정합니다. *lExpression3는* 논리적 식으로 평가해야 하며 사용자 정의 함수 또는 저장 프로시저일 수 있습니다.  
  
 오류 *c메시지텍스트3*  
 테이블 유효성 검사 규칙에서 오류를 생성할 때 표시되는 오류 메시지를 지정합니다. 데이터는 찾아보기 또는 편집 창 내에서 변경된 경우에만 메시지가 표시됩니다.  
  
 드롭 체크  
 테이블의 유효성 검사 규칙을 제거합니다.  
  
 기본 키 *eExpression3* *태그이름2* 추가  
 테이블에 기본 인덱스를 추가합니다. *eExpression3는* 기본 인덱스 키 식을 지정하고 *TagName2는* 기본 인덱스 태그의 이름을 지정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다. *태그TagName2가* 생략되고 *eExpression3이* 단일 필드인 경우 기본 인덱스 태그는 *eExpression3에*지정된 필드와 이름이 같습니다.  
  
 기본 키 삭제  
 기본 인덱스 와 해당 인덱스 태그를 제거합니다. 테이블에는 기본 키가 하나만 있을 수 있으므로 기본 키의 이름을 지정할 필요는 없습니다. 또한 기본 인덱스를 제거하면 기본 키를 기반으로 하는 영구 관계도 삭제됩니다.  
  
 고유 *eExpression4* *[태그네임3]* 추가  
 테이블에 후보 인덱스를 추가합니다. *eExpression4는* 후보 인덱스 키 식을 지정하고 *TagName3는* 후보 인덱스 태그의 이름을 지정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다. *TAGName3을* 생략하고 *eExpression4가* 단일 필드인 경우 후보 인덱스 태그의 이름은 *eExpression4에*지정된 필드와 동일합니다.  
  
 고유 태그 *태그 이름* 4 삭제  
 후보 인덱스와 해당 인덱스 태그를 제거합니다. 테이블에 여러 후보 키가 있을 수 있으므로 후보 인덱스 태그의 이름을 지정해야 합니다.  
  
 외래 키 추가 *[eExpression5]태그네임4* *TagName4*  
 테이블에 외래(비기본) 인덱스를 추가합니다. *eExpression5는* 외래 인덱스 키 식을 지정하고 *TagName4는* 외래 인덱스 태그의 이름을 지정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다.  
  
 참조 *표Name2* *[태그네임5]*  
 영구 관계가 설정된 상위 테이블을 지정합니다. 태그 *TagName5를* 포함하여 상위 테이블에 대한 기존 인덱스 태그를 기반으로 관계를 설정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다. *TAGName5를*생략하면 상위 테이블의 기본 인덱스 태그를 사용하여 관계가 설정됩니다.  
  
 드롭 이외 키 *태그네임6*[저장]  
 인덱스 태그가 *TagName6인*외래 키를 삭제합니다. SAVE를 생략하면 구조 인덱스에서 인덱스 태그가 삭제됩니다. 구조 인덱스에서 인덱스 태그가 삭제되지 않도록 SAVE를 포함합니다.  
  
 열 *필드이름4에서* *필드Name5로* 이름 바꾸기  
 테이블에서 필드 이름을 변경할 수 있습니다. *FieldName4는* 이름이 바뀌는 필드의 이름을 지정합니다. *FieldName5필드의* 새 이름을 지정합니다.  
  
> [!CAUTION]  
>  인덱스 식, 필드 및 테이블 유효성 검사 규칙, 명령 및 함수가 원래 필드 이름을 참조할 수 있으므로 테이블 필드의 이름을 바꿀 때 주의하십시오.  
  
 무효화 없음  
 Visual FoxPro에서 테이블 의 구조를 변경할 수 있도록 지정합니다. 이러한 변경 사항은 테이블의 데이터의 무결성을 위반할 수 있습니다. 기본적으로 Visual FoxPro는 ALTER TABLE에서 테이블의 데이터 무결성을 위반하는 변경을 하지 못하도록 합니다. 이 기본 동작을 재정의하려면 NOVALIDATE를 포함합니다.  
  
## <a name="remarks"></a>설명  
 ALTER TABLE은 데이터베이스에 추가되지 않은 테이블의 구조를 수정하는 데 사용할 수 있습니다. 그러나 Visual FoxPro는 사용 가능한 테이블을 수정할 때 기본값, 외래 키, 기본 키, 참조 또는 SET 절을 포함하는 경우 오류를 생성합니다.  
  
 ALTER TABLE은 새 테이블 헤더를 만들고 테이블 헤더에 레코드를 더하여 테이블을 다시 만들 수 있습니다. 예를 들어 필드의 형식이나 너비를 변경하면 테이블을 다시 빌드할 수 있습니다.  
  
 테이블을 다시 빌드한 후 형식 또는 너비가 변경된 모든 필드에 대해 필드 유효성 검사 규칙이 실행됩니다. 테이블의 모든 필드의 형식이나 너비를 변경하면 테이블 규칙이 실행됩니다.  
  
 레코드가 있는 테이블에 대한 필드 또는 테이블 유효성 검사 규칙을 수정하는 경우 Visual FoxPro는 기존 데이터에 대해 새 필드 또는 테이블 유효성 검사 규칙을 테스트하고 필드 또는 테이블 유효성 검사 규칙또는 트리거 위반의 첫 번째 발생에 대한 경고를 발행합니다.  
  
 수정한 테이블이 데이터베이스에 있는 경우 ALTER TABLE - SQL은 데이터베이스를 단독으로 사용해야 합니다. 단독 사용을 위해 데이터베이스를 열려면 OPEN 데이터베이스에 배타적 을 포함하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 만들기 - SQL 명령](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 명령](../../odbc/microsoft/index-command.md)
