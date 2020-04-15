---
title: 저장 프로시저에서 배열 매개 변수 반환 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc998dadc0e0c4a4bfe054bfd1d40296bc176393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292863"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>저장 프로시저에서 배열 매개 변수 반환
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 Oracle 7.3에서는 PL/SQL 프로그램을 제외한 PL/SQL 레코드 유형에 액세스할 수 있는 방법이 없습니다. 패키지된 프로시저 또는 함수에 PL/SQL 레코드 유형으로 정의된 형식 인수가 있는 경우 해당 형식 인수를 매개 변수로 바인딩할 수 없습니다. 오라클에 대한 Microsoft ODBC 드라이버의 PL/SQL TABLE 형식을 사용하여 올바른 이스케이프 시퀀스가 포함된 프로시저에서 배열 매개 변수를 호출합니다.  
  
 절차를 호출하려면 다음 구문을 사용합니다.  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  최대 \<레코드가 요청한> 매개 변수는 결과 집합에 있는 행 수보다 크거나 같아야 합니다. 그렇지 않으면 Oracle은 드라이버가 사용자에게 전달되는 오류를 반환합니다.  
>   
>  PL/SQL 레코드는 배열 매개 변수로 사용할 수 없습니다. 각 배열 매개 변수는 데이터베이스 테이블의 하나의 열만 나타낼 수 있습니다.  
  
 다음 예제에서는 서로 다른 결과 집합을 반환 하는 두 개의 프로시저를 포함 하는 패키지를 정의 하 고 패키지에서 결과 집합을 반환 하는 두 가지 방법을 제공 합니다.  
  
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
  
#### <a name="to-invoke-procedure-proc1"></a>프로시저 PROC1을 호출하려면  
  
1.  단일 결과 집합의 모든 열을 반환합니다.  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  각 열을 단일 결과 집합으로 반환합니다.  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     이렇게 하면 각 열에 대해 하나씩 세 개의 결과 집합이 반환됩니다.  
  
#### <a name="to-invoke-procedure-proc2"></a>프로시저 PROC2를 호출하려면  
  
1.  단일 결과 집합의 모든 열을 반환합니다.  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  각 열을 단일 결과 집합으로 반환합니다.  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 [SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API를 사용하여 응용 프로그램이 모든 결과 집합을 가져오는지 확인합니다. 자세한 내용은 *ODBC 프로그래머의 참조를*참조하십시오.  
  
> [!NOTE]  
>  Oracle 버전 2.0의 ODBC 드라이버에서는 PL/SQL 배열을 반환하는 Oracle 함수를 사용하여 결과 집합을 반환할 수 없습니다.
