---
title: SQL Server의 사용자 정의 형식을 등록 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 942f6c1fa0b6888aa936bfd4b557c570529e9894
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35697824"
---
# <a name="registering-user-defined-types-in-sql-server"></a>SQL Server의 사용자 정의 형식 등록
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 정의 형식 (UDT)를 사용 하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 등록 해야 합니다. UDT를 등록하려면 해당 형식을 사용할 데이터베이스에 어셈블리를 등록하고 형식을 만듭니다. UDT는 범위가 단일 데이터베이스로 한정되며, 데이터베이스마다 동일한 어셈블리와 UDT를 등록하지 않는 한 여러 데이터베이스에 사용할 수 없습니다. UDT 어셈블리가 등록되고 형식이 만들어지면 [!INCLUDE[tsql](../../includes/tsql-md.md)]과 클라이언트 코드에 UDT를 사용할 수 있습니다. 자세한 내용은 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)을 참조하세요.  
  
## <a name="using-visual-studio-to-deploy-udts"></a>Visual Studio를 사용하여 UDT 배포  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio를 사용하면 UDT를 간편하게 배포할 수 있습니다. 그러나 배포 시나리오가 복잡하거나 높은 유연성이 요구되는 경우에는 이 항목에서 설명하는 대로 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용해야 합니다.  
  
 다음 단계에 따라 Visual Studio를 사용하여 UDT를 만들고 배포하십시오.  
  
1.  새 **데이터베이스** 프로젝트에 **Visual Basic** 또는 **Visual C#** 언어 노드.  
  
2.  UDT를 포함할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 참조를 추가합니다.  
  
3.  추가 **사용자 정의 형식** 클래스입니다.  
  
4.  UDT를 구현하는 코드를 작성합니다.  
  
5.  **빌드** 메뉴 선택 **배포**합니다. 그러면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 어셈블리가 등록되고 형식이 만들어집니다.  
  
## <a name="using-transact-sql-to-deploy-udts"></a>Transact-SQL을 사용하여 UDT 배포  
 UDT를 사용할 데이터베이스에 어셈블리를 등록할 때는 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 구문을 사용합니다. 등록된 어셈블리는 파일 시스템에 외부적으로 저장되는 것이 아니라 데이터베이스 시스템 테이블에 내부적으로 저장됩니다. UDT가 외부 어셈블리에 종속되어 있는 경우 해당 어셈블리도 데이터베이스에 로드해야 합니다. UDT를 사용할 데이터베이스에 UDT를 만들 때는 CREATE TYPE 문을 사용합니다. 자세한 내용은 참조 [CREATE ASSEMBLY &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/create-assembly-transact-sql.md) 및 [CREATE TYPE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)합니다.  
  
### <a name="using-create-assembly"></a>CREATE ASSEMBLY 사용  
 CREATE ASSEMBLY 구문은 UDT를 사용할 데이터베이스에 어셈블리를 등록하는 데 사용됩니다. 등록된 어셈블리에는 종속성이 없습니다.  
  
 특정 데이터베이스에 같은 어셈블리를 여러 버전으로 만들 수 없습니다. 그러나 특정 데이터베이스의 culture에 따라 같은 어셈블리를 여러 버전으로 만들 수는 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 어셈블리의 여러 culture 버전을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 서로 다른 이름으로 등록하여 구분합니다. 자세한 내용은 .NET Framework SDK에서 "강력한 이름의 어셈블리 생성 및 사용"을 참조하십시오.  
  
 SAFE 또는 EXTERNAL_ACCESS 권한 집합을 사용하여 CREATE ASSEMBLY를 실행하면 확인할 수 있으며 형식이 안전한지 여부에 대해 어셈블리 검사가 수행됩니다. 권한 집합을 지정하지 않으면 SAFE가 사용됩니다. UNSAFE 권한 집합을 사용한 코드는 검사되지 않습니다. 어셈블리 권한 집합에 대한 자세한 내용은 [Designing Assemblies](../../relational-databases/clr-integration/assemblies-designing.md)를 참조하십시오.  
  
#### <a name="example"></a>예제  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 Point 어셈블리를 등록 하는 문을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 **AdventureWorks** 안전 권한 집합으로 데이터베이스입니다. WITH PERMISSION_SET 절을 생략하면 어셈블리가 SAFE 권한 집합을 사용하여 등록됩니다.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용 하 여 어셈블리를 등록 *< assembly_bits >* FROM 절에는 인수입니다. 이 **varbinary** 값의 바이트 스트림을으로 파일을 나타냅니다.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 … 21ac78  
```  
  
### <a name="using-create-type"></a>CREATE TYPE 사용  
 어셈블리가 데이터베이스에 로드되면 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE 문을 사용하여 형식을 만들 수 있습니다. 그러면 해당 데이터베이스에 사용 가능한 형식 목록에 해당 형식이 추가됩니다. 형식은 범위가 데이터베이스로 제한되므로 해당 형식을 만든 데이터베이스에만 사용할 수 있습니다. 데이터베이스에 해당 UDT가 이미 있으면 오류가 발생하며 CREATE TYPE 문이 실패합니다.  
  
> [!NOTE]  
>  CREATE TYPE 구문은 네이티브 작성용는 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 별칭 데이터 형식, 및 대체 하기 위한 **sp_addtype** 별칭 데이터 형식을 만들기 위한 수단으로 합니다. CREATE TYPE 구문의 일부 선택적 인수는 UDT 만들기와 관련이 있으며 기본 유형과 같은 별칭 데이터 형식을 만드는 데 사용할 수 없습니다.  
  
 자세한 내용은 참조 [CREATE TYPE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)합니다.  
  
#### <a name="example"></a>예제  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 만듭니다는 **지점** 유형입니다. 두 부분으로 이루어진 명명 구문을 사용 하 여 외부 이름을 지정 *AssemblyName*. *UDTName*합니다.  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>데이터베이스에서 UDT 제거  
 DROP TYPE 문은 현재 데이터베이스에서 UDT를 제거합니다. UDT를 삭제한 경우 DROP ASSEMBLY 문을 사용하여 데이터베이스에서 어셈블리를 삭제할 수 있습니다.  
  
 다음과 같은 상황에서는 DROP TYPE 문이 실행되지 않습니다.  
  
-   UDT를 사용하여 정의한 열이 포함된 데이터베이스의 테이블  
  
-   데이터베이스에 WITH SCHEMABINDING 절로 만든 함수, 저장 프로시저 또는 트리거가 있고 이러한 루틴이 UDT의 변수 또는 매개 변수를 사용하는 경우  
  
### <a name="example"></a>예제  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 다음과 같은 순서로 실행해야 합니다. 첫 번째 참조 하는 테이블의 **지점** 형식은, 및 어셈블리를 마지막으로 UDT 삭제할 수 있어야 합니다.  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>UDT 종속성 찾기  
 UDT 열 정의가 있는 테이블과 같은 종속 개체가 있으면 DROP TYPE 문이 실패합니다. 또한 WITH SCHEMABINDING 절을 사용하여 데이터베이스에 만든 함수, 저장 프로시저 또는 트리거가 있고 이러한 루틴에서 사용자 정의 형식의 변수 및 매개 변수를 사용하는 경우에도 실패합니다. 따라서 먼저 모든 종속 개체를 삭제한 다음 DROP TYPE 문을 실행해야 합니다.  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리는 열과에서 UDT를 사용 하는 매개 변수 모두를 찾습니다는 **AdventureWorks** 데이터베이스입니다.  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>UDT 유지 관리  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 만든 UDT는 수정할 수 없습니다. 단, 해당 형식의 기반이 되는 어셈블리는 변경할 수 있습니다. 대부분의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP TYPE 문을 사용하여 데이터베이스에서 UDT를 제거하고 기본 어셈블리를 변경한 다음 ALTER ASSEMBLY 문을 사용하여 다시 로드해야 합니다. 그런 다음 UDT와 모든 종속 개체를 다시 만들어야 합니다.  
  
### <a name="example"></a>예제  
 UDT 어셈블리의 원본 코드를 변경하여 다시 컴파일한 후에는 ALTER ASSEMBLY 문이 사용됩니다. 이 문은 .dll 파일을 서버에 복사하고 새 어셈블리에 다시 바인딩합니다. 전체 구문을 참조 하십시오. [ALTER ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)합니다.  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 문은 디스크의 지정된 위치에서 Point.dll 어셈블리를 다시 로드합니다.  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>ALTER ASSEMBLY를 사용하여 원본 코드 추가  
 ALTER ASSEMBLY 구문의 ADD FILE 절은 CREATE ASSEMBLY에 없습니다. 이 절을 사용하여 원본 코드나 어셈블리와 연결된 다른 파일을 추가할 수 있습니다. 이렇게 하면 파일이 원래 위치에서 복사되어 데이터베이스의 시스템 테이블에 저장됩니다. 따라서 UDT의 현재 버전을 다시 만들거나 문서화해야 할 경우 간편하게 원본 코드나 기타 파일을 사용할 수 있습니다.  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 문은 Point.cs 클래스 원본 코드에 대 한 추가 **지점** UDT입니다. 이 문은 Point.cs 파일에 있는 텍스트를 복사하여 "PointSource"라는 이름으로 데이터베이스에 저장합니다.  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 어셈블리 정보에 저장 됩니다는 **sys.assembly_files** 어셈블리가 설치 되어 있는 데이터베이스의 테이블입니다. **sys.assembly_files** 테이블에는 다음 열입니다.  
  
 **assembly_id**  
 어셈블리에 대해 정의되는 식별자입니다. 해당 어셈블리와 관련한 모든 개체에 이 번호가 할당됩니다.  
  
 **name**  
 개체 이름입니다.  
  
 **file_id**  
 와 연결 된 첫 번째 개체와 각 개체를 식별 하는 번호는 주어진 **assembly_id** 1의 값이 지정 되 고 있습니다. 같은 연결 개체가 여러 개 있는 경우 **assembly_id**차례로 **file_id** 값은 1 씩 증가 합니다.  
  
 **content**  
 어셈블리 또는 파일의 16진수 표현입니다.  
  
 콘텐츠를 변환 하려면 CAST 또는 CONVERT 함수를 사용할 수는 **콘텐츠** 읽기 쉬운 텍스트로 변환할 열입니다. 다음 쿼리는 WHERE 절에 이름을 사용하여 결과 집합을 단일 행으로 제한함으로써 Point.cs 파일의 내용을 읽기 쉬운 텍스트로 변환합니다.  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 결과를 복사하여 텍스트 편집기에 붙여 넣으면 원래 내용에 있던 줄 바꿈과 공백이 그대로 유지되는 것을 알 수 있습니다.  
  
## <a name="managing-udts-and-assemblies"></a>UDT 및 어셈블리 관리  
 UDT 구현을 계획할 때는 UDT 어셈블리 자체에 필요한 메서드와 별도의 어셈블리에 만들고 사용자 정의 함수 또는 저장 프로시저로 구현해야 할 메서드를 고려해야 합니다. 메서드를 별도의 어셈블리로 분리하면 테이블의 UDT 열에 저장되어 있을 수 있는 데이터에 영향을 주지 않고 코드를 업데이트할 수 있습니다. 새 정의에서 변경되지 않은 형식의 이전 값과 서명을 읽을 수 있는 경우에만 UDT 열 및 기타 종속 개체를 삭제하지 않고 UDT 어셈블리를 수정할 수 있습니다.  
  
 변경될 수 있는 프로시저 코드를 UDT 구현에 필요한 코드와 분리하면 유지 관리가 훨씬 쉬워집니다. UDT 작동에 필요한 코드만 포함하고 UDT 정의를 가능한 한 단순하게 하면 코드 수정이나 버그 수정을 위해 UDT 자체를 데이터베이스에서 삭제해야 하는 위험을 줄일 수 있습니다.  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>Currency UDT 및 통화 변환 함수  
 **통화** 에서 UDT는 **AdventureWorks** 예제 데이터베이스의 UDT 및 관련된 함수 구성 하는 권장된 방법은 유용한 예제를 제공 합니다. **통화** UDT는 특정 culture의 화폐 시스템에 따라 금액을 처리에 사용 되며 달러, 유로 등 다양 한 통화 유형 저장할 수 있습니다. UDT 클래스를 사용 하는 문자열과 금액으로로 문화권 이름을 노출 한 **10 진수** 데이터 형식입니다. 필요한 모든 직렬화 메서드는 클래스를 정의하는 어셈블리에 들어 있습니다. 다른 특정 문화권에서의 통화 변환을 구현 하는 함수를 구현 하 여 라는 외부 함수로 **ConvertCurrency**,이 함수는 별도 어셈블리에 있습니다. **ConvertCurrency** 환율이의 테이블에서 검색 하 여는 작업을 수행 하는 함수는 **AdventureWorks** 데이터베이스입니다. 환율의 원본을 변경 해야 하거나 영향을 주지 않고 어셈블리를 쉽게 수정할 수 있는 기존 코드를 다른 변경 해야 합니다는 **통화** UDT입니다.  
  
 코드에 대 한 샘플은 **통화** UDT 및 **ConvertCurrency** 공용 언어 런타임 (CLR) 예제를 설치 하 여 함수를 찾을 수 있습니다.  
  
### <a name="using-udts-across-databases"></a>여러 데이터베이스에 UDT 사용  
 UDT는 기본적으로 단일 데이터베이스로 범위가 한정됩니다. 따라서 한 데이터베이스에 정의된 UDT를 다른 데이터베이스의 열 정의에 사용할 수 없습니다. 여러 데이터베이스에서 UDT를 사용하려면 각 데이터베이스의 동일한 어셈블리에서 CREATE ASSEMBLY 문과 CREATE TYPE 문을 실행해야 합니다. 어셈블리는 해당 이름, 강력한 이름, culture, 버전, 권한 집합 및 이진 내용이 같으면 동일한 것으로 간주됩니다.  
  
 두 데이터베이스에 UDT가 등록되어 있고 액세스할 수 있는 경우 한 데이터베이스의 UDT 값을 다른 데이터베이스에서 사용할 수 있도록 변환할 수 있습니다. 다음 시나리오에서 여러 데이터베이스에 동일한 UDT를 사용할 수 있습니다.  
  
-   서로 다른 데이터베이스에 정의된 저장 프로시저 호출  
  
-   서로 다른 데이터베이스에 정의된 여러 테이블 쿼리  
  
-   한 데이터베이스 테이블의 UDT 열에서 UDT 데이터를 선택하여 동일한 UDT 열이 있는 다른 한 데이터베이스에 삽입  
  
 이러한 시나리오에서는 필요한 변환이 서버에서 자동으로 수행됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 함수나 CONVERT 함수를 사용하여 변환을 명시적으로 수행할 수는 없습니다.  
  
 Udt를 사용 하기 위한 조치를 취할 필요가 없습니다 참고 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에 작업 테이블을 만듭니다는 **tempdb** 시스템 데이터베이스입니다. 테이블 변수, 커서의 처리가 포함 및 사용자 정의 테이블 반환 함수 등이 포함 된 Udt를 투명 하 게 활용 **tempdb**합니다. 그러나의 임시 테이블을 명시적으로 만들면 **tempdb** UDT 열을 정의 하는 다음에 UDT를 등록 합니다 **tempdb** 사용자 데이터베이스의 경우와 동일 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
