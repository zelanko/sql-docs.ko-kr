---
title: 테이블 만들기 - SQL 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfc80a56a021b1bfeda38115e79f7086632900c8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298693"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 명령
지정된 필드가 있는 테이블을 만듭니다.  
  
 Visual FoxPro ODBC 드라이버는 이 명령에 대한 기본 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 **드라이버 설명**을 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>인수  
 테이블 만들기 &#124; DBF *테이블Name1*  
 만들 테이블 이름을 지정합니다. 테이블 및 DBF 옵션은 동일합니다.  
  
 이름 *롱테이블네임*  
 테이블에 대한 긴 이름을 지정합니다. 긴 테이블 이름은 데이터베이스에 저장되므로 데이터베이스가 열려 있는 경우에만 긴 테이블 이름을 지정할 수 있습니다.  
  
 긴 이름은 최대 128자까지 포함될 수 있으며 데이터베이스의 짧은 파일 이름 대신 사용할 수 있습니다.  
  
 FREE  
 테이블이 열려 있는 데이터베이스에 추가되지 않도록 지정합니다. 데이터베이스가 열려 있지 않은 경우 FREE가 필요하지 않습니다.  
  
 *(필드네임1 필드 타입* [(nFieldWidth [, *nFieldWidth* *nPrecision])]*  
 필드 이름, 필드 유형, 필드 너비 및 필드 정밀도(소수점 자리 수)를 각각 지정합니다.  
  
 *FieldType은* 필드의 [데이터 형식을](../../odbc/microsoft/visual-foxpro-field-data-types.md)나타내는 단일 문자입니다. 일부 필드 데이터 형식은 *nFieldWidth* 또는 *nPrecision* 또는 둘 다를 지정해야 합니다.  
  
 *n필드폭* 및 *nPrecision은* D, G, I, L, M, P, T 및 Y 유형에 대해 무시됩니다. *nPrecision* 기본값은 b, F 또는 N 형식에 *대해 nPrecision이* 포함되지 않은 경우 0(소수자릿수 없음)으로 설정합니다.  
  
 NULL  
 필드에서 null 값을 허용합니다.  
  
 NOT NULL  
 필드에서 null 값을 방지합니다.  
  
 NULL 및 NOT NULL을 생략하는 경우 SET NULL의 현재 설정은 필드에서 null 값이 허용되는지 여부를 결정합니다. 그러나 NULL 및 NOT NULL을 생략하고 기본 키 또는 UNIQUE 절을 포함하는 경우 SET NULL의 현재 설정은 무시되고 필드는 NULL이 아닌 기본값으로 설정됩니다.  
  
 체크 *lExpression1*  
 필드에 대한 유효성 검사 규칙을 지정합니다. *lExpression1은* 사용자 정의 함수일 수 있습니다. 빈 레코드가 추가될 때마다 유효성 검사 규칙이 검사됩니다. 유효성 검사 규칙이 추가된 레코드의 빈 필드 값을 허용하지 않는 경우 오류가 생성됩니다.  
  
 오류 *c메시지텍스트1*  
 필드 규칙에 오류가 생성될 때 Visual FoxPro가 표시되는 오류 메시지를 지정합니다. 데이터는 찾아보기 창 또는 편집 창 내에서 변경된 경우에만 메시지가 표시됩니다.  
  
 기본 *eExpression1*  
 필드에 대한 기본값을 지정합니다. *eExpression1의* 데이터 형식은 필드의 데이터 형식과 같아야 합니다.  
  
 PRIMARY KEY  
 필드에 대한 기본 인덱스를 만듭니다. 기본 인덱스 태그의 이름은 필드와 같습니다.  
  
 UNIQUE  
 필드에 대한 후보 인덱스를 만듭니다. 후보 인덱스 태그의 이름은 필드와 같습니다.  
  
> [!NOTE]  
>  후보 인덱스(테이블 만들기 또는 ALTER TABLE - SQL에 고유 옵션을 포함하여 생성됨)는 INDEX 명령에서 고유 옵션으로 만든 인덱스와 다다친 인덱스와 다다. INDEX 명령에서 고유 옵션으로 만든 인덱스는 중복 인덱스 키를 허용합니다. 후보 인덱스는 중복 인덱스 키를 허용하지 않습니다. 고유 옵션에 대한 자세한 내용은 [INDEX를](../../odbc/microsoft/index-command.md) 참조하십시오.  
  
 Null 값 및 중복 레코드는 기본 또는 후보 인덱스에 사용되는 필드에서 허용되지 않습니다. 그러나 visual FoxPronull 값을 지원하는 필드에 대한 기본 또는 후보 인덱스를 만들 면 오류를 생성 하지 않습니다. Visual FoxPro는 기본 또는 후보 인덱스에 사용되는 필드에 null 또는 중복 값을 입력하려고 하면 오류를 생성합니다.  
  
 참조 *표Name2* *[태그네임1]*  
 영구 관계가 설정된 상위 테이블을 지정합니다. *TAGName1을*생략하면 상위 테이블의 기본 인덱스 키를 사용하여 관계가 설정됩니다. 상위 테이블에 기본 인덱스가 없는 경우 Visual FoxPro에서 오류를 생성합니다.  
  
 태그 *태그Name1을* 포함하여 상위 테이블에 대한 기존 인덱스 태그를 기반으로 관계를 설정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다.  
  
 상위 테이블은 자유 테이블이 될 수 없습니다.  
  
 노CP트랜스  
 문자 및 메모 필드에 대한 다른 코드 페이지로 변환을 방지합니다. 테이블이 다른 코드 페이지로 변환되면 NOCPTRANS가 지정된 필드는 번역되지 않습니다. NOCPTRANS는 문자 및 메모 필드에 대해서만 지정할 수 있습니다.  
  
 다음 예제는 두 개의 문자 필드와 두 개의 메모 필드를 포함하는 mytable이라는 테이블을 만듭니다. 두 번째 문자 필드char2 및 두 번째 메모 필드인 memo2에는 번역을 방지하기 위해 NOCPTRANS가 포함됩니다.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 기본 키 *eExpression2* *태그이름2*  
 만들 기본 인덱스를 지정합니다. *eExpression2는* 테이블의 모든 필드 또는 필드 조합을 지정합니다. 태그 *이름2는* 생성된 기본 인덱스 태그의 이름을 지정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다.  
  
 테이블에는 하나의 기본 인덱스만 있을 수 있으므로 필드에 대한 기본 인덱스를 이미 만든 경우 이 절을 포함할 수 없습니다. Create 테이블에 두 개 이상의 기본 KEY 절을 포함하는 경우 Visual FoxPro에서 오류가 발생합니다.  
  
 고유 *eExpression3* *태그네임3*  
 후보 인덱스를 만듭니다. *eExpression3은* 테이블의 모든 필드 또는 필드 조합을 지정합니다. 그러나 기본 KEY 옵션 중 하나를 사용 하 고 기본 인덱스를 만든 경우 기본 인덱스에 대 한 지정 된 필드를 포함할 수 없습니다. 태그 *이름3* 는 생성된 후보 인덱스 태그에 대한 태그 이름을 지정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다.  
  
 테이블에는 여러 후보 인덱스가 있을 수 있습니다.  
  
 외래 키 *eExpression4* *태그네임4*[NODUP]  
 외래(기본이 아닌) 인덱스를 만들고 상위 테이블에 대한 관계를 설정합니다. *eExpression4는* 외래 인덱스 키 식을 지정하고 *TagName4는* 생성된 외래 인덱스 키 태그의 이름을 지정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다. NODUP를 사용하여 후보 외래 인덱스를 만듭니다.  
  
 테이블에 대해 여러 외래 인덱스를 만들 수 있지만 외시 인덱스 식은 테이블에서 다른 필드를 지정해야 합니다.  
  
 참조 *표Name3* *[태그네임5]*  
 영구 관계가 설정된 상위 테이블을 지정합니다. 태그 *TagName5를* 포함하여 상위 테이블에 대한 인덱스 태그를 기반으로 관계를 설정합니다. 인덱스 태그 이름은 최대 10자까지 포함될 수 있습니다. 기본적으로 *TAGName5를* 생략하면 상위 테이블의 기본 인덱스 키를 사용하여 관계가 설정됩니다.  
  
 *eExpression2*[오류 *cMessageText2]*  
 테이블 유효성 검사 규칙을 지정합니다. 오류 *cMessageText2는* 테이블 유효성 검사 규칙이 실행될 때 Visual FoxPro가 표시하는 오류 메시지를 지정합니다. 데이터는 찾아보기 창 또는 편집 창 내에서 변경된 경우에만 메시지가 표시됩니다.  
  
 배열 *배열 이름에서*  
 내용이 테이블의 각 필드에 대한 이름, 유형, 정밀도 및 배율인 기존 배열의 이름을 지정합니다. 배열의 내용은 **AFIELDS**() 함수로 정의할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 새 테이블은 사용 가능한 가장 낮은 작업 영역에서 열리며 별칭으로 액세스할 수 있습니다. 새 테이블은 SET EXCLUSIVE의 현재 설정에 관계없이 단독으로 열립니다.  
  
 데이터베이스가 열려 있고 FREE 절을 포함하지 않으면 새 테이블이 데이터베이스에 추가됩니다. 데이터베이스의 테이블과 이름이 같은 새 테이블을 만들 수 없습니다.  
  
 데이터베이스가 열려 있는 경우 테이블 만들기 - SQL은 데이터베이스를 단독으로 사용해야 합니다. 단독 사용을 위해 데이터베이스를 열려면 OPEN 데이터베이스에 배타적 을 포함하십시오.  
  
 이름, 확인, 기본값, 외래 키, 기본 키 또는 참조 절을 포함하여 새 테이블을 만들 때 데이터베이스가 열려 있지 않으면 오류가 생성됩니다.  
  
> [!NOTE]  
>  만들기 테이블 구문은 쉼표를 사용하여 특정 CREATE TABLE 옵션을 구분합니다. 또한 NULL, NULL, CHECK, 기본, 기본 키 및 UNIQUE 절은 열 정의를 포함하는 괄호 안에 배치되어야 합니다.  
  
## <a name="driver-remarks"></a>운전자 발언  
 응용 프로그램이 ODBC SQL 문 CREATE TABLE을 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 다음 표에 표시된 구문을 사용하여 명령을 Visual FoxProCREATE TABLE 명령으로 변환합니다.  
  
|ODBC 구문|비주얼 폭스프로 구문|  
|-----------------|--------------------------|  
|테이블 *기본 테이블 이름* 만들기<br /><br /> (열*식별자 데이터 형식*<br /><br /> [NULL 이 아님]<br /><br /> [,*열 식별자 데이터 형식*<br /><br /> [NULL 이 아님] ...)|테이블 *이름 만들기1* [이름 *긴 테이블 이름]*<br /><br /> *(필드네임1* *필드타입*<br /><br /> *[(n필드 폭* [, *nPrecision])]*<br /><br /> [NULL 아님])|  
  
 드라이버를 사용하여 테이블을 만들면 드라이버는 생성 직후 테이블을 닫아 다른 사용자가 테이블에 액세스할 수 있도록 합니다. 이는 Visual FoxPro와 다르며, 생성 시 테이블을 독점적으로 열어 둡습니다. 그러나 CREATE TABLE 문을 포함하는 데이터 원본에 저장된 프로시저가 실행되면 테이블은 열린 상태로 남아 있습니다.  
  
 데이터 원본이 데이터베이스(.dbc 파일)인 경우 Visual FoxPro ODBC 드라이버는 *기본 테이블 이름과*이름이 같은 *LongTableName이라는* 테이블을 만듭니다.  
  
### <a name="using-data-definition-language-ddl"></a>DDL(데이터 정의 언어) 사용  
 다음 위치에 DDL을 포함할 수 없습니다.  
  
-   트랜잭션이 필요한 일괄 처리 SQL 문에서  
  
-   수동 커밋 모드에서는 응용 프로그램이 **SQLTransact를**먼저 호출하지 않는 한 트랜잭션이 필요한 문 후 .  
  
 예를 들어 임시 테이블을 만들려면 트랜잭션이 필요한 문을 시작하기 전에 테이블을 만들어야 합니다. 트랜잭션이 필요한 일괄 처리 SQL 문에 CREATE TABLE 문을 포함하는 경우 드라이버는 오류 메시지를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 변경 - SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [지원되는 데이터 유형(비주얼 FoxPro ODBC 드라이버)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [삽입 - SQL 명령](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 명령](../../odbc/microsoft/select-sql-command.md)
