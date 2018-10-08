---
title: ALTER ASSEMBLY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_ASSEMBLY_TSQL
- ALTER ASSEMBLY
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], modifying
- refreshing assemblies
- assemblies [CLR integration], versioning
- assemblies [CLR integration], adding files
- modifying assemblies
- adding files
- ALTER ASSEMBLY statement
ms.assetid: 87bca678-4e79-40e1-bb8b-bd5ed8f34853
caps.latest.revision: 76
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 32f8f0b6aaaa44dc42a52babae398845779961d3
ms.sourcegitcommit: d8e3da95f5a2b7d3997d63c53e722d494b878eec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2018
ms.locfileid: "44171805"
---
# <a name="alter-assembly-transact-sql"></a>ALTER ASSEMBLY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  어셈블리의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카탈로그 속성을 수정하여 어셈블리를 변경합니다. ALTER ASSEMBLY는 어셈블리의 구현을 유지하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 모듈의 최신 복사본으로 어셈블리를 새로 고치고 어셈블리와 연관된 파일을 추가하거나 제거합니다. 어셈블리는 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)를 사용하여 만듭니다.  

>  [!WARNING]
>  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 자세한 내용은 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)를 참조하세요.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER ASSEMBLY assembly_name  
    [ FROM <client_assembly_specifier> | <assembly_bits> ]  
    [ WITH <assembly_option> [ ,...n ] ]  
    [ DROP FILE { file_name [ ,...n ] | ALL } ]  
    [ ADD FILE FROM   
    {   
        client_file_specifier [ AS file_name ]   
      | file_bits AS file_name   
    } [,...n ]   
    ] [ ; ]  
<client_assembly_specifier> :: =  
    '\\computer_name\share-name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
    { varbinary_literal | varbinary_expression }  
  
<assembly_option> :: =  
    PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
  | VISIBILITY = { ON | OFF }  
  | UNCHECKED DATA  
  
```  
  
## <a name="arguments"></a>인수  
 *assembly_name*  
 수정하려는 어셈블리의 이름입니다. *assembly_name*은 데이터베이스에 이미 있어야 합니다.  
  
 FROM \<client_assembly_specifier> | \<assembly_bits>  
 어셈블리의 구현을 유지하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 모듈의 최신 복사본으로 어셈블리를 업데이트합니다. 지정한 어셈블리와 관련된 파일이 없는 경우에만 이 옵션을 사용할 수 있습니다.  
  
 \<client_assembly_specifier>는 새로 고칠 어셈블리가 있는 네트워크 위치나 로컬 위치를 지정합니다. 네트워크 위치에는 컴퓨터 이름, 공유 이름 및 해당 공유 내의 경로가 포함됩니다. *manifest_file_name*은 어셈블리의 매니페스트가 들어 있는 파일의 이름을 지정합니다.  

> [!IMPORTANT]
> Azure SQL Database는 파일 참조를 지원하지 않습니다.
  
 \<assembly_bits>는 어셈블리에 대한 이진 값입니다.  
  
 업데이트도 필요한 모든 종속 어셈블리에 대해 별도의 ALTER ASSEMBLY 문을 실행해야 합니다.  
  
 PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
>  [!IMPORTANT]  
>  `PERMISSION_SET` 옵션은 시작 경고에 설명된 `clr strict security` 옵션의 영향을 받습니다. `clr strict security`을 사용하면 모든 어셈블리가 `UNSAFE`로 처리됩니다.  
 어셈블리의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 코드 액세스 권한 설정 속성을 지정합니다. 이 속성에 관한 자세한 내용은 [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 EXTERNAL_ACCESS 및 UNSAFE 옵션을 사용할 수 없습니다.  
  
 VISIBILITY = { ON | OFF }  
 어셈블리에 대해 CLR(공용 언어 런타임) 함수, 저장 프로시저, 트리거, 사용자 정의 형식 및 사용자 정의 집계 함수를 만들 때 어셈블리를 표시할지 여부를 나타냅니다. 이 인수가 OFF로 설정되어 있으면 어셈블리가 다른 어셈블리에서 호출되는 용도로만 사용됩니다. 어셈블리에 대해 생성된 기존 CLR 데이터베이스가 있는 경우 어셈블리의 표시 유형을 변경할 수 없습니다. *assembly_name*으로 참조되는 모든 어셈블리는 기본적으로 표시되지 않는 상태로 업로드됩니다.  
  
 UNCHECKED DATA  
 기본적으로 개별 테이블 행의 일관성을 확인해야 하는 경우 ALTER ASSEMBLY가 실패합니다. 이 옵션을 사용하면 나중에 DBCC CHECKTABLE을 사용할 때까지 일관성 확인을 연기할 수 있습니다. 이 옵션을 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터베이스에 다음을 포함하는 테이블이 있는 경우에도 ALTER ASSEMBLY 문을 실행합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 메서드를 통해 직접 또는 간접적으로 어셈블리의 메서드를 참조하는 지속형 계산 열  
  
-   직접 또는 간접적으로 어셈블리의 메서드를 참조하는 CHECK 제약 조건  
  
-   어셈블리에 종속된 CLR 사용자 정의 유형의 열 - 이 유형은 **UserDefined**(비**네이티브**) 직렬화 형식을 구현합니다.  
  
-   WITH SCHEMABINDING을 사용하여 생성된 뷰를 참조하는 CLR 사용자 정의 형식의 열  
  
 CHECK 제약 조건이 있는 경우 비활성화되며 신뢰할 수 없는 상태로 표시됩니다. 어셈블리에 의존하는 열이 포함된 모든 테이블은 명시적으로 확인되기 전까지 확인되지 않은 데이터를 포함하는 것으로 표시됩니다.  
  
 **db_owner** 및 **db_ddlowner** 고정 데이터베이스 역할의 멤버만이 이 옵션을 지정할 수 있습니다.  
  
 이 옵션을 지정하려면 **ALTER ANY SCHEMA** 권한이 필요합니다.  
  
 자세한 내용은 [Implementing Assemblies](../../relational-databases/clr-integration/assemblies-implementing.md)를 참조하세요.  
  
 [ DROP FILE { *file_name*[ **,***...n*] | ALL } ]  
 어셈블리와 관련된 특정 파일이나 모든 파일을 데이터베이스에서 제거합니다. ADD FILE이 뒤따를 경우 DROP FILE이 먼저 실행됩니다. 이 기능을 사용하여 같은 파일 이름의 파일을 대체할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 포함된 데이터베이스 또는 Azure SQL Database에서 사용할 수 없습니다.  
  
 [ ADD FILE FROM { *client_file_specifier* [ AS *file_name*] | *file_bits*AS *file_name*}  
 원본 코드, 디버그 파일 또는 기타 관련 정보와 같은 어셈블리와 관련된 파일을 서버로 업로드하고 **sys.assembly_files** 카탈로그 뷰에 표시합니다. *client_file_specifier*는 업로드할 파일이 있는 위치를 지정합니다. 이 옵션 대신 *file_bits*를 사용하면 파일을 구성하는 이진 값 목록을 지정할 수 있습니다. *file_name*은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 저장되어야 하는 파일 이름을 지정합니다. *file_bits*가 지정되면 *file_name*가 지정되어야 하고 *client_file_specifier*가 지정되면 선택적입니다. *file_name*을 지정하지 않으면 *client_file_specifier*의 file_name 부분이 *file_name*으로 사용됩니다.  
  
> [!NOTE]  
>  이 옵션은 포함된 데이터베이스 또는 Azure SQL Database에서 사용할 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
 ALTER ASSEMBLY는 현재 실행 중인 세션(수정 중인 어셈블리에서 실행 중인 코드)을 방해하지 않습니다. 현재 세션은 어셈블리의 변경되지 않은 비트를 사용하여 실행이 완료됩니다.  
  
 FROM 절이 지정되면 ALTER ASSEMBLY는 제공된 모듈의 최신 복사본을 기준으로 어셈블리를 업데이트합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 어셈블리에 대해 정의된 CLR 함수, 저장 프로시저, 트리거, 데이터 형식 및 사용자 정의 집계 함수가 있을 수 있으므로 ALTER ASSEMBLY 문은 이러한 항목을 어셈블리의 최신 구현에 다시 바인딩합니다. 이렇게 다시 바인딩하기 위해서는 동일한 서명의 수정된 어셈블리에도 CLR 함수, 저장 프로시저 및 트리거를 매핑하는 메서드가 있어야 합니다. CLR 사용자 정의 형식 및 사용자 정의 집계 함수를 구현하는 클래스는 여전히 사용자 정의 형식이나 집계에 대한 요구 사항을 충족해야 합니다.  
  
> [!CAUTION]  
>  WITH UNCHECKED DATA를 지정하지 않으면 새 어셈블리 버전이 테이블, 인덱스 또는 다른 영구 사이트의 기존 데이터에 영향을 주는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ALTER ASSEMBLY를 실행하지 못하도록 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CLR 어셈블리를 업데이트할 때 계산 열, 인덱스, 인덱싱된 뷰 또는 식이 기본 루틴 및 유형과 일치하도록 보장하지는 않습니다. ALTER ASSEMBLY를 실행하여 어셈블리에 저장된 해당 식을 기반으로 하는 식 결과와 값이 일치하는지 확인하는 경우 주의하십시오.  
  
 ALTER ASSEMBLY는 어셈블리 버전을 변경합니다. 어셈블리의 culture 및 공개 키 토큰은 동일하게 유지됩니다.  
  
 다음을 변경하는 데 ALTER ASSEMBLY 문을 사용할 수 없습니다.  
  
-   어셈블리를 참조하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 CLR 함수, 집계 함수, 저장 프로시저 및 트리거의 서명. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리의 새 버전으로 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체를 다시 바인딩할 수 없는 경우 ALTER ASSEMBLY가 실패합니다.  
  
-   다른 어셈블리에서 호출되는 어셈블리에 있는 메서드의 서명  
  
-   어셈블리의 **DependentList** 속성으로 참조되는 어셈블리에 종속된 어셈블리 목록  
  
-   해당 메서드에 직접 또는 간접적으로 의존하는 인덱스나 지속형 계산 열이 없는 경우 메서드의 인덱싱 가능성  
  
-   CLR 테이블 반환 함수의 **FillRow** 메서드 이름 특성  
  
-   사용자 정의 집계의 **Accumulate** 및 **Terminate** 메서드 서명.  
  
-   시스템 어셈블리  
  
-   어셈블리 소유권. 대신 [ALTER AUTHORIZATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)을 사용합니다.  
  
 또한 사용자 정의 형식을 구현하는 어셈블리에 대해 다음 변경을 수행하는 경우에만 ALTER ASSEMBLY를 사용할 수 있습니다.  
  
-   서명 또는 특성이 변경되지 않는 경우 사용자 정의 형식 클래스의 공용 메서드를 수정하는 경우  
  
-   새 공용 메서드를 추가하는 경우  
  
-   전용 메서드를 어떤 방식으로든 수정하는 경우  
  
 데이터 멤버 또는 기본 클래스를 비롯하여 기본적으로 직렬화된 사용자 정의 형식에 포함된 필드는 ALTER ASSEMBLY를 사용하여 변경할 수 없습니다. 다른 모든 변경은 지원되지 않습니다.  
  
 ADD FILE FROM을 지정하지 않을 경우 ALTER ASSEMBLY는 어셈블리와 관련된 모든 파일을 삭제합니다.  
  
 UNCHECKED 데이터 절 없이 ALTER ASSEMBLY를 실행하면 새 어셈블리 버전이 테이블의 기존 데이터에 영향을 미치지 않는지 확인하는 검사가 수행됩니다. 확인해야 하는 데이터 양에 따라 이 검사가 성능에 영향을 미칠 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 어셈블리에 대한 ALTER 권한이 필요합니다. 추가 요구 사항은 다음과 같습니다.  
  
-   기존 권한이 EXTERNAL_ACCESS로 설정되어 있는 어셈블리를 변경하려면 서버에 대한 **EXTERNAL ACCESS ASSEMBLY** 권한이 필요합니다.  
  
-   기존 권한이 UNSAFE로 설정되어 있는 어셈블리를 변경하려면 서버에 대한 **UNSAFE ASSEMBLY** 권한이 필요합니다.  
  
-   어셈블리의 사용 권한 설정을 EXTERNAL_ACCESS로 변경하려면 서버에 대한 **EXTERNAL ACCESS ASSEMBLY** 권한이 필요합니다.  
  
-   어셈블리의 사용 권한 설정을 UNSAFE로 변경하려면 서버에 대한 **UNSAFE ASSEMBLY** 권한이 필요합니다.  
  
-   WITH UNCHECKED DATA를 지정하려면 **ALTER ANY SCHEMA** 권한이 필요합니다.  


### <a name="permissions-with-clr-strict-security"></a>엄격한 CLR 보안 사용 권한    
`CLR strict security`를 사용할 때 CLR 어셈블리를 만드는 데 필요한 권한은 다음과 같습니다.

- 사용자에게 `ALTER ASSEMBLY` 권한이 있어야 합니다.  
- 다음 조건 중 하나가 충족되어야 합니다.  
  - 어셈블리는 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명됩니다. 어셈블리에 서명하는 것이 좋습니다.  
  - 데이터베이스는 `ON`으로 설정된 `TRUSTWORTHY` 속성을 가지고 있고 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 로그인으로 소유됩니다. 이 방법은 권장되지 않습니다.  
  
  
 어셈블리 권한 집합에 대한 자세한 내용은 [Designing Assemblies](../../relational-databases/clr-integration/assemblies-designing.md)를 참조하십시오.  
  
## <a name="examples"></a>예  
  
### <a name="a-refreshing-an-assembly"></a>1. 어셈블리 새로 고치기  
 다음 예에서는 `ComplexNumber` 어셈블리를 어셈블리의 구현을 유지하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 모듈의 최신 복사본으로 업데이트합니다.  
  
> [!NOTE]  
>  `ComplexNumber` 어셈블리는 UserDefinedDataType 예제 스크립트를 실행하여 만들 수 있습니다. 자세한 내용은 [사용자 정의 형식](http://msdn.microsoft.com/library/a9b75f36-d7f5-47f7-94d6-b4448c6a2191)을 참조하세요.  
  
 ```
 ALTER ASSEMBLY ComplexNumber 
 FROM 'C:\Program Files\Microsoft SQL Server\130\Tools\Samples\1033\Engine\Programmability\CLR\UserDefinedDataType\CS\ComplexNumber\obj\Debug\ComplexNumber.dll' 
  ```

> [!IMPORTANT]
> Azure SQL Database는 파일 참조를 지원하지 않습니다.

### <a name="b-adding-a-file-to-associate-with-an-assembly"></a>2. 어셈블리와 연결할 파일 추가  
 다음 예에서는 `Class1.cs` 어셈블리와 연결할 소스 코드 파일 `MyClass`를 업로드합니다. 이 예에서는 데이터베이스에 이미 `MyClass` 어셈블리가 있다고 가정합니다.  
  
```  
ALTER ASSEMBLY MyClass   
ADD FILE FROM 'C:\MyClassProject\Class1.cs';  
```  

> [!IMPORTANT]
> Azure SQL Database는 파일 참조를 지원하지 않습니다.

### <a name="c-changing-the-permissions-of-an-assembly"></a>3. 어셈블리의 사용 권한 변경  
 다음 예에서는 `ComplexNumber` 어셈블리 사용 권한 설정을 SAFE에서 `EXTERNAL ACCESS`로 변경합니다.  
  
```  
ALTER ASSEMBLY ComplexNumber WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
