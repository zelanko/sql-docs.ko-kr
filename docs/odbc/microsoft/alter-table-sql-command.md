---
title: ALTER TABLE-SQL 명령 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9897be4d0e594c82aa872f904d500bd1216d40f0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table---sql-command"></a>ALTER TABLE-SQL 명령
프로그래밍 방식으로 테이블의 구조를 수정합니다.  
  
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
 해당 구조를 수정할 테이블의 이름을 지정 합니다.  
  
 추가 [COLUMN] *FieldName1*  
 추가할 필드의 이름을 지정 합니다.  
  
 ALTER [COLUMN] *FieldName1*  
 수정할 기존 필드의 이름을 지정 합니다.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 새롭거나 수정 된 필드에 대 한 필드 형식, 필드 너비 및 필드 전체 자릿수 (소수 자릿수 초)을 지정합니다.  
  
 *FieldType* 은 단일 문자 필드의 나타내는 [데이터 형식을](../../odbc/microsoft/visual-foxpro-field-data-types.md)합니다. 일부 필드 데이터 유형을 지정 하는 필요한 *nFieldWidth* 또는 *nPrecision* 또는 둘 다 합니다.  
  
 *nFieldWidth* 및 *nPrecision* D, G, I, L, M, P, T, 및 Y에 대 한 무시 형식입니다. 기본적으로 *nPrecision* 경우 0 (소수 자릿수 없음)은 *nPrecision* B, F, 또는 N 형식에 대 한 포함 되지 않습니다.  
  
 NULL &#124; NOT NULL  
 허용 하거나 필드에 null 값을 방지 합니다.  
  
 NOT NULL 및 NULL를 생략 NULL 설정의 현재 설정을 필드에 null 값 허용 여부를 결정 합니다. 그러나 생략 NULL 및 NOT NULL 기본 키 또는 고유 절이 포함 NULL 설정의 현재 설정을 무시 되 고 필드가 기본적으로 NULL입니다.  
  
 확인 *lExpression1*  
 필드에 대 한 유효성 검사 규칙을 지정합니다. *lExpression1* 논리 식으로 계산 되어야 하 고 사용자 정의 함수 또는 저장된 프로시저일 수 있습니다. 빈 레코드가 추가 될 때마다 유효성 검사 규칙 검사 됩니다. 추가 된 레코드의 빈 필드 값에 대 한 유효성 검사 규칙을 허용 하지 않는 경우 오류가 생성 됩니다.  
  
 오류 *cMessageText1*  
 필드 유효성 검사 규칙 오류를 생성 하는 경우 오류 메시지가 표시를 지정 합니다.  
  
 기본 *eExpression1*  
 필드에 대 한 기본값을 지정합니다. 데이터 형식이 *eExpression1* 필드에 대 한 데이터 형식과 동일 해야 합니다.  
  
 PRIMARY KEY  
 기본 인덱스 태그를 만듭니다. 인덱스 태그 필드와 동일한 이름이 있습니다.  
  
 UNIQUE  
 필드와 동일한 이름을 가진 후보 인덱스 태그를 만듭니다.  
  
> [!NOTE]  
>  후보 INDEX 명령에 고유한 옵션을 사용 하 여 생성 된 인덱스에서 인덱스 (ALTER TABLE 또는 CREATE TABLE에서 ANSI 호환성을 위해 제공 하는 고유한 옵션을 포함 하 여 생성) 다릅니다. UNIQUE INDEX 명령에 사용 하 여 만든 인덱스를 사용 하면 중복 인덱스 키는; 후보 인덱스는 중복 인덱스 키를 허용 하지 않습니다.  
  
 Null 값과 중복 레코드는 주 가상 컴퓨터 또는 후보 인덱스에 사용 되는 필드에 허용 되지 않습니다.  
  
 열 추가 사용 하 여 새 필드를 만드는 경우 null 값을 지 원하는 필드에 주 가상 컴퓨터 또는 후보 인덱스를 만들면 Visual FoxPro 오류가 발생 하지 않습니다. 그러나 Visual FoxPro 주 가상 컴퓨터 또는 후보 인덱스에 사용 되는 필드에 null 또는 중복 값을 입력 하려고 하면 오류가 발생 합니다.  
  
 기존 필드와 주를 수정 하는 후보 인덱스 식 구성 테이블의 필드 또는, Visual FoxPro 필드를 null 값 이나 중복 레코드가 포함 되어 있는지를 확인 합니다. 그럴 경우 Visual FoxPro에 오류가 발생 하 고 테이블은 변경 되지 않습니다.  
  
 참조 *TableName2* 태그 *TagName1*  
 영구 관계가 설정 됩니다 부모 테이블을 지정 합니다. 태그 *TagName1* 관계의 기반이 되는 부모 테이블의 인덱스 태그를 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 NOCPTRANS  
 문자 및 메모 필드에 대 한 다른 코드 페이지를 변환을 하지 않습니다. 테이블에 다른 코드 페이지 변환, NOCPTRANS 지정 된 필드는 번역 되지 않습니다. NOCPTRANS 문자 및 메모 필드에 대해서만 지정할 수 있습니다.  
  
 다음 예제에서는 두 개의 문자 필드 및 두 개의 메모 필드가 포함 된 mytable 이라는 테이블을 만듭니다. 두 번째 문자 필드, char2, 및 두 번째 메모 필드 memo2, NOCPTRANS 번역을 방지 하기 위해 포함 됩니다.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 수정할 기존 필드의 이름을 지정 합니다.  
  
 집합 기본 *eExpression2*  
 기존 필드에 대 한 새 기본값을 지정합니다. 데이터 형식이 *eExpression2* 필드에 대 한 데이터 형식과 동일 해야 합니다.  
  
 집합 검사 *lExpression2*  
 기존 필드에 대 한 새 유효성 검사 규칙을 지정합니다. *lExpression2* 논리 식 평가 되어야 하며 사용자 정의 함수 또는 저장된 프로시저일 수 있습니다.  
  
 오류 *cMessageText2*  
 필드 유효성 검사 규칙 오류를 생성 하는 경우 오류 메시지가 표시를 지정 합니다. 메시지는 찾아보기 또는 편집 창 내에서 데이터가 변경 되는 경우에 표시 됩니다.  
  
 DROP DEFAULT  
 기존 필드에 대 한 기본값을 제거합니다.  
  
 삭제 확인  
 기존 필드에 대 한 유효성 검사 규칙을 제거합니다.  
  
 DROP [COLUMN] *FieldName3*  
 테이블에서 제거 하려면 필드를 지정 합니다. 필드의 기본값 설정 및 필드 유효성 검사 규칙 제거도 테이블에서 필드를 제거 합니다.  
  
 인덱스 키 또는 트리거의 식에서 필드를 참조 하는 경우 필드 제거 될 때 식이 유효 하지 않게 합니다. 이 경우에 필드가 제거 되지만 잘못 된 인덱스 키 또는 트리거의 식 실행 시 오류가 발생 합니다 오류가 생성 되지 않습니다.  
  
 집합 검사 *lExpression3*  
 테이블 유효성 검사 규칙을 지정합니다. *lExpression3* 논리 식 평가 되어야 하며 사용자 정의 함수 또는 저장된 프로시저일 수 있습니다.  
  
 오류 *cMessageText3*  
 테이블 유효성 검사 규칙 오류를 생성 하는 경우 오류 메시지가 표시를 지정 합니다. 메시지는 찾아보기 또는 편집 창 내에서 데이터가 변경 되는 경우에 표시 됩니다.  
  
 삭제 확인  
 테이블의 유효성 검사 규칙을 제거합니다.  
  
 기본 키 추가 *eExpression3*태그 *TagName2*  
 기본 인덱스를 테이블에 추가합니다. *eExpression3* 기본 인덱스 키 식을 지정 하 고 *TagName2* 기본 인덱스 태그의 이름을 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다. 하는 경우 태그 *TagName2* 를 생략 하면 및 *eExpression3* 는 단일 필드에 지정 된 필드와 이름이 같은 기본 인덱스 태그 *eExpression3*합니다.  
  
 기본 키 삭제  
 기본 인덱스 및 해당 인덱스 태그를 제거합니다. 테이블 기본 키가 하나만 있을 수 있습니다, 때문에 기본 키의 이름을 지정할 필요는 없습니다. 기본 키에 따라 모든 영구 관계 삭제도 기본 인덱스를 제거 합니다.  
  
 추가 UNIQUE *eExpression4*[태그 *TagName3*]  
 테이블에 후보 인덱스를 추가합니다. *eExpression4* 후보 인덱스 키 식을 지정 하 고 *TagName3* 후보 인덱스 태그의 이름을 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다. 태그를 생략할 경우 *TagName3* 쓰고 *eExpression4* 는 단일 필드에 지정 된 필드와 이름이 같은 후보 인덱스 태그 *eExpression4*합니다.  
  
 DROP 고유 태그 *TagName4*  
 후보 인덱스 및 해당 인덱스 태그를 제거합니다. 테이블에 후보 키가 여러 개 있을 수 있지만, 때문에 후보 인덱스 태그의 이름을 지정 해야 합니다.  
  
 외래 키 추가 [ *eExpression5*] 태그 *TagName4*  
 테이블에 외래 (비기본) 인덱스를 추가합니다. *eExpression5* 외래 인덱스 키 식을 지정 하 고 *TagName4* 외래 인덱스 태그의 이름을 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 참조 *TableName2*[태그 *TagName5*]  
 영구 관계가 설정 됩니다 부모 테이블을 지정 합니다. Include 태그 *TagName5* 부모 테이블에 대 한 기존 인덱스 태그에 따라 관계를 설정할 수 있습니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다. 태그를 생략할 경우 *TagName5*, 부모 테이블의 기본 인덱스 태그를 사용 하는 관계가 설정 됩니다.  
  
 DROP 외래 키 태그 *TagName6*[저장]  
 해당 인덱스 태그는 외래 키가 삭제 *TagName6*합니다. 저장을 생략 하면 인덱스 태그 구조적 인덱스에서 삭제 됩니다. 구조적 인덱스에서 인덱스 태그의 삭제를 방지 하려면 저장을 포함 합니다.  
  
 열 이름 바꾸기 *FieldName4*TO *FieldName5*  
 테이블에 있는 필드의 이름을 변경할 수 있습니다. *FieldName4* 이름이 바뀐 필드의 이름을 지정 합니다. *FieldName5* 필드의 새 이름을 지정 합니다.  
  
> [!CAUTION]  
>  인덱스 식, 테이블 및 필드 유효성 검사 규칙, 명령 및 함수는 원래 필드 이름을 참조할 수 있으므로 테이블 필드의 이름을 바꿀 때 특별히 주의 해야 합니다.  
  
 NOVALIDATE  
 Visual FoxPro 테이블의 구조 변경 해야 하는 변경할 수 있는지를 지정 합니다. 이러한 변경 테이블에 데이터의 무결성을 위반할 수 있습니다. 기본적으로 Visual FoxPro 테이블에 데이터의 무결성을 위반 하는 변경을 ALTER TABLE을 방지 합니다. 이 기본 동작을 재정의할 NOVALIDATE 포함 됩니다.  
  
## <a name="remarks"></a>주의  
 데이터베이스에 추가 되지 않은 테이블의 구조를 수정 하려면 ALTER TABLE는 사용할 수 있습니다. 그러나 Visual FoxPro 기본, 외래 키, 기본 키, 참조, 포함 하거나 빈 테이블을 수정할 때 SET 절의 경우 오류가 발생 합니다.  
  
 ALTER TABLE 새 테이블 머리글을 만들고 테이블 머리글에 레코드를 추가 하 여 테이블을 다시 작성 될 수 있습니다. 예를 들어, 필드의 형식 또는 너비를 변경 하면 표를 다시 작성 해야 합니다.  
  
 표를 다시 빌드한 후 종류나 너비가 변경 되는 모든 필드에 대 한 필드 유효성 검사 규칙 실행 됩니다. 유형 또는 테이블의 모든 필드의 너비를 변경 하면 테이블 규칙이 실행 됩니다.  
  
 레코드가 테이블에 대 한 필드 또는 테이블 유효성 검사 규칙을 수정 하는 경우 Visual FoxPro 기존 데이터에 대 한 새 필드 또는 테이블 유효성 검사 규칙을 테스트 하 고 맨 처음 발견 되는 필드 또는 테이블 유효성 검사 규칙 또는 트리거 위반에 경고를 발생 시킵니다.  
  
 수정 하면 테이블이 데이터베이스에서 ALTER TABLE-경우 SQL 데이터베이스를 배타적으로 사용을 해야 합니다. 독점적인 사용을 위해 데이터베이스를 열려면 배타적 데이터베이스 열에 포함 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블-SQL 명령을 만들려면](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 명령](../../odbc/microsoft/index-command.md)
