---
title: 저장 프로시저에서 배열 매개 변수를 반환 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a154a8739438b76f12e311d0dec0e9d98d886457
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837029"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>저장 프로시저에서 배열 매개 변수 반환
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 7.3, PL/SQL 프로그램에서 제외 하 고 PL/SQL 레코드 형식에 액세스할 방법이 있습니다. 패키지 된 프로시저 또는 함수를 PL/SQL 레코드 형식으로 정의 하는 형식 인수에 있으면 해당 형식 인수를 매개 변수로 바인딩할 수 아닙니다. Microsoft ODBC Driver for Oracle PL/SQL 테이블 유형의 사용 하 여 올바른 이스케이프 시퀀스가 포함 된 프로시저에서 배열 매개 변수를 호출 합니다.  
  
 프로시저를 호출 하려면 다음 구문을 사용 합니다.  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  \<최대 레코드 요청 > 매개 변수 보다 크거나 같은 결과 집합에 있는 행의 수 여야 합니다. 그렇지 않으면 Oracle 드라이버에서 사용자에 게 전달 되는 오류를 반환 합니다.  
>   
>  PL/SQL 레코드 배열 매개 변수로 사용할 수 없습니다. 각 배열 매개 변수는 데이터베이스 테이블의 열을 하나만 나타낼 수 있습니다.  
  
 다음 예제에서는 다양 한 결과 집합을 반환 하는 두 프로시저를 포함 하는 패키지를 정의 하 고 패키지에서 결과 집합을 반환 하는 두 가지를 제공 합니다.  
  
## <a name="package-definition"></a>패키지 정의:  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>PROC1 프로시저를 호출 하려면  
  
1.  단일 결과 집합의 모든 열을 반환 합니다.  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  단일 결과 집합으로 각 열을 반환 합니다.  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     각 열에 대해 하나씩 세 개의 결과 집합을 반환합니다.  
  
#### <a name="to-invoke-procedure-proc2"></a>PROC2 프로시저를 호출 하려면  
  
1.  단일 결과 집합의 모든 열을 반환 합니다.  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  단일 결과 집합으로 각 열을 반환 합니다.  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 응용 프로그램 사용 하 여 결과 집합 모두를 페치 있는지 확인 합니다 [SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API. 자세한 내용은 참조는 *ODBC 프로그래머 참조*합니다.  
  
> [!NOTE]  
>  Oracle 버전 2.0에 대 한 ODBC 드라이버에서 결과 집합을 반환할 PL/SQL 배열을 반환 하는 Oracle 함수를 사용할 수 없습니다.
