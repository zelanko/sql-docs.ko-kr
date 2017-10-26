---
title: "테이블-SQL 명령을 만들려면 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 35a22420b5ecaf21539fd16aecb3870e3f3049dc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="create-table---sql-command"></a>테이블-SQL 명령을 만들려면
지정된 된 필드가 있는 테이블을 만듭니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보를 참조 하십시오. **드라이버 주의**합니다.  
  
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
 테이블 &#124; 만들기 DBF *TableName1*  
 만들 테이블의 이름을 지정 합니다. 테이블 및 DBF 옵션은 동일 합니다.  
  
 이름 *LongTableName*  
 테이블에 대 한 긴 이름을 지정합니다. 긴 테이블 이름은 긴 테이블 이름은 데이터베이스에 저장 되므로 데이터베이스가 열려 있을 때만 지정할 수 있습니다.  
  
 긴 이름을 최대 128 자를 포함할 수 있습니다 및 데이터베이스에서 짧은 파일 이름 대신 사용할 수 있습니다.  
  
 FREE  
 테이블을 열려 있는 데이터베이스에 추가할를 지정 합니다. 무료는 데이터베이스 열려 있지 않으면 필요 하지 않습니다.  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [, *nPrecision*])]  
 필드 이름, 필드 형식, 필드 너비 및 필드 전체 자릿수 (소수 자릿수 초)을 각각 지정합니다.  
  
 *FieldType* 은 단일 문자 필드의 나타내는 [데이터 형식을](../../odbc/microsoft/visual-foxpro-field-data-types.md)합니다. 일부 필드 데이터 유형을 지정 하는 필요한 *nFieldWidth* 또는 *nPrecision* 또는 둘 다 합니다.  
  
 *nFieldWidth* 및 *nPrecision* D, G, I, L, M, P, T, 및 Y에 대 한 무시 형식입니다. *nPrecision* 0 (소수 자릿수 없음)을 *nPrecision* B, F, 또는 N 형식에 대 한 포함 되어 있지 않습니다.  
  
 NULL  
 필드에 null 값을 허용 합니다.  
  
 NOT  NULL  
 필드에 null 값을 방지합니다.  
  
 NOT NULL 및 NULL를 생략 NULL 설정의 현재 설정을 필드에 null 값 허용 여부를 결정 합니다. 그러나 생략 NULL 및 NOT NULL 및 PRIMARY KEY 또는 UNIQUE 절 포함 NULL 설정의 현재 설정을 무시 되 고는 필드는 기본적으로 NOT NULL입니다.  
  
 확인 *lExpression1*  
 필드에 대 한 유효성 검사 규칙을 지정합니다. *lExpression1* 사용자 정의 함수가 될 수 있습니다. 빈 레코드가 추가 될 때마다 유효성 검사 규칙 검사 됩니다. 유효성 검사 규칙 추가 된 레코드의 빈 필드 값에 대 한 허용 하지 않으면 오류가 생성 됩니다.  
  
 오류 *cMessageText1*  
 Visual FoxPro 표시 필드 규칙에 오류가 발생 하는 경우 오류 메시지를 지정 합니다. 메시지는 찾아보기 창이 나 편집 창 내에서 데이터가 변경 되는 경우에 표시 됩니다.  
  
 기본 *eExpression1*  
 필드에 대 한 기본값을 지정합니다. 데이터 형식이 *eExpression1* 필드의 데이터 형식과 동일 해야 합니다.  
  
 PRIMARY KEY  
 필드에 대 한 기본 인덱스를 만듭니다. 기본 인덱스 태그 필드와 동일한 이름이 있습니다.  
  
 UNIQUE  
 필드에 대 한 후보 인덱스를 만듭니다. 후보 인덱스 태그 필드와 동일한 이름이 있습니다.  
  
> [!NOTE]  
>  후보 인덱스가 (CREATE TABLE 또는 ALTER TABLE-SQL에서 고유한 옵션을 포함 하 여 생성) INDEX 명령에 고유한 옵션을 사용 하 여 만든 인덱스와 동일 하지 않습니다. INDEX 명령에 고유한 옵션을 사용 하 여 만든 인덱스를 사용 하면 중복 인덱스 키는; 후보 인덱스는 중복 인덱스 키를 허용 하지 않습니다. 참조 [인덱스](../../odbc/microsoft/index-command.md) 의 고유한 옵션에 대 한 자세한 내용은 합니다.  
  
 Null 값과 중복 레코드는 주 가상 컴퓨터 또는 후보 인덱스에 사용 되는 필드에 허용 되지 않습니다. 그러나 Visual FoxPro null 값을 지 원하는 필드에 대 한 주 가상 컴퓨터 또는 후보 인덱스를 만드는 경우 오류가 발생 하지 않습니다. Visual FoxPro 주 가상 컴퓨터 또는 후보 인덱스에 대 한 사용 되는 필드에 null 또는 중복 값을 입력 하려고 하면 오류가 발생 합니다.  
  
 참조 *TableName2*[태그 *TagName1*]  
 영구 관계가 설정 됩니다 부모 테이블을 지정 합니다. 태그를 생략할 경우 *TagName1*, 부모 테이블의 기본 인덱스 키를 사용 하는 관계가 설정 됩니다. Visual FoxPro 부모 테이블에 기본 인덱스를 찾을 수 없는 경우 오류가 발생 합니다.  
  
 Include 태그 *TagName1* 부모 테이블에 대 한 기존 인덱스 태그에 따라 관계를 설정할 수 있습니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 부모 테이블에는 사용 가능한 테이블 수 없습니다.  
  
 NOCPTRANS  
 문자 및 메모 필드에 대 한 다른 코드 페이지를 변환을 하지 않습니다. 테이블에 다른 코드 페이지 변환, NOCPTRANS 지정 된 필드는 번역 되지 않습니다. NOCPTRANS 문자 및 메모 필드에 대해서만 지정할 수 있습니다.  
  
 다음 예제에서는 두 개의 문자 필드와 두 개의 메모 필드가 포함 된 mytable 이라는 테이블을 만듭니다. 두 번째 문자 필드, char2, 및 두 번째 메모 필드 memo2, NOCPTRANS 번역을 방지 하기 위해 포함 됩니다.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 기본 키 *eExpression2* 태그 *TagName2*  
 기본 인덱스를 만들 지정 합니다. *eExpression2* 테이블의 모든 필드 또는 필드의 조합을 지정 합니다. 태그 *TagName2의*만들어지는 기본 인덱스 태그에 대 한 이름을 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 테이블에는 기본 인덱스는 하나만 있을 수 있지만, 때문에 필드에 대 한 기본 인덱스를 이미 만든 경우이 절을 포함할 수 없습니다. Visual FoxPro CREATE TABLE에 둘 이상의 기본 키 절을 포함 하는 경우에 오류가 발생 합니다.  
  
 고유 *eExpression3*태그 *TagName3*  
 후보 인덱스를 만듭니다. *eExpression3* 테이블의 모든 필드 또는 필드의 조합을 지정 합니다. 그러나 기본 인덱스와 기본 키 옵션 중 하나를 만든 경우 기본 인덱스에 대해 지정 된 필드를 포함할 수 없습니다. 태그 *TagName3의*만들어진 후보 인덱스 태그에 대 한 태그 이름을 지정 합니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다.  
  
 테이블에는 후보 인덱스를 여러 개 있을 수 있습니다.  
  
 외래 키 *eExpression4*태그 *TagName4*[NODUP]  
 외부 (기본) 인덱스를 만들고 부모 테이블에 대 한 관계를 설정 합니다. *eExpression4* 외래 인덱스 키 식을 지정 하 고 *TagName4* 만들어진 인덱스 외래 키 태그의 이름을 지정*합니다.* 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다. 후보 외래 인덱스를 만들려면 NODUP 포함 됩니다.  
  
 테이블에 대 한 여러 외부 인덱스를 만들 수 있지만 외래 인덱스 식을 테이블의 서로 다른 필드를 지정 해야 합니다.  
  
 참조 *TableName3*[태그 *TagName5*]  
 영구 관계가 설정 됩니다 부모 테이블을 지정 합니다. Include 태그 *TagName5* 부모 테이블에 대 한 인덱스 태그가에 따라 관계를 설정할 수 있습니다. 인덱스 태그 이름은 최대 10 개의 문자를 포함할 수 있습니다. 태그를 생략 하면 기본적으로 *TagName5,* 부모 테이블의 기본 인덱스 키를 사용 하는 관계가 설정 됩니다.  
  
 확인 *eExpression2*[오류 *cMessageText2*]  
 테이블 유효성 검사 규칙을 지정합니다. 오류 *cMessageText2* Visual FoxPro 테이블 유효성 검사 규칙이 실행 될 때 표시 됩니다. 오류 메시지를 지정 합니다. 데이터 찾아보기 창에서 변경 되거나 편집 창 경우에 메시지가 표시 됩니다.  
  
 배열에서 *ArrayName*  
 이름, 유형, 전체 자릿수 및 소수 자릿수는 테이블의 각 필드에 대 한 내용이 기존 배열의 이름을 지정 합니다. 배열의 내용을 정의할 수 있습니다는 **AFIELDS**() 함수입니다.  
  
## <a name="remarks"></a>주의  
 새 테이블의 가장 낮은 사용 가능한 작업 영역에서 열리고 해당 별칭으로 액세스할 수 있습니다. 새 테이블이 배타적 설정의 현재 설정에 관계 없이 단독으로 열립니다.  
  
 데이터베이스가 열려 있는 경우 무료 절을 포함 하지 않으면 데이터베이스에 새 테이블이 추가 됩니다. 데이터베이스의 테이블과 동일한 이름을 가진 새 테이블을 만들 수 없습니다.  
  
 데이터베이스에 열려 있으면 CREATE TABLE-SQL 데이터베이스를 배타적으로 사용이 필요 합니다. 독점적인 사용을 위해 데이터베이스를 열려면 배타적 데이터베이스 열에 포함 합니다.  
  
 새 테이블을 만들 때 데이터베이스 열려 있지 않으면, 이름, 확인, 기본, 외래 키, 기본 키 또는 참조 절을 포함 하 여 오류가 발생 합니다.  
  
> [!NOTE]  
>  CREATE TABLE 구문은 특정 CREATE TABLE 옵션을 구분 하려면 쉼표를 사용 합니다. 또한, NULL, 하지 NULL, 확인, 기본, 기본 키 및 고유 절 열 정의가 포함 된 괄호 안에 배치 되어야 합니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문을 Visual FoxPro ODBC 드라이버가 데이터 원본에 대 한 CREATE TABLE 명령은 다음 표에 표시 된 구문을 사용 하 여 비주얼 FoxProCREATE 테이블 명령으로 변환 합니다.  
  
|ODBC 구문|Visual FoxPro 구문|  
|-----------------|--------------------------|  
|CREATE TABLE *기본 테이블 이름*<br /><br /> (*식별자 열 데이터 형식*<br /><br /> [NOT NULL]<br /><br /> [,*식별자 열 데이터 형식*<br /><br /> [NOT NULL]...)|테이블 만들기 *TableName1* [이름 *LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [NOT NULL])|  
  
 드라이버를 사용 하 여 테이블을 만들 때 드라이버는 다른 사용자가 테이블에 대 한 액세스를 허용 하도록 만든 직후에 테이블을 닫습니다. Visual FoxPro 남용을 방지 하지만 테이블 작성 시 단독으로이 점에서 차이가 있습니다. 그러나 CREATE TABLE 문을 포함 하 여 데이터 소스에서 저장된 프로시저를 실행 하는 경우 테이블은 열려 있게 됩니다.  
  
 Visual FoxPro ODBC 드라이버 라는 테이블을 만들어 데이터 원본이 데이터베이스 (.dbc 파일) 인 경우 *LongTableName* 동일한 이름을 갖는 *기본 테이블 이름*합니다.  
  
### <a name="using-data-definition-language-ddl"></a>데이터 정의 언어 (DDL)를 사용 하 여  
 다음 위치에 DDL을 포함할 수 없습니다.  
  
-   트랜잭션이 필요로 하는 SQL 문 일괄 처리  
  
-   응용 프로그램을 먼저 호출 하지 않는 경우는 트랜잭션에 필요한 문 다음의 수동 커밋 모드에서 **SQLTransact**합니다.  
  
 예를 들어 임시 테이블을 만들려는 트랜잭션이 필요한 문의 시작 하기 전에 테이블을 만들어야 합니다. 트랜잭션이 필요로 하는 SQL 문 일괄 처리에서 CREATE TABLE 문을 포함 하는 경우 드라이버는 오류 메시지를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE-SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [지원 되는 데이터 형식 (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [SQL 명령-삽입](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 명령](../../odbc/microsoft/select-sql-command.md)

