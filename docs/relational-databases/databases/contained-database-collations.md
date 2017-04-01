---
title: "포함된 데이터베이스 데이터 정렬 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "포함된 데이터베이스, 데이터 정렬"
ms.assetid: 4b44f6b9-2359-452f-8bb1-5520f2528483
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# 포함된 데이터베이스 데이터 정렬
  여러 가지 속성이 대/소문자 구분, 악센트 구분 및 사용되는 기본 언어를 비롯한 텍스트 데이터의 같음 의미 체계 및 정렬 순서에 영향을 줍니다. 이러한 사항은 데이터에 대한 데이터 정렬 선택을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 전달됩니다. 데이터 정렬에 대한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
 데이터 정렬은 사용자 테이블에 저장된 데이터에 적용될 뿐만 아니라 메타데이터, 임시 개체, 변수 이름 등 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 처리하는 모든 텍스트에 적용됩니다. 이러한 항목의 처리 방식은 포함되지 않은 데이터베이스인지 여부에 따라 다릅니다. 이러한 변경 내용은 대부분의 사용자에게는 영향을 미치지 않지만 인스턴스 독립 및 일관성을 제공하는 데 도움이 됩니다. 하지만 이로 인해 일부 혼란이 발생할 수도 있고 포함된 데이터베이스와 포함되지 않은 데이터베이스에 모두 액세스하는 세션의 경우에는 문제가 될 수도 있습니다.  
  
 이 항목에서는 변경 내용에 대해 설명하고 변경으로 인해 문제가 발생할 수 있는 영역을 살펴봅니다.  
  
## 포함되지 않은 데이터베이스  
 모든 데이터베이스는 기본 데이터 정렬이 있습니다. 기본 데이터 정렬은 데이터베이스를 만들거나 변경할 때 설정할 수 있습니다. 이러한 데이터 정렬은 데이터베이스의 모든 메타데이터에 사용되며 데이터베이스 내 모든 문자열 열의 기본값으로 사용됩니다. 사용자는 **COLLATE** 절을 사용하여 특정 열의 데이터 정렬을 다르게 선택할 수 있습니다.  
  
### 예제 1  
 예를 들어 베이징에서 작업하는 경우 중국어 데이터 정렬을 사용할 것입니다.  
  
```tsql  
ALTER DATABASE MyDB COLLATE Chinese_Simplified_Pinyin_100_CI_AS;  
```  
  
 이제 열을 만들면 이 열의 기본 데이터 정렬은 중국어 데이터 정렬이 되지만 원하는 경우 다른 데이터 정렬을 선택할 수 있습니다.  
  
```tsql  
CREATE TABLE MyTable  
      (mycolumn1 nvarchar,  
      mycolumn2 nvarchar COLLATE Frisian_100_CS_AS);  
GO  
SELECT name, collation_name  
FROM sys.columns  
WHERE name LIKE 'mycolumn%' ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```tsql  
name            collation_name  
--------------- ----------------------------------  
mycolumn1       Chinese_Simplified_Pinyin_100_CI_AS  
mycolumn2       Frisian_100_CS_AS  
```  
  
 이러한 방법은 상당히 간단해 보이지만 몇 가지 문제가 있습니다. 열의 데이터 정렬은 테이블을 만든 데이터베이스에 종속되기 때문에 **tempdb**에 저장되는 임시 테이블 사용에서 문제가 발생합니다. **tempdb** 의 데이터 정렬은 대개 인스턴스의 데이터 정렬과 일치하는데 인스턴스 데이터 정렬은 데이터베이스 데이터 정렬과 일치할 필요가 없습니다.  
  
### 예제 2  
 예를 들어 **Latin1_General** 데이터 정렬을 사용하는 인스턴스에서 위의 중국어 데이터베이스가 사용되는 경우를 가정합니다.  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max)) ;  
GO  
```  
  
 얼핏 보면 두 테이블이 동일한 스키마를 가지고 있는 것처럼 보이지만 데이터베이스의 데이터 정렬이 다르기 때문에 실제로는 값이 호환되지 않습니다.  
  
```  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 메시지 468, 수준 16, 상태 9, 줄 2  
  
 같음 연산에서 "Latin1_General_100_CI_AS_KS_WS_SC"와 "Chinese_Simplified_Pinyin_100_CI_AS" 사이의 데이터 정렬 충돌을 해결할 수 없습니다.  
  
 임시 테이블에 대해 명시적으로 데이터 정렬을 수행하여 이 문제를 해결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **COLLATE** 절에 제공되는 **DATABASE_DEFAULT** 키워드를 사용하면 편리합니다.  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max) COLLATE DATABASE_DEFAULT);  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 이 구문은 이제 오류 없이 실행됩니다.  
  
 변수와 관련된 데이터 정렬 종속 동작도 볼 수 있습니다. 다음과 같은 함수가 있다고 합시다.  
  
```  
CREATE FUNCTION f(@x INT) RETURNS INT  
AS BEGIN   
      DECLARE @I INT = 1  
      DECLARE @İ INT = 2  
      RETURN @x * @i  
END;  
```  
  
 이 함수는 조금 특이한 함수입니다. 대/소문자를 구분하는 데이터 정렬에서 return 절의 @i는 @I 또는 @İ에 바인딩할 수 없습니다. 대/소문자를 구분하지 않는 Latin1_General 데이터 정렬에서 @i는 @I에 바인딩하고 함수는 1을 반환합니다. 하지만 대/소문자를 구분하지 않는 Turkish 데이터 정렬에서 @i는 @I에 바인딩하고 함수는 2를 반환합니다. 이런 동작은 데이터 정렬이 다른 인스턴스 간을 이동하는 데이터베이스에 혼란을 초래합니다.  
  
## 포함된 데이터베이스  
 포함된 데이터베이스의 디자인 목표는 독립적인 데이터베이스를 만드는 것이므로 인스턴스 및 **tempdb** 데이터 정렬에 대한 종속성은 존재하지 않아야 합니다. 이러한 목표를 위해 포함된 데이터베이스에는 카탈로그 데이터 정렬이라는 개념이 도입되었습니다. 카탈로그 데이터 정렬은 시스템 메타데이터 및 임시 개체에 사용됩니다. 자세한 내용은 아래에서 설명합니다.  
  
 포함된 데이터베이스에서 카탈로그 데이터 정렬이 **Latin1_General_100_CI_AS_WS_KS_SC**라고 가정합니다. 이 데이터 정렬은 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 포함된 데이터베이스에서 동일하며 변경할 수 없습니다.  
  
 데이터베이스 데이터 정렬은 유지되지만 사용자 데이터의 기본 데이터 정렬로만 사용됩니다. 기본적으로 데이터베이스 데이터 정렬은 model 데이터베이스 데이터 정렬과 같지만 포함되지 않은 데이터베이스와 마찬가지로 사용자가 **CREATE** 또는 **ALTER DATABASE** 명령을 통해 변경할 수 있습니다.  
  
 새 키워드 **CATALOG_DEFAULT**를 **COLLATE** 절에서 사용할 수 있습니다. 이 키워드는 포함된 데이터베이스와 포함되지 않은 데이터베이스 모두에서 현재 메타데이터 데이터 정렬에 대한 바로 가기로 사용됩니다. 즉, 포함되지 않은 데이터베이스에서 **CATALOG_DEFAULT**는 메타데이터가 데이터베이스 데이터 정렬로 정렬되기 때문에 현재 데이터베이스 데이터 정렬을 반환합니다. 포함된 데이터베이스에서는 사용자가 카탈로그 데이터 정렬과 일치하지 않도록 데이터베이스 데이터 정렬을 변경할 수 있으므로 이 두 값이 다를 수 있습니다.  
  
 포함된 데이터베이스와 포함되지 않은 데이터베이스의 여러 개체 동작은 다음 표에 요약되어 있습니다.  
  
||||  
|-|-|-|  
|**항목**|**포함되지 않은 데이터베이스**|**포함된 데이터베이스**|  
|사용자 데이터(기본값)|DATABASE_DEFAULT|DATABASE_DEFAULT|  
|임시 데이터(기본값)|TempDB 데이터 정렬|DATABASE_DEFAULT|  
|메타데이터|DATABASE_DEFAULT/CATALOG_DEFAULT|CATALOG_DEFAULT|  
|임시 메타데이터|TempDB 데이터 정렬|CATALOG_DEFAULT|  
|변수|인스턴스 데이터 정렬|CATALOG_DEFAULT|  
|Goto 레이블|인스턴스 데이터 정렬|CATALOG_DEFAULT|  
|커서 이름|인스턴스 데이터 정렬|CATALOG_DEFAULT|  
  
 앞에서 설명된 임시 테이블 예를 보면 이 데이터 정렬 동작 때문에 대부분의 임시 테이블 사용 시 명시적으로 **COLLATE** 절을 사용할 필요가 없음을 알 수 있습니다. 포함된 데이터베이스에서 데이터베이스와 인스턴스 데이터 정렬이 다른 경우에도 이제 이 코드는 오류 없이 실행됩니다.  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max));  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 `T1_txt` 와 `T2_txt` 가 포함된 데이터베이스의 데이터베이스 데이터 정렬로 정렬되기 때문에 이 코드는 정상적으로 작동합니다.  
  
## 포함된 컨텍스트와 포함되지 않은 컨텍스트 간 교차  
 포함된 데이터베이스의 세션은 포함된 상태로 유지되는 한 연결된 데이터베이스 내부에 남아 있어야 합니다. 이 경우의 동작은 매우 명확합니다. 하지만 세션이 포함된 컨텍스트와 포함되지 않은 컨텍스트 사이를 교차하는 경우 두 규칙 집합이 중재되어야 하므로 동작은 더 복잡해집니다. 사용자가 **USE**를 통해 다른 데이터베이스를 사용할 수 있는 부분적으로 포함된 데이터베이스에서 이러한 문제가 발생할 수 있습니다. 이 경우 데이터 정렬 규칙의 차이는 다음 원칙에 따라 처리됩니다.  
  
-   일괄 처리의 데이터 정렬 동작은 일괄 처리가 시작되는 데이터베이스에 의해 결정됩니다.  
  
 이러한 의사 결정은 최초의 **USE**를 포함하여 어떤 명령도 실행되기 이전에 이루어집니다. 즉, 일괄 처리가 포함된 데이터베이스에서 시작되지만 첫 번째 명령이 포함되지 않은 데이터베이스에 대한 **USE**인 경우 이 일괄 처리에 대해서는 포함된 데이터 정렬 동작이 사용됩니다. 이 점을 고려하면 예를 들어 변수에 대한 참조가 다음과 같은 여러 가지 결과를 생성할 수 있습니다.  
  
-   참조가 일치하는 항목을 정확히 한 개 찾습니다. 이 경우 참조는 오류 없이 작동합니다.  
  
-   참조가 이전에는 일치 항목이 있었던 현재 데이터 정렬에서 일치 항목을 찾지 못합니다. 이런 경우 변수가 분명히 만들어졌음에도 불구하고 변수가 없음을 나타내는 오류가 발생합니다.  
  
-   참조가 원래는 구별되었던 여러 개의 일치 항목을 찾습니다. 이 경우에도 오류가 발생합니다.  
  
 몇 가지 예를 들어 이러한 경우를 설명하겠습니다. 이 경우 데이터베이스 데이터 정렬이 기본 데이터 정렬(**Latin1_General_100_CI_AS_WS_KS_SC**)로 설정된 `MyCDB`라는 부분적으로 포함된 데이터베이스가 있다고 가정합니다. 인스턴스 데이터 정렬은 **Latin1_General_100_CS_AS_WS_KS_SC**라고 가정합니다. 두 데이터 정렬은 대/소문자 구분 여부에서만 다릅니다.  
  
### 예제 1  
 다음 예에서는 참조가 일치하는 항목을 정확히 하나 찾는 경우를 보여 줍니다.  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #a VALUES(1);  
GO  
  
USE master;  
GO  
  
SELECT * FROM #a;  
GO  
  
Results:  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
x  
-----------  
1  
```  
  
 이 경우 식별된 #a는 대/소문자를 구분하지 않는 카탈로그 데이터 정렬과 대/소문자를 구분하는 인스턴스 데이터 정렬 모두에 바인딩하고 코드는 정상적으로 작동합니다.  
  
### 예제 2  
 다음 예에서는 참조가 이전에는 일치하는 항목이 있었던 현재 데이터 정렬에서 일치하는 항목을 찾지 못하는 경우를 보여 줍니다.  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #A VALUES(1);  
GO  
```  
  
 여기에서 #A는 대/소문자를 구분하지 않는 기본 데이터 정렬에서 #a와 바인딩하고 삽입이 제대로 작동합니다.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
```  
  
 하지만 스크립트를 계속 실행하면...  
  
```  
USE master;  
GO  
  
SELECT * FROM #A;  
GO  
```  
  
 대/소문자를 구분하는 인스턴스 데이터 정렬에서 #A에 바인딩하려고 하는 동안 오류가 발생합니다.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 메시지 208, 수준 16, 상태 0, 줄 2  
  
 개체 이름 '#A'이(가) 잘못되었습니다.  
  
### 예 3  
 다음 예에서는 참조가 원래는 구별되었던 여러 개의 일치 항목을 찾는 경우를 보여 줍니다. 먼저 인스턴스와 동일한 대/소문자 구분 데이터 정렬을 가지고 있는 **tempdb**에서 시작하여 다음 문을 실행합니다.  
  
```  
USE tempdb;  
GO  
  
CREATE TABLE #a(x int);  
GO  
CREATE TABLE #A(x int);  
GO  
INSERT INTO #a VALUES(1);  
GO  
INSERT INTO #A VALUES(2);  
GO  
```  
  
 이 데이터 정렬에서는 테이블이 구별되므로 이 작업은 성공합니다.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
(1 row(s) affected)  
```  
  
 하지만 포함된 데이터베이스로 넘어가면 이러한 테이블에 더 이상 바인딩할 수 없습니다.  
  
```  
USE MyCDB;  
GO  
SELECT * FROM #a;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 메시지 12800, 수준 16, 상태 1, 줄 2  
  
 임시 테이블 이름 '#a'에 대한 참조는 모호하며 해결할 수 없습니다. 가능한 후보는 '#a' 및 '#A'입니다.  
  
## 결론  
 포함된 데이터베이스의 데이터 정렬 동작은 포함되지 않은 데이터베이스의 데이터 정렬 동작과 약간 다릅니다. 이 동작은 인스턴스 독립과 단순성을 제공하므로 일반적으로 유익합니다. 포함된 데이터베이스와 포함되지 않은 데이터베이스에 세션이 모두 액세스하는 경우 일부 사용자에게 문제가 발생할 수 있습니다.  
  
## 참고 항목  
 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)  
  
  