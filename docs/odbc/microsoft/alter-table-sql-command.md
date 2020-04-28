---
title: ALTER TABLE-SQL 명령 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304714"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL 명령
테이블의 구조를 프로그래밍 방식으로 수정 합니다.  
  
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
 *TableName1*  
 구조를 수정할 테이블의 이름을 지정 합니다.  
  
 [COLUMN] *FIELDNAME1* 추가  
 추가할 필드의 이름을 지정 합니다.  
  
 ALTER [COLUMN] *FieldName1*  
 수정할 기존 필드의 이름을 지정 합니다.  
  
 *FieldType* [( *nfieldwidth* [, *nprecision*]])  
 새 필드 또는 수정 된 필드의 필드 형식, 필드 너비 및 필드 전체 자릿수 (소수 자릿수)를 지정 합니다.  
  
 *FieldType* 는 필드의 [데이터 형식을](../../odbc/microsoft/visual-foxpro-field-data-types.md)나타내는 단일 문자입니다. 일부 필드 데이터 형식에는 *Nfieldwidth* 또는 *nprecision* 또는 둘 다를 지정 해야 합니다.  
  
 D, G, I, L, M, P, T 및 Y 유형에 대해서는 *Nfieldwidth* 및 *nprecision* 이 무시 됩니다. B, F 또는 N 형식에 대해 *nprecision* 이 포함 되지 않은 경우 기본적으로 *nprecision* 은 0 (소수 자릿수 없음)입니다.  
  
 NULL &#124; NOT NULL  
 필드에서 null 값을 허용 하거나 금지 합니다.  
  
 Null 및 NOT NULL을 생략 하는 경우 현재 설정 NULL 설정에 따라 필드에서 null 값을 사용할 수 있는지 여부가 결정 됩니다. 그러나 null 및 NOT NULL을 생략 하 고 PRIMARY KEY 또는 UNIQUE 절을 포함 하는 경우 SET NULL 설정의 현재 설정은 무시 되며 기본적으로 필드는 NULL이 아닙니다.  
  
 *LEXPRESSION1* 확인  
 필드에 대 한 유효성 검사 규칙을 지정 합니다. *lExpression1* 는 논리 식으로 계산 되어야 하며 사용자 정의 함수 또는 저장 프로시저일 수 있습니다. 빈 레코드가 추가 될 때마다 유효성 검사 규칙이 확인 됩니다. 유효성 검사 규칙이 추가 된 레코드의 빈 필드 값을 허용 하지 않는 경우 오류가 생성 됩니다.  
  
 오류 *cMessageText1*  
 필드 유효성 검사 규칙에서 오류가 생성 될 때 표시 되는 오류 메시지를 지정 합니다.  
  
 기본 *eExpression1*  
 필드의 기본값을 지정 합니다. *EExpression1* 의 데이터 형식은 필드의 데이터 형식과 동일 해야 합니다.  
  
 PRIMARY KEY  
 기본 인덱스 태그를 만듭니다. 인덱스 태그의 이름은 필드와 동일 합니다.  
  
 UNIQUE  
 필드와 동일한 이름을 사용 하 여 후보 인덱스 태그를 만듭니다.  
  
> [!NOTE]  
>  ALTER TABLE 또는 CREATE TABLE의 ANSI 호환성을 위해 제공 된 고유 옵션을 포함 하 여 만든 후보 인덱스는 인덱스 명령의 UNIQUE 옵션을 사용 하 여 생성 된 인덱스와 다릅니다. Index 명령에서 UNIQUE를 사용 하 여 만든 인덱스는 중복 된 인덱스 키를 허용 합니다. 후보 인덱스는 중복 된 인덱스 키를 허용 하지 않습니다.  
  
 기본 또는 후보 인덱스에 사용 되는 필드에는 Null 값과 중복 레코드를 사용할 수 없습니다.  
  
 열 추가를 사용 하 여 새 필드를 만드는 경우 null 값을 지 원하는 필드에 대 한 기본 또는 후보 인덱스를 만들면 Visual FoxPro에서 오류를 생성 하지 않습니다. 그러나 기본 또는 후보 인덱스에 사용 되는 필드에 null 값 또는 중복 값을 입력 하려고 하면 Visual FoxPro에서 오류를 생성 합니다.  
  
 기존 필드를 수정 하는 경우 기본 또는 후보 인덱스 식이 테이블의 필드로 구성 되는 경우 Visual FoxPro는 필드를 확인 하 여 null 값 또는 중복 레코드를 포함 하 고 있는지 확인 합니다. 이렇게 하면 Visual FoxPro에서 오류를 생성 하 고 테이블이 변경 되지 않습니다.  
  
 참조 *TableName2* TAG *TagName1*  
 영구 관계가 설정 되는 부모 테이블을 지정 합니다. 태그 *TagName1* 관계의 기반이 되는 부모 테이블의 인덱스 태그를 지정 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다.  
  
 NOCPTRANS  
 문자 및 메모 필드에 대해 다른 코드 페이지로 변환할 수 없습니다. 테이블이 다른 코드 페이지로 변환 되 면 NOCPTRANS이 지정 된 필드가 변환 되지 않습니다. NOCPTRANS은 문자 및 메모 필드에만 지정할 수 있습니다.  
  
 다음 예에서는 두 개의 문자 필드와 두 개의 메모 필드를 포함 하는 mytable 이라는 테이블을 만듭니다. 두 번째 문자 필드인 char2 및 두 번째 메모 필드인 memo2에는 변환을 방지 하기 위해 NOCPTRANS이 포함 됩니다.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 수정할 기존 필드의 이름을 지정 합니다.  
  
 기본 *EEXPRESSION2* 설정  
 기존 필드의 새 기본값을 지정 합니다. *EExpression2* 의 데이터 형식은 필드의 데이터 형식과 동일 해야 합니다.  
  
 CHECK *LEXPRESSION2* 설정  
 기존 필드에 대 한 새 유효성 검사 규칙을 지정 합니다. *lExpression2* 는 논리 식으로 계산 되어야 하며 사용자 정의 함수 또는 저장 프로시저일 수 있습니다.  
  
 오류 *cMessageText2*  
 필드 유효성 검사 규칙에서 오류가 생성 될 때 표시 되는 오류 메시지를 지정 합니다. 이 메시지는 찾아보기 또는 편집 창 내에서 데이터가 변경 된 경우에만 표시 됩니다.  
  
 DROP DEFAULT  
 기존 필드의 기본값을 제거 합니다.  
  
 삭제 검사  
 기존 필드에 대 한 유효성 검사 규칙을 제거 합니다.  
  
 DROP [COLUMN] *FieldName3*  
 테이블에서 제거할 필드를 지정 합니다. 테이블에서 필드를 제거 하면 필드의 기본값 설정 및 필드 유효성 검사 규칙도 제거 됩니다.  
  
 인덱스 키 또는 트리거 식이 필드를 참조 하는 경우에는 필드가 제거 될 때 식이 유효 하지 않게 됩니다. 이 경우 필드가 제거 될 때 오류가 생성 되지 않지만 런타임에 잘못 된 인덱스 키 또는 트리거 식에서 오류가 생성 됩니다.  
  
 CHECK *LEXPRESSION3* 설정  
 테이블 유효성 검사 규칙을 지정 합니다. *lExpression3* 는 논리 식으로 계산 되어야 하며 사용자 정의 함수 또는 저장 프로시저일 수 있습니다.  
  
 오류 *cMessageText3*  
 테이블 유효성 검사 규칙에서 오류가 생성 될 때 표시 되는 오류 메시지를 지정 합니다. 이 메시지는 찾아보기 또는 편집 창 내에서 데이터가 변경 된 경우에만 표시 됩니다.  
  
 삭제 검사  
 테이블의 유효성 검사 규칙을 제거 합니다.  
  
 ADD PRIMARY KEY *eExpression3*TAG *TagName2*  
 테이블에 기본 인덱스를 추가 합니다. *eExpression3* 는 기본 인덱스 키 식을 지정 하 고 *TagName2* 는 기본 인덱스 태그의 이름을 지정 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다. TAG *TagName2* 이 생략 되 고 *eExpression3* 가 단일 필드인 경우 기본 인덱스 태그는 *eExpression3*에 지정 된 필드와 동일한 이름을 갖습니다.  
  
 기본 키 삭제  
 기본 인덱스 및 해당 인덱스 태그를 제거 합니다. 테이블에는 기본 키가 하나만 있을 수 있으므로 기본 키의 이름을 지정할 필요가 없습니다. 기본 인덱스를 제거 하면 기본 키를 기반으로 하는 모든 영구 관계도 삭제 됩니다.  
  
 UNIQUE *eExpression4*[TAG *TagName3*] 추가  
 테이블에 후보 인덱스를 추가 합니다. *eExpression4* 는 후보 인덱스 키 식을 지정 하 고 *TagName3* 는 후보 인덱스 태그의 이름을 지정 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다. *TAGNAME3* 태그를 생략 하 고 *eExpression4* 가 단일 필드인 경우 후보 인덱스 태그는 *eExpression4*에 지정 된 필드와 동일한 이름을 갖습니다.  
  
 DROP UNIQUE TAG *TagName4*  
 후보 인덱스 및 해당 인덱스 태그를 제거 합니다. 테이블에 후보 키가 여러 개 있을 수 있으므로 후보 인덱스 태그의 이름을 지정 해야 합니다.  
  
 외래 키 추가 [ *eExpression5*] 태그 *TagName4*  
 테이블에 외래 (가 아닌) 인덱스를 추가 합니다. *eExpression5* 는 외래 인덱스 키 식을 지정 하 고 *TagName4* 는 외래 인덱스 태그의 이름을 지정 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다.  
  
 참조 *TableName2*[TAG *TagName5*]  
 영구 관계가 설정 되는 부모 테이블을 지정 합니다. 부모 테이블의 기존 인덱스 태그를 기준으로 관계를 설정 하는 태그 *TagName5* 포함 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다. *TAGNAME5*태그를 생략 하면 부모 테이블의 기본 인덱스 태그를 사용 하 여 관계가 설정 됩니다.  
  
 DROP FOREIGN KEY TAG *TagName6*[저장]  
 인덱스 태그가 *TagName6*인 외래 키를 삭제 합니다. 저장을 생략 하면 인덱스 태그가 구조적 인덱스에서 삭제 됩니다. 구조적 인덱스에서 인덱스 태그를 삭제 하지 않도록 하려면 저장을 포함 합니다.  
  
 *FIELDNAME4*열 이름을 *FieldName5* 로 바꾸기  
 테이블의 필드 이름을 변경할 수 있습니다. *FieldName4* 이름이 변경 되는 필드의 이름을 지정 합니다. *FieldName5* 는 필드의 새 이름을 지정 합니다.  
  
> [!CAUTION]  
>  인덱스 식, 필드 및 테이블 유효성 검사 규칙, 명령 및 함수에서 원래 필드 이름을 참조할 수 있으므로 테이블 필드의 이름을 바꿀 때 주의 해야 합니다.  
  
 NOVALIDATE  
 Visual FoxPro에서 테이블 구조를 변경할 수 있도록 지정 합니다. 이러한 변경 내용은 테이블의 데이터 무결성을 위반할 수 있습니다. 기본적으로 Visual FoxPro는 ALTER TABLE이 테이블의 데이터 무결성을 위반 하는 변경 작업을 수행 하지 못하도록 방지 합니다. 이 기본 동작을 재정의 하려면 NOVALIDATE를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 ALTER TABLE을 사용 하 여 데이터베이스에 추가 되지 않은 테이블의 구조를 수정할 수 있습니다. 그러나 자유 테이블을 수정 하는 경우에는 기본, 외래 키, 기본 키, 참조 또는 SET 절을 포함 하는 경우 Visual FoxPro에서 오류를 생성 합니다.  
  
 ALTER TABLE은 새 테이블 헤더를 만들고 테이블 헤더에 레코드를 추가 하 여 테이블을 다시 작성할 수 있습니다. 예를 들어 필드의 형식 또는 너비를 변경 하면 테이블이 다시 작성 될 수 있습니다.  
  
 테이블을 다시 작성 한 후 형식이 나 너비가 변경 된 모든 필드에 대해 필드 유효성 검사 규칙이 실행 됩니다. 테이블에 있는 필드의 유형 또는 너비를 변경 하면 테이블 규칙이 실행 됩니다.  
  
 레코드를 포함 하는 테이블에 대해 필드 또는 테이블 유효성 검사 규칙을 수정 하면 Visual FoxPro는 기존 데이터에 대해 새 필드 또는 테이블 유효성 검사 규칙을 테스트 하 고 첫 번째 필드 또는 테이블 유효성 검사 규칙이 나 트리거 위반이 발생 했을 때 경고를 표시 합니다.  
  
 수정한 테이블이 데이터베이스에 있는 경우 ALTER TABLE-SQL은 데이터베이스를 단독으로 사용 해야 합니다. 단독으로 사용할 데이터베이스를 열려면 OPEN DATABASE에 EXCLUSIVE를 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TABLE SQL 명령](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 명령](../../odbc/microsoft/index-command.md)
