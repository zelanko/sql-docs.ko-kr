---
title: CREATE ASSEMBLY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASSEMBLY
- CREATE ASSEMBLY
- CREATE_ASSEMBLY_TSQL
- ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], validating
- validating assemblies
- CREATE ASSEMBLY statement
- assemblies [CLR integration], creating
ms.assetid: d8d1d245-c2c3-4325-be52-4fc1122c2079
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 55324ac26eef5f685339b21162360544a4ae5af7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141106"
---
# <a name="create-assembly-transact-sql"></a>CREATE ASSEMBLY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  클래스 메타데이터와 관리 코드를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 개체로 포함하는 관리되는 애플리케이션 모듈을 만듭니다. 이 모듈을 참조하여 데이터베이스에서 CLR(공용 언어 런타임) 함수, 저장 프로시저, 트리거, 사용자 정의 집계 및 사용자 정의 형식을 만들 수 있습니다.  
  
> [!WARNING]
>  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 자세한 내용은 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE ASSEMBLY assembly_name  
[ AUTHORIZATION owner_name ]  
FROM { <client_assembly_specifier> | <assembly_bits> [ ,...n ] }  
[ WITH PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE } ]  
[ ; ]  
<client_assembly_specifier> :: =  
        '[\\computer_name\]share_name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```  
  
## <a name="arguments"></a>인수  
 *assembly_name*  
 어셈블리의 이름입니다. 이 이름은 데이터베이스 내에서 고유해야 하며 유효한 [식별자](../../relational-databases/databases/database-identifiers.md)여야 합니다.  
  
 AUTHORIZATION *owner_name*  
 어셈블리 소유자인 사용자 또는 역할의 이름을 지정합니다. *owner_name*은 현재 사용자가 멤버로 속한 역할의 이름이어야 합니다. 그렇지 않으면 현재 사용자가 *owner_name*에 대한 IMPERSONATE 권한이 있어야 합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.  
  
 \<client_assembly_specifier>  
업로드할 어셈블리가 있는 로컬 경로나 네트워크 위치와 어셈블리에 해당하는 매니페스트 파일 이름을 지정합니다.  \<client_assembly_specifier>는 고정 문자열 또는 고정 문자열에 대해 평가하는 변수가 있는 식으로 나타낼 수 있습니다. CREATE ASSEMBLY로는 다중 모듈 어셈블리를 로드할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 동일한 위치에서 이 어셈블리의 모든 종속 어셈블리를 찾은 다음 동일한 소유자를 사용하여 해당 종속 어셈블리를 루트 수준 어셈블리로 업로드합니다. 이러한 종속 어셈블리를 찾을 수 없으며 현재 데이터베이스에 종속 어셈블리가 로드되어 있지 않은 경우 CREATE ASSEMBLY는 실패합니다. 종속 어셈블리가 현재 데이터베이스에 로드되어 있는 경우 해당 어셈블리의 소유자는 새로 만든 어셈블리의 소유자와 동일해야 합니다.

> [!IMPORTANT]
> Azure SQL Database는 파일에서 어셈블리 생성을 지원하지 않습니다.
  
 로그인한 사용자가 가장되는 경우에는 \<client_assembly_specifier>를 지정할 수 없습니다.  
  
 \<assembly_bits>  
 어셈블리와 어셈블리의 종속 어셈블리를 구성하는 이진 값 목록입니다. 목록에서 첫 번째 값은 루트 수준 어셈블리로 간주됩니다. 종속 어셈블리에 해당하는 값은 순서에 관계없이 입력할 수 있습니다. 루트 어셈블리의 종속성에 해당하지 않는 값은 모두 무시됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 *varbinary_literal*  
 **varbinary** 리터럴입니다.  
  
 *varbinary_expression*  
 **varbinary** 형식의 식입니다.  
  
 PERMISSION_SET { **SAFE** | EXTERNAL_ACCESS | UNSAFE }  
> [!IMPORTANT]
>  `PERMISSION_SET` 옵션은 시작 경고에서 설명된 `clr strict security` 옵션의 영향을 받습니다. `clr strict security`을 사용하면 모든 어셈블리가 `UNSAFE`로 처리됩니다.
 
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리에 액세스할 때 이 어셈블리에 부여된 코드 액세스 권한 집합을 지정합니다. 지정하지 않으면 기본적으로 SAFE가 적용됩니다.  
  
 SAFE를 사용하는 것이 좋습니다. SAFE는 가장 제한적인 권한 집합입니다. SAFE 권한을 사용하여 어셈블리에서 실행한 코드는 파일, 네트워크, 환경 변수 또는 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 없습니다.  
  
 EXTERNAL_ACCESS를 사용하면 어셈블리에서 파일, 네트워크, 환경 변수 및 레지스트리와 같은 특정 외부 시스템 리소스에 액세스할 수 있습니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 UNSAFE를 사용하면 어셈블리에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 내부 리소스와 외부 리소스 모두에 제한 없이 액세스할 수 있습니다. UNSAFE 어셈블리 내에서 실행되는 코드는 비관리 코드를 호출할 수 있습니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
> [!IMPORTANT]  
>  SAFE 권한 설정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 외부 리소스에 액세스하지 않고 계산 및 데이터 관리 태스크를 수행하는 어셈블리에 권장됩니다.  
>   
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 외부 리소스에 액세스하는 어셈블리에는 EXTERNAL_ACCESS를 사용하는 것이 좋습니다. EXTERNAL_ACCESS 어셈블리는 SAFE 어셈블리 수준의 안정성 및 확장성 보호를 제공하지만 보안 측면에서는 UNSAFE 어셈블리와 유사합니다. 그 이유는 EXTERNAL_ACCESS 어셈블리의 코드에서 명시적으로 호출자를 가장하지 않는 한 기본적으로 코드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정으로 실행되고 이 계정을 통해 외부 리소스에 액세스하기 때문입니다. 따라서 EXTERNAL_ACCESS 어셈블리를 만드는 사용 권한은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에서 코드를 실행하도록 트러스트된 로그인에만 부여해야 합니다. 가장에 대한 자세한 내용은 [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md)을 참조하세요.  
>   
>  UNSAFE를 지정하면 어셈블리의 코드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 공간에서 모든 작업을 자유롭게 수행할 수 있게 되므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 취약해질 가능성이 있습니다. UNSAFE 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 공용 언어 런타임 중 하나의 보안 시스템을 손상시킬 수도 있습니다. 따라서 UNSAFE 권한은 가장 높은 수준의 트러스트된 어셈블리에만 부여해야 합니다. **sysadmin** 고정 서버 역할의 멤버만 UNSAFE 어셈블리를 만들고 변경할 수 있습니다.  
  
 어셈블리 권한 집합에 대한 자세한 내용은 [Designing Assemblies](../../relational-databases/clr-integration/assemblies-designing.md)를 참조하십시오.  
  
## <a name="remarks"></a>Remarks  
 CREATE ASSEMBLY는 관리 코드에서 .dll 파일로 미리 컴파일된 어셈블리를 SQL Server 인스턴스 내부에서 사용할 수 있도록 업로드합니다.  
 
사용하도록 설정되면 `CREATE ASSEMBLY` 및 `ALTER ASSEMBLY` 문의 `PERMISSION_SET` 옵션은 런타임에서 무시되지만 `PERMISSION_SET` 옵션은 메타데이터에서 유지됩니다. 이 옵션을 무시하면 기존 코드 문의 중단을 최소화합니다.
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이름, culture 및 공개 키가 동일한 서로 다른 버전의 어셈블리를 등록할 수 없습니다.  
  
\<client_assembly_specifier>에 지정된 어셈블리에 액세스하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 Windows 로그인의 보안 컨텍스트를 가장합니다. \<client_assembly_specifier>에서 네트워크 위치(UNC 경로)를 지정하는 경우에는 위임 제한 때문에 현재 로그인의 가장이 해당 네트워크 위치로 전달되지 않습니다. 이 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트를 사용하여 액세스합니다. 자세한 내용은 [자격 증명 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)를 참조하세요.
  
 *assembly_name*에서 지정한 루트 어셈블리 외에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 업로드할 루트 어셈블리에서 참조하는 모든 어셈블리를 업로드합니다. 참조하는 어셈블리가 이전의 CREATE ASSEMBLY 문에 의해 이미 데이터베이스에 업로드된 경우에는 루트 어셈블리에서 사용할 수 있으므로 해당 어셈블리는 업로드되지 않습니다. 종속 어셈블리가 이전에 업로드되지 않았지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 원본 디렉터리에서 해당 매니페스트 파일을 찾지 못하는 경우 CREATE ASSEMBLY는 오류를 반환합니다.  
  
 루트 어셈블리에서 참조하는 종속 어셈블리가 데이터베이스에 없으며 암시적으로 루트 어셈블리와 함께 로드되는 경우 해당 종속 어셈블리의 권한 집합은 루트 수준 어셈블리와 동일합니다. 종속 어셈블리를 루트 수준 어셈블리와 다른 권한 집합을 사용하여 만들어야 한다면 적절한 권한 집합을 사용하여 루트 수준 어셈블리보다 먼저 명시적으로 업로드해야 합니다.  
  
## <a name="assembly-validation"></a>어셈블리 유효성 검사  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CREATE ASSEMBLY 문으로 업로드된 어셈블리 이진 파일에 대해 다음 사항을 확인합니다.  
  
-   어셈블리 이진 파일이 유효한 메타데이터와 코드 세그먼트로 된 올바른 형식인지 확인하고 코드 세그먼트에 유효한 MSIL(Microsoft Intermediate Language) 명령이 있는지 확인합니다.  
  
-   어셈블리 이진 파일에서 참조하는 시스템 어셈블리 집합이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 어셈블리인 Microsoft.Visualbasic.dll, Mscorlib.dll, System.Data.dll, System.dll, System.Xml.dll, Microsoft.Visualc.dll, Custommarshallers.dll, System.Security.dll, System.Web.Services.dll, System.Data.SqlXml.dll, System.Core.dll 및 System.Xml.Linq.dll 중 하나입니다. 다른 시스템 어셈블리는 참조할 수 있지만 데이터베이스에 명시적으로 등록해야 합니다.  
  
-   SAFE 또는 EXTERNAL ACCESS 권한 집합을 사용하여 만든 어셈블리의 경우  
  
    -   어셈블리 코드가 안전한 형식이어야 합니다. 형식 안전성은 어셈블리에 대해 공용 언어 런타임 검증 도구를 실행하여 설정합니다.  
  
    -   어셈블리의 클래스에는 읽기 전용으로 표시되지 않은 정적 데이터 멤버가 포함되어서는 안 됩니다.  
  
    -   어셈블리의 클래스는 파이널라이저 메서드를 포함할 수 없습니다.  
  
    -   어셈블리의 클래스나 메서드에는 허용되는 코드 특성만 사용하여 주석을 추가해야 합니다. 자세한 내용은 [CLR 루틴용 사용자 지정 특성](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)을 참조하세요.  
  
 CREATE ASSEMBLY를 실행할 때 수행되는 위와 같은 확인 작업 외에도 어셈블리의 코드를 실행할 때 수행되는 추가 확인 작업이 있습니다.  
  
-   특정 코드 액세스 권한이 필요한 특정 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] API를 호출할 경우 어셈블리의 권한 집합에 해당 사용 권한이 포함되지 않는다면 호출은 실패할 수 있습니다.  
  
-   SAFE 및 EXTERNAL_ACCESS 어셈블리의 경우 특정 HostProtectionAttributes를 사용하여 주석을 추가한 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] API를 호출하려고 하면 실패합니다.  
  
 자세한 내용은 [Designing Assemblies](../../relational-databases/clr-integration/assemblies-designing.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 CREATE ASSEMBLY 권한이 필요합니다.  
  
 PERMISSION_SET = EXTERNAL_ACCESS를 지정한 경우 서버에 대한 **EXTERNAL ACCESS ASSEMBLY** 권한이 있어야 합니다. PERMISSION_SET = EXTERNAL_ACCESS를 지정한 경우 서버에 대한 **UNSAFE ASSEMBLY** 권한이 있어야 합니다.  
  
 업로드할 어셈블리에서 참조하는 어셈블리가 이미 데이터베이스에 있는 경우 사용자는 해당 어셈블리의 소유자여야 합니다. 파일 경로를 사용하여 어셈블리를 업로드하려면 현재 사용자가 Windows 인증 로그인이거나 **sysadmin** 고정 서버 역할의 멤버여야 합니다. CREATE ASSEMBLY를 실행하는 사용자의 Windows 로그인에는 문에서 로드할 공유와 파일에 대한 읽기 권한이 있어야 합니다.  

### <a name="permissions-with-clr-strict-security"></a>엄격한 CLR 보안 사용 권한    
`CLR strict security`를 사용할 때 CLR 어셈블리를 만드는 데 필요한 권한은 다음과 같습니다.

- 사용자에게 `CREATE ASSEMBLY` 권한이 있어야 합니다.  
- 다음 조건 중 하나가 충족되어야 합니다.  
  - 어셈블리는 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명됩니다. 어셈블리에 서명하는 것이 좋습니다.  
  - 데이터베이스는 `ON`으로 설정된 `TRUSTWORTHY` 속성을 가지고 있고 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 로그인으로 소유됩니다. 이 방법은 권장되지 않습니다.  
  
 어셈블리 권한 집합에 대한 자세한 내용은 [Designing Assemblies](../../relational-databases/clr-integration/assemblies-designing.md)를 참조하십시오.  
  
## <a name="examples"></a>예  
  
### <a name="example-a-creating-an-assembly-from-a-dll"></a>예제 A: dll에서 어셈블리 만들기  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 예제를 로컬 컴퓨터의 기본 위치에 설치하고 HelloWorld.csproj 예제 애플리케이션을 컴파일했다고 가정합니다. 자세한 내용은 [Hello World 예제](https://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7)를 참조하세요.  
  
```  
CREATE ASSEMBLY HelloWorld   
FROM <system_drive>:\Program Files\Microsoft SQL Server\100\Samples\HelloWorld\CS\HelloWorld\bin\debug\HelloWorld.dll  
WITH PERMISSION_SET = SAFE;  
```  

> [!IMPORTANT]
> Azure SQL Database는 파일에서 어셈블리 생성을 지원하지 않습니다.
  
### <a name="example-b-creating-an-assembly-from-assembly-bits"></a>예제 B: 어셈블리 비트에서 어셈블리 만들기  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 샘플 비트(완전하거나 유효하지 않은)를 사용자 어셈블리 비트로 대체 합니다.  
  
```  
CREATE ASSEMBLY HelloWorld  
    FROM 0x4D5A900000000000  
WITH PERMISSION_SET = SAFE;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DROP ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE AGGREGATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [공용 언어 런타임 &#40;CLR&#41; 통합에 대한 사용 시나리오 및 예제](https://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
  
  
