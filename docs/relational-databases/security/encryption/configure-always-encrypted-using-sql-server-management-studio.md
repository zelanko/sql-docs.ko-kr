---
title: "SQL Server Management Studio를 사용하여 상시 암호화 구성 | Microsoft 문서"
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords: Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
caps.latest.revision: "15"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d4181262d713918c834d7dc971444118f11fe623
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 상시 암호화 구성
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

이 문서에서는 [SSMS(SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md)를 사용하여 상시 암호화를 구성하고 상시 암호화를 사용하는 데이터베이스를 관리하는 작업에 대해 설명합니다.

SSMS를 사용하여 상시 암호화를 구성하는 경우 SSMS에서 상시 암호화 키와 중요한 데이터를 둘 다 처리하므로 키와 데이터가 SSMS 프로세스 내에서 일반 텍스트로 모두 표시됩니다. 따라서 보안 컴퓨터에서 SSMS를 실행하는 것이 중요합니다. 데이터베이스가 SQL Server에서 호스트된 경우 SQL Server 인스턴스를 호스트하는 컴퓨터 이외의 다른 컴퓨터에서 SSMS를 실행합니다. 상시 암호화의 주요 목표는 데이터베이스 시스템이 손상된 경우에도 암호화된 중요한 데이터를 안전하게 보호하는 것이므로 SQL Server 컴퓨터에서 키 또는 중요한 데이터를 처리하는 PowerShell 스크립트를 실행하면 기능의 이점이 감소하거나 무효화될 수 있습니다. 추가 권장 사항을 보려면 [키 관리에 대한 보안 고려 사항](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)을 참조하세요.

SSMS는 데이터베이스를 관리하는 사용자(DBA)와 암호화 암호를 관리하고 일반 텍스트 데이터에 액세스할 수 있는 사용자(보안 관리자 및/또는 응용 프로그램 관리자) 간의 역할 구분을 지원하지 않습니다. 조직에서 역할 구분을 적용하는 경우 PowerShell을 사용하여 상시 암호화를 구성해야 합니다. 자세한 내용은 [상시 암호화를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) 및 [PowerShell을 사용하여 상시 암호화 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)을 참조하세요.

## <a name="configuring-always-encrypted-using-the-always-encrypted-wizard"></a>상시 암호화 마법사를 사용하여 상시 암호화 구성

[상시 암호화 마법사](../../../relational-databases/security/encryption/always-encrypted-wizard.md) 는 선택한 데이터베이스 열에 대해 원하는 암호화 구성을 설정할 수 있는 강력한 도구입니다. 현재 상시 암호화 구성 및 원하는 대상 구성에 따라 마법사에서 열을 암호화하거나, 암호를 해독(암호화 제거)하거나, 다시 암호화(예: 열에 대해 구성된 현재 형식과 다른 암호화 형식 또는 새 열 암호화 키 사용)할 수 있습니다. 마법사를 한 번 실행하여 여러 열을 구성할 수 있습니다.

상시 암호화에 대해 키를 프로비전하지 않은 경우 마법사에서 자동 생성합니다. 열 마스터 키의 키 저장소를 Windows 인증서 저장소 또는 Azure 주요 자격 증명 모음 중에서 선택하기만 하면 됩니다. 마법사가 데이터베이스에 키 이름과 키 메타데이터 개체를 자동 생성합니다. 키 프로비전 방법에 대한 추가 제어 및 열 마스터 키를 포함하는 키 저장소에 대한 추가 선택 항목이 필요한 경우 마법사를 시작하기 전에 **새 열 마스터 키** 및 **새 열 암호화 키** 대화 상자(아래 설명 참조)를 사용하여 키를 프로비전할 수 있습니다. 그런 다음 상시 암호화 마법사에서 기존 열 암호화 키를 선택할 수 있습니다.

마법사를 사용하는 방법에 대한 자세한 내용은  [상시 암호화 마법사](../../../relational-databases/security/encryption/always-encrypted-wizard.md)를 참조하세요.

## <a name="querying-encrypted-columns"></a>암호화된 열 쿼리

이 섹션에서는 다음 작업 수행 방법에 대해 설명합니다.   
-   암호화된 열에 저장된 암호 텍스트 값을 검색합니다.   
-   암호화된 열에 저장된 일반 텍스트 값을 검색합니다.   
-   암호화된 열을 대상으로 하는 일반 텍스트 값을 보냅니다(예: `INSERT` 또는 `UPDATE` 문에 포함하거나 `WHERE` 문에서 `SELECT` 절의 조회 매개 변수로).   

### <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>암호화된 열에 저장된 암호 텍스트 값 검색    

암호화된 열에서 값의 암호를 해독하지 않고 암호 텍스트 값을 검색하려면
1.  `SELECT` 쿼리를 실행 중인 쿼리 편집기 창에 대한 데이터베이스 연결에 Always Encrypted가 사용하지 않도록 설정되어 있는지 확인합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#en-dis) 을 참조하세요.      
2.  `SELECT` 쿼리를 실행합니다. 암호화된 열에서 검색된 모든 데이터는 이진(암호화) 값으로 반환됩니다.   

*예제*   
`SSN` 이 `Patients` 테이블의 암호화된 열이라고 가정할 경우, 아래 표시된 쿼리는 데이터베이스 연결에 Always Encrypted가 사용되지 않는 경우 이진 암호 텍스트 값을 검색합니다.   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
### <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>암호화된 열에 저장된 일반 텍스트 값 검색    

암호화된 열에서 일반 텍스트 값을 검색하여 값의 암호를 해독하려면   
1.  `SELECT` 쿼리를 실행 중인 쿼리 편집기 창에 대한 데이터베이스 연결에 Always Encrypted가 사용하도록 설정되어 있는지 확인합니다. 이는 SSMS에서 사용하는 .NET Framework Data Provider for SQL Server에 암호화된 열에서 검색된 데이터의 암호를 해독하도록 지시합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#en-dis) 을 참조하세요.
2.  암호화된 열에 대해 구성된 모든 열 마스터 키에 액세스할 수 있는지 확인합니다. 예를 들어 열 마스터 키가 인증서인 경우 SSMS가 실행되는 컴퓨터에 인증서를 배포해야 합니다. 또는 열 마스터 키가 Azure Key Vault에 저장된 키인 경우 해당 키에 대한 액세스 권한이 있는지 확인해야 합니다(Azure에 로그인하라는 메시지가 표시될 수도 있음).
3.  `SELECT` 쿼리를 실행합니다. 암호화된 열에서 검색된 모든 데이터는 원래 데이터 형식의 값으로 일반 텍스트 형식으로 반환됩니다.   

*예제*   
SSN이 `char(11)` 테이블의 암호화된 `Patients` 열이라고 가정할 경우, 아래 표시된 쿼리는 Always Encrypted가 데이터베이스 연결에 사용되고 `SSN` 열에 대해 구성된 열 마스터 키에 대한 액세스 권한이 있는 경우 일반 텍스트 값을 반환합니다.   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
### <a name="sending-plaintext-values-targeting-encrypted-columns"></a>암호화된 열을 대상으로 하는 일반 텍스트 값 보내기       

암호화된 열을 대상으로 하는 값을 보내는 쿼리(예: 암호화된 열에 저장된 값을 삽입, 업데이트 또는 필터링하는 쿼리)를 실행하려면 다음을 수행합니다.   
1.  `SELECT` 쿼리를 실행 중인 쿼리 편집기 창에 대한 데이터베이스 연결에 Always Encrypted가 사용하도록 설정되어 있는지 확인합니다. 이는 SSMS에서 사용하는 .NET Framework Data Provider for SQL Server에 암호화된 열을 대상으로 하는 매개 변수화된 Transact-SQL(아래 참조)을 암호화하도록 지시합니다. 아래의 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#en-dis) 을 참조하세요.   
2.  암호화된 열에 대해 구성된 모든 열 마스터 키에 액세스할 수 있는지 확인합니다. 예를 들어 열 마스터 키가 인증서인 경우 SSMS가 실행되는 컴퓨터에 인증서를 배포해야 합니다. 또는 열 마스터 키가 Azure Key Vault에 저장된 키인 경우 해당 키에 대한 액세스 권한이 있는지 확인해야 합니다(Azure에 로그인하라는 메시지가 표시될 수도 있음).   
3.  쿼리 편집기 창에 Always Encrypted에 대한 매개 변수화가 사용하도록 설정되어 있는지 확인합니다. SSMS 버전 17.0 이상이 필요합니다. Transact-SQL 변수를 선언하고 데이터베이스로 전송(삽입, 업데이트 또는 필터링)할 값으로 초기화합니다. 자세한 내용은 아래의 [Always Encrypted에 대한 매개 변수화](#param)를 참조하세요.   
    >   [!NOTE]
    >   Always Encrypted는 형식 변환의 제한된 하위 집합을 지원하므로 대부분의 경우 Transact-SQL 변수의 데이터 형식은 대상으로 하는 대상 데이터베이스 열의 형식과 같아야 합니다.   
4.  데이터베이스에 TRANSACT-SQL 변수 값을 전송하는 쿼리를 실행합니다. SSMS은 이 변수를 쿼리 매개 변수로 변환하고 해당 값을 암호화하여 데이터베이스로 전송합니다.   

*예제*   
`SSN` 이 `char(11)` 테이블의 암호화된 `Patients` 열이라고 가정할 경우, 아래 스크립트는 Always Encrypted가 데이터베이스 연결에 사용되고, Always Encrypted에 대한 매개 변수화가 쿼리 편집기 창에 사용하도록 설정되며, `'795-73-9838'` 열에 대해 구성된 열 마스터 키에 대한 액세스 권한이 있는 경우 SSN 열에서 `LastName` 이 포함된 행을 찾아서 `SSN` 열의 값을 반환합니다.   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)
 
### <a name="en-dis"></a> 데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함   

데이터베이스 연결에 Always Encrypted를 사용하도록 설정하면 SQL Server Management Studio에서 사용하는 .NET Framework Data Provider for SQL Server가 다음 작업을 투명하게 시도합니다.   
-   암호화된 열에서 검색된 값의 암호를 해독하여 쿼리 결과에 반환합니다.   
-   암호화된 데이터베이스 열을 대상으로 하는 매개 변수화된 TRANSACT-SQL 변수의 값을 암호화합니다.   
데이터베이스 연결에 Always Encrypted를 사용하도록 설정하려면 `Column Encryption Setting=Enabled` 서버에 연결 **대화 상자의** 추가 속성 **탭에서** 를 지정합니다.    
데이터베이스 연결에 Always Encrypted를 사용하지 않도록 설정하려면 `Column Encryption Setting=Disabled` 서버에 연결 **대화 상자의** 추가 속성 **탭에서** 열 암호화 설정 **의 설정을 제거하거나** 을 지정합니다(기본값은 **사용 안 함**).   

>  [!TIP] 
>  기존 쿼리 편집기 창에 대해 Always Encrypted의 사용을 설정하거나 해제하려면 다음을 수행합니다.   
>  1.   쿼리 편집기 창의 아무 곳이나 마우스 오른쪽 단추로 클릭합니다.
>  2.   **연결** > **연결 변경...**을 선택합니다. 
>  3.   **옵션**을 클릭합니다.
>  4.   **추가 속성** 탭을 선택하고 `Column Encryption Setting=Enabled`(Always Encrypted 동작 사용)를 입력하거나 설정을 제거(Always Encrypted 동작 사용 안 함)합니다.   
>  5.   **연결**을 클릭합니다.   
   
### <a name="param"></a>Always Encrypted에 대한 매개 변수화   
 
Always Encrypted에 대한 매개 변수화는 Transact-SQL 변수를 쿼리 매개 변수([SqlParameter 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)의 인스턴스)로 자동으로 변환하는 SQL Server Management Studio의 기능입니다. SSMS 버전 17.0 이상이 필요합니다. 이 기능을 사용하면 기본 .NET Framework Data Provider for SQL Server이 암호화된 열을 대상으로 하는 데이터를 검색하고, 이러한 데이터를 데이터베이스로 전송하기 전에 암호화합니다. 
  
매개 변수화하지 않으면 .NET Framework Data Provider가 쿼리 편집기에서 작성한 각 문을 매개 변수화되지 않은 쿼리로 전달합니다. 쿼리에 암호화된 열을 대상으로 하는 리터럴 또는 Transact-SQL 변수가 포함된 경우 .NET Framework Data Provider for SQL Server는 쿼리를 데이터베이스로 전송하기 전에 검색 및 암호화할 수 없습니다. 따라서 일반 텍스트 리터럴 Transact-SQL 변수와 암호화된 열 간의 형식 불일치로 인해 쿼리에 실패합니다. 예를 들어 `SSN` 열이 암호화된 것으로 가정할 경우 매개 변수화하지 않으면 다음 쿼리가 실패합니다.   

```tsql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

#### <a name="enablingdisabling-parameterization-for-always-encrypted"></a>Always Encrypted에 대한 매개 변수화 사용/사용 안 함   


Always Encrypted에 대한 매개 변수화를 기본적으로 사용하지 않도록 설정됩니다.    

현재 쿼리 편집기 창에 Always Encrypted에 대한 매개 변수화를 사용하도록/사용하지 않도록 설정하려면 다음을 수행합니다.   
1.  주 메뉴에서 **쿼리** 를 선택합니다.   
2.  **쿼리 옵션...**을 선택합니다.   
3.  **실행** > **고급**으로 이동합니다.   
4.  **Always Encrypted에 대해 매개 변수화 사용**을 선택하거나 선택 취소합니다.   
5.  **확인**을 클릭합니다.   

향후 쿼리 편집기 창에 Always Encrypted에 대한 매개 변수화를 사용하도록/사용하지 않도록 설정하려면 다음을 수행합니다.   
1.  주 메뉴에서 **도구** 를 선택합니다.   
2.  **옵션...**을 선택합니다.   
3.  **쿼리 실행** > **SQL Server** > **고급**으로 이동합니다.   
4.  **Always Encrypted에 대해 매개 변수화 사용**을 선택하거나 선택 취소합니다.   
5.  **확인**을 클릭합니다.   

Always Encrypted가 설정된 데이터베이스 연결을 사용하지만 매개 변수화가 사용되지 않는 쿼리 편집기 창에서 쿼리를 실행하는 경우 사용하도록 설정하라는 메시지가 나타납니다.   
>   [!NOTE]   
>   Always Encrypted에 대해 매개 변수화는 Always Encrypted가 설정된 데이터베이스 연결을 사용하는 쿼리 편집기 창에서만 작동합니다( [데이터베이스에 Always Encrypted 사용/사용 안 함](#en-dis)참조). 쿼리 편집기 창에서 Always Encrypted가 설정되지 않은 데이터베이스 연결을 사용하는 경우에는 Transact-SQL 변수가 매개 변수화되지 않습니다.   

#### <a name="how-parameterization-for-always-encrypted-works"></a>Always Encrypted에 대한 매개 변수화의 작동 방식   

쿼리 편집기 창에 대해 데이터베이스 연결에서 Always Encrypted에 대한 매개 변수화와 Always Encrypted 동작이 둘 다 사용하도록 설정된 경우 SQL Server Management Studio는 다음 필수 조건을 충족하는 Transact-SQL 변수를 매개 변수화합니다.    
- 동일한 문에 선언되고 초기화된 변수(인라인 초기화). 별도의 `SET` 문을 사용하여 선언된 변수는 매개 변수화되지 않습니다.   
- 단일 리터럴을 사용하여 초기화된 변수. 연산자나 함수가 포함된 식을 사용하여 초기화된 변수는 매개 변수화되지 않습니다.      

다음은 SQL Server Management Studio가 매개 변수화하는 변수의 예입니다.   
```tsql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

또한 SQL Server Management Studio가 매개 변수화하지 않는 변수의 몇 가지 예도 있습니다.   
```tsql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';
   
DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal
   
DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
시도한 매개 변수화가 성공하려면   
- 매개 변수화할 변수의 초기화에 사용된 리터럴 형식이 변수 선언의 형식과 일치해야 합니다.   
- 변수의 선언된 형식이 날짜 형식이거나 시간 형식인 경우 변수는 다음 ISO 8601 규격 형식 중 하나를 사용하는 문자열을 사용하여 초기화되어야 합니다.   

매개 변수화 오류가 발생하는 TRANSACT-SQL 변수 선언의 예는 다음과 같습니다.   
```tsql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio는 Intellisense를 사용하여 성공적으로 매개 변수화할 수 있는 변수와 매개 변수화 시도에 실패하는 변수(및 이유)를 알려 줍니다.   

성공적으로 매개 변수화할 수 있는 변수의 선언은 쿼리 편집기에 경고 밑줄로 표시됩니다. 경고 밑줄이 표시된 선언 문에 마우스를 놓으면 결과 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 개체(매핑된 변수)의 키 속성 값( [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), [Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx), [Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx), [Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx), [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx))을 포함하여 매개 변수화 프로세스의 결과가 표시됩니다. **오류 목록** 보기의 **경고** 탭에서 성공적으로 매개 변수화된 모든 변수의 전체 목록을 볼 수 있습니다. **오류 목록** 보기를 열려면 주 메뉴에서 **보기** 를 선택한 다음 **오류 목록**을 선택합니다.    

SQL Server Management Studio가 변수를 매개 변수화하려고 시도했지만 매개 변수화에 실패한 경우 해당 변수의 선언이 오류 밑줄로 표시됩니다. 오류 밑줄이 표시된 선언문 위에 마우스를 놓으면 오류에 대한 결과가 표시됩니다. **오류 목록** 보기의 **오류** 탭에서 모든 변수에 대한 전체 매개 변수화 오류 목록을 볼 수도 있습니다는. **오류 목록** 보기를 열려면 주 메뉴에서 **보기** 를 선택한 다음 **오류 목록**을 선택합니다.   

아래 스크린샷은 6개 변수 선언의 예를 보여 줍니다. SQL Server Management Studio에서 처음 세 개의 변수를 성공적으로 매개 변수화했습니다. 마지막 세 변수는 매개 변수화에 대한 필수 조건을 충족하지 않았으므로 SQL Server Management Studio에서 매개 변수화를 시도하지 않았습니다(선언이 표시되지 않음).   

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
아래의 또 다른 예제는 매개 변수화에 대한 필수 조건을 충족하지만 변수가 잘못 초기화되어 매개 변수화 시도에 실패한 두 변수를 보여 줍니다.    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
>   [!NOTE]
>   Always Encrypted는 형식 변환의 제한된 하위 집합을 지원하므로 대부분의 경우 Transact-SQL 변수의 데이터 형식은 대상으로 하는 대상 데이터베이스 열의 형식과 같아야 합니다. 예를 들어 `SSN` 테이블의 `Patients` 열 형식이 `char(11)`이라고 가정할 경우, 아래 쿼리는 `@SSN` 변수의 형식( `nchar(11)`)이 열 형식과 일치하지 않으므로 실패합니다.   

```tsql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.

>   [!NOTE]
>   매개 변수화를 사용하지 않으면 형식 변환을 포함하여 전체 쿼리가 SQL Server/Azure SQL Database 내에서 처리됩니다. 매개 변수화를 사용하면 일부 형식 변환이 SQL Server Management Studio 내의 .NET Framework에서 수행됩니다. .NET Framework 형식 시스템과 SQL Server 형식 시스템 간의 차이(예: float와 같은 일부 형식의 정밀도 차이)로 인해 매개 변수화를 사용하여 실행된 쿼리는 매개 변수화를 사용하지 않고 실행된 쿼리와 다른 결과를 생성할 수 있습니다. 

#### <a name="permissions"></a>Permissions      

암호 텍스트 데이터를 검색하는 쿼리를 포함하여 암호화된 열에 대해 쿼리를 실행하려면 데이터베이스에서 `VIEW ANY COLUMN MASTER KEY DEFINITION` 및 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 권한이 있어야 합니다.   
위 권한 외에도 쿼리 결과의 암호를 해독하거나 쿼리 매개 변수(Transact-SQL 변수를 매개 변수화하여 생성된)를 암호화하려면 대상 열을 보호하는 열 마스터 키에 대한 액세스 권한도 필요합니다.   
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 `Read` 권한이 있거나 컴퓨터의 관리자여야 합니다.   
- **Azure 주요 자격 증명 모음** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 `get`, `unwrapKey`및 verify 권한이 필요합니다.   
- **CNG(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.   
- **CAPI(암호화 서비스 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.   

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.


<a name="provisioncmk"></a>
## <a name="provisioning-column-master-keys-new-column-master-key"></a>열 마스터 키(새 열 마스터 키) 프로비전

**새 열 마스터 키** 대화 상자에서 열 마스터 키를 생성하거나 키 저장소를 통해 기존 키를 선택하고 데이터베이스에서 생성된 키 또는 선택한 키에 대한 열 마스터 키 메타데이터를 만들 수 있습니다.

1.  **개체 탐색기**를 사용하여 데이터베이스 아래의 **보안>상시 암호화 키** 폴더로 이동합니다.
2.  **열 마스터 키** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 열 마스터 키...**를 선택합니다. 
3.  **새 열 마스터 키** 대화 상자에서 열 마스터 키 메타데이터 개체의 이름을 입력합니다.
4.  키 저장소를 선택합니다.
    - **인증서 저장소 - 현재 사용자** – 개인 저장소인 Windows 인증서 저장소의 현재 사용자 인증서 저장소 위치를 나타냅니다. 
    - **인증서 저장소 - 로컬 컴퓨터** – Windows 인증서 저장소의 로컬 컴퓨터 인증서 저장소 위치를 나타냅니다. 
    - **Azure 주요 자격 증명 모음** – Azure에 로그인해야 합니다( **로그인**클릭). 로그인하면 Azure 구독 및 주요 자격 증명 모음 중 하나를 선택할 수 있습니다.
    - **CNG(키 저장소 공급자)** – CNG(Cryptography Next Generation) API를 구현하는 KSP(키 저장소 공급자)를 통해 액세스할 수 있는 키 저장소를 나타냅니다. 일반적으로 이 유형의 저장소는 HSM(하드웨어 보안 모듈)입니다. 이 옵션을 선택한 후 KSP를 선택해야 합니다. 기본적으로**Microsoft 소프트웨어 키 저장소 공급자** 가 선택되어 있습니다. HSM에 저장된 열 마스터 키를 사용하려는 경우 장치에 대해 KSP를 선택합니다(대화 상자를 열기 전에 컴퓨터에 설치 및 구성해야 함).
    -   **CAPI(암호화 서비스 공급자)** - CAPI(암호화 API)를 구현하는 CSP(암호화 서비스 공급자)를 통해 액세스할 수 있는 키 저장소입니다. 일반적으로 이러한 저장소는 HSM(하드웨어 보안 모듈)입니다. 이 옵션을 선택한 후 CSP를 선택해야 합니다.  HSM에 저장된 열 마스터 키를 사용하려는 경우 장치에 대해 CSP를 선택합니다(대화 상자를 열기 전에 컴퓨터에 설치 및 구성해야 함).
    
    >   [!NOTE]
    >   CAPI가 사용되지 않는 API이기 때문에 CAPI(암호화 서비스 공급자) 옵션은 기본적으로 비활성화되어 있습니다. Windows 레지스트리에서 **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** 키 아래에 CAPI Provider Enabled DWORD 값을 만들고 1로 설정하면 사용할 수 있습니다. 키 저장소가 CNG를 지원하는 한, CAPI 대신 CNG를 사용해야 합니다.
   
    위의 키 저장소에 대한 자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

5.  키 저장소에서 기존 키를 선택하거나 **키 생성** 또는 **인증서 생성** 단추를 클릭하여 키 저장소에 키를 만듭니다. 
6.  **확인** 을 클릭하면 새 키가 목록에 표시됩니다. 

SQL Server Management Studio에서 데이터베이스에 열 마스터 키에 대한 메타데이터를 만듭니다. 대화 상자에서 이 작업을 위해 [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 생성하고 실행합니다.


<a name="provisioncek"></a> 
## <a name="provisioning-column-encryption-keys-new-column-encryption-key"></a>열 암호화 키(새 열 암호화 키) 프로비전

**새 열 암호화 키** 대화 상자에서 새 열 암호화 키를 생성하고, 열 마스터 키로 암호화하고, 데이터베이스에 열 암호화 키 메타데이터를 만들 수 있습니다.

1.  **개체 탐색기**를 사용하여 데이터베이스 아래의 **보안/상시 암호화 키** 폴더로 이동합니다.
2.  **열 암호화 키** 폴더를 마우스 오른쪽 단추로 클릭하고 **새 열 암호화 키...**를 선택합니다. 
3.  **새 열 암호화 키** 대화 상자에서 열 암호화 키 메타데이터 개체의 이름을 입력합니다.
4.  데이터베이스에서 열 마스터 키를 나타내는 메타데이터 개체를 선택합니다.
5.  **확인**을 클릭합니다. 


SQL Server Management Studio에서 새 열 암호화 키를 생성한 다음 데이터베이스에서 선택한 열 마스터 키에 대한 메타데이터를 검색합니다. 그런 다음 SQL Server Management Studio는 열 마스터 키 메타데이터를 사용하여 열 마스터 키가 포함된 키 저장소에 연결하고 열 암호화 키를 암호화합니다. 마지막으로, 새 열 암호화 키에 대한 메타데이터가 데이터베이스에 생성됩니다. 대화 상자에서 이 작업을 위해 [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 문을 생성하고 실행합니다.

### <a name="permissions"></a>Permissions

대화 상자에서 열 암호화 키 메타데이터를 만들고 열 마스터 키 메타데이터에 액세스하려면 데이터베이스에서 *ALTER ANY ENCRYPTION MASTER KEY* 및 *VIEW ANY COLUMN MASTER KEY DEFINITION* 권한이 있어야 합니다.
키 저장소에 액세스하고 열 마스터 키를 사용하려면 키 저장소 또는/및 키에 대한 사용 권한이 필요할 수 있습니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure 주요 자격 증명 모음** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 *get*, *unwrapKey*, *wrapKey*, *sign*및 *verify*  권한이 필요합니다.
- **CNG(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급자)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

<a name="rotatecmk"></a>
## <a name="rotating-column-master-keys"></a>열 마스터 키 순환

열 마스터 키 순환은 기존 열 마스터 키를 새 열 마스터 키로 대체하는 프로세스입니다. 키가 손상된 경우 또는 암호화 키를 정기적으로 순환하도록 요구하는 조직의 정책이나 규정 준수 규칙을 준수하기 위해 키를 순환해야 할 수 있습니다. 열 마스터 키 순환에서는 현재 열 마스터 키로 보호된 열 암호화 키의 암호를 해독하고 새 열 마스터 키를 사용하여 다시 암호화한 다음 키 메타데이터를 업데이트합니다. 자세한 내용은 [상시 암호화를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.

**1단계: 새 열 마스터 키 프로비전**

위의 열 마스터 키 프로비전 섹션에 있는 단계를 수행하여 새 열 마스터 키를 프로비전합니다.

**2단계: 새 열 마스터 키로 열 암호화 키 암호화**

열 마스터 키는 일반적으로 하나 이상의 열 암호화 키를 보호합니다. 각 열 암호화 키에는 데이터베이스에 저장된 암호화된 값이 있으며 열 마스터 키로 열 암호화 키를 암호화하는 제품입니다.
이 단계에서는 순환할 열 마스터 키로 보호된 각 열 암호화 키를 새 열 마스터 키로 암호화하고 새로 암호화된 값을 데이터베이스에 저장합니다. 따라서 순환의 영향을 받는 각 열 암호화 키에는 기존 열 마스터 키로 암호화된 값과 새 열 마스터 키로 암호화된 새 값의 두 가지 암호화된 값이 있습니다.

1.  **개체 탐색기**를 사용하여 **보안>상시 암호화 키>열 마스터 키** 폴더로 이동한 다음 순환할 열 마스터 키를 찾습니다.
2.  열 마스터 키를 마우스 오른쪽 단추로 클릭하고 **순환**을 선택합니다.
3.  **열 마스터 키 순환** 대화 상자의 **대상** 필드에서, 1단계에서 만든 새 열 마스터 키의 이름을 선택합니다.
4.  기존 열 마스터 키로 보호되는 열 암호화 키의 목록을 검토합니다. 이러한 키에 회전이 적용됩니다.
5.  **확인**을 클릭합니다.

SQL Server Management Studio에서 이전 열 마스터 키로 보호된 열 암호화 키의 메타데이터와 이전 및 새 열 마스터 키의 메타데이터를 가져옵니다. 그런 다음 SSMS는 열 마스터 키 메타데이터를 사용하여 이전 열 마스터 키가 포함된 키 저장소에 연결하고 열 암호화 키의 암호를 해독합니다. 이후에 SSMS는 새 열 마스터 키가 포함된 키 저장소에 액세스하여 열 암호화 키의 새로 암호화된 값 집합을 생성한 다음 새 값을 메타데이터에 추가합니다( [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 문 생성 및 실행).

> [!NOTE]
> 이전 열 마스터 키로 암호화된 각 열 암호화 키가 다른 열 마스터 키로 암호화되지 않도록 합니다. 즉, 회전이 적용되는 각 열 암호화 키는 데이터베이스에 정확히 하나의 암호화된 값만 포함해야 합니다. 영향을 받는 열 암호화 키에 암호화된 값이 두 개 이상 있는 경우 순환을 진행하기 전에 값을 제거해야 합니다(열 암호화 키의 암호화된 값을 제거하는 방법은 *4단계* 참조).

**3단계: 새 열 마스터 키로 응용 프로그램 구성**

이 단계에서는 순환할 열 마스터 키로 보호된 데이터베이스 열(즉, 순환할 열 마스터 키로 암호화된 열 암호화 키로 암호화된 데이터베이스 열)을 쿼리하는 모든 클라이언트 응용 프로그램이 새 열 마스터 키에 액세스할 수 있는지 확인해야 합니다. 이 단계는 새 열 마스터 키가 있는 키 저장소의 유형에 따라 달라집니다. 예를 들어
- 새 열 마스터 키가 Windows 인증서 저장소에 저장된 인증서인 경우 데이터베이스에서 열 마스터 키의 키 경로에 지정된 위치와 동일한 인증서 저장소 위치(*현재 사용자* 또는 *로컬 컴퓨터*)에 인증서를 배포해야 합니다. 응용 프로그램에서 인증서에 액세스할 수 있어야 합니다.
    - 인증서가 *현재 사용자* 인증서 저장소 위치에 저장된 경우 인증서를 응용 프로그램 Windows ID(사용자)의 현재 사용자 저장소로 가져와야 합니다.
    - 인증서가 *로컬 컴퓨터* 인증서 저장소 위치에 저장된 경우 응용 프로그램의 Windows ID에 인증서에 액세스할 권한이 있어야 합니다.
- 새 열 마스터 키가 Microsoft Azure 주요 자격 증명 모음에 저장된 경우 응용 프로그램이 Azure에 인증할 수 있고 키에 대한 액세스 권한이 있도록 응용 프로그램을 구현해야 합니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

> [!NOTE]
> 순환의 이 시점에서는 이전 열 마스터 키와 새 열 마스터 키가 모두 유효하며 데이터에 액세스하는 데 사용할 수 있습니다.

**4단계: 이전 열 마스터 키로 암호화된 열 암호화 키 값 정리**

새 열 마스터 키를 사용하도록 모든 응용 프로그램을 구성했으면 데이터베이스에서 *이전* 열 마스터 키로 암호화된 열 암호화 키 값을 제거합니다. 이전 값을 제거하면 다음 순환을 수행할 준비가 된 것입니다(순환할 열 마스터 키로 보호된 각 열 암호화 키에 정확히 하나의 암호화된 값이 있어야 함).

이전 열 마스터 키를 보관 또는 제거하기 전에 이전 값을 정리하는 다른 이유는 성능 때문입니다. 암호화된 열을 쿼리할 때 상시 암호화 가능 클라이언트 드라이버가 두 값(이전 값과 새 값)의 암호를 모두 해독해야 할 수도 있습니다. 드라이버는 응용 프로그램 환경에서 두 열 마스터 키 중 어떤 것이 유효한지 모르기 때문에 서버에서 암호화된 두 값을 모두 검색합니다. 사용 불가능한 열 마스터 키로 보호되기 때문에 값 중 하나의 암호 해독에 실패하는 경우(예: 저장소에서 제거된 이전 열 마스터 키) 드라이버는 새 열 마스터 키를 사용하여 다른 값의 암호 해독을 시도합니다.

> [!WARNING]
> 응용 프로그램에 해당 열 마스터 키가 제공되기 전에 열 암호화 키 값을 제거하면 응용 프로그램에서 데이터베이스 열의 암호를 더 이상 해독할 수 없습니다.

1.  **개체 탐색기**를 사용하여 **보안>상시 암호화 키** 폴더로 이동한 다음 대체할 기존 열 마스터 키를 찾습니다.
2.  기존 열 마스터 키를 마우스 오른쪽 단추로 클릭하고 **정리**를 선택합니다.
3.  제거할 열 암호화 키 값의 목록을 검토합니다.
4.  **확인**을 클릭합니다.

SQL Server Management Studio에서 [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 문을 실행하여 이전 열 마스터 키로 암호화된 열 암호화 키의 암호화된 값을 삭제합니다.

**5단계: 이전 열 마스터 키에 대한 메타데이터 삭제**

데이터베이스에서 이전 열 마스터 키의 정의를 제거하도록 선택한 경우 아래 단계를 따르세요. 
1.  **개체 탐색기**를 사용하여 **보안>상시 암호화 키>열 마스터 키** 폴더로 이동한 다음 데이터베이스에서 제거할 이전 열 마스터 키를 찾습니다.
2.  이전 열 마스터 키를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다. 이렇게 하면 [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) 문이 생성 및 실행되어 열 마스터 키 메타데이터를 제거합니다.
3.  **확인**을 클릭합니다.

> [!NOTE]
> 순환 후에 이전 열 마스터 키를 영구적으로 삭제하지 않는 것이 좋습니다. 대신, 이전 열 마스터 키를 현재 키 저장소에 유지하거나 다른 안전한 장소에 보관해야 합니다. 백업 파일에서 새 열 마스터 키가 구성되기 전의 시점으로 데이터베이스를 복원하는 경우 데이터에 액세스하려면 이전 키가 필요합니다.

### <a name="permissions"></a>Permissions

열 마스터 키를 순환하려면 다음과 같은 데이터베이스 사용 권한이 있어야 합니다.

- **ALTER ANY COLUMN MASTER KEY** – 새 열 마스터 키에 대한 메타데이터를 만들고 이전 열 마스터 키에 대한 메타데이터를 삭제하는 데 필요합니다.
- **ALTER ANY COLUMN ENCRYPTION KEY** - 열 암호화 키 메타데이터를 수정하고 새로 암호화된 값을 추가하는 데 필요합니다.
- **VIEW ANY COLUMN MASTER KEY DEFINITION** - 열 마스터 키의 메타데이터를 액세스하고 읽는 데 필요합니다.
- **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** - 열 암호화 키의 메타데이터를 액세스하고 읽는 데 필요합니다. 

또한 키 저장소에서 이전 열 마스터 키와 새 열 마스터 키를 모두 액세스할 수 있어야 합니다. 키 저장소에 액세스하고 열 마스터 키를 사용하려면 키 저장소 또는/및 키에 대한 사용 권한이 필요할 수 있습니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure 주요 자격 증명 모음** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 *create*, *get*, *unwrapKey*, *wrapKey*, *sign*및 *verify* 권한이 필요합니다.
- **CNG(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급자)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

<a name="rotatecek"></a> 
## <a name="rotating-column-encryption-keys"></a>열 암호화 키 순환

열 암호화 키를 순환하려면 모든 열에서 순환할 키로 암호화된 데이터의 암호를 해독하고 새 열 암호화 키를 사용하여 데이터를 다시 암호화해야 합니다.

>[!NOTE]
> 순환할 키로 암호화된 열을 포함하는 테이블이 크면 열 암호화 키를 순환하는 데 시간이 오래 걸릴 수 있습니다. 데이터를 다시 암호화하는 동안에는 응용 프로그램이 영향을 받는 테이블에 쓸 수 없습니다. 따라서 조직에서 열 암호화 키 순환을 계획할 때는 주의해야 합니다.
열 암호화 키를 순환하려면 상시 암호화 마법사를 사용합니다.

1.  데이터베이스에 대한 마법사를 엽니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업**을 가리킨 다음 **열 암호화**를 클릭합니다.
2.  **소개** 페이지를 검토하고 **다음**을 클릭합니다.
3.  **열 선택** 페이지에서 테이블을 확장하고 이전 열 암호화 키로 현재 암호화된, 바꾸려는 열을 모두 찾습니다.
4.  이전 열 암호화 키로 암호화된 각 열에 대해 **암호화 키** 를 자동 생성된 새 키로 설정합니다. **참고:** 또는 마법사를 실행하기 전에 새 열 암호화 키를 만들 수 있습니다. 위의 *열 암호화 키 프로비전* 섹션을 참조하세요.
5.  **마스터 키 구성** 페이지에서 새 키를 저장할 위치를 선택하고 마스터 키 원본을 선택한 후 **다음**을 클릭합니다. **참고:** 자동 생성된 열 암호화 키가 아니라 기존 열 암호화 키를 사용하는 경우에는 이 페이지에서 수행할 작업이 없습니다.
6.  **유효성 검사**페이지에서 스크립트를 즉시 실행할지 아니면 PowerShell 스크립트를 만들지 선택하고 **다음**을 클릭합니다.
7.  **요약** 페이지에서 선택한 옵션을 검토하고 **마침** 을 클릭합니다. 완료되면 마법사를 닫습니다.
8.  **개체 탐색기**를 사용하여 **보안/상시 암호화 키/열 암호화 키** 폴더로 이동한 다음 데이터베이스에서 제거할 이전 열 암호화 키를 찾습니다. 키를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.

### <a name="permissions"></a>Permissions

열 암호화 키를 순환하려면 다음과 같은 데이터베이스 권한이 있어야 합니다. **ALTER ANY COLUMN MASTER KEY** – 자동 생성된 새 열 암호화 키를 사용하는 경우에 필요합니다(새 열 마스터 키와 새 메타데이터도 생성됨).
**ALTER ANY COLUMN ENCRYPTION KEY** – 새 열 암호화 키에 대한 메타데이터를 추가하는 데 필요합니다.
**VIEW ANY COLUMN MASTER KEY DEFINITION** - 열 마스터 키의 메타데이터를 액세스하고 읽는 데 필요합니다.
**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** - 열 암호화 키의 메타데이터를 액세스하고 읽는 데 필요합니다.

또한 새 열 암호화 키와 이전 열 암호화 키 둘 다의 열 마스터 키에 액세스할 수 있어야 합니다. 키 저장소에 액세스하고 열 마스터 키를 사용하려면 키 저장소 또는/및 키에 대한 사용 권한이 필요할 수 있습니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure 주요 자격 증명 모음** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 get, unwrapKey 및 verify 권한이 필요합니다.
- **CNG(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급자)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

## <a name="performing-dac-upgrade-operations-when-database-or-dacpac-uses-always-encrypted"></a>데이터베이스 또는 DACPAC에서 상시 암호화를 사용하는 경우 DAC 업그레이드 작업 수행

[DAC 작업](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) 은 암호화된 열을 포함하는 스키마가 있는 DACPAC 파일 및 데이터베이스에서 지원됩니다. DAC 업그레이드 작업에는 특별한 고려 사항이 적용됩니다. SSMS를 비롯한 다양한 도구에서 DAC 업그레이드 작업을 수행하는 방법은 [데이터 계층 응용 프로그램 업그레이드](../../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md) 를 참조하세요. 

DACPAC를 사용하여 데이터베이스를 업그레이드하고 DACPAC 또는 대상 데이터베이스에 암호화된 열이 있는 경우 다음 조건이 모두 충족되면 업그레이드 작업에서 데이터 암호화 작업을 트리거합니다.
- 데이터베이스에 데이터를 포함하는 열이 있습니다.
- DACPAC에 동일한 열이 있습니다.
- 데이터베이스에 있는 열의 암호화 구성이 DACPAC에 있는 해당 열의 구성과 다릅니다. 자세한 내용은 아래 표를 참조하세요.

| 조건|동작|
|:---|:---|
|DACPAC에서는 열이 암호화되고 데이터베이스에서는 암호화되지 않습니다.| 열의 데이터가 암호화됩니다.|
|DACPAC에서는 열이 암호화되지 않고 데이터베이스에서는 암호화됩니다.| 열의 데이터 암호가 해독됩니다(열에 대한 암호화가 제거됨).|
| DACPAC와 데이터베이스 둘 다에서 열이 암호화되지만 DACPAC의 열은 데이터베이스의 해당 열과 다른 암호화 유형 또는/및 다른 열 암호화 키를 사용합니다.|열의 데이터 암호가 해독된 다음 DACPAC의 암호화 구성에 맞게 다시 암호화됩니다.|

> [!NOTE]
> 데이터베이스 또는 DACPAC의 열에 대해 구성된 열 마스터 키가 Azure 주요 자격 증명 모음에 저장된 경우 Azure에 로그인하라는 메시지가 표시됩니다(로그인하지 않은 경우).

### <a name="permissions"></a>Permissions

DACPAC 또는 대상 데이터베이스에서 상시 암호화가 설정된 경우 DAC 업그레이드 작업을 수행하려면 DACPAC의 스키마와 대상 데이터베이스 스키마 간의 차이에 따라 아래 사용 권한 중 일부 또는 모두가 필요할 수 있습니다.

*ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*, *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

업그레이드 작업이 데이터 암호화 작업을 트리거하는 경우 영향을 받는 열에 대해 구성된 열 마스터 키에도 액세스할 수 있어야 합니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure 주요 자격 증명 모음** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 *create*, *get*, *unwrapKey*, *wrapKey*, *sign*및 *verify* 권한이 필요합니다.
- **CNG(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급자)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

## <a name="migrating-databases-with-encrypted-columns-using-bacpac"></a>BACPAC를 사용하여 암호화된 열이 있는 데이터베이스 마이그레이션

데이터베이스를 내보낼 때 암호화된 열에 저장된 모든 데이터가 검색되어 결과 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) (암호화된 형태)에 저장됩니다. 결과 BACPAC에는 상시 암호화 키에 대한 메타데이터도 포함됩니다.

BACPAC를 데이터베이스로 가져올 때 BACPAC의 암호화된 데이터가 데이터베이스에 로드되고 상시 암호화 키 메타데이터가 다시 생성됩니다.

원본 데이터베이스(내보낸 데이터베이스)에 저장된 암호화된 데이터를 수정하거나 검색하도록 구성된 응용 프로그램이 있는 경우 두 데이터베이스의 키가 동일하기 때문에 응용 프로그램이 대상 데이터베이스의 암호화된 데이터를 쿼리할 수 있도록 특별히 수행해야 하는 작업은 없습니다.


### <a name="permissions"></a>Permissions

원본 데이터베이스에 대한 *ALTER ANY COLUMN MASTER KEY* 및 *ALTER ANY COLUMN ENCRYPTION KEY* 권한이 필요합니다. 대상 데이터베이스에 대한 *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*및 *VIEW ANY COLUMN ENCRYPTION* 권한이 필요합니다.

## <a name="migrating-databases-with-encrypted-columns-using-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사를 사용하여 암호화된 열이 있는 데이터베이스 마이그레이션

[SQL Server 가져오기 및 내보내기 마법사](~/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) 를 사용할 경우 BACPAC 파일에 비해 데이터 마이그레이션 중 암호화된 열에 저장된 데이터의 처리 방법을 보다 자세하게 제어할 수 있습니다.

- 데이터 원본이 상시 암호화를 사용하는 데이터베이스인 경우 암호화된 열에 저장된 데이터가 내보내기 작업 중 암호 해독되거나 암호화된 상태로 유지되도록 데이터 원본 연결을 구성할 수 있습니다.
- 데이터 대상이 상시 암호화를 사용하는 데이터베이스인 경우 암호화된 열을 대상으로 하는 데이터가 암호화되도록 데이터 대상 연결을 구성할 수 있습니다.

암호 해독(데이터 원본) 또는 암호화(데이터 대상)를 사용할 수 있으려면 [.NET Framework Data Provider for SqlServer](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) 를 사용하도록 데이터 원본/대상 연결을 구성해야 하며, 열 암호화 설정 연결 문자열 키워드를 *사용*으로 설정해야 합니다.

아래 표에서는 가능한 마이그레이션 시나리오와 각 연결에 대한 데이터 원본 및 데이터 대상 구성과 함께 상시 암호화와 어떤 관계가 있는지를 보여 줍니다.

| 시나리오|원본 연결 구성| 대상 연결 구성
|:---|:---|:---
|마이그레이션 시 데이터를 암호화합니다. 데이터가 일반 텍스트로 데이터 원본에 저장되고 데이터 대상의 암호화된 열로 마이그레이션됩니다.| 데이터 공급자/드라이버: *임의*<br><br>열 암호화 설정 = 사용 안 함<br><br>(.Net Framework Data Provider for SqlServer 및 .NET Framework 4.6 이상을 사용하는 경우) | 데이터 공급자/드라이버: *.Net Framework Data Provider for SqlServer* (.NET Framework 4.6 이상 필요)<br><br>열 암호화 설정 = 사용
| 마이그레이션 시 데이터 암호를 해독합니다. 데이터가 데이터 원본의 암호화된 열에 저장되고 데이터 대상에 일반 텍스트로 마이그레이션됩니다. 데이터 대상이 데이터베이스인 경우 대상 열은 암호화되지 않습니다.<br><br>**참고:** 마이그레이션 전에 암호화된 열이 포함된 대상 테이블이 있어야 합니다.|데이터 공급자/드라이버: *.Net Framework Data Provider for SqlServer* (.NET Framework 4.6 이상 필요)<br><br>추가 속성|데이터 공급자/드라이버: *임의*<br><br>열 암호화 설정 = 사용 안 함<br><br>(.Net Framework Data Provider for SqlServer 및 .NET Framework 4.6 이상을 사용하는 경우)
|마이그레이션 시 데이터를 다시 암호화합니다. 데이터가 데이터 원본의 암호화된 열에 저장되고 열 암호화 키의 다른 암호화 유형을 사용하는 데이터 대상의 열에 일반 텍스트로 마이그레이션됩니다.<br><br>**참고:** 마이그레이션 전에 암호화된 열이 포함된 대상 테이블이 있어야 합니다.| 데이터 공급자/드라이버: *.Net Framework Data Provider for SqlServer* (.NET Framework 4.6 이상 필요)<br><br>추가 속성|데이터 공급자/드라이버: *.Net Framework Data Provider for SqlServer* (.NET Framework 4.6 이상 필요)<br><br>추가 속성
|암호를 해독하지 않고 암호화된 데이터를 이동합니다.<br><br>**참고:** 마이그레이션 전에 암호화된 열이 포함된 대상 테이블이 있어야 합니다.| 데이터 공급자/드라이버: *임의*<br>열 암호화 설정 = 사용 안 함<br><br>(.Net Framework Data Provider for SqlServer 및 .NET Framework 4.6 이상을 사용하는 경우)| 데이터 공급자/드라이버: *임의*<br>열 암호화 설정 = 사용 안 함<br><br>(.Net Framework Data Provider for SqlServer 및 .NET Framework 4.6 이상을 사용하는 경우)<br><br>사용자에 대해 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS가 ON으로 설정되어 있어야 합니다.<br><br>자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.


### <a name="permissions"></a>Permissions

데이터 원본에 저장된 데이터를 **암호화** 또는 **암호 해독** 하려면 원본 데이터베이스에 대한 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 권한이 있어야 합니다.

암호화했거나 암호를 해독할 데이터를 저장하는 열에 대해 구성된 열 마스터 키도 액세스할 수 있어야 합니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure 주요 자격 증명 모음** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 get, unwrapKey, wrapKey, sign 및 verify 권한이 필요합니다.
- **CNG(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

## <a name="see-also"></a>참고 항목
- [Always Encrypted(데이터베이스 엔진)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 마법사](../../../relational-databases/security/encryption/always-encrypted-wizard.md)
- [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [열 마스터 키 만들기 및 저장(Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Always Encrypted(클라이언트 개발)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
- [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)












