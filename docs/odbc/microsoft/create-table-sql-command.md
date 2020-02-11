---
title: CREATE TABLE SQL 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f979ccb5a44ada8e86424e0f6134f39d28a021d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096598"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 명령
지정 된 필드가 있는 테이블을 만듭니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원 합니다. 드라이버 관련 정보는 **드라이버 설명**을 참조 하세요.  
  
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
 CREATE TABLE &#124; DBF *TableName1*  
 만들 테이블의 이름을 지정 합니다. 테이블 및 DBF 옵션은 동일 합니다.  
  
 이름 없는 *tablename*  
 테이블의 긴 이름을 지정 합니다. 긴 테이블 이름은 데이터베이스에 저장 되므로 긴 테이블 이름은 데이터베이스를 열 때만 지정할 수 있습니다.  
  
 긴 이름은 최대 128 문자를 포함할 수 있으며 데이터베이스에서 짧은 파일 이름 대신 사용할 수 있습니다.  
  
 무료  
 테이블이 열려 있는 데이터베이스에 추가 되지 않도록 지정 합니다. 데이터베이스가 열려 있지 않으면 FREE가 필요 하지 않습니다.  
  
 *(FieldName1 FieldType* [( *nfieldwidth* [, *nprecision*])]  
 필드 이름, 필드 형식, 필드 너비 및 필드 전체 자릿수 (소수 자릿수)를 각각 지정 합니다.  
  
 *FieldType* 은 필드의 [데이터 형식을](../../odbc/microsoft/visual-foxpro-field-data-types.md)나타내는 단일 문자입니다. 일부 필드 데이터 형식에는 *Nfieldwidth* 또는 *nprecision* 또는 둘 다를 지정 해야 합니다.  
  
 D, G, I, L, M, P, T 및 Y 유형에 대해서는 *Nfieldwidth* 및 *nprecision* 이 무시 됩니다. n precision은 B, F 또는 N 형식에 대해 *Nprecision* 이 포함 되지 않은 *경우 기본값은* 0 (소수 자릿수 없음)입니다.  
  
 NULL  
 필드에 null 값을 허용 합니다.  
  
 NOT NULL  
 필드의 null 값을 방지 합니다.  
  
 Null 및 NOT NULL을 생략 하는 경우 현재 설정 NULL 설정에 따라 필드에서 null 값을 사용할 수 있는지 여부가 결정 됩니다. 그러나 null 및 NOT NULL을 생략 하 고 PRIMARY KEY 또는 UNIQUE 절을 포함 하는 경우 SET NULL 설정의 현재 설정은 무시 되 고 필드의 기본값은 NULL이 아닙니다.  
  
 *LEXPRESSION1* 확인  
 필드에 대 한 유효성 검사 규칙을 지정 합니다. *lExpression1* 은 사용자 정의 함수 일 수 있습니다. 빈 레코드가 추가 될 때마다 유효성 검사 규칙이 확인 됩니다. 유효성 검사 규칙이 추가 된 레코드에서 빈 필드 값을 허용 하지 않는 경우 오류가 생성 됩니다.  
  
 오류 *cMessageText1*  
 필드 규칙에서 오류를 생성할 때 Visual FoxPro가 표시 하는 오류 메시지를 지정 합니다. 이 메시지는 찾아보기 창이 나 편집 창 내에서 데이터가 변경 된 경우에만 표시 됩니다.  
  
 기본 *eExpression1*  
 필드의 기본값을 지정 합니다. *EExpression1* 의 데이터 형식은 필드의 데이터 형식과 동일 해야 합니다.  
  
 PRIMARY KEY  
 필드에 대 한 기본 인덱스를 만듭니다. 기본 인덱스 태그의 이름은 필드와 동일 합니다.  
  
 UNIQUE  
 필드에 대 한 후보 인덱스를 만듭니다. 후보 인덱스 태그의 이름은 필드와 동일 합니다.  
  
> [!NOTE]  
>  CREATE TABLE 또는 ALTER TABLE-SQL에서 UNIQUE 옵션을 포함 하 여 만든 후보 인덱스는 인덱스 명령에서 UNIQUE 옵션을 사용 하 여 만든 인덱스와 동일 하지 않습니다. Index 명령에서 UNIQUE 옵션을 사용 하 여 만든 인덱스는 중복 된 인덱스 키를 허용 합니다. 후보 인덱스는 중복 된 인덱스 키를 허용 하지 않습니다. 고유 옵션에 대 한 자세한 내용은 [인덱스](../../odbc/microsoft/index-command.md) 를 참조 하세요.  
  
 기본 또는 후보 인덱스에 사용 되는 필드에는 Null 값과 중복 레코드를 사용할 수 없습니다. 그러나 null 값을 지 원하는 필드에 대 한 기본 또는 후보 인덱스를 만드는 경우에는 Visual FoxPro에서 오류를 생성 하지 않습니다. 기본 또는 후보 인덱스에 사용 되는 필드에 null 값 또는 중복 값을 입력 하려고 하면 Visual FoxPro에서 오류를 생성 합니다.  
  
 참조 *TableName2*[TAG *TagName1*]  
 영구 관계가 설정 되는 부모 테이블을 지정 합니다. *TAGNAME1*태그를 생략 하면 부모 테이블의 기본 인덱스 키를 사용 하 여 관계가 설정 됩니다. 부모 테이블에 기본 인덱스가 없으면 Visual FoxPro에서 오류를 생성 합니다.  
  
 부모 테이블의 기존 인덱스 태그를 기준으로 관계를 설정 하는 태그 *TagName1* 포함 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다.  
  
 부모 테이블은 free 테이블 일 수 없습니다.  
  
 NOCPTRANS  
 문자 및 메모 필드에 대해 다른 코드 페이지로 변환할 수 없습니다. 테이블이 다른 코드 페이지로 변환 되 면 NOCPTRANS이 지정 된 필드가 변환 되지 않습니다. NOCPTRANS은 문자 및 메모 필드에만 지정할 수 있습니다.  
  
 다음 예에서는 두 개의 문자 필드와 두 개의 메모 필드를 포함 하는 mytable 이라는 테이블을 만듭니다. 두 번째 문자 필드인 char2 및 두 번째 메모 필드인 memo2에는 변환을 방지 하기 위해 NOCPTRANS이 포함 됩니다.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 PRIMARY KEY *eExpression2* 태그 *TagName2*  
 만들 기본 인덱스를 지정 합니다. *eExpression2* 는 테이블의 필드 또는 필드 조합을 지정 합니다. *TAGNAME2* 태그는 생성 되는 기본 인덱스 태그의 이름을 지정 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다.  
  
 테이블에는 기본 인덱스가 하나만 있을 수 있기 때문에 필드에 대 한 기본 인덱스를 이미 만든 경우에는이 절을 포함할 수 없습니다. CREATE TABLE에 둘 이상의 기본 키 절을 포함 하는 경우 Visual FoxPro에서 오류를 생성 합니다.  
  
 고유 *eExpression3*태그 *TagName3*  
 후보 인덱스를 만듭니다. *eExpression3* 는 테이블의 필드 또는 필드 조합을 지정 합니다. 그러나 기본 키 옵션 중 하나를 사용 하 여 기본 인덱스를 만든 경우 기본 인덱스에 대해 지정 된 필드를 포함할 수 없습니다. 태그 *TagName3* 생성 되는 후보 인덱스 태그의 태그 이름을 지정 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다.  
  
 테이블에는 여러 개의 후보 인덱스가 있을 수 있습니다.  
  
 FOREIGN KEY *eExpression4*TAG *TagName4*[nodup]  
 외래 (가 아닌) 인덱스를 만들고 부모 테이블에 대 한 관계를 설정 합니다. *eExpression4* 는 외래 인덱스 키 식을 지정 하 고 *TagName4* 는 생성 되는 외래 인덱스 키 태그의 이름을 지정 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다. NODUP를 포함 하 여 후보 외래 인덱스를 만듭니다.  
  
 테이블에 대 한 외래 인덱스를 여러 개 만들 수 있지만 외래 인덱스 식은 테이블에 다른 필드를 지정 해야 합니다.  
  
 참조 *TableName3*[TAG *TagName5*]  
 영구 관계가 설정 되는 부모 테이블을 지정 합니다. 부모 테이블의 인덱스 태그를 기준으로 관계를 설정 하려면 TAG *TagName5* 를 포함 합니다. 인덱스 태그 이름에는 최대 10 개의 문자를 사용할 수 있습니다. 기본적으로 *TAGNAME5 태그를* 생략 하면 부모 테이블의 기본 인덱스 키를 사용 하 여 관계가 설정 됩니다.  
  
 CHECK *eExpression2*[ERROR *cMessageText2*]  
 테이블 유효성 검사 규칙을 지정 합니다. 오류 *cMessageText2* 테이블 유효성 검사 규칙이 실행 될 때 Visual FoxPro에 표시 되는 오류 메시지를 지정 합니다. 이 메시지는 찾아보기 창이 나 편집 창 내에서 데이터가 변경 된 경우에만 표시 됩니다.  
  
 배열의 *Arrayname* 에서  
 테이블의 각 필드에 대 한 이름, 유형, 전체 자릿수 및 소수 자릿수를 포함 하는 기존 배열의 이름을 지정 합니다. 배열의 내용은 **Afields**() 함수를 사용 하 여 정의할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 새 테이블은 사용 가능한 가장 낮은 작업 영역에서 열리며 해당 별칭으로 액세스할 수 있습니다. SET EXCLUSIVE의 현재 설정에 관계 없이 새 테이블은 단독으로 열립니다.  
  
 데이터베이스가 열려 있고 FREE 절이 포함 되지 않은 경우 새 테이블이 데이터베이스에 추가 됩니다. 데이터베이스의 테이블과 동일한 이름을 사용 하 여 새 테이블을 만들 수 없습니다.  
  
 데이터베이스가 열려 있으면 CREATE TABLE-SQL에서 데이터베이스를 단독으로 사용 해야 합니다. 단독으로 사용할 데이터베이스를 열려면 OPEN DATABASE에 EXCLUSIVE를 포함 합니다.  
  
 새 테이블을 만들 때 데이터베이스를 열지 않은 경우 CHECK, DEFAULT, FOREIGN KEY, PRIMARY KEY 또는 REFERENCES 절을 포함 하 여 오류를 생성 합니다.  
  
> [!NOTE]  
>  CREATE TABLE 구문은 쉼표를 사용 하 여 특정 CREATE TABLE 옵션을 구분 합니다. 또한 NULL, NOT NULL, CHECK, DEFAULT, PRIMARY KEY 및 UNIQUE 절은 열 정의를 포함 하는 괄호 안에 배치 해야 합니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문을 데이터 원본으로 CREATE TABLE 보내면 Visual FoxPro ODBC 드라이버는 다음 표에 나와 있는 구문을 사용 하 여 명령을 Visual FoxProCREATE TABLE 명령으로 변환 합니다.  
  
|ODBC 구문|Visual FoxPro 구문|  
|-----------------|--------------------------|  
|CREATE TABLE *기본 테이블 이름*<br /><br /> (*열 식별자 데이터 형식*<br /><br /> [NOT NULL]<br /><br /> [,*열 식별자 데이터 형식*<br /><br /> [NOT NULL] ...)|CREATE TABLE *TableName1* [이름 없는 *tablename*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*Nfieldwidth* [, *nprecision*])]<br /><br /> [NOT NULL])|  
  
 드라이버를 사용 하 여 테이블을 만들 때 드라이버는 다른 사용자가 테이블에 대 한 액세스를 허용 하기 위해 테이블을 만든 후 즉시 닫습니다. 이는 테이블이 생성 될 때만 테이블이 열린 상태로 유지 되는 Visual FoxPro와는 다릅니다. 그러나 CREATE TABLE 문을 포함 하는 데이터 원본의 저장 프로시저를 실행 하면 테이블이 열려 있습니다.  
  
 데이터 원본이 데이터베이스 (dbc 파일) 인 경우 Visual FoxPro ODBC 드라이버는 *기본 테이블 이름과*같은 이름 *으로 라는 테이블* 을 만듭니다.  
  
### <a name="using-data-definition-language-ddl"></a>DDL (데이터 정의 언어) 사용  
 DDL은 다음 위치에 포함할 수 없습니다.  
  
-   트랜잭션이 필요한 batch SQL 문  
  
-   응용 프로그램에서 **Sqltransact**을 먼저 호출 하지 않는 한, 수동 커밋 모드에서 트랜잭션이 필요한 문 다음에 실행 됩니다.  
  
 예를 들어 임시 테이블을 만들려면 트랜잭션이 필요한 문을 시작 하기 전에 테이블을 만들어야 합니다. 트랜잭션이 필요한 일괄 처리 SQL 문에 CREATE TABLE 문을 포함 하는 경우 드라이버에서 오류 메시지를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE-SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [지원 되는 데이터 형식 (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [SQL 명령 삽입](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 명령](../../odbc/microsoft/select-sql-command.md)
