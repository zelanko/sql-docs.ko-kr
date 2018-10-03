---
title: CREATE TABLE-SQL 명령 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e1451ddc8ec43b1960ed6073fb836b05e8384bb2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47683014"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 명령
지정 된 필드가 있는 테이블을 만듭니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보를 참조 하세요 **드라이버 주의**합니다.  
  
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
 테이블 만들기 &#124; DBF *TableName1*  
 만들 테이블의 이름을 지정 합니다. 테이블 및 DBF 옵션은 동일 합니다.  
  
 이름 *LongTableName*  
 긴 테이블 이름을 지정합니다. 긴 테이블 이름은 긴 테이블 이름을 데이터베이스에 저장 되므로 데이터베이스가 열려 있을 때만 지정할 수 있습니다.  
  
 긴 이름을 최대 128 자의 문자를 포함할 수 있습니다 하 고 데이터베이스에서 짧은 파일 이름 대신 사용할 수 있습니다.  
  
 FREE  
 열려 있는 데이터베이스에 추가 되지 않습니다 지정 합니다. 무료는 데이터베이스는 열려 있지 않은 경우 필요 하지 않습니다.  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [합니다 *nPrecision*])]  
 필드 이름, 필드 형식, 필드 너비 및 필드 전체 자릿수 (소수 자릿수의 수)를 각각 지정합니다.  
  
 *FieldType* 은 필드를 나타내는 단일 문자 [데이터 형식](../../odbc/microsoft/visual-foxpro-field-data-types.md)합니다. 필드 데이터 형식도 지정 해야 *nFieldWidth* 하거나 *nPrecision* 또는 둘 다.  
  
 *nFieldWidth* 하 고 *nPrecision* D, G, I, L, M, P, T, 및 Y에 대해 무시 됩니다 형식입니다. *nPrecision* 경우에 0 (소수 자릿수 없이)를 기본값으로 *nPrecision* B, F 또는 N 형식에 대 한 포함 되지 않습니다.  
  
 NULL  
 필드에 null 값을 허용 합니다.  
  
 NOT NULL  
 필드에 null 값을 방지합니다.  
  
 NULL을 생략 하 고이 정보를 NOT NULL, SET NULL의 현재 설정을 필드에 null 값 허용 되는지 여부를 결정 합니다. 그러나 생략 NULL 및 NOT NULL 기본 키 또는 고유 절 포함 NULL 설정의 현재 설정을 무시 되 고 필드 기본값은 NOT NULL입니다.  
  
 확인 *lExpression1*  
 필드에 대 한 유효성 검사 규칙을 지정합니다. *lExpression1* 사용자 정의 함수 일 수 있습니다. 빈 레코드가 추가 될 때마다 유효성 검사 규칙을 확인 합니다. 추가 된 레코드의 빈 필드 값에 대 한 유효성 검사 규칙을 허용 하지 않으면 오류가 생성 됩니다.  
  
 오류 *cMessageText1*  
 Visual FoxPro 필드 규칙이 생성 오류가 표시 됩니다. 오류 메시지를 지정 합니다. 메시지는 찾아보기 창 또는 편집 창 내에서 데이터가 변경 되는 경우에 표시 됩니다.  
  
 기본 *eExpression1*  
 필드에 대 한 기본값을 지정 합니다. 데이터 형식이 *eExpression1* 필드의 데이터 형식과 동일 해야 합니다.  
  
 PRIMARY KEY  
 필드에 대 한 기본 인덱스를 만듭니다. 기본 인덱스 태그 필드와 동일한 이름이 있습니다.  
  
 UNIQUE  
 필드에 대 한 후보 인덱스를 만듭니다. 후보 인덱스 태그 필드와 동일한 이름이 있습니다.  
  
> [!NOTE]  
>  후보 (CREATE TABLE 또는 ALTER TABLE-SQL의 고유한 옵션을 포함 하 여 만든) 인덱스가 UNIQUE INDEX 명령 옵션을 사용 하 여 만든 인덱스와 동일 하지 않습니다. INDEX 명령에는 고유한 옵션을 사용 하 여 만든 인덱스를 사용 하면 중복 인덱스 키 후보 인덱스는 중복 인덱스 키를 허용 하지 않습니다. 참조 [인덱스](../../odbc/microsoft/index-command.md) 해당 옵션에 대 한 자세한 내용은 합니다.  
  
 기본 또는 후보 인덱스에 사용 되는 필드에 null 값과 중복 레코드가 허용 되지 않습니다. 그러나 Visual FoxPro null 값을 지 원하는 필드에 대 한 기본 또는 후보 인덱스를 만드는 경우 오류를 생성 하지 않습니다. Visual FoxPro 주 또는 후보 인덱스에 사용 되는 필드에 null 또는 중복 값을 입력 하려고 하면 오류가 발생 합니다.  
  
 참조 *TableName2*[태그 *TagName1*]  
 영구 관계가 설정 됩니다는 부모 테이블을 지정 합니다. 태그를 생략 *TagName1*, 부모 테이블의 기본 인덱스 키를 사용 하 여 관계가 성립 합니다. Visual FoxPro 부모 테이블에 기본 인덱스를 찾을 수 없는 경우 오류가 발생 합니다.  
  
 태그가 *TagName1* 부모 테이블에 대 한 기존 인덱스 태그에 따라 관계를 설정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 부모 테이블에는 사용 가능한 테이블 수 없습니다.  
  
 NOCPTRANS  
 문자 및 메모 필드에 대 한 다른 코드 페이지로 변환을 하지 않습니다. 테이블은 다른 코드 페이지로 변환 됩니다, NOCPTRANS 지정 된 필드는 번역 되지 않습니다. NOCPTRANS 문자와 메모 필드에 대해서만 지정할 수 있습니다.  
  
 다음 예제에서는 두 개의 문자 필드와 두 메모 필드를 포함 하는 mytable 이라는 테이블을 만듭니다. 두 번째 문자 필드, char2, 및 두 번째 메모 필드 memo2, NOCPTRANS 번역을 방지 하기 위해 포함 됩니다.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 기본 키 *eExpression2* 태그 *TagName2*  
 만들려는 기본 인덱스를 지정 합니다. *eExpression2* 테이블의 모든 필드 또는 필드의 조합은 지정 합니다. 태그 *TagName2의*만들어지는 기본 인덱스 태그에 대 한 이름을 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 테이블에서 하나의 기본 인덱스를 가질 수 있으므로 필드에 대 한 기본 인덱스를 이미 만든 경우이 절을 포함할 수 없습니다. Visual FoxPro CREATE TABLE에서 둘 이상의 기본 키 절을 포함 하는 경우에 오류가 발생 합니다.  
  
 고유한 *eExpression3*태그 *TagName3*  
 후보 인덱스를 만듭니다. *eExpression3* 테이블의 모든 필드 또는 필드의 조합은 지정 합니다. 그러나 키 옵션 중 하나를 사용 하 여 기본 인덱스를 만든 경우 기본 인덱스에 대해 지정 된 필드를 포함할 수 없습니다. 태그 *TagName3의*만든 후보 인덱스 태그의 태그 이름을 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 테이블에는 여러 후보 인덱스가 있을 수 있습니다.  
  
 외래 키 *eExpression4*태그 *TagName4*[NODUP]  
 외부 (기본) 인덱스를 만들고 부모 테이블에 대 한 관계를 설정 합니다. *eExpression4* 외래 인덱스 키 식을 지정 하 고 *TagName4* 만들어지는 외래 인덱스 키 태그의 이름을 지정*합니다.* 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다. 후보 외래 인덱스를 만들려면 NODUP 포함 됩니다.  
  
 테이블에 대 한 여러 외부 인덱스를 만들 수 있지만 외래 인덱스 식을 테이블의 다른 필드를 지정 해야 합니다.  
  
 참조 *TableName3*[태그 *TagName5*]  
 영구 관계가 설정 됩니다는 부모 테이블을 지정 합니다. 태그가 *TagName5* 부모 테이블에는 인덱스 태그를 기반으로 하는 관계를 설정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다. 태그를 생략 하면 기본적으로 *TagName5,* 부모 테이블의 기본 인덱스 키를 사용 하 여 관계가 성립 합니다.  
  
 확인할 *eExpression2*[오류 *cMessageText2*]  
 테이블 유효성 검사 규칙을 지정합니다. 오류 *cMessageText2* Visual FoxPro 테이블 유효성 검사 규칙이 실행 될 때 표시 됩니다. 오류 메시지를 지정 합니다. 경우에 데이터 찾아보기 창에서 변경 된 편집 창에는 메시지가 표시 됩니다.  
  
 배열에서 *ArrayName*  
 기존 배열 내용이 이름, 형식, 전체 자릿수 및 테이블의 각 필드에 대 한 확장 이름을 지정 합니다. 배열의 내용을 정의할 수 있습니다 합니다 **AFIELDS**() 함수입니다.  
  
## <a name="remarks"></a>Remarks  
 새 테이블에는 가장 낮은 사용 가능한 작업 영역에서 열 및 해당 별칭으로 액세스할 수 있습니다. 새 테이블 전용 설정의 현재 설정에 관계 없이 단독으로 열려 있습니다.  
  
 데이터베이스가 열려 있는 경우 무료 절을 포함 하지 않으면 새 테이블 데이터베이스에 추가 됩니다. 데이터베이스의 테이블과 동일한 이름을 가진 새 테이블을 만들 수 없습니다.  
  
 데이터베이스를 연 하는 경우 CREATE TABLE-SQL 데이터베이스를 배타적으로 사용을 해야 합니다. 단독 사용을 위해 데이터베이스를 열려면 배타적 데이터베이스 열에 포함 합니다.  
  
 데이터베이스를 새 테이블을 만들 때 열려 있지 않으면, 이름, 확인, 기본, 외래 키, 기본 키 또는 참조 절을 포함 하 여 오류가 발생 합니다.  
  
> [!NOTE]  
>  CREATE TABLE 구문에 특정 CREATE TABLE 옵션을 구분 하려면 쉼표를 사용 합니다. 또한 NULL, 없습니다 NULL, 확인, 기본, 기본 키 및 고유 절 열 정의가 포함 된 괄호 안에 배치 되어야 합니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문을 전송 하는 경우 Visual FoxPro ODBC 드라이버는 데이터 원본에 대 한 CREATE TABLE 명령은 다음 표에 표시 된 구문을 사용 하 여 Visual FoxProCREATE 테이블 명령으로 변환 합니다.  
  
|ODBC 구문|Visual FoxPro 구문|  
|-----------------|--------------------------|  
|CREATE TABLE *기본 테이블 이름*<br /><br /> (*식별자 열 데이터 형식*<br /><br /> [NOT NULL]<br /><br /> [,*식별자 열 데이터 형식*<br /><br /> [NOT NULL]...)|테이블을 만듭니다 *TableName1* [이름 *LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [합니다 *nPrecision*])]<br /><br /> [NOT NULL])|  
  
 드라이버를 사용 하 여 테이블을 만들 때 드라이버는 다른 사용자가 테이블에 액세스할 수 있도록 만든 직후에 테이블을 닫습니다. 이 테이블을 만들 때만 열기 상태로 유지 하는 Visual FoxPro에서 서로 다릅니다. 그러나 CREATE TABLE 문이 포함 된 데이터 원본에서 저장된 프로시저를 실행 하는 경우 테이블은 열려 있게 됩니다.  
  
 Visual FoxPro ODBC 드라이버 라는 테이블을 만들어 데이터 원본 데이터베이스 (.dbc 파일) 이면 *LongTableName* 와 같은 이름을 사용 하 여 합니다 *기본 테이블 이름*합니다.  
  
### <a name="using-data-definition-language-ddl"></a>DDL (데이터 정의 언어)을 사용 하 여  
 다음 위치에서 DDL을 포함할 수 없습니다.  
  
-   SQL 문 일괄 처리에서 트랜잭션 필요  
  
-   응용 프로그램을 먼저 호출 하지 않는 경우 트랜잭션이 필요한 문 후 수동 커밋 모드로 **SQLTransact**합니다.  
  
 예를 들어, 임시 테이블을 만들려는 트랜잭션이 필요한 문의 시작 하기 전에 테이블을 만들어야 합니다. CREATE TABLE 문 일괄 처리 트랜잭션이 필요로 하는 SQL 문 포함 하는 경우 드라이버는 오류 메시지를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER TABLE-SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [지원 되는 데이터 형식 (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT-SQL 명령](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 명령](../../odbc/microsoft/select-sql-command.md)
